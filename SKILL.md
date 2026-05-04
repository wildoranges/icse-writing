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

## Section-by-Section Deep Dives

### 1. Abstract

ICSE Research Track abstracts usually run 150 to 250 words and work best as a compact, self-contained argument. Use the four-part template: Problem → Gap → Approach → Result or Mechanism. For pre-results papers, replace the final result sentence with a concrete mechanism sentence. A strong ICSE abstract often has 5 to 7 sentences:

1. **Problem sentence**: State the software engineering problem and why it matters. Keep it grounded in practice.
2. **Gap sentence**: Explain what current tools, methods, datasets, or evaluations miss.
3. **Approach sentence**: Name the proposed method, study, framework, or benchmark. If the paper has a named system, introduce it here.
4. **Mechanism sentence**: Explain the core technical idea.
5. **Evaluation sentence**: State the evaluation setting (datasets, benchmarks, subject systems, tools, RQs).
6. **Result sentence**: Give the main quantitative or qualitative finding with concrete numbers when available.
7. **Implication sentence**: State what the result means for researchers, tool builders, or practitioners.

Pre-results variant replaces Result with Mechanism and skips numbers.

**Do's**: Use 150-250 words. Make abstract self-contained. Define every acronym. Name the method. Include evaluation scale. Use active voice. Put strongest result near end. Make final sentence about implication.

**Don'ts**: No citations. No undefined acronyms. No broad opening ("Software is everywhere"). No vague result language ("promising", "effective"). No listing all contributions mechanically. No claims the paper doesn't prove.

### 2. Introduction

ICSE Research Track introductions commonly use 5 to 7 paragraphs:

- **P1 Problem and motivation**: Open with a concrete SE problem. Good ICSE introductions begin with a real task or failure mode. Avoid generic statements.
- **P2 Gap**: State the missing capability. A strong gap: current methods can do A, but they fail under condition B, and this matters because B is common.
- **P3 Named approach**: Introduce the paper's main artifact/study/method by name. State the core idea in one paragraph.
- **P4-P5 Contributions**: Use 3-5 contribution items. Each must be evidence-bound. What counts: new method, tool, benchmark, dataset, empirical finding, reproducible artifact, validated improvement. What doesn't count: literature review, background, implementation without evaluation, restating method title.
- **P6 Result preview**: Post-results: headline quantitative result. Pre-results: planned evaluation scope.
- **P7 Roadmap**: One or two sentences. Keep it short and conventional.

**Do's**: 5-7 paragraphs. Concrete problem first. Move quickly to gap. Name approach early. 3-5 contributions. Evidence-bound claims. Active voice.

**Don'ts**: No broad software platitudes. No long history of the field. No hiding the approach. No more than 5 contributions. No claiming generality from narrow evidence. No roadmap that introduces new content.

### 3. Background / Motivation / Challenges

Use this section to deepen the problem. 3 to 5 paragraphs. Should not repeat the Introduction.

- **P1 Concrete problem context**: Reframe the problem from a concrete perspective. Explain what makes the task difficult in practice. Narrower than Introduction.
- **P2-P4 Explicit challenges**: Present 2-3 challenges. Each includes: technical obstacle, concrete manifestation in running example, why naive solutions fail, and design pressure created. Good challenge types for LLM+static analysis papers: noisy program evidence, missing semantic context, LLM overreach, scalability limits, precision-recall tension, verification gap.
- **Final paragraph Challenge-to-design-goal bridge**: Map each challenge to a design goal explicitly. Make the Approach section feel inevitable.

**Running example discipline**: Introduce one example in P1. Reuse in each challenge. Show how each challenge appears. Keep concrete: name artifact type, failure mode, decision needed.

**Pattern anchors**: InferROI (two-phase LLM inference then static verification). TaintP2X (taint analysis + LLM pruning). LLM-Aided Partial Program Dependence Analysis (compact partial program evidence). ReinFix (static retrieval then LLM reasoning).

**Do's**: Concrete challenges. Running example threaded. Design goal mapping. Precise static analysis limits. Precise LLM limits. Measured language ("ground", "check", "support").

**Don'ts**: No restating Introduction. No generic challenges. No challenges method doesn't address. No "proves correctness" claims. No framing LLM as oracle. No survey-style multiple examples.

### 4. Approach / Methodology / System Design

Explain how the system works. Concrete but not an implementation manual.

