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
> AI-Powered Earth Observation & Tactical Intelligence Platform for Satellite Thermal Anomaly Classification, Risk Prioritization, and Emergency Dispatch.

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
  - Frontend Engineering & GIS Integration (MapLibre GL, 3D WebGL Globe, Spatial Layer Architecture)
  - Tactical UI & Real-Time Data Visualization (Recharts, Incident Triage, Dynamic Event Drawers)
  - UI/UX Design & Human-in-the-Loop Interaction (Ergonomic Operator Workflows, Dark/Warm Palettes)
  - AI/ML Pipeline & Model Training (XGBoost 6-Class Classification, 14-Feature Schema, SHAP Explainability)
  - Backend Architecture & Spatial Ingestion (FastAPI, PostGIS, Overpass API, FIRMS Stream Processing)
  - Systems Integration & Reliability Testing (Dual-mode live/offline resilience, telemetry validation)

---

## 2. Problem Statement

Every 10 to 20 minutes, satellites including **NASA VIIRS (Suomi NPP & NOAA-20)** and **MODIS (Aqua & Terra)** detect thermal anomalies across the globe. However, disaster management authorities, civil defence operators, and environmental regulators face critical operational bottlenecks:

1. **Context Blindness & Identity Ambiguity:** Raw FIRMS telemetry delivers only geographic coordinates (`latitude`, `longitude`), Brightness Temperature (Kelvin), and Fire Radiative Power (MW). It **cannot distinguish between benign routine industrial heat and catastrophic disasters**. A routine refinery gas flare or blast furnace produces thermal signatures nearly identical to an accidental explosion, toxic industrial chemical fire, or spreading wildfire.
2. **Severe Alert Fatigue:** Industrial corridors and agricultural belts generate thousands of unclassified thermal hotspots daily, flooding control rooms with false positives and noise.
3. **Delayed Escalation Response:** Without automated cross-referencing against industrial plant boundaries, land-use classifications, and human settlement exposure, emergency responders cannot triage incidents or prioritize evacuation and fire-fighting resources effectively.

---

## 3. Proposed Solution

**THERMOS** transforms raw satellite heat spots into **actionable tactical intelligence** through an automated, multi-modal pipeline:

1. **Automated Satellite Ingestion:** Continuously ingests active thermal anomaly detections from NASA FIRMS feeds with spatial clustering (DBSCAN) to prevent duplicate alerts.
2. **Multi-Source Context Enrichment:**
   - **OpenStreetMap (OSM Overpass API):** Cross-references coordinates against industrial complexes, refineries, chemical storage, and mining boundaries.
   - **ESA WorldCover:** Determines exact land-cover classification (industrial zone, cropland, forest, scrub, urban fringe).
   - **WorldPop Demographic Buffers:** Calculates human population exposure within 1 km and 5 km impact zones.
   - **Temporal History Engine:** Computes thermal persistence across 24h, 7d, and 30d time horizons, measuring fire radiative power escalation rates ($\Delta\text{FRP}$).
3. **Machine Learning Classification:** A tuned **XGBoost Classifier** evaluates a 14-dimensional feature vector to categorize anomalies into **6 distinct operational classes**:
   - `Industrial Fire` (Emergency accidental blaze requiring immediate dispatch)
   - `Industrial Thermal Source` (Permitted operational furnace, kiln, or smokestack)
   - `Gas Flare` (Permitted petrochemical venting and flaring)
   - `Wildfire` (Vegetation and forest fire outbreak)
   - `Agricultural Burning` (Seasonal crop residue stubble burning)
   - `Mining Activity` (Open-cast and coal mining extraction heat signatures)
4. **Operational Risk Engine:** Computes an actionable **Risk Score (0–100)** ranking incidents into `Critical`, `High`, `Moderate`, and `Low` priority tiers based on classification hazard, proximity to infrastructure, population density, and thermal escalation.
5. **Tactical GIS Command Centre:** A high-performance web dashboard featuring interactive MapLibre GL mapping, 3D WebGL thermal Earth globe, automated triage queue, SHAP explainable evidence cards, and an AI-assisted incident investigator.

