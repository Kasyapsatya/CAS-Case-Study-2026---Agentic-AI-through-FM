# CAS Case Study — Runnable Environment

Companion environment for the notebooks behind *From Exam Question to Autonomous Agent: Teaching Agentic AI
Through Financial Mathematics* (CAS Global Teaching Materials Innovation Challenge submission).

## Local (VS Code, PyCharm, JupyterLab, terminal)

Requires [uv](https://docs.astral.sh/uv/) (`curl -LsSf https://astral.sh/uv/install.sh | sh`, or see the uv docs
for Windows). uv reads `pyproject.toml` and `uv.lock` and creates an isolated `.venv` with every package pinned
to the exact version this environment was tested against.

```bash
uv sync                        # creates .venv/ and installs everything in one shot
cp .env.example .env           # then edit .env and paste your Gemini API key
uv run jupyter lab             # or: point your editor's Python interpreter at .venv/bin/python
```

VS Code / PyCharm: open this folder, then select `.venv/bin/python` (or `.venv\Scripts\python.exe` on Windows) as
the interpreter/kernel for the notebooks. No other setup is needed — the notebooks pick up `.env` automatically
through `python-dotenv`.

No uv? `pip install -r requirements.txt` works as a plain-pip fallback inside your own virtual environment.

## Google Colab

Nothing here needs to be downloaded. Each notebook's setup cell installs the same packages directly
(`%pip install -q "agno[google,opentelemetry,sqlite]" google-genai python-dotenv`) and detects that it is running
in Colab, so `.env` is skipped in favor of either pasting the key directly or reading it from a Colab secret named
`GEMINI_API_KEY`.

## Files

- `pyproject.toml` — the project's dependencies (uv- and pip-compatible).
- `uv.lock` — exact resolved versions, for a reproducible install with `uv sync`.
- `requirements.txt` — plain-pip fallback, generated from the same dependencies.
- `.env.example` — copy to `.env` and add your Gemini API key (never commit the real `.env`).
