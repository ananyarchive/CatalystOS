# CatalystOS

CatalystOS is a high-throughput virtual screening platform designed to predict chemical catalytic yields and selectivities. Instead of relying on manual trial-and-error or expensive laboratory runs, the system uses a sequential Gradient Boosting regression model trained on structured chemical property data mined directly from scientific literature.

The platform addresses the "combinatorial explosion" of catalyst design by allowing researchers to simulate and pre-screen thousands of element, support, and temperature combinations before conducting physical laboratory experiments.

---

## 🛠️ Key Features

* **Literature-Driven Data Pipeline:** Integrates custom text-mining scripts to parse experimental sections of chemical journal PDFs, converting unstructured research notes into clean, tabular datasets.
* **Atomic Feature Engineering:** Converts raw chemical components into high-dimensional numerical feature vectors using physical constants (atomic radius, electronegativity, valence electron counts, and reaction environment parameters).
* **Gradient Boosting Predictive Engine:** Utilizes a precise decision-tree ensemble configured for regression tasks to isolate subtle non-linear interactions between mixed metals and operational conditions.
* **Dockerized Dependency Stabilization:** Fully containerized backend deployment to explicitly lock down library versions (`scikit-learn==1.7.2` and `numpy==1.26.x` / `2.x` environments), eliminating potential binary incompatibilities and runtime environment crashes during model unpickling.
* **Lightweight Real-Time UI:** A high-contrast React dashboard that handles state management on the client side, flashing real-time yield estimates and confidence scores in under 200 milliseconds.

---

## 💻 Tech Stack

### Frontend (The Dashboard)
* **Framework:** React.js (via Vite for optimized build performance)
* **Styling:** Tailwind CSS (High-contrast, responsive interface)
* **Deployment:** Vercel

### Backend (The Inference Engine)
* **API Framework:** Python 3.12+ / FastAPI (Asynchronous request handling)
* **Machine Learning:** Scikit-Learn (Gradient Boosting Regressor) / NumPy
* **Environment Control:** Docker (Containerized deployment)
* **Hosting:** Render

---

## 📁 Repository Structure

```text
catalystos/
├── backend/
│   ├── app/
│   │   ├── api/             # FastAPI routers handling prediction endpoints
│   │   ├── core/            # Feature vector construction and physics lookups
│   │   ├── models/          # Location for serialized model binaries (.pkl)
│   │   └── main.py          # Backend server initialization
│   ├── requirements.txt     # Pinned Python package dependencies
│   └── Dockerfile           # Multi-stage build definition for cloud hosting
└── frontend/
    ├── src/
    │   ├── components/      # UI components (Parameter inputs, metric readouts)
    │   ├── App.jsx          # Central state and API call orchestration
    │   └── main.jsx
    ├── package.json         # Node.js dependencies and script shortcuts
    └── vite.config.js