---

## 4. Key Features

- 🌐 **Interactive 3D Thermal Globe:** WebGL digital Earth built with Three.js rendering global satellite hot spots, heat intensity, and spatial density.
- 🗺️ **High-Performance GIS Command Centre:** MapLibre GL tactical map with thermal heat signatures, industrial perimeter boundaries, dynamic buffer circles, and real-time popups.
- 🎯 **Multi-Class ML Classification:** 6-class XGBoost model with per-category confidence probabilities and automated evidence breakdowns.
- 🚨 **Automated Priority Queue & Triage:** Algorithmic ranking sorting anomalies into `Critical` ($\ge 80$), `High` ($\ge 60$), `Moderate` ($\ge 35$), and `Low` ($< 35$) risk tiers.
- 🔍 **AI Incident Investigator & Forensic Drawer:** Deep-dive diagnostics featuring multi-spectral anomaly dynamics, local environmental matrix, decision audit trails, and exportable reports.
- 📊 **Historical Analytics & Trend Intelligence:** Spatial and temporal heat-maps, classification distribution, risk distribution, and 30-day timeline charts powered by Recharts.
- 🛰️ **Threat Correlation & Satellite Passes:** Ingestion monitoring of SNPP VIIRS, NOAA-20 VIIRS, Aqua/Terra MODIS, and Sentinel-2 with industrial cluster risk assessment.
- ⚡ **Resilient Dual-Mode Operation:** Instant automatic fallback to high-fidelity simulated telemetry when offline or rate-limited, guaranteeing 100% operator uptime.

---

## 5. Technology Stack (Verified Against Codebase)

### 5.1 Frontend Client (Implemented in this Repository)
| Component | Library / Framework | Version | Purpose in Codebase |
|---|---|---|---|
| **Core Framework** | React | `19.2.8` | Component lifecycle, hooks, and virtual DOM |
| **DOM Renderer** | React DOM | `19.2.8` | Web application DOM mounting |
| **Routing** | React Router DOM | `7.18.3` | Client-side routing (`/dashboard`, `/priority`, `/analytics`, `/investigator`, `/system`) |
| **Build Engine** | Vite | `8.2.2` | Ultra-fast HMR and optimized production bundling |
| **Styling** | TailwindCSS | `4.3.3` | Utility-first CSS using `@theme` design tokens in `src/index.css` |
| **Vite Tailwind Plugin** | `@tailwindcss/vite` | `4.3.3` | Native Tailwind v4 Vite compiler plugin |
| **Geospatial 2D Map** | MapLibre GL | `6.6.0` | Vector tile rendering, industrial polygons, heat layers (`src/components/map/`) |
| **3D Graphics** | Three.js | `0.185.1` | WebGL 3D rotating thermal Earth globe (`src/components/landing/GlobeCanvas.jsx`) |
| **State Management** | Zustand | `5.0.15` | Global reactive store for active filters, selected event, and time window (`useStore.js`) |
| **Data Visualization** | Recharts | `3.10.1` | Line charts, bar graphs, and FRP history graphs (`Analytics.jsx`, `EventHistoryChart.jsx`) |
| **Animations** | Framer Motion | `13.1.1` | Micro-animations, drawer transitions, and timeline reveals |
| **Linter** | Oxlint | `1.79.0` | High-speed Rust-based code quality linter |

### 5.2 Backend & Machine Learning Pipeline Specification
| Layer | Technologies | Purpose |
|---|---|---|
| **API Server** | Python 3.10+, FastAPI, Uvicorn, Pydantic | High-performance async REST service (`/api/anomalies`, `/api/stats`, `/api/investigator`) |
| **ML Inference** | XGBoost (`3.4.1`), Scikit-learn, Joblib | Multi-class gradient boosting model predicting event categories |
| **Explainability** | SHAP (`0.52.0`) | Model interpretability and normalized feature attribution |
| **Spatial Analysis** | GeoPandas, Shapely, OpenStreetMap Overpass API | Industrial boundary proximity calculation and spatial geometry buffering |
| **Spatial Database** | PostgreSQL + PostGIS, SQLAlchemy, GeoAlchemy2 | Spatial indexing (GiST), geometry storage, and spatio-temporal query execution |
| **Scheduling** | APScheduler | Automated polling of NASA FIRMS NRT active fire feeds |

