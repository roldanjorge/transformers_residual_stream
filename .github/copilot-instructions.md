# GitHub Copilot instructions — transformers_residual_stream

**Purpose:** Help AI coding agents get productive quickly in this repo by listing the project’s important entry points, conventions, and the questions to ask when information is missing.

## Quick status
- Repository currently appears to have no source files or docs checked in. If that’s expected (private submodule / separate data store), please point the agent to the code location or upload the relevant files.

## What to look for first (search patterns)
- Look for top-level project descriptors: `README.md`, `requirements.txt`, `environment.yml`, `pyproject.toml`, `setup.py`, `Pipfile`, `Dockerfile`, `Makefile`, `.github/workflows/*`.
- Find runtime/train/eval entrypoints: filenames or functions containing `train`, `evaluate`, `run`, `main`, or `if __name__ == "__main__"`.
- Tests & CI: `tests/`, `pytest.ini`, `tox.ini`, `.github/workflows/*` referencing `pytest`.
- Notebooks and experiments: `notebooks/`, `experiments/`, `scripts/`, or `examples/`.
- Model/data artifacts: `checkpoints/`, `models/`, `data/`, `datasets/`, or references to S3/GCS URIs.

## If a file/command is present, prefer it (examples)
- If `requirements.txt` or `environment.yml` exists, use that to create the environment.
- If Dockerfile is present, prefer `docker build` / `docker run` for reproducible experiments.
- If `.github/workflows` contains `pytest` or `pytest -q`, mirror those flags locally when running tests.

## Missing or ambiguous items — what to ask the maintainer (short prompts for the agent)
- “Where is the main source code? (path to the package or scripts the project uses for training and evaluation)”
- “What is the canonical way to create a dev environment? (pip install -r requirements.txt, conda env create -f environment.yml, Docker image name, etc.)”
- “How do you run the test suite locally? (exact command, any env vars, expected runtimes or GPU needs)”
- “Are there large data or model checkpoints stored externally? Where are credentials stored and how are they accessed?”
- “Any preferred formatting/linting/commit conventions (black, isort, pre-commit hooks, commit message template)?”

## Project-specific guidance (how to act WHEN files are present)
- When editing model or training code: include a small reproducer (tiny dataset, fixed RNG seed) and a short test verifying training loop runs for one batch and produces expected shapes.
- When adding a new script: register it in `scripts/` or add a brief snippet in `README.md` showing how to run it with arguments.
- When changing data I/O: document expected schema, and add a small fixture to `tests/` covering parsing and basic validation.

## PR & commit guidance for AI agents
- Keep changes focused and atomic: one behavioral change per PR.
- Add or update tests that demonstrate the intended behavior and guard against regressions.
- Update `README.md` or `docs/` for any developer-facing change (new install steps, new CLI args, new env vars).

## Example TODO checklist for a human to complete (please fill these in)
- [ ] Primary language/runtime (e.g., Python 3.11) and exact install command
- [ ] Canonical test command (e.g., `pytest -q`) and CI expectations
- [ ] Dev environment instructions (conda/pip/Docker) 
- [ ] Any external data/model storage locations and access instructions
- [ ] Typical GPU/CPU requirements for training runs

---

If any of the above is unclear or you want a more opinionated agent behavior (for example: always create PRs with a single commit and a specific branch naming convention), reply here with the missing specifics and I will update the guidance.

> Note: I created this initial draft because the repository currently lacks discoverable code or documentation — please tell me where the source lives or paste the `README.md` / a representative training script and I will update these instructions with concrete examples from your codebase.