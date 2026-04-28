---
name: paper-brief
description: Create audience-adaptive research paper briefs using the 6-Lens Framework. Use when asked to explain, summarize, understand, or translate a paper for PM/TPM, engineer, designer, student, parent, or kid audiences. Produces trust level, evidence labels, limitations, context-fit questions, opportunity, and next move; not for generic article summaries.
license: Proprietary
compatibility: Markdown-only skill. Works with pasted papers, uploaded PDFs, abstracts, arXiv/DOI links, and extracted paper text when available.
metadata:
  version: "2.2.0"
---

# Paper Brief Skill

## Overview

Transforms any research paper into audience-adaptive, evidence-calibrated briefs using the **6-Lens Framework v2.2**. One paper. Six lenses. Multiple audiences. The skill is not generic summarization: it turns research into calibrated understanding, explicit limitations, context-fit questions, opportunity, and a next move.

---

## Core Concept

Every research paper is answering a question nobody had fully answered before. The reader's job is not to understand every detail — it's to extract what *they* need. What they need depends entirely on who they are.

This skill applies the same six questions to every paper, adapts the answers per audience, and outputs a structured brief. For product contexts, the beachhead audience is the AI/ML TPM or PM who needs research-to-understanding translation in under 30 minutes.

---

## The 6 Lenses (Universal — Never Change)

| # | Lens | Universal Question |
|---|------|--------------------|
| 🎯 | **The Problem** | What broken thing is this fixing — and does it affect me? |
| 💡 | **The Insight** | What's the single clever idea at the heart of this? |
| 🔬 | **The Proof** | Did it actually work — and how much should I trust that? |
| 🚨 | **The Catch** | What doesn't it prove, and what could still go wrong? |
| 📦 | **The Opportunity** | What does this open up — for me specifically? |
| ❓ | **The Next Move** | What do I do or think about differently because of this? |

The lenses never change. What changes per audience: vocabulary, depth, framing, trust calibration language, and the target of "The Next Move."

For professional audiences, the lenses should produce a next-move recommendation — not just comprehension:

| Recommendation | When to use it |
|---|---|
| **Act now** | Strong evidence, high relevance, and clear near-term implication. |
| **Prototype** | Promising evidence, but requires a small internal experiment before commitment. |
| **Ask the team** | Important implication depends on internal system, data, infra, or product context. |
| **Monitor** | Interesting signal, but too early, narrow, or outside the current roadmap. |
| **Ignore for now** | Weak evidence, low relevance, or poor fit for the audience's context. |

Use evidence labels across all audience outputs whenever they help prevent overclaiming. Adapt the wording to the audience, but keep the distinction intact:

- **Paper-supported** — directly stated or measured in the paper
- **Inferred** — reasonable implication based on the paper, but not directly tested
- **Speculative** — possible future implication with limited support
- **Needs validation** — important claim that must be checked in the reader's context

---

## Supported Audiences

| ID | Audience | Mindset |
|----|----------|---------|
| `pm` | 💼 PM / TPM | Making product decisions. Is this worth acting on, and when? |
| `eng` | ⚙️ Engineer | How does it work? Can I reproduce or build on it? |
| `des` | 🎨 Designer | What does this mean for how I design AI experiences? |
| `stu` | 🎓 Student | What's the contribution? How strong is the evidence? What's next? |
| `par` | 👨‍👩‍👧 Parent | Is this real or hype? Should I be concerned? What does it mean for my family? |
| `kid` | 🧒 Kid (8–12) | What was broken? What was the cool fix? Why is this exciting? |

The MVP wedge is PM/TPM. Engineer and designer briefs are professional extensions. Parent and kid briefs are proof that the lenses generalize into plain language; do not let those modes drive the default product behavior.

---

## When to use / When not to use

Use this skill when the user asks to:
- Explain, summarize, understand, translate, or brief a research paper
- Create a paper brief for a PM/TPM, engineer, designer, student, parent, or kid
- Prepare for a paper discussion with an AI/ML team
- Identify what to ask Applied Scientists about a paper
- Decide whether a paper is worth acting on, prototyping, monitoring, or ignoring

Do not use this skill for:
- Generic web articles, blog posts, news stories, or marketing pages
- Literature reviews across many papers unless the user wants each paper converted into this brief format
- Writing a new research paper or academic publication summary
- Deep implementation planning before a specific paper has been understood and deemed relevant

---

## Inputs

