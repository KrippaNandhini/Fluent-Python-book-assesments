# Fluent Python Assessments — QnA Repository

**Mission:** A no-fluff, high-signal assessment bank to operationalize mastery of *Fluent Python, 2nd Ed.* (Luciano Ramalho). Built for top-tier candidates who want airtight fundamentals, production-grade thinking, and measurable outcomes.

---

## Scope & Outcomes

This repo stress-tests the following competencies aligned to the syllabus:

- **Idiomatic Python & Data Model** (Ch. 1–3) — dunder methods, protocols, containers, hashing/equality semantics.
- **First-Class Functions, Data Classes, Typing** (Ch. 5–7) — closures, higher-order patterns, `@dataclass`, structural typing, `typing`/`mypy` muscle memory.
- **Decorators & Closures** (Ch. 9) — logging, metrics, error envelopes, idempotency wrappers.
- **Special Methods & Inheritance** (Ch. 11–12) — OOP trade-offs, composition vs inheritance, custom collections.
- **Iterables & Generators** (Ch. 14) — lazy pipelines, backpressure, iterator invalidation traps.
- **Context Managers & Coroutines** (Ch. 15–16) — resource safety, cancellation, concurrency pitfalls.
- **Type Hints in Practice** (Ch. 17) — pragmatic typing for schema validation, public APIs, and refactors.

---

## Assessment Taxonomy (Must-Follow Pattern)

Every assessment set **must** follow this layered blueprint:

1. **Layer 1 – Comprehension & Recall (10 Qs)**  
2. **Layer 2 – Conceptual Integration (12 Qs)**  
3. **Layer 3 – Application (20 Qs)**  
4. **Layer 4 – Analysis (18 Qs)**  
5. **Layer 5 – Synthesis (15 Qs)**  
6. **Layer 6 – Evaluation (12 Qs)**  
7. **Layer 7 – Creation (13 Qs)**

> **Non-negotiable:** Do not ship a module without all **100** questions (10+12+20+18+15+12+13). This keeps difficulty curve, coverage, and comparability consistent.

---

## Module-to-Chapter Mapping

- **Module 01 — Data Model & Data Structures:** Chapters **1–3**  
- **Module 02 — First-Class Functions, Data Classes, Typing:** Chapters **5–7**  
- **Module 03 — Decorators & Closures:** Chapter **9**  
- **Module 04 — Special Methods & Inheritance:** Chapters **11–12**  
- **Module 05 — Iterables & Generators:** Chapter **14**  
- **Module 06 — Context Managers & Coroutines:** Chapters **15–16**  
- **Module 07 — Type Hints in Practice:** Chapter **17**

Each module ships **exactly 7 layers** with the counts above.

---

## Question File Schema

Each question is a Markdown file with required front-matter:

```yaml
---
id: M01-L3-Q014
module: 01-data-model
layer: 3            # 1..7
chapter_refs: [1,2,3]
estimated_time_min: 7
difficulty: medium  # easy|medium|hard|elite
tags: [dunder, hashing, equality, protocol]
learning_objective: >
  Implement value semantics with __eq__ and __hash__, and explain the trade-offs.
answer_type: code   # code|essay|mcq|hybrid
rubric_ref: rubrics/rubric-layered.md#layer-3
---
```

**Body sections (mandatory):**
1. **Prompt**  
2. **Constraints** (timeouts, memory bounds, forbidden imports, etc.)  
3. **Edge Cases & Hidden Tests** (bullet list)  
4. **Expected Interfaces** (function/class signature)  
5. **Starter Snippet** (optional)  
6. **Solution (in /solutions only)**  
7. **Rationale** (why this is the right approach; common wrong turns)

> **Answers live under `solutions/` mirroring the path** (e.g., `qna/module-01-data-model/solutions/layer-3/Q014.md`). Keep questions spoiler-free.

---

## Rubric & Scoring

- **Layer Weights:** L1 5%, L2 10%, L3 25%, L4 20%, L5 18%, L6 12%, L7 10%.  
  *Rationale:* maximize applied competence without gaming with rote recall.
