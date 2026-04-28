# Audience Profiles — Paper Brief Skill

Full depth profiles for all 6 audiences. Read this file when you need detailed
guidance on how a specific audience thinks, what they prioritize, and how to
calibrate language for them.

These profiles are a **reader model**, not the output template. Reading order notes explain how a human in that audience would approach a paper and how the agent should prioritize extraction. The generated output must still follow `brief-template.md`.

Evidence labels are universal across audiences: **Paper-supported**, **Inferred**, **Speculative**, and **Needs validation**. Use simpler wording for parent and kid briefs, but keep the distinction between what the paper showed, what it suggests, what is still a guess, and what needs checking.

Product priority: PM/TPM is the wedge. Engineer and designer modes are professional extensions. Parent and kid modes demonstrate that the six lenses generalize into plain language; they are not coequal MVP targets.

---

## 💼 PM / TPM

**Core mindset:** I need to make product decisions. Is this worth acting on, and when?

**What they're actually asking:**
- Should my team care about this?
- How confident should I be in these findings?
- What do I do with this — now, next quarter, or never?
- What do I ask my Applied Scientists that shows I understood the implication?
- Should the recommendation be Act now, Prototype, Ask the team, Monitor, or Ignore for now?

**Language calibration:**
- Use product vocabulary: roadmap, quality lift, confidence level, production, eval, harness
- Use decision vocabulary: act now, prototype, ask the team, monitor, ignore for now, validate, commit resources
- Avoid: formal notation, ablation details, dataset construction specifics
- OK to use: "evidence strength," "baseline," "generalization" — but define briefly if in doubt

**Reading order (what they actually do):**
Abstract → Conclusion → Results → Limitations → Done

**Time target:** 20–30 minutes

**What to emphasize in each lens:**
- Problem: "Is this our problem too?" — explicit mapping to their product context
- Insight: One sentence only. If it takes two, the PM doesn't have it yet.
- Proof: Assign Strong/Medium/Weak/Too early explicitly. Give the key number and name the one or two trust drivers that most affected the rating.
- Catch: Separate research limitations from context-fit questions. The skill can state what the paper did not prove; if team context is missing, it should ask what needs checking rather than inventing context-specific risks.
- Opportunity: Map to a roadmap slot — Now, Next, Later, or Skip. Give confidence level.
- Next Move: State Act now / Prototype / Ask the team / Monitor / Ignore for now, then give 3 questions for Applied Scientists. Questions should reveal implication, not just comprehension.

**What to ignore:** Include a short note for TPMs when the paper has dense technical content they can safely skip unless implementation is planned.

**Failure mode to avoid:** Writing a brief that sounds like an abstract. The PM brief should build an evidence-calibrated point of view, not just report findings.

---

## ⚙️ Engineer / Applied Scientist

**Core mindset:** I need to understand how this works, whether it's reproducible, and whether I can use or build on it.

**What they're actually asking:**
- What's the actual mechanism — not the claim, the mechanism?
- Are the baselines strong enough to trust the comparison?
- Can I reproduce this? What would I need?
- Is this worth a sprint to prototype?

**Language calibration:**
- Full technical vocabulary is welcome: ablations, hyperparameters, dataset splits, OOD, MTok, latency, inference, tokenization
- File names, function names, pseudocode — all welcome for architecture papers
- Be precise about what's known vs. inferred vs. reconstructed

**Reading order:**
Abstract → Methodology (carefully) → Results → Appendices → Code/data availability

**Time target:** 45–90 minutes. They will read the methodology. Budget accordingly.

**What to emphasize in each lens:**
- Problem: Design space framing. What axis does this beat prior work on — accuracy, cost, latency, generalization?
- Insight: The precise mechanism. What specific change (objective, feedback signal, data structure, inference strategy) makes it work?
- Proof: Baseline quality. Ablation presence and whether it isolates the key contribution. Compute cost. Replication risk (code/data available?). Failure modes documented?
- Catch: Infra dependencies. Latency/memory constraints. Assumptions that may not hold in their system. Worst-case behavior.
- Opportunity: Build / Use / Adapt / Watch / Skip. What would a prototype actually take?
- Next Move: Build / Use / Adapt / Watch / Skip, followed by questions for their codebase and team, not abstract advice.

**Failure mode to avoid:** Over-simplifying the mechanism to be "accessible." Engineers want precision. Give it to them.

---

## 🎨 Designer / UX Researcher

**Core mindset:** I need to understand what this means for how people experience AI systems — and whether it changes how I should design.

**What they're actually asking:**
- Does this change the interaction surface I'm designing for?
- What human factors does this paper surface that I wasn't accounting for?
- Are there new failure modes I need to design around?
- Did they actually test with real users?

**Language calibration:**
- Use design vocabulary: interaction pattern, mental model, trust trajectory, approval fatigue, transparency, affordance
- Human factors vocabulary: over-reliance, skill atrophy, ecological validity, accessibility
- Avoid: formal notation, ablation tables, dataset construction details

**Reading order:**
Abstract → Problem framing → User behavior findings → Limitations → Discussion

**Time target:** 30–45 minutes

**What to emphasize in each lens:**
- Problem: Who experiences this? Is it a technical failure or a human factors failure? What does it look like from the user's perspective?
- Insight: What does this reveal about human-AI interaction? Mental model gap? Trust calibration? Workflow mismatch?
- Proof: Were real users tested? Were tasks ecologically valid? Did diversity/accessibility get considered? "Good result" from user perspective vs. metric perspective.
- Catch: Approval fatigue, over-reliance, skill atrophy, trust miscalibration, accessibility gaps. What interaction patterns does the system assume that real users won't exhibit?
- Opportunity: Does this change what controls or transparency to design? New interaction pattern? Shifts where human attention should be?
- Next Move: Questions for design team about what to redesign as a result.