Expected inputs:
- **Paper source:** uploaded PDF, arXiv/DOI link, pasted abstract, pasted full text, or already-provided paper content
- **Audience:** PM/TPM, engineer, designer, student, parent, kid, all audiences, or unspecified
- **Brief mode:** Signal Scan, TPM Brief, Technical Review, Plain-English Brief, or unspecified
- **Reader context:** optional product, team, system, class, family, or discussion context

Defaults:
- If the audience is unspecified, ask once. If the user wants a default anyway, use PM/TPM.
- If the brief mode is unspecified, use TPM Brief for PM/TPM, Technical Review for engineers, and Plain-English Brief for nonprofessional audiences.
- If reader context is missing, avoid over-personalized claims and mark applicability as **Needs validation**.

---

## Brief Modes

Choose the brief mode based on the user's time horizon and depth request:

| Mode | Target time | Best for | Output depth |
|---|---:|---|---|
| **Signal Scan** | 3–5 minutes | Quick triage | One sentence per lens plus recommendation |
| **TPM Brief** | 20–30 minutes | AI/ML TPMs and PMs | Product understanding, trust level, risks, team questions, decision recommendation |
| **Technical Review** | 45–90 minutes | Engineers and Applied Scientists | Methodology, baselines, reproducibility, implementation risk, experiment plan |
| **Plain-English Brief** | 10–20 minutes | Students, parents, kids, stakeholders | Conceptual clarity, analogies, human implications, discussion questions |

---

## Steps

### Step 1 — Ingest the Paper

Accept input in any of these forms:
- **PDF upload** → extract text from the priority sections first; read all sections only when the paper fits comfortably in the current model context
- **arXiv / DOI link** → fetch the paper
- **Pasted abstract or text** → work with what's provided
- **Paper already in conversation** → use it directly

Read in this order: **Abstract → Conclusion → Results/Experiments → Limitations/Discussion → Introduction → Methodology**. This is the PM order of importance, not the author's order. Methodology is last because it's rarely what determines the brief's quality.

**Standard-context fallback:** If Claude reports that 1M context or extra usage is required, do not retry the same full-paper request. Switch to a standard-context workflow: summarize only the priority sections above, process one audience first, and ask the user whether to continue with additional audiences or sections. If the user explicitly wants full-paper coverage, tell them to enable extra usage for 1M context or rerun Claude with a standard non-1M model and a shorter excerpt.

**Extract before writing:**
- Core problem the paper is solving
- The key insight / contribution type (new method / dataset / system / analysis / result)
- Evidence strength signals: baseline quality, benchmark realism, ablation presence, OOD generalization, code/data availability, compute/data cost transparency, limitation honesty
- Directly supported claims vs. inferred or speculative claims
- Research limitations the authors acknowledge
- Context-fit questions: what the reader would need to know about their own data, infra, latency budget, compliance regime, users, or operations before applying the paper

---

### Step 2 — Clarify Audience(s)

If the user hasn't specified an audience, ask:

> "Who should I write this brief for? I can target: 💼 PM/TPM, ⚙️ Engineer, 🎨 Designer, 🎓 Student, 👨‍👩‍👧 Parent, or 🧒 Kid — or any combination. I can also do all six."

If they say "all" or "everyone", generate all six. If they name a specific role, generate that one. Default to PM if truly no context is given.

For long papers, start with the requested audience if there is one. If the user asks for all six and the paper is long, generate the PM brief first, then offer to continue audience-by-audience.

---

### Step 3 — Assign Trust Level and Evidence Labels

Before writing, assess the evidence and assign **one overall trust level** for the paper. Use `references/evidence-calibration.md` when results are technical or ambiguous.

| Level | Criteria |
|-------|----------|
| **Strong** | Multiple domains tested · Strong baselines · Realistic benchmarks · Results generalize OOD · Ablations confirm the key claim · Code/data available · Costs reported |
| **Medium** | Promising results but narrow setting · Some weak baselines · Unclear production relevance · Limited ablations · Partial reproducibility |
| **Weak** | Academic benchmarks only · No production validation · Weak or missing baselines · No ablations · Hard to reproduce |
| **Too early** | Conceptual / theoretical · No empirical results yet |

This trust level appears in every brief at the top and drives the Proof lens framing.

Label important claims as **Paper-supported**, **Inferred**, **Speculative**, or **Needs validation** when this helps prevent overclaiming.

Do not silently average all evidence criteria. Surface the **one or two trust drivers** that most influenced the rating, such as a decisive ablation, weak baseline, narrow benchmark, missing code, or strong held-out generalization.

