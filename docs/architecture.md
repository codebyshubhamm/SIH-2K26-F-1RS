# THERMOS System Architecture

## 1. Overview
THERMOS (Thermal Event Recognition and Monitoring Operational System) is an automated geospatial machine learning system designed to ingest, contextualize, classify, and triage satellite-detected thermal anomalies in real time.

---

## 2. End-to-End Pipeline

```text
                        ┌────────────────────────┐
                        │    NASA FIRMS API      │
                        │ (VIIRS SNPP/NOAA, MODIS│
                        └───────────┬────────────┘
                                    │
                                    ▼
                        ┌────────────────────────┐
                        │   Ingestion Service    │
                        │  (Clustering & Dedupe) │
                        └───────────┬────────────┘
                                    │
                        ┌───────────┴────────────┐
                        ▼                        ▼
             ┌─────────────────────┐  ┌─────────────────────┐
             │   Temporal Engine   │  │   Geo-Enrichment    │
             │ (Persistence, Delta │  │ (OSM, ESA LandCover,│
             │   FRP, Recurrence)  │  │   WorldPop Buffer)  │
             └──────────┬──────────┘  └──────────┬──────────┘
                        └───────────┬────────────┘
                                    │
                                    ▼
                        ┌────────────────────────┐
                        │ Feature Engine Vector  │
                        │     (14 Dimensions)    │
                        └───────────┬────────────┘
                                    │
                                    ▼
                        ┌────────────────────────┐
                        │  ML Classification     │
                        │ (XGBoost - 6 Classes)  │
                        └───────────┬────────────┘
                                    │
                        ┌───────────┴────────────┐
                        ▼                        ▼
             ┌─────────────────────┐  ┌─────────────────────┐
             │ Explainable Factors │  │ Operational Risk    │
             │  (SHAP & Evidence)  │  │ Engine (0-100 Score)│
             └──────────┬──────────┘  └──────────┬──────────┘
                        └───────────┬────────────┘
                                    │
                                    ▼
                        ┌────────────────────────┐
                        │ PostgreSQL + PostGIS   │
                        │     Storage Layer      │
                        └───────────┬────────────┘
                                    │
                        ┌───────────┴────────────┐
                        ▼                        ▼
             ┌─────────────────────┐  ┌─────────────────────┐
             │     FastAPI REST    │  │   AI Investigator   │
             │   Telemetry & Stats │  │   (LLM Reasoning)   │
             └──────────┬──────────┘  └──────────┬──────────┘
                        └───────────┬────────────┘
                                    │
                                    ▼
                        ┌────────────────────────┐
                        │ THERMOS GIS Dashboard  │
                        │ (React 19 + MapLibre GL│
                        │    + 3D Globe View)    │
                        └────────────────────────┘
```

---

## 3. Core Architectural Modules

### 3.1 Satellite Ingestion Engine (`firms_service`)
- Polling mechanism against NASA FIRMS feeds (VIIRS 375m and MODIS 1km).
- Handles satellite orbital revisit intervals (10–20 min intervals).
- Performs spatial-temporal deduplication and active cluster association within a 750m buffer.

### 3.2 Geospatial & Context Enrichment
- **OSM Overpass Integration:** Computes spatial distance to nearest designated industrial infrastructure (refineries, petrochemical tanks, steel fabrication plants, mining sites, power substations).
- **ESA WorldCover Categorization:** Extracts categorical land-use classification (cropland, industrial land, woodland, open scrub, water body).
- **WorldPop Demographics:** Queries high-resolution raster tiles to aggregate population count within 1 km and 5 km circles.

### 3.3 Temporal Engine
- Tracks historical hotspot longevity at the given coordinates.
- Derives persistence metrics: continuous operating hours in past 24 hours, 7 days, and 30 days.
- Calculates delta-FRP ($\Delta \text{FRP}$) rate to detect rapid thermal escalation.

### 3.4 Feature Engineering (14-Dimensional Vector)
The model synthesizes tabular variables:
1. `cropland_proximity_km`
2. `mine_proximity_km`
3. `forest_proximity_km`
4. `observation_count_7d`
5. `industrial_proximity_km`
6. `population_5km`
7. `refinery_proximity_km`
8. `land_cover`
9. `persistence_hours_7d`
10. `frp_trend_pct`
11. `brightness_k` (Kelvin)
12. `frp_mw` (MW)
13. `daynight` (Day/Night flag)
14. `firms_confidence_pct`

### 3.5 ML Classification & Risk Engine
- **Model:** Tuned multi-class XGBoost classifier (`n_estimators: 200`, `max_depth: 6`, `learning_rate: 0.1`).
- **Target Classes (6):**
  1. `Agricultural Burning`
  2. `Gas Flare`
  3. `Industrial Fire`
  4. `Industrial Thermal Source`
  5. `Mining Activity`
  6. `Wildfire`
- **Explainability:** Generates normalized evidence contributions using SHAP (SHapley Additive exPlanations) values.
- **Risk Score Formulation:**
  $$\text{Risk} = w_1 \cdot \text{ClassificationRisk} + w_2 \cdot \text{ProximityHazard} + w_3 \cdot \text{PopulationExposure} + w_4 \cdot \text{EscalationRate}$$

### 3.6 Storage, API & Client Presentation
- **PostgreSQL / PostGIS:** Spatial indexing with GiST indices for fast bounding-box queries.
- **FastAPI REST Service:** Serves GeoJSON endpoints (`/api/anomalies`, `/api/stats`, `/api/investigator`).
- **Tactical Frontend:** Built with React 19, MapLibre GL vector tiles, Three.js WebGL globe, and Zustand reactive state.
