# THERMOS — Thermal Event Recognition and Monitoring Operational System

[![SIH 2026](https://img.shields.io/badge/SIH-2026-orange.svg?style=flat-square)](https://www.sih.gov.in/)
[![Problem Statement](https://img.shields.io/badge/PS_ID-SIH26162-blue.svg?style=flat-square)](https://www.sih.gov.in/)
[![Category](https://img.shields.io/badge/Category-Software-green.svg?style=flat-square)](https://www.sih.gov.in/)
[![Theme](https://img.shields.io/badge/Theme-Disaster_Management-red.svg?style=flat-square)](https://www.sih.gov.in/)
[![Live App](https://img.shields.io/badge/Demo-Live_on_Vercel-success.svg?style=flat-square&logo=vercel)](https://sih-2026-nu-ten.vercel.app/)
[![React](https://img.shields.io/badge/Frontend-React_19_+_Vite-61dafb.svg?style=flat-square&logo=react)](https://react.dev/)
[![TailwindCSS v4](https://img.shields.io/badge/Styling-TailwindCSS_v4-38bdf8.svg?style=flat-square&logo=tailwindcss)](https://tailwindcss.com/)
[![MapLibre GL](https://img.shields.io/badge/Maps-MapLibre_GL-3274a3.svg?style=flat-square)](https://maplibre.org/)
[![Three.js](https://img.shields.io/badge/3D-Three.js-black.svg?style=flat-square&logo=threedotjs)](https://threejs.org/)
[![XGBoost](https://img.shields.io/badge/ML-XGBoost_Classifier-eb5424.svg?style=flat-square)](https://xgboost.readthedocs.io/)

> **SIH 2026 Project Submission**  
> AI-Powered Earth Observation & Disaster Management Platform for Satellite Thermal Anomaly Classification, Risk Scoring, and Tactical Triage.

---

## 1. Project Information

- **Project Title:** THERMOS (Thermal Event Recognition and Monitoring Operational System)
- **Problem Statement ID (PS ID):** SIH26162
- **Problem Statement Title:** AI-Based Detection and Classification of Industrial Fires and Persistent Thermal Sources Using NASA FIRMS, OSM & Satellite Data
- **Category:** Software
- **Theme:** Disaster Management
- **Institution:** Netaji Subhas University of Technology (NSUT), New Delhi
- **Team:** Team THERMOS
- **Live Deployment:** [https://sih-2026-nu-ten.vercel.app/](https://sih-2026-nu-ten.vercel.app/)
- **Team Composition (6 Members):**
  - Frontend Engineering & GIS Integration (MapLibre GL, 3D WebGL Globe, Spatial Visualization)
  - Dashboard UI & Real-Time Data Visualization (Recharts, Incident Triage, Event Drawers)
  - UI/UX Design & Human-in-the-Loop Workflow (Ergonomic Incident Management)
  - AI/ML Pipeline & Model Training (XGBoost Classification, Feature Engineering, Explainability)
  - Backend Architecture & Geospatial Ingestion (FastAPI, PostGIS, Overpass API, FIRMS Pipeline)
  - Systems Integration & Reliability Testing

---

## 2. Problem Statement

Every 10 to 20 minutes, satellites including **NASA VIIRS (Suomi NPP & NOAA-20)** and **MODIS (Aqua & Terra)** transmit raw thermal anomaly detections worldwide. However, current disaster response and industrial safety systems suffer from critical operational bottlenecks:

1. **Lack of Identity & Context:** Raw FIRMS telemetry provides coordinates (`latitude`, `longitude`), Brightness Temperature, and Fire Radiative Power (FRP), but **cannot distinguish between benign routine operations and catastrophic disasters**. A legitimate refinery flare stack or blast furnace generates thermal readings nearly identical to an accidental explosion or a spreading forest wildfire.
2. **Alert Fatigue:** Industrial hubs and agricultural belts trigger thousands of unclassified hotspots daily, overwhelming disaster management agencies and civil defence operators.
3. **Delayed Escalation Response:** Without automated cross-referencing against industrial plant boundaries, land-use data, and human population exposure, emergency responders face critical delays in identifying high-risk industrial fires.

---

## 3. Proposed Solution

**THERMOS** transforms raw satellite heat spots into **actionable tactical intelligence**. It operates as an end-to-end multi-modal pipeline:

1. **Automated Satellite Ingestion:** Ingests active thermal anomaly detections from NASA FIRMS feeds.
2. **Multi-Source Context Enrichment:**
   - **OpenStreetMap (OSM Overpass API):** Identifies proximity to industrial perimeters, refineries, chemical plants, and hazardous infrastructure.
   - **ESA WorldCover / Land Cover Rasters:** Pinpoints land use (industrial complexes, cropland, dense forest, scrubland, urban fringes).
   - **WorldPop Density Buffers:** Estimates affected human population within 1 km and 5 km impact radiuses.
   - **Temporal History Engine:** Evaluates persistence over 24-hour, 7-day, and 30-day windows to detect recurring operational heat vs. sudden anomalous escalation.
3. **Machine Learning Ensemble:** An optimized multi-class **XGBoost Classifier** evaluates a 14-dimensional feature vector to classify anomalies across 6 verified event categories:
   - `Industrial Fire` (Accidental fire outbreak requiring emergency response)
   - `Industrial Thermal Source` (Routine operational kiln, blast furnace, or stack)
   - `Gas Flare` (Petrochemical venting and flaring)
   - `Wildfire` (Vegetation and forest fire spread)
   - `Agricultural Burning` (Seasonal crop residue stubble burning)
   - `Mining Activity` (Active mining and extraction thermal signatures)
4. **Dynamic Operational Risk Engine:** Calculates a prioritized **Risk Score (0–100)** factoring thermal escalation (+FRP velocity), industrial proximity hazard, and population vulnerability.
5. **Tactical Command Centre:** An interactive web dashboard with GIS mapping, 3D Earth thermal anomaly globe, automated priority triage queue, explainable evidence cards, and an AI-driven incident investigator.

---

## 4. Key Features

- 🌐 **Interactive 3D Thermal Globe:** WebGL digital Earth built with Three.js showcasing global satellite hot spots and event density.
- 🗺️ **Tactical GIS Command Centre:** Interactive vector map powered by MapLibre GL with thermal heat signatures, industrial boundary polygons, and dynamic radius buffers.
- 🎯 **Multi-Class ML Classification:** 6-class XGBoost model with per-category confidence probabilities and transparent evidence factors.
- 🚨 **Automated Priority Queue & Triage:** Events automatically ranked into `Critical`, `High`, `Moderate`, and `Low` risk tiers for rapid responder dispatch.
- 🔍 **Incident Investigator & Explainability:** Detailed forensic drawer displaying thermal history, FRP trend charts, spatial context, and SHAP-grounded explainable evidence.
- 📊 **Historical Analytics & Trend Intelligence:** Spatial and temporal heat-maps, category distribution, persistence analysis, and cluster patterns via Recharts.
- ⚡ **Resilient Dual-Mode Operation:** Built with automatic fallback to high-fidelity simulated telemetry when offline or during rate-limited conditions, ensuring uninterrupted operator uptime.

---

## 5. Technology Stack (Verified Against Codebase)

### Frontend
- **Framework:** React 19 (`react` 19.2.8, `react-dom` 19.2.8, `react-router-dom` 7.18.3)
- **Build Tool:** Vite 8.2.2 with `@vitejs/plugin-react`
- **Styling:** TailwindCSS v4 (`@tailwindcss/vite` 4.3.3, `tailwindcss` 4.3.3) with `@theme` design tokens in `src/index.css`
- **Geospatial 2D Mapping:** MapLibre GL (`maplibre-gl` 6.6.0)
- **3D Visualization:** Three.js (`three` 0.185.1) WebGL canvas
- **Animation & Transitions:** Framer Motion (`framer-motion` 13.1.1)
- **Data Charts:** Recharts (`recharts` 3.10.1)
- **State Management:** Zustand (`zustand` 5.0.15)
- **Linting:** Oxlint (`oxlint` 1.79.0)

### Backend & Machine Learning
- **API Framework:** FastAPI, Uvicorn, Pydantic
- **ML Classifier:** XGBoost (`xgboost` 3.4.1), Scikit-learn, SHAP (`shap` 0.52.0)
- **Data & Geospatial:** NumPy, Pandas, GeoPandas, Shapely, OpenStreetMap Overpass API
- **Database & Spatial ORM:** PostgreSQL + PostGIS, SQLAlchemy, GeoAlchemy2, Alembic
- **Task Scheduling:** APScheduler

---

## 6. Architecture & Data Flow

Detailed architectural specification is documented in [docs/architecture.md](docs/architecture.md).

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
                        │   (XGBoost Ensemble)   │
                        └───────────┬────────────┘
                                    │
                        ┌───────────┴────────────┐
                        ▼                        ▼
             ┌─────────────────────┐  ┌─────────────────────┐
             │ Explainable Factors │  │ Operational Risk    │
             │   (Evidence Card)   │  │ Engine (0-100 Score)│
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

## 7. Machine Learning Model Details

| Attribute | Specification |
|---|---|
| **Model Type** | Multi-class XGBoost Classifier (`n_estimators: 200`, `max_depth: 6`, `lr: 0.1`) |
| **Output Classes (6)** | `Agricultural Burning`, `Gas Flare`, `Industrial Fire`, `Industrial Thermal Source`, `Mining Activity`, `Wildfire` |
| **Input Features (14)** | `cropland_proximity_km`, `mine_proximity_km`, `forest_proximity_km`, `observation_count_7d`, `industrial_proximity_km`, `population_5km`, `refinery_proximity_km`, `land_cover`, `persistence_hours_7d`, `frp_trend_pct`, `brightness_k`, `frp_mw`, `daynight`, `firms_confidence_pct` |
| **Explainability** | SHAP (SHapley Additive exPlanations) & Feature attribution scores |

---

## 8. Repository Structure

```text
thermos-sih/
├── docs/
│   └── architecture.md         # In-depth architectural & data-flow specification
├── submission/
│   ├── DEMO.md                 # Video walk-through link and instructions
│   └── PRESENTATION.md         # Pitch presentation deck & slide notes
├── public/                     # Static icons, map markers, and web assets
├── src/
│   ├── components/
│   │   ├── landing/            # Landing page hero, Three.js 3D globe, feature cards
│   │   ├── layout/             # Topbar navigation, side drawers, application shell
│   │   ├── map/                # MapLibre GL controls, heat layers, marker popups
│   │   └── shared/             # Stat widgets, badges, risk meters, buttons
│   ├── data/
│   │   └── mockData.js         # Realistic baseline telemetry for offline resilience
│   ├── pages/
│   │   ├── Landing.jsx         # Project presentation & executive overview
│   │   ├── CommandCentre.jsx   # Tactical GIS map & live incident board
│   │   ├── PriorityQueue.jsx   # Triage list sorted by operational urgency
│   │   ├── Analytics.jsx       # Long-term heat-map & temporal trend reports
│   │   ├── Intelligence.jsx    # Anomaly correlation matrix & deep telemetry
│   │   ├── Investigator.jsx    # Evidence card explorer & case analysis
│   │   └── SystemHealth.jsx    # Pipeline ingestion rate & ML latency monitor
│   ├── services/
│   │   └── api.js              # REST client connecting to backend API
│   ├── store/
│   │   └── useStore.js         # Central Zustand state management store
│   ├── App.jsx                 # Client-side router configuration
│   ├── index.css               # Global typography, color tokens, and map styles
│   └── main.jsx                # Application root entrypoint
├── index.html                  # HTML5 boilerplate & meta tags
├── package.json                # Project dependencies and operational scripts
├── vite.config.js              # Vite bundler configuration
└── README.md                   # Primary project documentation
```

---

## 9. Getting Started & Local Setup

### Prerequisites
- **Node.js**: v18.0.0 or higher
- **npm** or **yarn**
- **Modern Web Browser**: Chrome, Firefox, Safari, or Edge with WebGL enabled

### Installation Steps

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/codebyshubhamm/thermos-sih-.git
   cd thermos-sih-
   ```

2. **Install Dependencies:**
   ```bash
   npm install
   ```

3. **Launch Development Server:**
   ```bash
   npm run dev
   ```
   Open your browser at `http://localhost:5173`.

4. **Build for Production:**
   ```bash
   npm run build
   npm run preview
   ```

---

## 10. Submission & Demonstration Links

- **Live Web Application (Vercel):** [https://sih-2026-nu-ten.vercel.app/](https://sih-2026-nu-ten.vercel.app/)
- **Presentation Deck:** See [submission/PRESENTATION.md](submission/PRESENTATION.md)
- **Demo Video Walkthrough:** See [submission/DEMO.md](submission/DEMO.md)

---

## 11. Acknowledgements & Data Sources

- **NASA FIRMS (Fire Information for Resource Management System):** Real-time thermal anomaly data from VIIRS and MODIS instruments.
- **OpenStreetMap & Overpass API:** Global open crowd-sourced spatial infrastructure and industrial boundary polygons.
- **ESA WorldCover:** 10m global land cover classification data derived from Sentinel-1 and Sentinel-2.
- **WorldPop:** High-resolution spatial demographic and population distribution estimates.
- **Smart India Hackathon (SIH 2026):** Ministry of Education’s Innovation Cell & AICTE.
