# ICSE Writing Skill

A custom skill for [OhMyOpenCode](https://github.com/code-yeongyu/oh-my-opencode) that encodes structural conventions, narrative patterns, evidence boundaries, and writing discipline from verified **ICSE 2025/2026 Research Track** papers.

Designed for software engineering papers combining LLMs with static/program analysis, vulnerability detection, code graphs, and false-positive mitigation.

## What's inside

- **Venue profile**: acceptance rate, format, page budget, style conventions
- **Structural conventions**: abstract → intro → motivating example → approach → evaluation → related work → discussion → conclusion
- **Hybrid LLM+static analysis framing**: two-phase decomposition patterns
- **ICSE evidence sourcing rules**: what counts as ICSE Research Track vs. SEIP/workshop/NIER/arXiv
- **Writing style**: active voice, claim discipline, terminology consistency
- **Pre-results vs post-results rules**: what to write before and after experiments
- **Anti-patterns**: common ICSE paper writing mistakes to avoid

## Install

```bash
# Project-level
cp SKILL.md .opencode/skills/icse-writing/SKILL.md

# Or user-level
cp SKILL.md ~/.config/opencode/skills/icse-writing/SKILL.md
```

## Usage

```python
task(
    category="writing",
    load_skills=["icse-writing"],
    prompt="Rewrite the introduction of my ICSE paper..."
)
```

Combine with `academic-writing-refiner` and `research-paper-writer` for full paper drafting.

## Evidence Sourcing Convention

### Primary evidence: what can be called "ICSE Research Track"

Only papers with a verified official ICSE Research Track page (e.g., `https://conf.researchr.org/details/icse-2025/icse-2025-research-track/<number>/`) may be used as ICSE Research Track evidence.

### Downgraded sources: label honestly

| Source type | How to cite in prose |
|---|---|
| ICSE SEIP | "an industrial study" or "in an ICSE SEIP paper" — never "ICSE Research Track" |
| ICSE NIER | "an ICSE NIER paper" — never Research Track |
| Workshop paper | "in a workshop paper" — never ICSE |
| Journal-first (TSE → ICSE) | "a journal-first paper at ICSE" — never Research Track |
| arXiv-only | "an arXiv preprint" — never ICSE |
| Non-ICSE venue | Cite by actual venue (USENIX, ICLR, etc.) |

### Primary ICSE Research Track exemplars

| Paper | Year | Key pattern |
|---|---|---|
| InferROI (Wang et al.) | 2025 | LLM inference + static analysis verification hybrid |
| Code Language Models: How Far Are We? (Ding et al.) | 2025 | Dataset caution, quantitative-claim discipline |
| Nondeterminism in SA Tools (Miao et al.) | 2025 | Static analysis reliability and threats framing |
| ROCODE | 2025 | Repository-level code understanding and evaluation scope discipline |
| npm Malicious Packages (Zahan et al.) | 2025 | Static pre-screening + LLM security review hybrid |
| SAST Tools for Python (Liu et al.) | 2026 | SAST tool limitations and empirical framing |
| LLM Vulnerability Discovery via Code Metrics (Weissberg et al.) | 2026 | Caution against shallow LLM vulnerability reasoning |
| LLM-Aided Partial Program Dependence Analysis (Rong et al.) | 2026 | LLM-aided dependence context |
| TaintP2X | 2026 | Static taint analysis + LLM-assisted FP pruning |
| Out of Distribution Out of Luck | 2026 | Distribution shift, dataset scope, and external-validity framing |
| ReinFix (Zhang et al.) | 2026 | Static analysis retrieves ingredients for LLM reasoning |
| LoopRepair | 2026 | Repair-system design choices, case studies, and threats framing |
| Rethinking AVR | 2026 | Memorization versus generalization in automated vulnerability repair |
| Vulnerability Data Generation | 2026 | Benchmark/data generation scope and label-quality threats |
| SymRadar | 2026 | Symbolic reasoning, vulnerability localization, and evidence ranking |
| Repairing LLM Executions | 2026 | LLM execution repair, iterative feedback, and failure analysis |
| INTENTFIX | 2026 | Intent-grounded repair and semantic constraint framing |
| BFix | 2026 | Bug-fix generation, validation boundaries, and repair evaluation |
