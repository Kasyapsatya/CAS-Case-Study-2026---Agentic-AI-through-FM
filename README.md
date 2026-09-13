# CAS Case Study — Runnable Environment

**Repository:** [github.com/Kasyapsatya/CAS-Case-Study-2026---Agentic-AI-through-FM](https://github.com/Kasyapsatya/CAS-Case-Study-2026---Agentic-AI-through-FM)

Companion environment for the notebooks behind *From Exam Question to Autonomous Agent: Teaching Agentic AI
Through Financial Mathematics* (CAS Global Teaching Materials Innovation Challenge submission).

## Notebooks

- `01_rate_conversion_agent.ipynb` — Section 4.1: the rate-conversion agent, plus the Section 3.3 agent-loop
  warm-up, a Section 3.6 guardrail demo, a Section 3.7 reliability evaluation, and Section 3.8 tracing.
- `02_annuity_agent.ipynb` — Section 4.2: the annuity present/accumulated-value agent, with a due-vs-immediate
  comparison and a reliability evaluation.
- `03_loan_amortization_agent.ipynb` — Section 4.3: the loan amortization agent (payment + schedule tools) and
  a reliability evaluation.
- `04_multi_agent_team.ipynb` — Section 5: the two-specialist bond/rate-risk team coordinated by a team leader,
  with a delegation-check evaluation.

Each notebook is self-contained and runs top to bottom in either Google Colab or a local editor.

## Getting a Gemini API key

These notebooks call Google's Gemini API, which has a free tier that is enough to run every example here.

1. Go to [aistudio.google.com/app/apikey](https://aistudio.google.com/app/apikey) and sign in with a Google account.
2. Click **Create API key** and copy the key it generates.
3. Set it, depending on where you're running the notebooks:
   - **Google Colab:** click the key icon in the left sidebar, add a secret named `GEMINI_API_KEY`, and paste
     the key as its value (recommended — this is picked up automatically). Alternatively, paste the key
     directly into the `GEMINI_API_KEY` cell near the top of each notebook.
   - **Local:** copy `.env.example` to `.env` in this folder and paste the key after `GEMINI_API_KEY=`.

Never commit a real API key to source control — `.gitignore` already excludes `.env`.

## Local (VS Code, PyCharm, JupyterLab, terminal)

Requires [uv](https://docs.astral.sh/uv/) (`curl -LsSf https://astral.sh/uv/install.sh | sh`, or see the uv docs
for Windows). uv reads `pyproject.toml` and `uv.lock` and creates an isolated `.venv` with every package pinned
to the exact version this environment was tested against.

```bash
uv sync                        # creates .venv/ and installs everything in one shot
cp .env.example .env           # then edit .env and paste your Gemini API key (see above)
uv run jupyter lab             # or: point your editor's Python interpreter at .venv/bin/python
```

VS Code / PyCharm: open this folder, then select `.venv/bin/python` (or `.venv\Scripts\python.exe` on Windows) as
the interpreter/kernel for the notebooks. No other setup is needed — the notebooks pick up `.env` automatically
through `python-dotenv`.

No uv? `pip install -r requirements.txt` works as a plain-pip fallback inside your own virtual environment.

## Google Colab

Nothing here needs to be downloaded. Open any notebook in Colab and run the setup cell — it detects that it's
running in Colab and installs the required packages directly into the runtime:

```python
subprocess.run([sys.executable, "-m", "pip", "install", "-q",
    "agno[google,opentelemetry,sqlite]", "google-genai",
    "openinference-instrumentation-agno", "python-dotenv"], check=True)
```

`.env` is skipped in Colab in favor of either a Colab secret named `GEMINI_API_KEY` or pasting the key directly
(see "Getting a Gemini API key" above).

## Files

- `pyproject.toml` — the project's dependencies (uv- and pip-compatible).
- `uv.lock` — exact resolved versions, for a reproducible install with `uv sync`.
- `requirements.txt` — plain-pip fallback, generated from the same dependencies.
- `.env.example` — copy to `.env` and add your Gemini API key (never commit the real `.env`).
- `01_rate_conversion_agent.ipynb`, `02_annuity_agent.ipynb`, `03_loan_amortization_agent.ipynb`,
  `04_multi_agent_team.ipynb` — the four notebooks described above.
