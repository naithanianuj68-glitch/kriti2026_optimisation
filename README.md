# Kriti Optimization 2026

A full-stack **Vehicle Routing Problem (VRP)** optimization platform for corporate employee transportation. Solves a **Multi-Trip Capacitated VRP with Time Windows (MT-CVRPTW)** — minimizing costs and travel time while respecting vehicle capacities, employee time windows, preferences, and priority-based scheduling.

**Live Demo:** [https://fkw404kkcccwg8k4gkg8wgwk.65.21.154.72.sslip.io/](https://fkw404kkcccwg8k4gkg8wgwk.65.21.154.72.sslip.io/)

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| **C++ Solver** | C++17, ALNS metaheuristic, 9 construction heuristics |
| **Backend** | Python 3.11, Flask, Gunicorn |
| **Web Frontend** | React 18, TypeScript, Vite, Tailwind CSS, Leaflet, Recharts |
| **Mobile App** | Flutter 3.10+, Supabase (Auth + PostgreSQL) |
| **Deployment** | Docker, Nginx, Coolify / Railway / Render |

---

## Features

- **Adaptive Large Neighborhood Search (ALNS)** with 9 construction heuristics for high-quality solutions
- **Real road distances** via OpenRouteService API (with haversine fallback)
- **Multi-trip support** — vehicles can make multiple round trips
- **Priority-aware scheduling** — higher-priority employees get stricter time guarantees
- **Preference matching** — vehicle type (premium/normal) and sharing preferences (single/double/triple)
- **Interactive map visualization** — Leaflet-based route explorer with actual road geometry
- **Comprehensive exports** — JSON, Excel, and PDF reports with cost projections
- **Real-time progress tracking** — live optimization stage updates
- **Mobile app** — Flutter app with Supabase auth and cloud-synced test cases

---

## Project Structure

```
├── server/                         # Backend + C++ Solver
│   ├── app.py                      # Flask REST API
│   ├── convert_excel_to_json.py    # Excel → JSON converter
│   ├── solver_config.json          # ALNS tunable parameters
│   ├── Dockerfile
│   ├── Makefile
│   ├── src/                        # C++ solver source
│   │   ├── vrp_solver_custom.cpp   # Main solver entry
│   │   ├── vrp_alns.h              # ALNS metaheuristic
│   │   ├── vrp_construction.h      # 9 construction heuristics
│   │   ├── vrp_local_search.h      # Local search operators
│   │   ├── vrp_constraints.h       # Constraint engine
│   │   ├── vrp_types.h             # Data structures
│   │   ├── vrp_parser.h            # JSON input parser
│   │   ├── vrp_output.h            # JSON output formatter
│   │   ├── vrp_validators.h        # Solution validation
│   │   └── ...
│   └── output/                     # Solver output files
│
├── frontend/                       # React Web Dashboard
│   ├── src/
│   │   ├── pages/                  # 11 feature pages
│   │   ├── components/             # Layout, Sidebar, Charts
│   │   ├── services/api.ts         # Backend API client
│   │   ├── context/                # Global state (AppContext, SidebarContext)
│   │   └── utils/                  # Data mappers & helpers
│   ├── Dockerfile
│   └── nginx.conf
│
├── App/flutter_application_1/      # Flutter Mobile App
│   ├── lib/
│   │   ├── screen/                 # Auth, Home, Input, Output pages
│   │   ├── services/               # Supabase, Upload, Optimize, Export
│   │   ├── widgets/                # UI components (maps, charts, cards)
│   │   ├── config/                 # Environment & map config
│   │   └── main.dart
│   └── assets/                     # Lottie animations
│
└── DEPLOYMENT.md                   # Deployment guide
```

---

## Running Locally

### Prerequisites

| Requirement | Version | What it's for |
|-------------|---------|---------------|
| **Python** | 3.11+ | Backend Flask server |
| **g++ (MinGW)** | C++17 support | Compiling the VRP solver |
| **Node.js** | 18+ | Frontend React app |
| **npm** | 9+ | Frontend package manager |
| **Flutter SDK** | 3.10+ | Mobile app (optional) |
| **ORS API Key** | Free | Real road distances ([sign up here](https://openrouteservice.org/dev/#/signup)) |

> **Windows users**: Install [MinGW-w64](https://www.mingw-w64.org/) or use MSYS2 to get `g++`. Make sure `g++` is in your PATH.

---

### 1. Backend (Python + C++ Solver)

Open a terminal in the project root:

```bash
cd server
```

#### Step 1 — Install Python dependencies

```bash
pip install -r requirements.txt
```