---

## 6. System Architecture

Detailed architectural specifications and data pipelines are documented in [docs/architecture.md](docs/architecture.md).

```text
                        ┌────────────────────────┐
                        │    NASA FIRMS API      │
                        │ (VIIRS SNPP/NOAA, MODIS│
                        └───────────┬────────────┘
                                    │
                                    ▼
                        ┌────────────────────────┐
                        │   Ingestion Service    │
                        │ (DBSCAN Cluster/Dedupe)│
                        └───────────┬────────────┘
                                    │
                        ┌───────────┴────────────┐
                        ▼                        ▼
             ┌─────────────────────┐  ┌─────────────────────┐
             │   Temporal Engine   │  │   Geo-Enrichment    │
             │ (Persistence, Delta │  │ (OSM Overpass, ESA, │
             │   FRP, Recurrence)  │  │   WorldPop Buffers) │
             └──────────┬──────────┘  └──────────┬──────────┘
                        └───────────┬────────────┘
                                    │
                                    ▼
                        ┌────────────────────────┐
                        │ 14-Feature Schema Vector│
                        │ (Tabular Transformation│
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

## 7. Machine Learning Model & Feature Schema

The classifier is a multi-class **XGBoost Classifier** (`n_estimators: 200`, `max_depth: 6`, `learning_rate: 0.1`) trained on multi-modal spatio-temporal thermal features.

### 7.1 Target Classes (6 Verified Categories)
1. **Industrial Fire:** Accidental industrial escalation requiring emergency fire service dispatch.
2. **Industrial Thermal Source:** Continuous operational signature (blast furnace, cement kiln, foundry).
3. **Gas Flare:** Routine petrochemical flare stack flaring.
4. **Wildfire:** Vegetation, grassland, and forest wildfire spread.
5. **Agricultural Burning:** Seasonal crop residue and stubble burning.
6. **Mining Activity:** Active open-cast and coal mining extraction heat signatures.

### 7.2 14 Engineered Feature Variables
| Feature Name | Type | Importance Weight | Description |
|---|---|---|---|
| `cropland_proximity_km` | Float | **0.170** | Distance to nearest agricultural cropland zone |
| `mine_proximity_km` | Float | **0.156** | Distance to nearest registered mining site |
| `forest_proximity_km` | Float | **0.144** | Distance to designated forest or woodland biome |
| `observation_count_7d` | Integer | **0.124** | Number of satellite passes detecting this hotspot over 7 days |
| `industrial_proximity_km` | Float | **0.106** | Distance to mapped OpenStreetMap industrial polygon boundary |
| `population_5km` | Integer | **0.095** | Aggregated population count within a 5km radius buffer |
| `refinery_proximity_km` | Float | **0.079** | Distance to nearest high-hazard petrochemical refinery boundary |
| `land_cover` | Categorical | **0.052** | ESA WorldCover land category index |
| `persistence_hours_7d` | Float | **0.039** | Total cumulative active hours logged in past 7 days |
| `frp_trend_pct` | Float | **0.027** | Rate of change in Fire Radiative Power ($\Delta\text{FRP}$) over 24h |
| `brightness_k` | Float | **0.003** | Peak Brightness Temperature in Kelvin |
| `frp_mw` | Float | **0.002** | Total Fire Radiative Power in Megawatts |
| `daynight` | Binary | **0.002** | Day (1) or Night (0) satellite pass flag |
| `firms_confidence_pct` | Float | **0.001** | Raw NASA FIRMS instrument detection confidence |

### 7.3 Operational Risk Score Formulation
$$\text{Risk Score} = \min\left(100, \;\; w_1 \cdot C_{\text{risk}} + w_2 \cdot P_{\text{prox}} + w_3 \cdot E_{\text{pop}} + w_4 \cdot \Delta_{\text{FRP}}\right)$$
- **Critical ($\ge 80$):** Immediate emergency alert dispatched to responder queue.
- **High ($60–79$):** Active monitoring with priority verification.
- **Moderate ($35–59$):** Scheduled review; typical for permitted continuous industrial sources.
- **Low ($< 35$):** Benign low-impact heat spot.

---

## 8. Repository Structure (Exact Codebase File Tree)

```text
thermos-sih/
├── docs/
│   └── architecture.md               # Comprehensive system architecture & data pipeline
├── public/
│   └── vite.svg                      # Static browser icon asset
├── src/
│   ├── components/
│   │   ├── landing/
│   │   │   └── GlobeCanvas.jsx       # Three.js 3D interactive satellite thermal globe
│   │   ├── layout/
│   │   │   ├── AppLayout.jsx         # Shell layout with navigation wrapper & drawer
│   │   │   ├── Sidebar.jsx           # Tactical sidebar navigation & active route links
│   │   │   └── TopBar.jsx            # Header with search, sensor count, and live feed badge
│   │   ├── map/
│   │   │   ├── HeatmapLayer.jsx      # MapLibre GL thermal density heatmap layer
│   │   │   ├── HotspotLayer.jsx      # Cluster & individual hotspot markers with popups
│   │   │   ├── IndustrialBoundaryLayer.jsx # OSM industrial perimeter polygons & buffers
│   │   │   ├── MapControls.jsx       # Layer toggles, zoom, and spatial style switchers
│   │   │   ├── MapCore.jsx           # Core MapLibre GL map instance initialization
│   │   │   ├── MapView.jsx           # Composite map container with active store sync
│   │   │   └── TimeSlider.jsx        # Interactive temporal timeline scrubber (24H/7D/30D)
│   │   └── shared/
│   │       ├── AskThermos.jsx        # AI conversational query assistant for event diagnostics
│   │       ├── ChartCard.jsx         # Card wrapper for analytics charts
│   │       ├── EventHistoryChart.jsx # Recharts FRP historical trend visualization
│   │       ├── EvidenceCard.jsx      # Explainable ML decision factors with percentage weights
│   │       └── IncidentDetailDrawer.jsx # Slide-out forensic inspection drawer
│   ├── data/
│   │   └── mockData.js               # High-fidelity realistic telemetry across Indian industrial hubs
│   ├── pages/
│   │   ├── Analytics.jsx             # Temporal timelines, category pie charts, risk bar charts
│   │   ├── CommandCentre.jsx         # Main GIS tactical map + live priority sidebar
│   │   ├── Intelligence.jsx          # Sensor pass schedule, industrial cluster risk ranking
│   │   ├── Investigator.jsx          # Tabbed forensic analysis (Spectral, Weather, Decision Tree)
│   │   ├── Landing.jsx               # SIH presentation landing page with 3D globe & workflow
│   │   ├── PriorityQueue.jsx         # Multi-filter operational triage list sorted by risk
│   │   └── SystemHealth.jsx          # Pipeline telemetry, API latency, and sensor uptime
│   ├── services/
│   │   └── api.js                    # REST service client connecting to backend API
│   ├── store/
│   │   └── useStore.js               # Central Zustand store (filters, selection, live data)
│   ├── utils/
│   │   └── formatters.js             # Risk color coding, duration, coordinate, and label formatters
│   ├── App.jsx                       # Client router configuration with React Router v7
│   ├── index.css                     # Global styles, font imports, TailwindCSS v4 @theme tokens
│   └── main.jsx                      # Application root bootstrap
├── submission/
│   ├── DEMO.md                       # Video demonstration outline & links
│   └── PRESENTATION.md               # Presentation slide deck link & pitch highlights
├── .gitignore                        # Git exclusion rules
├── .oxlintrc.json                    # Oxlint code inspection rules
├── index.html                        # HTML5 entrypoint with Google Fonts
├── package.json                      # NPM dependencies, scripts, and engine specifications
├── SUBMISSION_GUIDE.md               # SIH 2026 repository submission checklist
├── vite.config.js                    # Vite configuration with React & Tailwind plugins
└── README.md                         # Primary project documentation
```

---

## 9. Getting Started & Local Setup

### Prerequisites
- **Node.js**: `v18.0.0` or higher
- **npm** (included with Node.js)
- **Modern Web Browser**: Chrome, Firefox, Safari, or Edge with WebGL enabled

### Installation & Execution

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/codebyshubhamm/thermos-sih-.git
   cd thermos-sih-
   ```

