# LLM Zoomcamp — Module 4: Evaluation

Evaluation of a RAG (Retrieval-Augmented Generation) system for the [DataTalks.Club](https://datatalks.club) LLM Zoomcamp FAQ.

## What it does

- **Synthetic data generation** — Uses OpenAI's structured output (Responses API + Pydantic) to create a ground-truth dataset of question-document pairs from FAQ records.
- **Search evaluation** — Loads the ground truth and evaluates retrieval quality using `minsearch`, a lightweight TF-IDF search engine.

## Project structure

| File | Purpose |
|---|---|
| `01-data-gen.ipynb` | Generates synthetic ground-truth questions via GPT |
| `02-search-eval.ipynb` | Loads ground truth and evaluates search retrieval |
| `ingest.py` | Fetches FAQ data and builds a `minsearch` index |
| `rag_helper.py` | `RAGBase` class for search, context building, and LLM calls |
| `evaluation_utils.py` | Pricing calculators, structured LLM calls, `RAGWithUsage`, parallel progress mapping |
| `data/ground_truth-new.csv` | 515 synthetic question-document pairs |
| `main.py` | Stub entry point |

## Setup

1. Python 3.12+ required.
2. Install [uv](https://docs.astral.sh/uv/) (recommended) or use pip.
3. Clone and sync:
   ```
   uv sync
   ```
4. Copy `.env.example` to `.env` and add your OpenAI API key:
   ```
   OPENAI_API_KEY=sk-...
   OPENAI_MODEL_NAME=gpt-5.4-mini
   ```

## Usage

Run the notebooks in order:
1. `01-data-gen.ipynb` — generates `data/ground_truth-new.csv`
2. `02-search-eval.ipynb` — evaluates search retrieval

## Dependencies

`minsearch`, `openai`, `pandas`, `pydantic`, `requests`, `tqdm`

## Notes

- Uses the OpenAI **Responses API** (not the older Chat Completions API).
- Structured output via `responses.parse()` with Pydantic models.
- Search index built with `minsearch` (TF-IDF + field-level boosting).
- Pricing calculators included for `gpt-5.4-mini` and `gpt-oss-120b`.
