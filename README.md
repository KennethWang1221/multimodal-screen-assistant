# Multimodal screenshot assistant

Screenshot and text query in, grounded answers out—coding help, debugging, and UI explanation. Trains on **Qwen3.5-4B-Base** (SFT, then preference / RL when ready), with **OCR** alongside the vision model.

Details: **[docs/PROJECT.md](docs/PROJECT.md)**

## Repository layout

| Directory | Purpose |
|-----------|---------|
| `docs/` | Project guide (`PROJECT.md`) |
| `configs/` | Model, data, train, eval, deploy YAML |
| `datasets/` | Dataset builders and schemas |
| `ocr/` | OCR / layout preprocessing |
| `training/` | SFT, prompts, collators |
| `post_training/` | Preference and RL (later) |
| `eval/` | Offline evaluation |
| `inference/` | Local serving |
| `deployment/` | Docker and Kubernetes |
| `scripts/` | Launch helpers |
| `reports/` | Experiment notes |
| `artifacts/` | Checkpoints (use DVC, not Git, for large files) |
| `data/` | Raw and processed data (DVC) |

## Setup

Install [uv](https://github.com/astral-sh/uv), then:

```bash
cd multimodal-screen-assistant   # repository root
uv venv
source .venv/bin/activate
uv pip install -r requirements.txt
```

## Next steps

Follow **Immediate next actions** in [docs/PROJECT.md](docs/PROJECT.md).
