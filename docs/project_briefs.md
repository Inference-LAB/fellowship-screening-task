# Fellowship Project Briefs — Summary

**INFERENCE Lab Engineering Fellowship · Cohort 01**

This document summarises all three fellowship projects. Read the project you applied for fully before submitting your screening task — your Expected Contribution paragraph and your Question must show you understood the specific project and role you applied for.

Full project briefs and role guides are shared with selected fellows after final selection.

---

## Project A — docling-pk

**Pakistani Document Intelligence Library**

### The Problem

No open-source, pip-installable Python library exists for structured data extraction from Pakistani documents. International OCR tools return unstructured text — they do not know what a CNIC looks like, do not handle the field layouts of Pakistani matric and intermediate certificates, and do not return structured JSON with named fields.

Pakistani developers building KYC pipelines, HR systems, and edtech platforms currently solve this problem manually or with expensive proprietary APIs that underperform on Pakistani document layouts.

### What It Builds

A pip-installable Python library — `docling-pk` — that takes an image of a Pakistani document as input and returns a structured JSON object containing the extracted fields.

```python
from docling_pk import extract

result = extract("cnic_scan.jpg", document_type="cnic")
# Returns:
# {
#   "document_type": "cnic",
#   "fields": {
#     "name":           "Muhammad Ali",
#     "father_name":    "Muhammad Akram",
#     "cnic_number":    "35202-1234567-9",
#     "date_of_birth":  "01-01-1995",
#     "date_of_issue":  "15-03-2020",
#     "date_of_expiry": "14-03-2025",
#     "gender":         "M",
#     "address":        "House 12, Street 4, Multan"
#   },
#   "confidence": 0.91,
#   "warnings": []
# }
```

**Documents supported in v1:** CNIC (old green and new blue formats), Matric Certificate, Intermediate Certificate, University Degree/Transcript.

**Core technology:** EasyOCR for text extraction, OpenCV for image preprocessing (deskewing, denoising, adaptive thresholding), regex-based field extraction, Typer CLI, PyPI packaging.

### Real-World Applications

Every Pakistani fintech, edtech, and HR platform processes these documents manually today. A KYC pipeline that can extract and validate a CNIC number automatically reduces onboarding time from days to seconds. University admissions offices that process thousands of matric certificates per cycle can automate aggregate calculation. INFERENCE Lab itself uses this for research contributor verification and dataset provenance records.

### The Three Roles

**Lead Engineer** owns the overall architecture, the `extract()` public API design, the `DocumentResult` dataclass schema, the Typer CLI, the README, and PyPI packaging. The most important decision in Week 1 is the public API contract — what does `extract()` accept, what does it return, and how does a caller handle partial results when a field is obscured? If this is designed cleanly, the Research Engineer's modules plug in without friction. Requires comfort with API design, software structure, and thinking about how external developers will use the library.

**Research / Implementation Engineer** owns the image preprocessing pipeline (OpenCV — deskewing, denoising, adaptive thresholding), the OCR wrapper (EasyOCR), and all parser modules (CNIC, matric, intermediate). This is the most algorithmically demanding role. It involves understanding what OCR output actually looks like on real messy phone-camera images — not clean scanned PDFs — and writing regex extraction that handles real-world variation (OCR reading dashes as underscores, stamps partially covering fields, documents rotated 90 degrees). Requires hands-on comfort with image processing and regex, and a willingness to test against real documents in Week 1 before writing any extraction logic.

**Integration / Evaluation Engineer** owns the test suite (pytest, 90%+ coverage target), the synthetic test fixture bank (document images with known expected outputs), the accuracy benchmark, and deployment verification. The hardest part of this role is building the fixture library — you need test images where you already know exactly what the correct output should be, so you can write assertions. Requires strong testing instincts, methodical thinking about edge cases, and the discipline to write tests before implementation is finished rather than after.

---

## Project B — llm-eval-kit

**LLM Response Evaluation Library**

### The Problem

Every team building on top of an LLM — a chatbot, a RAG system, a document Q&A tool — eventually faces the same question: how do you know if the model is giving good responses? Current approaches are eyeballing outputs manually, calling another expensive LLM to evaluate the first one, or platform-locked tools that require a subscription. There is no lightweight, pip-installable, offline-capable Python library that evaluates LLM responses using interpretable, fast, local methods and returns structured results.

### What It Builds

A pip-installable Python library — `llm-eval-kit` — that takes a (prompt, response) pair, runs structured evaluation checks against defined criteria, and returns a scored JSON report.

