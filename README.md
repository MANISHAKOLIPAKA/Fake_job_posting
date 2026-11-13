# Fake Job Posting Detector

A multi-agent application for assessing whether a job posting may be fraudulent. It combines machine-learning and rule-based analysis with optional AI-assisted analysis, and includes a Flask API, a Streamlit interface, resume matching, and browser-based tools.

## Features

- Analyze job descriptions and return a risk score, risk level, and explanation.
- Coordinate extraction, company verification, scam analysis, and ML prediction with LangGraph.
- Match a resume against a job description.
- Use the Flask API from the Streamlit app and the tools in `extensions/`.
- View model and analysis visualizations in the Streamlit interface.

## Requirements

- Python and pip
- Packages listed in `requirements.txt`
- Optional provider credentials for AI-assisted features

## Run locally (Windows PowerShell)

From the project directory:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

Set the same API key in both terminals. Keep credentials in environment variables or a local `.env` file; do not commit them.

Terminal 1 — start the API:

```powershell
$env:API_KEY = "replace-with-a-private-value"
python api.py
```

Terminal 2 — start the interface:

```powershell
$env:API_KEY = "replace-with-the-same-private-value"
streamlit run streamlit_app_simple.py
```

The Streamlit app is available at the local address printed by Streamlit. The API listens on port `5000` and provides `/health`, `/predict`, and `/match_resume` endpoints.

Optional integrations can be configured with environment variables such as `OPENAI_API_KEY`, `ANTHROPIC_API_KEY`, `GOOGLE_SEARCH_API_KEY`, and `GOOGLE_SEARCH_ENGINE_ID`. The application can use its non-provider analysis paths when these are not set.

## Training

`python train.py` expects both `data/raw/challenging_training_data.csv` and `data/raw/enhanced_training_data.csv`, each with `description` and `label` columns. Training CSVs and generated model files are excluded from Git; supply the datasets locally before training.

## Project layout

- `api.py` — Flask API
- `streamlit_app_simple.py` — Streamlit application
- `src/` — detection agents, orchestration, model, preprocessing, and visualizations
- `extensions/` — Chrome, resume, and WhatsApp interfaces
- `tests/` and `test_*.py` — test code
- `train.py` — model training entry point
- `VISUALIZATION_*.md` — visualization guides and notes

## Local files and credentials

The `.gitignore` excludes environment files, local account data, logs, databases, generated datasets, and trained model artifacts. Never put API keys, passwords, or other credentials in source code.
