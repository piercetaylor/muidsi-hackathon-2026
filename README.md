# AgriFlow

AgriFlow is a Missouri food supply chain analysis prototype developed for the MUIDSI Hackathon 2026. A LangGraph agent connects a FastAPI service and React interface to food access, crop, census, disaster, weather, mapping, and route tools. The project was built by Pierce Taylor, Alfiya, Suyog, and Christophe; the [original project README](docs/legacy-readme.md) records team roles and the full technical inventory.

## What is in the repository

The agent can answer questions about food access and agricultural risk, produce charts and maps, and estimate delivery routes. Its local SQLite database draws on the USDA Food Environment Atlas and Food Access Research Atlas. Optional live tools call USDA NASS Quick Stats, Census ACS, FEMA, and Open-Meteo. Source datasets carry their providers' respective terms; this repository does not declare a software license.

The research notebooks record county and census-tract risk modeling. The earlier README reports high fitted model scores, but some targets and predictors represent closely related measures. Those scores should be read as prototype validation, not evidence that the system predicts future food insecurity or crop losses. See the [notebook-to-tool account](docs/NOTEBOOKS_TO_AGENT.md) for the feature definitions and reported metrics.

## Run locally

Use Python 3.10 or newer and Node.js 18 or newer. The conversational agent requires an Archia token. USDA NASS queries require a separate NASS API key. Copy `.env.example` to `.env` and set the credentials there.

```sh
git clone https://github.com/piercetaylor/muidsi-hackathon-2026.git
cd muidsi-hackathon-2026
python -m venv .venv
# Activate .venv using the command for your shell.
pip install -r requirements.txt
cp .env.example .env
cd frontend
npm install
cd ..
```

Start the API and interface in separate terminals from the repository root:

```sh
uvicorn src.api.main:app --reload --port 8000
```

```sh
cd frontend
npm run dev
```

The interface runs at `http://localhost:5173`; the API health check is `http://localhost:8000/api/health`. The CLI entry point is `python run_agent.py`. The committed `data/agriflow.db` provides the local database, and [setup instructions](docs/SETUP.md) describe its tables and data loading. Live API access and cloud deployment depend on external services.

## Documentation

The [architecture](docs/AGRIFLOW_ARCHITECTURE.md) explains the agent graph and tools. [Running agents](docs/RUNNING_AGENTS.md) covers local and cloud modes. The [database schema](docs/DATABASE_SCHEMA.md) lists tables and fields. The [legacy README](docs/legacy-readme.md) preserves the detailed tool inventory, model table, and hackathon context.