---

### Step 4 — Write Each Brief

For each requested audience, write a complete brief using the template in `references/brief-template.md`.

**Adaptation rules per lens:**

#### 🎯 The Problem
- **PM:** Map to product context. "Is this our problem too?"
- **Engineer:** What design space? What prior approaches does it beat and on what axis?
- **Designer:** Who experiences this? Is it a technical or human-factors failure?
- **Student:** What is the research gap? What did prior work miss?
- **Parent:** What real-world situation were scientists trying to fix? Does it affect families?
- **Kid:** What annoyed the scientists enough to try to fix it? Use a relatable analogy.

#### 💡 The Insight
- **PM:** One sentence. If you can't say it in one sentence, you don't have it.
- **Engineer:** The architectural or algorithmic move. What specifically is new and why does it work?
- **Designer:** What does this reveal about human-AI interaction?
- **Student:** Name the contribution type (new method / dataset / system / analysis / result). What makes it novel?
- **Parent:** If a scientist had to explain this at dinner, what would they say?
- **Kid:** The one thing to tell a friend at lunch. Max one sentence.

#### 🔬 The Proof
- **PM:** Assign Strong / Medium / Weak / Too early. Explain baseline strength, benchmark realism, generalization, ablations, reproducibility, cost transparency, and limitation honesty.
- **Engineer:** Are baselines strong and current? Ablations present? Compute cost reported? Code available?
- **Designer:** Were real users tested or just models? Were tasks ecologically valid?
- **Student:** What's the baseline? What's the delta? Statistically significant? Could you reproduce this?
- **Parent:** "Is this real or hype?" Did they test with real people? Who funded this? Is this one study or many?
- **Kid:** "Did it work? How do we know?" Frame it like testing a game strategy — score before vs. after.

#### 🚨 The Catch
- **PM:** Separate research limitations from context-fit questions. State what the paper did not prove from the text. If product context is missing, do not invent context-specific risks; ask what must be checked about data, infra, latency, compliance, users, or operations.
- **Engineer:** Latency, memory, infra dependencies. Worst-case behavior. What assumptions may not hold?
- **Designer:** Approval fatigue, over-reliance, skill atrophy, accessibility gaps. What interaction patterns does it assume?
- **Student:** What open questions do the authors acknowledge? What would a skeptical reviewer push back on?
- **Parent:** What should I pay attention to? What are the risks for children or families specifically?
- **Kid:** What's still tricky? What would need to happen for this to work even better?

#### 📦 The Opportunity
- **PM:** Assign High / Medium / Low / Too early confidence. Map to new capability, quality lift, cost reduction, risk reduction, or strategic positioning. Add time horizon: Now / Next / Later / Skip.
- **Engineer:** Build / Use / Adapt / Watch / Skip. What would a prototype take?
- **Designer:** What changes about what I design? New interaction pattern? New failure mode to design around?
- **Student:** What research threads does this connect to? What gap could you work on?
- **Parent:** Is this a positive development, a risk, or too early to know? What does it mean for my family?
- **Kid:** If this keeps working, what cool thing could it make possible in the future?

#### ❓ The Next Move
- **PM:** End with Act now / Prototype / Ask the team / Monitor / Ignore for now, then give 3 smart questions for Applied Scientists.
- **Engineer:** Decide Build / Use / Adapt / Watch / Skip, then give 3 questions for your team/codebase and the smallest useful experiment.
- **Designer:** 3 questions for your design team. What needs to be redesigned as a result?
- **Student:** 3 questions for your advisor or study group. What would the most interesting follow-up be?
- **Parent:** 3 questions to sit with — or raise with teachers, your child, or other parents.
- **Kid:** 3 things to wonder about next. Open-ended curiosity questions.

---

### Step 5 — Add the Key Signal

Every lens ends with a **Key Signal** — a single italicised sentence that is the most important takeaway from that lens for that audience. This is not a summary of the lens — it's the one thing to carry out of it.

Format: *Key signal: [one sentence.]*

---

### Step 6 — Output Format

**Default output:** Markdown brief(s) directly in the conversation.

**If user requests a file:** Save as `[paper-slug]-[audience]-brief.md` in outputs. If all audiences requested, save as `[paper-slug]-all-briefs.md`.

**If user is on PaperDrop or requests a structured format:** Follow the template exactly as specified in `references/brief-template.md`.

