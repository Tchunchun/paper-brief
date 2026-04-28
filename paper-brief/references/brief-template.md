# Brief Template — Paper Brief Skill

The canonical **skill output specification** for every generated brief. Use this structure exactly unless the user requests Signal Scan mode.
Annotations in [brackets] are instructions — remove them from actual output.

Field placement is fixed:
- **Trust level** belongs to 🔬 The Proof.
- **Confidence** and **Time horizon** belong to 📦 The Opportunity.
- **Recommendation** belongs to ❓ The Next Move.
- **Research limitations** are reading-derived. **Context-fit questions** are prompts for what the user or team must validate.

---

## Single Audience Brief

```markdown
# Paper Brief: [Full Paper Title]
### [Authors · Institution · Date · arXiv/DOI link if available]

**Trust level:** Strong / Medium / Weak / Too early
**Audience:** [Audience emoji + label]
**Brief mode:** Signal Scan / TPM Brief / Technical Review / Plain-English Brief

---

## 🎯 The Problem
[2–4 sentences. What's broken. Who experiences it. Why it hasn't been fixed before. Why now.]

*Key signal: [One sentence — the most important takeaway from this lens for this audience.]*

---

## 💡 The Insight
[1–3 sentences. The single clever idea in plain English. Why it works when prior approaches didn't.]

*Key signal: [One sentence.]*

---

## 🔬 The Proof
**Trust level: Strong / Medium / Weak / Too early**

[Key results. The most important number and what it means. What makes the evidence credible — or not. Audience-calibrated framing.]

**Why this trust level:**
[Name the one or two trust drivers that most affected the rating. Do not silently average all possible criteria. Examples: decisive ablation, weak baseline, narrow benchmark, missing code, strong held-out generalization.]

**Evidence labels:**
- **Paper-supported:** [Directly stated or measured claims]
- **Inferred:** [Reasonable implications not directly tested]
- **Speculative:** [Future implications with limited support]
- **Needs validation:** [Claims or assumptions that must be checked in the reader's context]

*Key signal: [One sentence.]*

---

## 🚨 The Catch
**Research limitations:**
[What the paper does not prove, did not test, or may overclaim.]

**Context-fit questions:**
[Questions the reader's team must answer about their own data, infra, latency budget, cost, compliance, users, or operations. If the user provided enough context, include clearly labeled context-specific risk hypotheses; otherwise do not invent generic risks.]

**Needs validation:**
[The most important assumptions to test before acting.]

*Key signal: [One sentence.]*

---

## 📦 The Opportunity
**Confidence: High / Medium / Low / Too early**
**Time horizon: Now / Next / Later / Skip**

[What this opens up — for this specific audience. Concrete, not generic. Named action direction.]

*Key signal: [One sentence.]*

---

## ❓ The Next Move
**Recommendation: Act now / Prototype / Ask the team / Monitor / Ignore for now**

1. [First action / question — specific, not generic]
2. [Second action / question]
3. [Third action / question]

*Key signal: [One sentence — the single most important thing to do or think about as a result of reading this paper.]*

## What to ignore
[Optional for time-constrained professional audiences. Name the technical sections or details that are safe to skip unless implementation is planned.]
```

---

## All-Audiences Brief (Combined)

When generating briefs for all 6 audiences in one document:

```markdown
# Paper Brief: [Full Paper Title]
### [Authors · Institution · Date · arXiv/DOI link]

**Trust level:** Strong / Medium / Weak / Too early
**Brief mode:** [Mode used]
**Tags:** [comma-separated topic tags]

---
---

# 💼 PM / TPM Brief

[Full 6-lens brief for PM audience]

---
---

# ⚙️ Engineer Brief

[Full 6-lens brief for Engineer audience]

---
---

# 🎨 Designer Brief

[Full 6-lens brief for Designer audience]

---
---

# 🎓 Student Brief

[Full 6-lens brief for Student audience]

---
---

# 👨‍👩‍👧 Parent Brief

[Full 6-lens brief for Parent audience]

---
---

# 🧒 Kid Brief

[Full 6-lens brief for Kid audience]
```

---

## Annotated Example — PM Brief (Meta-Harness paper)

This example shows what a well-executed PM brief looks like. Use it as a calibration reference.

