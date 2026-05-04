---
name: icse-writing
description: Write and revise software engineering papers targeting ICSE Research Track. Encodes structural conventions, narrative patterns, evidence boundaries, and writing style from verified ICSE 2025/2026 Research Track papers in SAST, LLM+program analysis, vulnerability detection, and false-positive mitigation. Use when the user asks to write, revise, restructure, or polish a paper targeting ICSE, or when they mention ICSE Research Track, SE conference writing, or need ICSE-style structural guidance.
---

# ICSE Research Track Paper Writing

This skill encodes the structural conventions, narrative patterns, and writing discipline observed in verified ICSE 2025/2026 Research Track papers. It is designed for software engineering papers, particularly those combining LLMs with static/program analysis, vulnerability detection, code graphs, and false-positive mitigation.

## Core Philosophy

ICSE Research Track papers share a common expectation: every claim about a system's behavior, performance, or contribution must be tied to evidence. Good ICSE papers do not persuade through vocabulary — they persuade through clear problem framing, concrete motivating examples, explicit contribution lists, and results anchored in numbers. When results do not yet exist, the paper must frame contributions as design/method contributions without pretending to have empirical validation.

This means:
- **Problem first**: Always establish a concrete, specific gap before describing the approach. Generic "prior work is insufficient" is not enough — show exactly what fails through a motivating example.
- **Evidence-bound claims**: Never write "our approach significantly improves" without numbers. Never write "evaluation protocol" as if it were a result. Either have results, or frame the paper as a design/method contribution with deferred validation.
- **Hybrid framing**: When combining LLMs with static analysis, always describe the LLM as providing semantic reasoning/context organization, and static analysis as providing deterministic grounding/verification — not one replacing the other.
- **Late related work**: ICSE systems and empirical papers conventionally place Related Work after the method and before the conclusion, or after the evaluation. Do not default to Literature Review-style early related work unless the paper is a survey.

## ICSE Venue Profile

| Attribute | ICSE 2025/2026 Research Track |
|---|---|
| Acceptance rate | ~21-22% |
| Review type | Double-anonymous |
| Format | IEEE Conference Proceedings (two-column, 10pt) |
| Page budget | 10 pages + 2 for references (typical) |
| Style | Active voice ("we"), first-person plural, past tense for completed work |
| Contribution level | 3-5 contributions; avoid 7+ item lists |
| Evaluation expectation | Empirical results with RQs, baselines, metrics, and threats; design papers allowed but weaker without results |
| Related Work position | After method or after evaluation; rarely at the beginning |

## Structural Conventions

### Abstract: Problem → Gap → Named Approach → Mechanism/Result

Every ICSE abstract in our verified corpus follows this four-part structure:

1. **Problem/motivation** (1-2 sentences): The real-world importance.
2. **Limitation/gap** (1-2 sentences): What existing approaches fail to do.
3. **Proposed approach** (2-3 sentences): The novel technique, named tool.
4. **Mechanism or key results** (2-3 sentences): What the approach achieves, with numbers when available.

```
Example (InferROI, ICSE 2025):
[Problem] Resource leaks cause performance issues...
[Gap] Existing static detection techniques suffer from both false negatives and false positives...
[Approach] We propose InferROI, which leverages LLMs to directly infer resource-oriented intentions...
[Results] Experimental results demonstrate 59.3% and 62.5% bug detection rate... identifies 29 unknown resource leak bugs
```

Pre-results adaptation: Replace the results slot with mechanism description (what the design does, not how well it performs) and omit quantitative claims.

### Introduction: Motivation → Gap → Named Approach → 3 Contributions → Roadmap

- Open with a concrete problem, not a definition. The first paragraph should make the reader understand why this matters in practice.
- State the gap explicitly: what prior work does, and what specific capability is missing.
- Name the approach early (by the second or third paragraph).
- End with exactly 3-5 numbered contributions. Each must be a specific, checkable claim about the work.
- The final paragraph is a roadmap: "Section 2 presents... Section 3 describes..."

### Contributions: What counts as one

Acceptable ICSE contributions:
- A new technique, tool, or system design.
- An empirical finding that changes understanding (surprising result, debunking, large-scale study).
- A new dataset or benchmark that enables future work.
- A conceptual reframing of a known problem with design consequences.

