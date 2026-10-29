# Day 50 - Product-Specific Evaluation (PayEasy Support Assistant)

Product: a RAG support chatbot over a 20-chunk knowledge base (`knowledge_base.py`).

| File | Purpose |
|---|---|
| `eval_dataset.json` | 30 questions: 10 easy, 10 medium, 10 hard (4 adversarial: no-answer x2, misleading phrasing, hallucination bait) |
| `rag_pipeline.py` | BM25 retrieval + generation. `BASELINE` and `FIXED` configs |
| `llm_judge.py` | Domain judge: correctness, groundedness, completeness, refusal_appropriateness |
| `run_eval.py` | Baseline run -> tier breakdown -> 5 worst + diagnosis -> fixes + re-eval -> `REPORT.md` |
| `regression_test.py` | `regression_test_runner()` -> timestamped file in `results/`, prints PASS / FAIL + dimension + score |
| `REPORT.md` | Submission document (tables for everything the task asks) |

## Run
```bash
python run_eval.py                      # offline, no API key needed
python regression_test.py
# real LLM numbers:
pip install openai && export OPENAI_API_KEY=sk-...   # Windows: set OPENAI_API_KEY=sk-...
python run_eval.py --mode openai
python regression_test.py --mode openai
```
**Offline mode** uses a deterministic extractive generator and rule-based judge so the harness can run without network.
For your final submission, re-run with `--mode openai` so the generation and the LLM judge are real.