```markdown
# Paper Brief: Meta-Harness
### Stanford · MIT · KRAFTON · March 2026 · arXiv:2603.28052

**Trust level:** Strong
**Audience:** 💼 PM / TPM
**Brief mode:** TPM Brief

---

## 🎯 The Problem
LLM systems don't just depend on the model — they depend on the *harness*, the code
controlling what information the model sees at each step. The same model with a
different harness can perform 6× differently on the same task. Yet harnesses are
still designed entirely by hand. Existing automation tools fail because they compress
feedback too aggressively — they only see scores, not *why* something failed.

*Key signal: If your team ships any LLM-powered feature, you have a harness — and
you almost certainly designed it by hand.*

---

## 💡 The Insight
Instead of compressing past attempts into scores or summaries, Meta-Harness stores
everything — source code, execution traces, scores — in a filesystem the AI agent
navigates freely. This enables causal reasoning: not just "attempt 4 scored lower"
but "this failed because the prompt edit and structural fix were confounded."

*Key signal: Richer access to prior experience produces better optimization —
compression destroys exactly the diagnostic signal you need.*

---

## 🔬 The Proof
**Trust level: Strong**

Text classification: +7.7 accuracy points over best hand-crafted baseline using 4×
fewer context tokens. Math reasoning: +4.7 points on 200 IMO-level problems,
generalizing across 5 held-out models. Agentic coding: #1 ranked Haiku 4.5 agent.
The ablation is the most important result: removing execution trace access collapsed
performance from 56.7% to 41.3%. Summaries hurt vs. scores-only — directly
validating the core claim.

**Why this trust level:**
Two trust drivers dominate: the decisive ablation and the held-out generalization.
Removing execution trace access collapsed performance from 56.7% to 41.3%, and the
math result generalized across 5 held-out models. Those matter more than a generic
checklist of all evidence criteria.

**Evidence labels:**
- **Paper-supported:** The reported accuracy gains, held-out model results, and ablation drop.
- **Inferred:** Harness optimization may beat model upgrades for some team workflows.
- **Speculative:** This will generalize to every LLM product team.
- **Needs validation:** Whether your team has a discriminative eval set and harness worth optimizing.

*Key signal: The ablation showed summaries made it worse — not better. That's how
you know the full history access is the real mechanism.*

---

## 🚨 The Catch
**Research limitations:**
The proposer was only tested with one configuration, so performance with weaker
agents or different search policies is unknown.

**Context-fit questions:**
- Do we have a stable baseline harness the search can modify?
- Do we have a discriminative eval set that would reveal a real quality lift?
- Is the target task valuable enough to justify ~10M tokens/iteration and hours of search?

**Needs validation:**
Confirm that your team has a stable harness, measurable eval set, and enough task
value to justify the search cost.

*Key signal: Before committing resources, validate: do we have a well-defined
harness and a measurable eval set that could seed this search?*

---

## 📦 The Opportunity
**Confidence: Medium-High**
**Time horizon: Next**

If your team has a well-defined LLM task with a measurable eval set, a
Meta-Harness run could yield a 5–8 point quality lift. The output is readable Python
— not a black box — so your team can own it. Strategic implication: harness quality
is likely a bigger lever than your next model upgrade.

*Key signal: The harness around your model may matter more than the model itself —
and it can now be optimized automatically.*

---

## ❓ The Next Move
**Recommendation: Prototype**

1. "Do we have a harness and eval set that could seed a Meta-Harness search?"
   — This immediately tells you if you're ready to act.
2. "The ablation showed summaries hurt more than scores-only. Does that surprise
   you?" — Tests whether your scientists have read it and whether it shifts their
   mental model.
3. "Appendix D has a practical implementation checklist — is there anything on
   that list we'd struggle with?" — Surfaces real blockers before you commit.

*Key signal: Don't ask your scientists to summarize this paper — ask them
whether your current eval infrastructure could run this experiment today.*

## What to ignore
Skip the formal search mechanics unless the team is planning implementation. Focus
first on the ablation, cost profile, and whether your eval infrastructure is ready.
```

---

## Length Guidance

| Audience | Target length per lens | Total brief |
|----------|----------------------|-------------|
| PM | 3–5 sentences | ~600–800 words |
| Engineer | 4–8 sentences | ~800–1200 words |
| Designer | 3–5 sentences | ~600–900 words |
| Student | 5–8 sentences | ~900–1200 words |
| Parent | 2–4 sentences | ~400–600 words |
| Kid | 2–3 sentences + analogy | ~300–500 words |

The Kid brief should feel like reading a magazine article written for a curious 10-year-old.
The Engineer brief should feel like reading a technical blog post from a senior researcher.
Both should be equally rigorous — just at different levels of abstraction.

---

## Key Signal Rules

The Key Signal is NOT:
- A summary of the lens ("So in summary, the proof shows...")
- A generic statement ("This is an important finding")
- A repeat of the heading

The Key Signal IS:
- The one thing to carry out of this lens that you'd remember in a week
- Specific to both the lens AND the audience
- Actionable or understanding-forming
- One sentence, maximum 25 words

**Test:** If you removed everything else from the lens and kept only the Key Signal, would the reader still leave with the most important understanding? If yes — you have it.