NOT acceptable as stand-alone contributions:
- Implementation details (e.g., "we used LangGraph").
- Evaluation protocols or planned measurements without actual results.
- Future work or deferred validation.
- "We built a system" without specifying the design novelty.

### Motivating Example: Early, Concrete, Threaded Through

Place a concrete motivating example in the Introduction or early in the approach. Best practices from ICSE papers:

- Show a specific code snippet, alert, or failure case.
- Demonstrate why naive or existing approaches fail with this example.
- Thread the example through the paper: refer back to it in design goals, challenges, approach description, and evaluation.
- Always include a boundary sentence: "The case is used as a motivating example rather than empirical evidence."

### Approach Section: Two-Phase Hybrid Decomposition

For papers combining LLMs with static analysis, the ICSE convention is a two-phase decomposition:

1. **LLM inference phase**: Describes how the LLM is prompted, what it extracts/infers, and its role in the workflow. The LLM should be framed as a semantic organizer, hypothesis proposer, or evidence requester — not as an oracle.
2. **Static analysis verification phase**: Describes how traditional program analysis validates, refines, or acts on LLM output. This phase provides determinism, precision, and grounding.

Language conventions:
- Use "ground," "check," "verify," "support," or "bound" — never "prove," "guarantee soundness," or "establish correctness" unless the paper contains a formal proof.
- When describing weight or parameter choices, call them "implementation heuristics" not "empirically optimized parameters" unless tuned on held-out data.

### Evaluation: RQ-Driven When Results Exist

Standard ICSE evaluation structure:
1. Research Questions (RQs): 3-5 explicit questions.
2. Experimental Setup: datasets (with exact counts), baselines, metrics (precision, recall, F1, uncertain rate...).
3. Results: answer each RQ with tables and answer-to-RQ paragraphs.
4. Ablation Study: a dedicated subsection showing which components matter.
5. Case Studies: qualitative analysis of representative cases (FP, TP, uncertain, failure).

Pre-results rule: Do NOT substitute "evaluation protocol" or "evaluation design" for real results in the paper body. Either:
- Have results and write a real Evaluation section.
- Do not have a visible Evaluation section; state explicitly in the paper that results are deferred and reserve the section for post-results insertion.

### Related Work: Late, Thematic, Comparative

- Place Related Work after the method or after the evaluation. ICSE convention is post-evaluation for systems/empirical papers.
- Group by theme (e.g., SAST false-positive mitigation, LLMs for vulnerability analysis, LLM + static analysis hybrids, graph/CPG evidence and grounding).
- Never list papers one by one in "X did A. Y did B. Z did C." style.
- Each paragraph ends by distinguishing the current paper from that theme: "Unlike these approaches, FPMAgent..."
- Use the hedge "in the systems we reviewed" rather than claiming "no prior system has ever..."

### Discussion: Construct / Internal / External / Conclusion Validity

Standard ICSE threats structure:
- Construct validity: do metrics/labels measure what they claim?
- Internal validity: could the results be caused by something other than the claimed contribution?
- External validity: do findings generalize beyond the studied setting?
- Conclusion validity: are statistical claims supported?
- Reproducibility: what artifacts, hashes, model versions are needed?

### Conclusion: Contributions Restated, No New Claims

- Restate the 3 contributions (not the whole paper).
- Acknowledge limitations honestly.
- Suggest concrete next steps that follow from the current work.
- Never introduce new claims, results, or contributions in the conclusion.

## Evidence Sourcing Convention

### Primary evidence: what can be called "ICSE Research Track"

Only papers with a verified official ICSE Research Track page (e.g., `https://conf.researchr.org/details/icse-2025/icse-2025-research-track/<number>/`) may be used as ICSE Research Track evidence. The paper must have been accepted to and presented at the ICSE Research Track.

### Downgraded sources: label honestly

| Source type | How to cite in prose |
|---|---|
| ICSE SEIP | "an industrial study" or "in an ICSE SEIP paper" — never "ICSE Research Track" |
| ICSE NIER | "an ICSE NIER paper" — never Research Track |
| Workshop paper | "in a workshop paper" — never ICSE |
| Journal-first (TSE → ICSE) | "a journal-first paper at ICSE" — never Research Track |
| arXiv-only | "an arXiv preprint" — never ICSE |
| Non-ICSE venue | Cite by actual venue (USENIX, ICLR, etc.) |

### Primary ICSE Research Track exemplars for this domain

These verified ICSE 2025/2026 Research Track papers can be used as structural models:

| Paper | Year | Key pattern |
|---|---|---|
| InferROI (Wang et al.) | 2025 | LLM inference + static analysis verification hybrid |
| Code Language Models: How Far Are We? (Ding et al.) | 2025 | Dataset caution, quantitative-claim discipline |
| Nondeterminism in SA Tools (Miao et al.) | 2025 | Static analysis reliability and threats framing |
| npm Malicious Packages (Zahan et al.) | 2025 | Static pre-screening + LLM security review hybrid |
| SAST Tools for Python (Liu et al.) | 2026 | SAST tool limitations and empirical framing |
| LLM Vulnerability Discovery via Code Metrics (Weissberg et al.) | 2026 | Caution against shallow LLM vulnerability reasoning |
| LLM-Aided Partial Program Dependence Analysis (Rong et al.) | 2026 | LLM-aided dependence context |
| TaintP2X | 2026 | Static taint analysis + LLM-assisted FP pruning |
| ReinFix (Zhang et al.) | 2026 | Static analysis retrieves ingredients for LLM reasoning |

## Writing Style

### Voice and tone
- Use active voice and first-person plural: "we propose," "we evaluate," "we find."
- Past tense for completed work, present tense for design description.
- No passive voice ("the system was designed to...") unless the agent is genuinely irrelevant.

### Claim discipline
- Every quantitative claim must have a number: "improves F1 by 3.2 points" not "improves performance."
- Every comparative claim must name the baseline and metric: "outperforms InferROI on recall" not "outperforms baselines."
- No hedging when claiming what the paper contributes: "In this paper, we present..." not "In this paper, we attempt to..."
- For pre-results papers: describe mechanism, not performance. "FPMAgent grounds competing hypotheses through typed claims" not "FPMAgent achieves higher accuracy."

### Terminology conventions
- Define acronyms on first use: "Hypothesis Validated Claim Graph (HVCG)."
- Be consistent: never use two names for the same component.
- Name the tool/system exactly once and use it throughout (not "our system" / "the framework" / "the tool" interchangeably).

### Table and figure conventions
- Tables for results comparisons, figures for architecture/flow.
- Every table and figure must have a descriptive caption that can stand alone.
- All tables and figures must be referenced in the text before they appear.
- Use `\begin{table}[t]` for placement; avoid `[h]` or `[H]`.

## Pre-Results vs Post-Results Rules

### Pre-results draft (experiments running, no numbers available)
- No visible Evaluation section with protocol prose.
- No "Evaluation Design," "planned datasets," "planned baselines," "future frozen experiments" as visible section content.
- Abstract: Problem → Gap → Named Approach → Mechanism (skip results).
- Introduction: contributions are design/method contributions only.
- No Scope / Non-Claims paragraph (it implies the paper is only a protocol).
- Discussion/Threats: focus on design limitations and risks that apply regardless of results.

### Post-results insertion (after experiments complete)
1. Add visible `\section{Evaluation}`.
2. Write RQs matching actual metrics.
3. Add dataset/baseline/metric tables with exact counts.
4. Add results table and answer-to-RQ paragraphs.
5. Add ablation table.
6. Update Abstract with one calibrated numeric sentence.
7. Update Introduction with one result-preview paragraph.
8. Update Conclusion with the same calibrated claim.
9. Update Discussion/Threats to reflect actual dataset, model nondeterminism, and missing/uncertain cases.

## Anti-Patterns

Do NOT:
- Begin a paper with "With the rapid development of..." or "In recent years..."
- Use "leverage" when "use" works, "utilize" when "use" works, "elucidate" when "explain" works.
- Hedge excessively: "it could potentially be argued that this might possibly indicate..." — qualify appropriately, then commit.
- Add Scope / Non-Claims paragraphs as a substitute for missing results.
- Present an evaluation protocol as a paper section or contribution.
- Cite arXiv-only, workshop, SEIP, or NIER papers as ICSE Research Track.
- Invent author names, DOI values, page numbers, or venue metadata.
- Use qualitative-only claims when quantitative evidence is expected.

## Loading This Skill

```python
task(
    category="writing",
    load_skills=["icse-writing"],
    prompt="Rewrite the introduction of my ICSE paper following the Problem → Gap → Named Approach → 3 Contributions structure..."
)
```

Combine with `academic-writing-refiner` and `research-paper-writer` for full paper drafting and polishing.