```python
from llm_eval_kit import Evaluator

ev = Evaluator()
result = ev.evaluate(
    prompt="What causes inflation?",
    response="Inflation is caused by excess money supply.",
    context="Inflation occurs when the general price level rises. "
            "Common causes include excess money supply and demand-pull factors.",
    criteria=["factual_grounding", "relevance", "refusal_check", "completeness"]
)
# Returns:
# {
#   "overall_score": 0.87,
#   "criteria": {
#     "factual_grounding": {"score": 0.91, "explanation": "Response grounded in context"},
#     "relevance":         {"score": 0.89, "explanation": "Directly addresses the prompt"},
#     "refusal_check":     {"score": 1.0,  "is_refusal": false, "explanation": "No refusal detected"},
#     "completeness":      {"score": 0.68, "explanation": "Covers main cause, misses demand-pull"}
#   },
#   "metadata": {"response_length_words": 9, "evaluation_time_ms": 210}
# }
```

**All four criteria run locally — no internet, no API calls, no subscription.** The sentence-transformers model (~80MB) downloads once on first use and works offline after that.

**Core technology:** sentence-transformers (all-MiniLM-L6-v2) for embedding similarity, scikit-learn cosine_similarity, Python regex for refusal detection, Typer CLI, PyPI packaging.

### Real-World Applications

Any developer who has shipped an LLM-powered product needs a systematic way to answer: "Did my latest prompt change make things better or worse?" llm-eval-kit makes that question answerable in code. It can run as a CI check — fail the build if evaluation score drops below a threshold after a prompt update. Researchers evaluating fine-tuned models can use it to produce reproducible, citable evaluation reports. INFERENCE Lab uses it to evaluate model outputs on its NLP research datasets.

### The Three Roles

**Lead Engineer** owns the `Evaluator` class architecture, the criteria registry pattern (the system that allows `criteria=["factual_grounding", "relevance"]` to work dynamically without hardcoding each criterion into the Evaluator), the CLI, the README, and PyPI packaging. The registry pattern is the most important architectural decision in this project — if designed cleanly, adding a fifth criterion in v2 requires writing one function with one decorator and nothing else. If designed badly, adding a criterion requires editing four files. Requires comfort with API design and Python patterns like decorators and registries.

**Research / Implementation Engineer** owns all four criterion implementations: `refusal_check` (pattern matching — critically, "I cannot stress enough how important this is" must NOT be flagged as a refusal), `factual_grounding` (cosine similarity between response and context embeddings using sentence-transformers), `relevance` (embedding similarity between prompt and response), and `completeness` (sentence-level coverage of prompt aspects in the response). Also owns the singleton model loading pattern — the embedding model must load once per session, not once per evaluate() call, or the library will be unusably slow. Requires comfort with NLP concepts and working with pre-trained embedding models.

**Integration / Evaluation Engineer** owns the test fixture dataset (a curated collection of prompt/response/context tuples where you define in advance what score range the library should return), the pytest suite (90%+ coverage), the performance benchmark (full evaluation with all four criteria must complete in under 2 seconds), and deployment verification. The fixture dataset design is the most demanding part — you must construct cases where you know ahead of time what the correct evaluation result should be, which requires understanding each criterion well enough to predict its output. Requires strong testing instincts and the ability to think about evaluation from first principles.

---

## Project C — inference-audit

**NLP Dataset Quality Auditor**

### The Problem

When a researcher publishes an NLP dataset, the first thing a serious reviewer asks is not "what accuracy did your model achieve?" It is: "How do you know your dataset is clean?" Label distribution imbalance, near-duplicate samples, annotation inconsistency, and language contamination are the four most common reasons a dataset paper is rejected or asked for major revision.

Every lab answers these questions the same way: by writing one-off scripts, running them once, and hoping the reviewer does not ask follow-up questions that require re-running slightly different code that may no longer exist. INFERENCE Lab has this problem directly — RUEmoCorp (134K samples), RUDaSA, and the vocal load monitoring corpus all required manual quality analysis during their submission cycles. Each time, the analysis was reconstructed from fragmented scripts rather than reproduced from a standardised tool.

There is no open-source, pip-installable, reproducible NLP dataset quality auditing library. inference-audit fills that gap.

### What It Builds

A pip-installable Python library and CLI — `inference-audit` — that takes an NLP dataset file (CSV, JSON, or Parquet) as input, runs five structured quality checks, and produces a scored HTML report and machine-readable JSON summary.

```python
from inference_audit import Auditor

auditor = Auditor()
report  = auditor.audit("ruemocorp_v1.csv", label_col="emotion", text_col="text")
report.save("audit_report.html")    # human-readable, self-contained HTML
report.to_json("audit_report.json") # machine-readable for CI pipelines
```

Or from the command line with no code at all:

```bash
inference-audit run ruemocorp_v1.csv \
  --label-col emotion \
  --text-col  text \
  --output    audit_report.html \
  --fail-below 70   # exits with code 1 if overall_score < 70 — enables CI integration
```

