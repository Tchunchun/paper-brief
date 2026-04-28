# Paper Brief

Paper Brief is an Agent Skill for turning research papers into audience-adaptive, evidence-calibrated briefs. It is built for AI/ML TPMs and PMs first, with additional modes for engineers, designers, students, parents, and kids.

## Problem to Solve

This project is based on the problem statement for research paper understanding by AI/ML TPMs: dense academic papers are written for researchers, but product and program decision-makers need to extract what the paper claims, how much to trust it, what the paper does not prove, and what context-fit questions to ask their Applied Science partners.

The core problem is not generic summarization. It is research-to-understanding translation under time pressure. A good brief should help a TPM walk into a paper discussion with a calibrated point of view, sharper questions, and a recommendation shape: act now, prototype, ask the team, monitor, or ignore for now.

## Approach

Paper Brief uses the 6-Lens Framework v2:

| Lens | Question |
|---|---|
| 🎯 The Problem | What broken thing is this fixing — and does it affect me? |
| 💡 The Insight | What's the single clever idea at the heart of this? |
| 🔬 The Proof | Did it actually work — and how much should I trust that? |
| 🚨 The Catch | What doesn't it prove, and what could still go wrong? |
| 📦 The Opportunity | What does this open up — for me specifically? |
| ❓ The Next Move | What do I do or think about differently because of this? |

Framework v2 separates reading guidance from the generated skill output. It also keeps evidence calibration explicit:

- **Trust level:** Strong, Medium, Weak, or Too early
- **Trust drivers:** the one or two reasons that most affected the rating
- **Evidence labels:** Paper-supported, Inferred, Speculative, or Needs validation
- **Catch split:** research limitations vs. context-fit questions
- **Next move:** Act now, Prototype, Ask the team, Monitor, or Ignore for now

The PM/TPM brief is the product wedge. Engineer and designer briefs are professional extensions. Student, parent, and kid modes demonstrate that the same six lenses can adapt depth and language without changing the underlying structure.

## Skill Overview

The skill source lives in [`paper-brief/`](paper-brief/):

```text
paper-brief/
├── SKILL.md
└── references/
    ├── audience-profiles.md
    ├── brief-template.md
    └── evidence-calibration.md
```

The packaged skill archive is [`paper-brief.skill`](paper-brief.skill).

### What It Produces

For a research paper, Paper Brief can produce:

- A quick signal scan
- A 20–30 minute TPM brief
- A deeper technical review
- A plain-English brief for nontechnical audiences
- Audience-specific next-move questions
- Evidence labels and trust calibration

### How to Run

Use the skill by invoking it from an agent environment that supports Agent Skills, then provide:

1. A paper source: PDF, arXiv/DOI link, abstract, or pasted paper text
2. A target audience: PM/TPM, engineer, designer, student, parent, kid, or all audiences
3. Optional reader context: product, team, system, class, or family context

Example prompts:

```text
Use paper-brief to create a TPM brief for this paper: [paste abstract or paper text]
```

```text
Use paper-brief to explain this arXiv paper for an engineer and a PM: [link]
```

```text
Use paper-brief to create a plain-English parent brief from this paper: [paste text]
```

### Rebuild the Skill Package

After editing the skill source, rebuild the archive from this directory:

```bash
rm -f paper-brief.skill
zip -qr paper-brief.skill paper-brief -x '*/.DS_Store'
```

Inspect the archive before publishing:

```bash
unzip -l paper-brief.skill
```

Expected files:

```text
paper-brief/SKILL.md
paper-brief/references/audience-profiles.md
paper-brief/references/brief-template.md
paper-brief/references/evidence-calibration.md
```

## Repository Notes

- Keep skill source under `paper-brief/`.
- Keep the directory name aligned with the `name` field in `SKILL.md`.
- Do not package `.DS_Store`, editor state, or temporary files.
- Rebuild and inspect `paper-brief.skill` after every source change.

## Skill Authoring Standards

Paper Brief follows the Agent Skills format. The core maintenance rules are:

- A skill must be a directory with a `SKILL.md` file.
- The directory name must exactly match the `name` field in `SKILL.md` frontmatter.
- Skill names must be lowercase, hyphenated, and limited to letters, digits, and hyphens.
- The `description` should be a single-line, action-first summary that says what the skill does, when to use it, and what not to use it for.
- Set `license`, `compatibility`, and `metadata.version` explicitly.
- Keep `SKILL.md` concise; move detailed operating guidance into focused files under `references/`.
- Use `references/` for on-demand documentation, `assets/` for static templates/data, and `scripts/` only for executable helpers.
- Keep examples and internal file references relative to the skill root.
- Document inputs, steps, outputs, failure modes, and validation checks in the skill body.
- Rebuild and inspect the `.skill` archive after every source change.
- Do not package `.DS_Store`, editor state, logs, temporary files, or local planning artifacts.

Before publishing a change, verify:

1. `paper-brief/SKILL.md` frontmatter name is `paper-brief`.
2. The description is under 1024 characters and includes high-signal triggers.
3. `SKILL.md` stays under 500 lines.
4. Reference files are focused and only loaded when needed.
5. `paper-brief.skill` contains only the skill source and reference files.
