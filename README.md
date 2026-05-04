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

## Based on

Verified papers from ICSE 2025 and 2026 Research Track, including InferROI, TaintP2X, ReinFix, SAST Tools for Python, and others in SAST + LLM + program analysis.
