# Evidence Calibration Guide — Paper Brief Skill

Use this file when assigning trust levels and when writing the Proof lens.
It helps distinguish strong from weak evidence — a critical skill for honest briefs.

---

## Trust Level Assignment

Use these criteria to assign the overall trust level. Then label specific claims as **Paper-supported**, **Inferred**, **Speculative**, or **Needs validation** so the brief does not overstate what the paper actually proves.

Important: do not make the trust level feel like a black-box average across every criterion. After assigning the level, identify the **one or two trust drivers** that most affected it. Examples: decisive ablation, weak baseline, narrow benchmark, missing code/data, strong held-out generalization, or unreported compute cost.

### Strong Evidence
All of these should be true:
- [ ] Tested across multiple domains or datasets
- [ ] Strong, current baselines (not straw-man comparisons)
- [ ] Benchmarks are realistic, not obviously saturated or disconnected from the target use case
- [ ] Results generalize out-of-distribution (OOD) — new datasets or models not seen during development
- [ ] Ablations isolate the key contribution (removing the key ingredient degrades performance)
- [ ] Code and/or data publicly available for replication
- [ ] Compute cost and latency reported
- [ ] Limitations are stated honestly enough to support calibrated adoption decisions

### Medium Evidence
Some of these apply:
- [ ] Good results but only in one narrow domain
- [ ] Weak or outdated baselines
- [ ] Benchmarks are useful but not clearly production-representative
- [ ] No OOD generalization test
- [ ] Limited or no ablations
- [ ] No code/data release
- [ ] Unclear production relevance

### Weak Evidence
Multiple of these apply:
- [ ] Only academic benchmarks (SWE-Bench, HumanEval, etc.) — no real-world tasks
- [ ] No baseline comparison, or trivially easy baselines
- [ ] Highly specific conditions that won't generalize
- [ ] No ablations at all
- [ ] Improvement is statistically significant but practically tiny
- [ ] Single dataset, single domain

### Too Early
- Conceptual or theoretical paper with no empirical results
- Early preprint with clearly preliminary experiments
- Proof-of-concept with no comparison

---

## Evidence Labels

Use labels when writing the Proof, Catch, and Opportunity sections for any audience. The label language can be simplified for parent and kid briefs, but the distinction must remain.

| Label | Meaning | Use when |
|---|---|---|
| **Paper-supported** | Directly stated or measured in the paper | Reporting results, ablations, limitations, datasets, or methods |
| **Inferred** | Reasonable implication based on the paper, but not directly tested | Connecting results to product or engineering implications |
| **Speculative** | Possible future implication with limited support | Describing long-term opportunities or broad market impact |
| **Needs validation** | Important claim that must be checked in the reader's context | Applying the paper to a specific product, codebase, user group, or roadmap |

Rule: if a claim affects roadmap, staffing, user trust, production cost, or system architecture, it should be either paper-supported or explicitly marked as needing validation.

Context rule: adoption fit is rarely paper-supported. Unless the user provides their system context, convert adoption concerns into **Needs validation** questions rather than generic risk statements.

---

## Reading Results Tables

### What to look for

**The key number:** Find the single result that most directly validates the core claim. Not the best-looking number — the most relevant one.

**The delta:** How much better is the new method vs. the next-best baseline? Rule of thumb:
- <2% improvement: small — may not matter in practice
- 2–5% improvement: meaningful in most settings
- 5–10% improvement: substantial
- >10% improvement: large — look carefully, may be cherry-picked

**Statistical vs. practical significance:** A result can be statistically significant (p < 0.001) and practically irrelevant (0.1% improvement). Always ask: is this big enough to matter in the real world for this application?

**The ablation result:** The most important row in any table. If removing the key ingredient of the method causes performance to collapse, the contribution is real. If performance barely changes, be skeptical.

Example to calibrate against (from Meta-Harness):
- Scores only: 41.3% best
- Scores + summary: 38.7% best ← summaries hurt!
- Full Meta-Harness: 56.7% best

The 15-point gap between full and ablated, AND the fact that summaries hurt vs. scores-only — both validate the core claim that full history access is the real mechanism.

### Red flags in results