2. **Install Dependencies:**
   ```bash
   npm install
   ```

3. **Start the Development Server:**
   ```bash
   npm run dev
   ```
   Navigate to `http://localhost:5173` in your browser.

4. **Code Quality Linting:**
   ```bash
   npm run lint
   ```

5. **Build for Production:**
   ```bash
   npm run build
   npm run preview
   ```

---

## 10. Future Scope & Roadmap

THERMOS is engineered with modular interfaces, positioning it for immediate operational scale:

### Phase 1: Industrial IoT & Fence-Line Sensor Integration
- Deploy MQTT and WebSockets gateways to ingest real-time ground telemetry (industrial perimeter optical IR flame detectors, ambient temperature probes, and VOC / hydrocarbon gas monitors).
- Enable multi-tier cross-corroboration: satellite observation confirmed by ground sensors triggers instantaneous automated alarm states.

### Phase 2: Autonomous Drone (UAV) Dispatch Triggers
- Direct integration with autonomous drone stations (DJI Dock, PX4-based UAVs).
- When a `Critical` industrial fire is classified, THERMOS automatically calculates an optimized GPS waypoint mission for immediate autonomous aerial thermal reconnaissance.

### Phase 3: High-Resolution Optical Satellite Corroboration
- Implement automated API tasking with high-resolution constellations (Sentinel-2 10m/20m and PlanetScope 3m).
- Apply lightweight vision transformers (ViT) to optical bands to detect and measure smoke plume volume, direction, and combustion completeness.