**Typical subsections**: 4.1 Design Goals (operational, from challenges). 4.2 Overview (full pipeline, input/output, figure). 4.3 Stage 1 Evidence/Retrieval/Pruning. 4.4 Stage 2 LLM Reasoning. 4.5 Stage 3 Static Checking/Verification (if applicable). 4.6 Implementation Boundary.

**Two-phase decompositions for LLM+static analysis**:
- LLM then static verification (InferROI pattern)
- Static analysis then LLM pruning (TaintP2X pattern)
- Partial program analysis then LLM reasoning (LλMDA pattern)
- Static retrieval then LLM reasoning (ReinFix pattern)

**Pipeline figure conventions**: Inputs left, outputs right. Static analysis and LLM visually distinct. Label intermediate artifacts. Use same names as subsection headings. Descriptive caption.

**Algorithm/pseudocode**: Use for nontrivial control flow, filtering, ranking, iterative loops, checking procedures. Place after overview. Define inputs before, outputs after.

**Terminology rules**: Prefer "ground", "check", "support", "verify against facts". Avoid "prove", "guarantee soundness", "ensure absence", "fully understand", "eliminate hallucinations" unless formally justified.

**Weights/thresholds**: Describe as "implementation heuristics" unless empirically optimized. State when fixed across experiments.

**Artifact boundaries**: End by defining what the system implements, what it consumes/produces, what's engineering vs method, what's outside contribution boundary. Don't introduce new contribution.

**Do's**: Explicit stage boundaries. Define every intermediate artifact. Connect design goals to components. Clear LLM input/output. Pipeline figure for multi-stage. Pseudocode for loops/checking. Evidence-bound terminology. End with artifact boundary.

**Don'ts**: No "we ask an LLM" if pipeline is the contribution. No hiding static analysis. No unsupported guarantees. No figure-text name mismatch. No undefined algorithm artifacts. No over-explaining prompts while under-explaining evidence. No new contribution at end.

### 5. Evaluation / Experiments / Results

Prove central claims with numbers, controlled comparisons, and error analysis.

**Subsection order**:
1. **Experimental Setup**: Datasets, benchmarks, tools, models, hardware, prompts, seeds, timeouts, filtering, labeling. Name all baselines. Define every metric. Report runs and aggregation for nondeterministic pipelines.
2. **Research Questions**: 3-5 RQs. Each maps to one main claim. Evaluable questions.
3. **Results per RQ**: Each RQ gets own subsection. Start with one-sentence summary. Present table/figure. Explain trends. End with explicit **Answer to RQn** paragraph.
4. **Ablation Study**: Compare full method against variants removing one component. Same datasets, metrics, protocol. Each ablation tests a real design claim. Report effect as number. Explain gains and tradeoffs.
5. **Case Studies**: One clear FP, one clear TP, one uncertain, one failure. For each: project source, warning type/CWE, code context, tool output, method output, ground truth, what it teaches.

**Pre-results vs post-results**: NO visible Evaluation section with only protocol prose when results aren't ready. Either have numbers or reserve the section. After numbers: every claim includes named method, metric, numeric value, dataset.

**Metrics table**: Compact table with Metric/Definition/Unit/Direction/Used for before first result. Results comparison table per major RQ with Dataset/Method/Baseline category/Precision/Recall/F1/Runtime columns.

**Table/figure conventions**: Tables for comparisons, figures for trends. Reference before appearing. Descriptive captions. Bold best value when fair. Report negative results.

**Do's**: 3-5 RQs answered explicitly. Setup before results. Named baselines. Numbers in every comparison. Same metrics for full method and ablations. Effectiveness AND efficiency. Root cause analysis. Nondeterminism controls. Case studies explain why.

**Don'ts**: No evaluation-protocol-only section. No improvement claim without baseline+metric+number. No mixed datasets/metrics across baselines. No multi-component ablation without justification. No averages-only reporting. No cherry-picked cases. No hiding failures. No single-run results for nondeterministic tools. No invented results.

### 6. Related Work

Position the paper, not survey the field. Place AFTER method or evaluation.

**Placement rule**: After Method or Evaluation. Do NOT place before the approach. Introduction may include gap paragraph with key citations.

**Subsection structure**: 3-5 thematic groups (NOT one per paper). Themes: static analysis/SAST, false positive mitigation, LLMs for vulnerability, hybrid LLM+program analysis, nondeterminism/reproducibility, benchmarks/datasets.

