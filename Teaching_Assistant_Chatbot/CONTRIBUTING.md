# Contributing

Thanks for your interest in contributing!

## Quick setup
1. Fork the repo and clone your fork.
2. Create a virtual environment and install deps:
   - `python -m venv .venv`
   - `source .venv/bin/activate` (macOS/Linux) or `.venv\\Scripts\\activate` (Windows)
   - `pip install -r requirements.txt`
3. Create `.env` from `.env.example` and add your keys.
4. Run: `streamlit run app.py`

## Guidelines
- Do **not** commit secrets (`.env`, credentials, tokens).
- Keep PRs small and focused.
- If you add a new integration/API, document required environment variables in `README.md` and `.env.example`.