**Cherry-picking symptoms:**
- Only one metric reported (accuracy) when others (latency, cost) would tell a different story
- Best result across many runs reported, not mean ± std
- Comparison only against methods the authors implemented (not authors' official implementations)
- Test set used during development (overfitting)

**Weak baseline symptoms:**
- Baseline is "zero-shot" when few-shot is standard
- Baseline is a 2-year-old method when newer ones exist
- Baseline is the authors' own prior work (convenient)

**Generalization concerns:**
- Only tested on data from the same distribution as training
- Only tested with the model used during development (not held-out models)
- Only tested in one language, one domain, one task type

---

## Calibration Examples

### Strong — Meta-Harness (arXiv:2603.28052)
- Three distinct domains (text classification, math, coding)
- Strong baselines (ACE, OpenEvolve, TTT-Discover)
- OOD: 9 unseen classification datasets; 5 unseen models on math
- Ablation: scores-only 41.3%, scores+summary 38.7%, full 56.7% — confirms core claim
- Code and artifacts published
- Trust level: **Strong** ✓

### Medium — Dive into Claude Code (arXiv:2604.14228)
- Architectural analysis, not empirical performance study
- Source code verified for Tier B claims
- External behavioral findings (93% approval rate, trust trajectories) from Anthropic documentation
- Long-term effects (comprehension -17%, complexity +40.7%) from adjacent tools, not Claude Code
- 1.6%/98.4% ratio is reconstructed, not officially confirmed
- Trust level: **Medium** ✓

---

## Proof Lens Framing by Audience

The same evidence gets framed differently per audience. Use these templates:

### PM framing
> **Trust level: [level]**
> [Key result in plain English]. Trust driver 1: [ablation/generalization/baseline/etc.]. Trust driver 2 if needed: [known gap or supporting strength].

### Engineer framing
> **Technical validity: [level]**
> Baselines: [quality assessment]. Ablations: [present/absent + what they show]. Replication: [code available? what's needed?]. Compute: [reported? worth the overhead?].

### Designer framing
> **Trust level: [level]**
> Were real users tested? [Yes/No + what kind]. Were tasks ecologically valid? [Assessment]. What does a "good result" mean from the user's perspective vs. the metric's?

### Student framing
> **Trust level: [level]**
> Baseline: [the simplest comparison]. Delta: [how much better, and is it practically meaningful?]. Ablations: [what they confirm or don't]. Reproducibility: [could you do this with the information provided?].

### Parent framing
> **Is this real or hype? [assessment]**
> Did they test with real people? [Yes/No]. Was the improvement big enough to matter in daily life? [Assessment]. Is this one study or confirmed by many? [Assessment]. Who funded it? [If known and relevant].

### Kid framing
> **Did it work? [Yes/No + how well]**
> Scientists tested the idea kind of like testing a game strategy — they tried it, saw what score they got, and compared to the old way. Before: [old score]. After: [new score]. The cool proof: they [removed the key part] and the score [dropped/changed], which shows the [key idea] was really doing the work.

---

## Trust Level Communication by Audience

| Trust Level | PM says | Engineer says | Parent says | Kid says |
|-------------|---------|---------------|-------------|----------|
| Strong | "Act on this" | "Reproduce-worthy" | "This looks real" | "It really worked!" |
| Medium | "Validate first" | "Promising, prototype carefully" | "Interesting but more studies needed" | "It mostly worked" |
| Weak | "Watch, don't act" | "Methodology concerns" | "Be skeptical" | "Scientists aren't sure yet" |
| Too early | "Too early" | "Interesting direction, no data yet" | "Too soon to know" | "Scientists are still figuring it out" |

---

## Recommendation Mapping for Professional Briefs

Use the trust level plus context relevance to choose the Next Move recommendation.

| Recommendation | Evidence condition | Context condition |
|---|---|---|
| **Act now** | Strong evidence | Directly relevant to current planning, with enough user-provided context to make fit plausible |
| **Prototype** | Strong or Medium evidence | Relevant, but internal fit or cost needs a small experiment |
| **Ask the team** | Medium evidence or mixed signals | Applicability depends on internal system, data, infra, or user context |
| **Monitor** | Medium, Weak, or Too early | Interesting but not aligned to current roadmap or too immature |
| **Ignore for now** | Weak evidence or poor fit | Low relevance, poor applicability, or known blocker makes action wasteful |

Do not recommend **Act now** unless the paper's evidence is strong *and* the reader has provided enough context to make near-term fit plausible. If context is missing, prefer **Ask the team** or **Prototype** and state the context-fit questions explicitly.