### Phase 4: National Disaster Framework & CAP Integration
- Direct webhook integration with the **Common Alerting Protocol (CAP)** to dispatch real-time emergency broadcasts to:
  - National Disaster Response Force (NDRF)
  - State Disaster Management Authorities (SDMA)
  - District Emergency Operations Centres (DEOC)
  - State Pollution Control Boards (SPCB)

### Phase 5: Atmospheric Plume Dispersion & Evacuation Modeling
- Couple Gaussian plume dispersion algorithms with real-time ECMWF / IMD meteorological wind vectors.
- Automatically project toxic smoke dispersion cones and calculate dynamic evacuation perimeters for downwind residential populations.

---

## 11. Demonstration & Submission Links

- **Live Web Application (Vercel):** [https://sih-2026-nu-ten.vercel.app/](https://sih-2026-nu-ten.vercel.app/)
- **Presentation Deck:** See [submission/PRESENTATION.md](submission/PRESENTATION.md)
- **Demo Video Walkthrough:** See [submission/DEMO.md](submission/DEMO.md)
- **Submission Checklist:** See [SUBMISSION_GUIDE.md](SUBMISSION_GUIDE.md)

---

## 12. Acknowledgements & Data Sources

- **NASA FIRMS (Fire Information for Resource Management System):** Real-time thermal anomaly data from VIIRS and MODIS instruments.
- **OpenStreetMap & Overpass API:** Global open crowd-sourced spatial infrastructure and industrial boundary polygons.
- **ESA WorldCover:** 10m global land cover classification data derived from Sentinel-1 and Sentinel-2.
- **WorldPop:** High-resolution spatial demographic and population distribution estimates.
- **Smart India Hackathon (SIH 2026):** Ministry of Education’s Innovation Cell & AICTE.