**Paragraph structure per theme**: (1) 2-3 sentences describing theme. (2) 1-2 distinguishing sentences. (3) Comparative ending.

**Source labeling**: Label by actual venue (ICSE 2026 Research Track, ICSE SEIP, ICSE NIER, workshop, journal-first, arXiv preprint). Never call SEIP/workshop/NIER an "ICSE Research Track paper."

**Evidence boundary**: Primary evidence: ICSE/FSE/ASE/ISSTA Research Track. Background: SEIP, workshop, NIER, journal-first, arXiv, tool docs.

**Anti-laundry-list rule**: Synthesize, don't list. If a paragraph can be reordered sentence by sentence without changing meaning, it's a laundry list.

**Do's**: Late placement. 3-5 thematic groups. Theme-first paragraphs. Comparative endings. Actual venue labels. ICSE RT papers as primary evidence. Specific differences.

**Don'ts**: No early long Related Work. No one-paper-per-paragraph. No citation laundry list. No SEIP/workshop as primary evidence. No calling everything "ICSE". No implying prior paper studied something it didn't. No generic "our work is different". No attacking prior work.

### 7. Discussion / Limitations / Threats to Validity

Show understanding of boundaries. Honest but not self-defeating. Name limit, consequence, mitigation.

**Structure**: Short Discussion subsection then Threats to Validity. 1-2 paragraphs per validity type.

**Validity taxonomy**:
- **Construct Validity**: Does the study measure what it claims? Label quality, duplicate examples, data leakage, metric fit, evaluation setting realism.
- **Internal Validity**: Can the effect be attributed to the proposed method? Implementation correctness, baseline fairness, parameter selection, prompt construction, data preprocessing, nondeterminism controls.
- **External Validity**: Where do findings generalize? Language, project type, task type, bug class, code size, benchmark source, model family, tool family. Separate capability claims from deployment claims.
- **Conclusion Validity**: Does analysis support conclusions? Sample size, effect sizes, confidence intervals, statistical tests, variance, ablation design, negative results.
- **Reproducibility**: What artifacts are released? Code, datasets, scripts, prompts, raw outputs, logs, Docker images, model identifiers, hashes. For nondeterministic systems: don't promise bit-exact reproduction. Support auditable reproduction instead.

**Nondeterminism**: Treat as first-class concern, not footnote. Report runs, settings, versions, variance, aggregation rule.

**Pre-results vs post-results**: Pre-results: design limitations and risks regardless of numbers. Post-results: tie threats to actual measured outcomes.

**ICSE pattern anchors**: Nondeterminism studies (treat as measurable behavior), code model vulnerability studies (question dataset quality), AVR rethinking studies (separate memorization from generalization), LoopRepair-style (Discussion for design choices, Threats for systematic risk).

**Do's**: Validity taxonomy. 1-2 paragraphs per type. Name limitation + consequence. Connect threat to mitigation. Dataset scope boundaries. Nondeterminism controls. Calibrated claims.

**Don'ts**: No generic checklist. No self-defeating tone. No claimed generality beyond evidence. No hiding data leakage or label noise. No treating exact match as perfect. No new results in threats. No exact reproducibility promises for hosted systems.

### 8. Conclusion

Close the paper. 3-4 paragraphs. More specific than abstract, less detailed than results.

- **P1**: Restate problem and approach (1-2 sentences). Don't repeat full motivation.
- **P2**: Restate 3 contributions succinctly in compressed prose. Mirror Introduction contributions, not copy.
- **P3**: Acknowledge limitations (1 compact paragraph). Steady tone: limitation narrows claim, doesn't erase contribution.
- **P4 (optional)**: Future work. Grounded in results and limitations. Don't promise unrelated research agenda.

**Pre-results vs post-results**: Pre-results: close with mechanism significance. Post-results: close with calibrated numeric claim with scope.

**No new claims rule**: Conclusion can't introduce new datasets, baselines, metrics, case studies, explanations. Every claim must already be supported.

**Do's**: 3-4 paragraphs. Problem+approach in P1. Three contributions in P2. Calibrated limitation in P3. Grounded future work in P4. Confident, precise, bounded tone.

**Don'ts**: No repeating abstract sentences. No new results/interpretations. No overpromising. No vague impact language. No apologizing. No final sentence broader than evidence.

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
