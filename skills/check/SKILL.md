---
name: check
description: |
  Checks one artifact — a plan, a task brief, a report, a decision, or a process or config rule —
  against the six NUPP principles (Nearly Universal Principles of Projects) and returns only the
  violations: where it is, what it costs, how to fix it. Read-only; a clean artifact gets a
  one-line "clean" verdict.
  TRIGGER when: user says "сверься с NUPP", "проверь по NUPP", "проверь план по принципам",
  "что тут нарушает NUPP", "NUPP-сверка", "check against NUPP", "NUPP check", "lint this plan
  with NUPP"; or a session working by nupp:guide has written a plan, brief or decision for a large, expensive
  or irreversible piece of work.
  DO NOT TRIGGER when: the principles should guide the whole session (use /nupp:guide); a human
  project needs a diagnosis or a methodology choice (use /nupp:nupp); the facts of a plan need
  verifying — this checks how the work is built, not whether its claims are true.
argument-hint: "<path to a plan, brief, report or decision — or nothing for the one under discussion>"
allowed-tools: Read, Glob, Grep
---

# NUPP check

Some of this content is adapted from OMIMO's NUPP (https://omimo.org/), used under the Creative Commons Attribution license; OMIMO does not endorse this adaptation.

Check one artifact against the six NUPs and report only what is broken. This is a lint of how the work is built — purpose, evidence, foresight, the whole chain, saved resources, reuse — not a fact-check of its claims.

## 1. Take the artifact

- `$ARGUMENTS` holds a path → Read it. Several paths → check each, one verdict per file.
- No argument → take the plan, brief, report or decision under discussion in this conversation. If two candidates fit, ask which one; if none does, ask for a path.
- Name its kind; the kind selects the tagged questions in step 3: **plan** · **brief** (a task for another agent or person) · **report** · **decision** (a choice between options) · **rule** (a process, ritual, configuration or skill text).
- Read what the artifact depends on only when a question below cannot be answered without it (the plan a report answers, the goal a plan cites) — two or three files at most.

## 2. Load the principles

If the text of `/nupp:guide` is not already in this conversation, Read `${CLAUDE_PLUGIN_ROOT}/skills/guide/SKILL.md`; its section "The six principles, read for agent work" is the rule set. For the original wording of one principle: `${CLAUDE_PLUGIN_ROOT}/skills/nupp/references/nupN-*.md`.

## 3. Ask all six

Go through all six for every artifact: the principle that "does not seem relevant" is where root causes hide. Untagged questions apply to every kind.

- **NUP1 — truth over affiliation.** Are the claims backed by evidence from this case (measured, read, run), with facts kept apart from assumptions? Is a choice justified by habit, a brand, or the author's own earlier plan? *Report:* are failures and divergences from the plan stated; was a worker's claim accepted without a check? *Decision:* does it say what would change the choice?
- **NUP2 — energy and resources.** Is "good enough" defined, or is the scope open-ended? Is the effort proportional to the stakes? Does it hand the owner decisions that defaults could settle, or one at a time instead of batched? *Brief:* does it prescribe steps where a goal and an acceptance test would do? *Report:* is it short enough to be read by the person it is for?
- **NUP3 — proactivity.** Is the plan as detailed as the uncertainty allows — neither missing nor falsely precise? Are risks named with responses before expensive or irreversible steps? Are roles settled: who writes what, who accepts? *Decision:* options beyond the obvious two, including pause and rescope; a bias check? *Report:* are unsolved problems reported, not only solved ones? *Rule:* how will anyone know it is read and used?
- **NUP4 — weakest link.** Does it cover the whole chain to the end result, or optimise one link or one number? Which link is the weakest, and does the effort go there? What may be dropped if resources run short? Does a new element fit the rules already in place, or contradict one? Is there a person at the end who can read the output and act on it? *Report:* was the result verified past the part that was touched?
- **NUP5 — purpose.** Can you state from the artifact alone which benefit or decision it serves? Run the parallel-worlds test on each major step, section or rule: what differs without it? Is it aimed at the problem, or at a presumed solution? Is the level of detail set by the purpose, or by a template? *Plan:* is there a check, after completion, that the purpose was reached?
- **NUP6 — repeatable elements.** Does it build something that already exists (a skill, script, checklist, earlier research, method)? Does it repeat by hand what should be an element or a cycle? Is a borrowed element tailored to this case, or pasted? *Rule:* is it light enough that people will not route around it?

## 4. Keep only real violations

A finding stays only if all three hold:

- You can point to the place: a quote, a section, or a named absence ("no done criterion anywhere").
- Left as it is, it would probably make the work miss its purpose, cost materially more, or do damage that cannot be undone. "Something could go wrong" is not enough — say what is likely to.
- The fix is worth its cost at this artifact's stakes. A small reversible task earns only the findings that would make it fail, and a named absence counts only when the stakes need that element: a small artifact does not need risks, options or a bias check written out.

Improvements, wording, more detail, and extra safety on top of a safeguard the artifact already has are not violations — leave them out. An artifact can be clean; then say so. A manufactured finding breaks NUP1 and NUP2 itself.

One root cause is one finding, filed under the principle it hurts most. Rank by impact on the outcome. Report at most five; if more passed the filter, say how many you left out.

## 5. Report

Answer in the conversation's language. The labels below are in Russian; translate them for another language.

```
NUPP-сверка: <artifact> — <kind>
Вердикт: чисто | поправить и идти | остановиться

1. NUP5 · <where: quote or section>
   Что не так: <one sentence>
   Чем грозит: <consequence for the outcome, cost or risk>
   Как поправить: <text the author can paste, or one concrete step>
2. …

Без нарушений: NUP1, NUP4, …
```

- «Остановиться» only when a violation makes the main result unreachable or risks irreversible damage; otherwise «поправить и идти».
- Clean artifact: the header, `Вердикт: чисто`, and one line on what makes it sound. Nothing more.
- Write each fix as a rewritten line or a missing section, not as advice to "consider".
- Leave the artifact as it is; apply the fixes only when the owner asks.