**The five quality checks:**

| Check | What It Catches |
|---|---|
| Label Distribution | Class imbalance that produces misleading accuracy numbers |
| Near-Duplicate Detection | Verbatim or near-verbatim repeated samples — same label inflates accuracy, different label indicates annotation error |
| Language Contamination | Samples in the wrong language for a monolingual corpus |
| Missing Value Analysis | Null, whitespace-only, and suspiciously short text fields |
| Annotation Consistency | Low-confidence samples that indicate genuine annotator disagreement |

Each check returns a score (0–100) and a warning string if issues are found. The overall score is a weighted average — label distribution and near-duplicates are weighted 1.5× because they are the most common causes of peer review rejection in the lab's own submission history.

**Core technology:** datasketch (MinHash + LSH for near-duplicate detection at scale — O(n) instead of O(n²)), langdetect for language identification, pandas for data loading (CSV/JSON/Parquet), Jinja2 for HTML report generation, matplotlib for embedded charts, Typer CLI, PyPI packaging.

### Real-World Applications

**INFERENCE Lab internal use — immediate.** From the day inference-audit ships, every corpus release from the lab includes an audit report as a supplementary file. Reviewers can verify: "Dataset quality was assessed using inference-audit v1.0.0. Full audit report available as Supplementary File S1." This makes quality claims in papers falsifiable and removes the need to reconstruct quality scripts for each submission cycle.

**NLP researchers globally.** Anyone building a corpus for a low-resource language — and there are thousands doing this — faces identical problems. inference-audit becomes the standard tool they cite in methods sections.

**ML teams doing data-centric AI.** The `--fail-below` CLI flag makes inference-audit a quality gate in a CI pipeline. A dataset update that drops the quality score below threshold blocks the merge automatically.

### The Three Roles

**Lead Engineer** owns the overall library architecture, the `AuditReport` and `CheckResult` dataclasses (the schema everything else returns data into), the `Auditor` class orchestration, the data loader module (CSV/JSON/Parquet with validated column checking), the Jinja2 HTML report renderer, the Typer CLI including the `--fail-below` flag, the README, and PyPI packaging. The two most important design decisions in Week 1 are the `CheckResult` dataclass schema (every check returns one — if the schema is wrong, every check has to be refactored) and the data loader (it must validate column existence before any check runs, not inside each check). Requires comfort with API design, data class patterns, and thinking about how to handle partial results gracefully when a check cannot run.

**Research / Implementation Engineer** owns all five check modules: `check_label_distribution` (class counts, imbalance ratio, scoring formula), `check_near_duplicates` (MinHash + LSH using datasketch — character 3-gram fingerprints, not word tokens, because Roman Urdu has no standard tokenizer), `check_language_contamination` (langdetect with DetectorFactory.seed = 0 for reproducibility — this single line is more important than most of the function without it langdetect is non-deterministic), `check_missing_values` (null, whitespace-only, very-short text detection), and `check_annotation_consistency` (confidence column analysis, or graceful skip with explanation if no confidence column exists). Also owns the scoring formula for each check — the mapping from raw metrics (e.g. imbalance_ratio = 49.3) to a 0–100 score, which must be documented and justified in the design document. This is the most statistically and algorithmically demanding role across all three projects.

**Integration / Evaluation Engineer** owns the synthetic fixture generator (a Python script that creates test datasets with precisely controlled quality problems — deliberately imbalanced, deliberately duplicated, deliberately contaminated — so that expected scores are calculable before any test is run), the pytest suite (90%+ coverage), the performance benchmark (full audit on a 100K-row dataset must complete in under 60 seconds on CPU), output validation (JSON structure, HTML rendering, `--fail-below` exit code behaviour), and deployment verification. The fixture generator is the hardest deliverable in this role — fixtures must be generated programmatically, not hand-crafted, so they are reproducible. Requires methodical thinking, strong testing instincts, and comfort with pandas for constructing synthetic datasets.

---

## Across All Three Projects

**What all three projects share:**

- pip-installable Python library published on PyPI
- Typer CLI
- pytest suite with 90%+ coverage
- Complete README with installation, quickstart, and worked example
- All public functions documented with docstrings
- Clean PR history under the Inference-LAB GitHub organisation
- Lab note (500 words) published on inference-lab.org under each fellow's name

**What the fellowship does not provide:**

- Lectures or recorded sessions
- Step-by-step tutorials
- Hand-holding through standard Python or Git operations

The role guides and project briefs shared with selected fellows contain detailed technical guidance, real code scaffolding, and week-by-week deliverable breakdowns. The screening task is the first filter for who receives those materials.

---

*INFERENCE Lab · inference-lab.org · github.com/Inference-LAB · huggingface.co/Inferencelab*
*Evidence over hype. Engineering over branding.*