Multiple audiences: write each as a separate section with a clear `---` divider and audience header.

For TPM briefs, include a short **What to ignore** note when useful, so time-constrained readers know which technical details are safe to skip unless implementation is planned.

---

### Step 7 — Offer Follow-Ups

After delivering the brief(s), always offer:

> "Want me to also:
> - Generate briefs for additional audiences?
> - Create a discussion guide for your team meeting?
> - Identify 3 related papers to read next?
> - Save this as a formatted file?"

---

## Outputs

Default output is a Markdown brief in the conversation. If the user requests a file, save Markdown as `[paper-slug]-[audience]-brief.md`; for all audiences, use `[paper-slug]-all-briefs.md`. A successful output includes the six lenses, trust level with trust drivers, evidence labels when useful, research limitations, context-fit questions, confidence, time horizon, recommendation, three next-move items, and key signals.

---

## Failure modes

- **Missing audience:** Ask the user which audience to target; if they insist on a default, use PM/TPM.
- **Partial paper content:** Produce a caveated brief from available sections and label missing claims as **Needs validation**.
- **No results or empirical evidence:** Use **Too early** unless the paper is explicitly theoretical; do not invent proof.
- **Ambiguous product applicability:** Use **Ask the team** or **Monitor**, not **Act now**. Ask context-fit questions instead of generating generic adoption-risk boilerplate.
- **Context-limit error:** Switch to priority sections and one audience at a time; do not retry the same full-paper request.
- **Unsupported source access:** Ask the user to paste the abstract, PDF text, or priority sections.

---

## Validation

Before returning a brief, verify the quality checklist below. If any item fails, revise the brief before output.

---

## Quality Standards

**Every brief must pass these checks before output:**

- [ ] The Problem is specific — not "AI is improving" but "X specific failure was blocking Y"
- [ ] The Insight is one sentence in plain English — no jargon without immediate explanation
- [ ] The Proof assigns a trust level and names the one or two trust drivers that most affected it
- [ ] Evidence labels are used consistently when claims mix paper-supported facts, inference, speculation, or context assumptions
- [ ] The Catch separates research limitations from context-fit questions and avoids generic adoption-risk boilerplate
- [ ] The Opportunity gives confidence and, for professional audiences, a time horizon
- [ ] The Next Move contains a recommendation plus exactly 3 actionable items, not generic advice
- [ ] Every lens ends with a Key Signal
- [ ] Language is calibrated to the audience — test: would a kid actually understand the kid brief?

**Common failure modes to avoid:**
- Writing the same brief for every audience (just with different introductory words)
- Making the Insight too long — if it takes more than 2 sentences, simplify
- Proof lens that just repeats numbers without assessing what they mean
- Catch lens that is too polite — be honest about what doesn't work
- Next Move that gives generic advice ("talk to your team") instead of specific questions

**Context-limit failure mode:**
- Signal: Claude returns "Extra usage is required for 1M context" or a similar context-window error.
- Cause: The conversation, extracted PDF text, skill references, and requested output exceeded the standard model's context budget or selected a gated 1M-context model.
- Required behavior: Do not tell the user the skill is broken. Restart or continue with a shorter standard-context request: priority sections only, one audience at a time, then expand incrementally.

---

## Reference Files

Read these when needed:

- `references/brief-template.md` — The exact output template for each audience, with annotated examples
- `references/audience-profiles.md` — Full depth profiles for all 6 audiences including reading order, time targets, and what to skip
- `references/evidence-calibration.md` — Detailed guide for assigning trust levels and reading results tables

---

## Quick Reference — Audience Adaptation Table

| Lens | PM | Engineer | Designer | Student | Parent | Kid |
|------|----|----------|----------|---------|--------|-----|
| Problem | Product fit | Design space | Human failure | Research gap | Family impact | Annoyance |
| Insight | 1-sentence | Mechanism | Human-AI signal | Contribution type | Dinner explanation | Lunch sentence |
| Proof | Strong/Med/Weak | Baselines + ablations | Real users? | Delta + reproducible? | Real or hype? | Score before/after |
| Catch | Research limits + context-fit questions | Infra assumptions | Human factors | Open questions | Family cautions | What's still hard |
| Opportunity | Confidence + time horizon | Build/Use/Skip | Design change | Research direction | Family implication | Future cool thing |
| Next Move | Recommendation + 3 Qs | Decision + experiment | 3 Qs for design team | 3 Qs for advisor | 3 Qs to sit with | 3 things to wonder |
