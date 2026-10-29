# JobSwipe: Bias-Mitigated AI Placement Automation Platform

A mathematically fair, audited machine learning placement automation system designed to score candidate-job profile fit while enforcing algorithmic fairness across gender, departmental, and demographic attributes.

---

## Overview

Traditional algorithmic recruitment often inherits historical selection biases. JobSwipe addresses this challenge by embedding algorithmic fairness constraints directly into the candidate ranking and classification pipeline.

Using a synthetic population of 800 candidates and 50 corporate hiring profiles, the system optimizes candidate-opportunity matching under strict fairness constraints (Demographic Parity and Equalized Odds), ensuring no demographic group experiences disparate impact above standard regulatory thresholds.

---

## 7-Phase System Architecture

```
1. Synthetic Generation ──► 800 correlated candidate profiles & 50 corporate specs
          │
          ▼
2. Preprocessing        ──► Numeric feature extraction & protected attribute isolation
          │
          ▼
3. Rule-Based Labeling  ──► Deterministic ground-truth generation (CGPA, backlogs, skills)
          │
          ▼
4. Fair Model Training  ──► LightGBM ensemble with Fairlearn disparity constraints
          │
          ▼
5. Disparity Auditing   ──► Automated rejection for models exceeding 10% demographic gap
          │
          ▼
6. Explainable AI (XAI) ──► Transparent, actionable feedback generation for candidates
          │
          ▼
7. Admin Dashboard      ──► Real-time evaluation console (FastAPI + React 18)
```

---

## Core Capabilities

- **Fairness-Constrained ML**: Wraps gradient boosted trees (LightGBM) within Fairlearn optimization to maintain high predictive utility while bounding disparate impact.
- **Explainable Feedback (XAI)**: Generates human-interpretable rejection rationales and candidate improvement roadmaps rather than opaque numerical scores.
- **Interactive Evaluation Arena**: Supports both single-candidate diagnostic evaluation and batch ranking across the full applicant cohort.
- **Auditing Dashboard**: Visualizes model performance curves, Demographic Parity ratios, and Equalized Odds differences across gender and department partitions.

---

## Technology Stack

- **Machine Learning & Backend**: Python 3.9+, FastAPI, LightGBM, Fairlearn, Scikit-learn, Pandas, NumPy, Faker.
- **Frontend & Visualization**: React 18, Vite, Zustand, Tailwind CSS, Lucide Icons.
- **Data & Configuration**: Supabase / PostgreSQL (optional persistent layer, see `SUPABASE_SETUP.md`).

---

## Repository Structure

```
.
├── backend/
│   ├── app/                   # FastAPI routes, schemas, and models
│   ├── models/                # Trained LightGBM and fairness checkpoints
│   ├── requirements.txt       # Python dependencies
│   └── main.py                # Server entry point
├── frontend/
│   ├── src/                   # React components, pages, and store
│   ├── package.json
│   └── vite.config.js
├── approach_summary.md        # Detailed mathematical formulations
├── project_workflow.md        # Architectural flow and design choices
├── SUPABASE_SETUP.md          # Database migration and cloud schema
├── run_backend.bat / .sh      # Automated backend startup script
├── run_frontend.bat / .sh     # Automated frontend startup script
└── README.md
```

---

## Setup and Quickstart

### Automated Startup (Windows)
1. Launch the backend:
   ```cmd
   run_backend.bat
   ```
2. Launch the frontend:
   ```cmd
   run_frontend.bat
   ```

### Manual Installation

#### Backend
```bash
cd backend
python -m venv venv

# Activate environment
# Windows:
.\venv\Scripts\activate
# Linux/macOS:
source venv/bin/activate

pip install -r requirements.txt
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```
Backend API interactive Swagger docs available at `http://localhost:8000/docs`.

#### Frontend
```bash
cd frontend
npm install
npm run dev
```
Frontend application available at `http://localhost:3000` or `http://localhost:5173`.

---

## Evaluation Workflow

1. Navigate to the `/eligibility` section in the web interface.
2. Select a target student profile and prospective hiring company.
3. Review the real-time fairness audit, eligibility classification, and generated explainability factors.
4. Execute batch mode to examine cohort-level ranking and disparity metrics.