**Failure mode to avoid:** Treating this audience the same as PM. Designers care about human experience first, business impact second. Lead with the human.

---

## 🎓 Student (University / Graduate)

**Core mindset:** I'm learning how research works, building domain knowledge, and trying to understand where this fits in the bigger picture.

**What they're actually asking:**
- What's the research gap — what did prior work miss?
- What type of contribution is this (method / dataset / system / analysis / result)?
- How strong is the evidence really? Could I reproduce it?
- What should I read next? Could I build on this?

**Language calibration:**
- Full research vocabulary: contribution type, research gap, baseline, ablation, statistical significance, replication, related work
- Frame things in terms of the field's conversation — what prior work does this respond to?
- Teaching moments are welcome: explain what an ablation is, what "OOD" means, etc.

**Reading order:**
Abstract → Introduction (carefully) → Figures and tables → Conclusion → Related Work → Methodology

**Time target:** 60–120 minutes for a paper in their field. More if outside their domain.

**What to emphasize in each lens:**
- Problem: The research gap. Every paper positions itself against prior work — what did prior work get wrong or miss?
- Insight: Name the contribution type. What makes it novel? Contribution types: new method, new dataset/benchmark, new system, new analysis, new result.
- Proof: Baseline (simplest reasonable alternative), delta (how much better?), statistical vs. practical significance, ablation interpretation, reproducibility.
- Catch: Open questions the authors themselves acknowledge. Assumptions that limit generalization. What a skeptical reviewer would push back on.
- Opportunity: Research threads to follow. Gaps the student could work on. Impact on thesis/class project direction.
- Next Move: Questions for advisor or study group. Community reaction to this work?

**Failure mode to avoid:** Making the student brief too accessible — they want to develop research taste, which requires engaging with the complexity.

---

## 👨‍👩‍👧 Parent

**Core mindset:** My kids are growing up with AI everywhere. I want to understand what's actually happening — without the hype or the fear — so I can have honest conversations with my family.

**What they're actually asking:**
- Is this real, or is this media hype?
- Should I be worried about this for my kids?
- Is there anything I should do differently as a parent?
- What would I want my child's school to know about this?

**Language calibration:**
- No technical vocabulary at all — explain every term
- Use analogies to everyday family life: school, sports, cooking, parenting
- Be honest about uncertainty — parents can handle "we don't know yet" better than overconfident claims
- Don't be condescending — parents are intelligent adults who simply lack domain vocabulary

**Reading order:**
Plain-language summary → The Catch → The Opportunity → Done

**Time target:** 15–20 minutes using the brief. They don't read the paper.

**What to emphasize in each lens:**
- Problem: What real-world human situation were scientists trying to fix? Could this affect families?
- Insight: The dinner table explanation. Two sentences maximum. No jargon.
- Proof: Is this real or hype? Was it tested with real people? Who funded it? One study or many? Big enough to matter in daily life?
- Catch: What should they pay attention to or be cautious about? Risks for children specifically.
- Opportunity: Positive development, risk to be aware of, or too early to know? What to do differently?
- Next Move: Questions to raise with teachers, their child, or other parents.

**Failure mode to avoid:** Being patronizing. Explain terms, don't avoid complexity — just make it accessible. Parents can understand difficult ideas when explained well.

**Special attention:** The long-term human capability concern (AI reducing comprehension, skill atrophy) is especially relevant for parents. Surface it in the Catch when the paper touches on it.

---

## 🧒 Kid (Ages 8–12)

**Core mindset:** I'm curious. I want to understand the cool idea. I don't need every detail — just the part that makes me go "whoa."

**What they're actually asking:**
- What problem did this fix?
- What was the clever trick?
- Did it work?
- Why should I care?
- What can I wonder about next?

**Language calibration:**
- Short sentences. Active voice. Concrete examples.
- Use analogies to things kids know: video games, school tests, puzzles, sports, cooking, magic tricks
- Every abstract concept needs a physical or experiential analogy
- Enthusiasm is welcome — science is exciting
- Avoid: percentages without context, any acronyms, passive voice, "significant," "baseline," "ablation"

**Test before outputting:** Read the kid brief aloud. If you'd feel embarrassed reading it to a 10-year-old because it's too complex — rewrite it.

**Reading order:**
Problem → Insight → Opportunity → Done (Proof and Catch are secondary)

**Time target:** 10–15 minutes. Short is a feature, not a bug.

**What to emphasize in each lens:**
- Problem: What annoyed the scientists? Every invention starts with annoyance. Make it relatable.
- Insight: The one thing to tell a friend at lunch. One sentence. Use a game or puzzle analogy.
- Proof: "Did it work? How do we know?" Frame like testing a game strategy — try it, see the score, compare to old way.
- Catch: "What's still hard?" Even if the idea worked, what problems are still left?
- Opportunity: "Why is this exciting?" What cool future thing does this make possible?
- Next Move: "Three things to wonder about" — open-ended curiosity questions, not tasks.

**Failure mode to avoid:** Oversimplifying to the point of inaccuracy. Kids deserve honest, accurate explanations — just in accessible language. The goal is "a 10-year-old could understand this" not "a 10-year-old would read this in school."

**Analogy bank for common concepts:**
- Context window → "the AI's desk — it can only see what fits on the desk at once"
- Training data → "all the books the AI read before it started working"
- Harness → "the instructions and rules around the AI, like the rules of a game"
- Baseline → "the old way of doing things that you're comparing against"
- Ablation → "turning parts of the invention off to see which parts actually matter"
- Generalization → "works on new problems it hasn't seen before, not just the ones it practiced on"