- **Code Quality Gate:** PEP8 + type-clean (`mypy --strict`), docstrings, invariants, property-based tests where applicable.
- **Review Checklist:** see `rubrics/code-review-checklist.md` (correctness, complexity, failure modes, resource safety, typing quality, test depth).

---

## Authoring Guidance (Skeptical, No-Excuses Standard)

- **No trick trivia.** Every question must map to a production-relevant skill or a known failure mode.
- **Negative testing.** At least one test must break naive or overfitted solutions.
- **Trade-offs explicit.** Prompts should force decisions (e.g., composition vs inheritance; context manager vs try/finally).
- **Type rigor.** Prefer structural types and protocols over nominal coupling. Include `TypedDict` / `Protocol` where instructive.
- **Concurrency reality.** For coroutines, test cancellation, timeouts, and resource finalization.

---

## Local Development

```bash
# 1) Clone
git clone https://github.com/<you>/fluent-python-qna.git
cd fluent-python-qna

# 2) (Optional) Tooling
pipx install poetry
poetry install

# 3) Validate structure & metadata
python scripts/validate_qna.py

# 4) Build index (updates README TOC blocks)
python scripts/build_index.py
```

**Tooling expectations (recommended):**
- `ruff`, `black`, `mypy --strict`, `pytest`, `hypothesis`
- Pre-commit hooks to block schema violations.

---

## CI/CD

- **validate.yml** runs on PRs: schema check, broken link scan, front-matter lints, `mypy`, and sample solution tests.  
- **Required checks:** must pass before merge; no red builds into `main`.  
- **Release cadence:** tag modules when a full 7-layer set is green.

---

## Contributing

1. Pick an open issue or propose a new question set with chapter mappings.  
2. Follow the **Question File Schema** and **Layer counts** exactly.  
3. Add tests (where code is expected) under `tests/<module>/<layer>/`.  
4. Run `scripts/validate_qna.py`; fix any violations.  
5. Open a PR with a crisp rationale (“what misconception this detects,” “what production failure this prevents”).

**Review will be adversarial**—expect pushback on ambiguity, low signal, or theoretical busywork.

---

## Usage Modes

- **Solo study:** Attempt by layer, time-box per file’s `estimated_time_min`, then review solutions + rationale.  
- **Mock interviews:** Use L3–L7 only; enforce constraints verbally and with a shared editor.  
- **Team upskilling:** Assign modules by chapter coverage; rotate reviewers; track scores against rubric.

---

## Pros & Cons of This Structure (Trade-off Register)

**Pros**
- Deterministic coverage across Bloom’s levels; easy benchmarking across cohorts.
- Enforces production-grade discipline (typing, tests, resource safety).
- Modular by chapter groups; incremental adoption is straightforward.

**Cons**
- 100 Qs per module is heavy—content velocity must be managed.  
- Strict schema + CI can feel rigid for exploratory contributions.  
- Answers in a `solutions/` mirror require diligent sync (risk of drift if reviewers are lax).

---

## Roadmap

- Add **autograders** for common code prompts (signature, I/O contracts, property tests).  
- Seed **reference implementations** per module for baseline scoring.  
- Publish **difficulty calibration** using anonymized attempt analytics.

---

## Attribution & License

- **Book Reference:** *Fluent Python, 2nd Edition* by Luciano Ramalho. This repository contains **original assessments inspired by the book’s topics**, not reproductions of copyrighted text.  
- **License:** MIT for repository content. Contributors retain copyright to their submissions, licensed under MIT upon merge.

---

## Quick Start Checklist

- [ ] Select a module (e.g., `module-05-iterators`).  
- [ ] Author **exactly 100** questions across Layers 1–7 per the counts.  
- [ ] Provide matching solutions under `solutions/`.  
- [ ] Add or update tests.  
- [ ] Pass `validate_qna.py` and CI.  
- [ ] Open PR with a concise, evidence-backed rationale.

> If it doesn’t hold in production, it doesn’t belong here.
