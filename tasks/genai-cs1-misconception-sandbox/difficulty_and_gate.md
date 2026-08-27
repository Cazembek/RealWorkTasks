# Difficulty Analysis & Difficulty Gate

## What makes this task hard

No single sub-skill in this task is individually difficult — a competent generalist
model can write plausible UX copy, list plausible risks, or summarize misconception
categories in isolation. The difficulty is in **simultaneous constraint satisfaction
across a long, internally cross-referenced professional document**, combined with
resistance to several well-known LLM failure patterns:

1. **Constraint load.** The director's memo alone embeds 8 hard, independently
   checkable constraints (budget cap, sub-cap on API spend, 6-week build window,
   2-week pilot window, fixed vendor, no-new-integration mandate, TA hour/phase cap,
   non-punitive policy) plus FERPA. A correct answer must hold all of them true *at
   once*, in a document with 9 different sections — a budget error in §6 or a TA
   hour in §7 that's inconsistent with §6's timeline both count as failures, even if
   every other section is excellent.
2. **Resisting the "solve the constraint away" reflex.** Models commonly respond to a
   tight constraint by quietly proposing to lift it — e.g., "we recommend requesting
   additional API budget," "IT should make an exception for this integration," or
   switching to a different, unnamed LLM vendor "for better guardrail support." The
   task explicitly forbids this, but it is a strong default completion pattern.
3. **Grounding vs. fabrication.** The task requires citing specific figures (42%, 38%,
   68%, 12%, 18%, etc.) and specific named failures from the packet, not generic
   pedagogical advice, and explicitly forbids inventing external statistics or
   citations. Models often default to citing plausible-sounding external "research"
   instead of the specific internal packet data actually provided.
4. **Non-superficial heuristic application.** It is easy to name Nielsen heuristics;
   it is harder to tie each one to a specific, non-redundant design decision rather
   than restating its definition next to an unrelated feature.
5. **Arithmetic and scheduling consistency.** The budget must sum correctly to at or
   under the cap with traceable line items, and the timeline must fit two different
   fixed windows (6 weeks build, 2 weeks pilot) without any prerequisite (e.g., the
   accessibility audit) scheduled after the thing it's supposed to gate.
6. **A subtle stakes trap.** The survey data is intentionally mixed on gamification
   (39% positive, 30% negative, explicit comments rejecting leaderboards) and on the
   incentive question (60% want low-stakes practice; but a naive answer will attach the
   $10 incentive to *tool usage* rather than *survey completion only*, which would
   quietly violate the "participation must not affect grades/incentives in a way that
   pressures engagement" spirit of the Faculty-Senate constraint).

Because the rubric weights the "hard constraint" criteria (budget, timeline, vendor,
integration, TA hours, privacy/policy — criteria 6–11 and 15, 51 of 100 points) about
as heavily as the pedagogy/UX criteria, a response that is well-written and
pedagogically sound but drops even two or three of these operational constraints
lands well short of full marks, even though it would likely "feel" high-quality to a
non-expert reader.

## Difficulty gate

**Gate:** an expert-run result from GPT-5.5 on this task, graded against the rubric
above by a subject-matter-expert grader, should score **below 80%**.

**Rationale for the gate:** the task is designed so that strong general writing and
domain knowledge are necessary but not sufficient — passing requires simultaneously
tracking ~15 independently checkable constraints across a 9-section document with no
internal contradictions. In practice, capable models reliably nail the pedagogy/UX/
risk narrative sections but drop 2–4 of the operational constraints (most often: budget
arithmetic/traceability, the vendor/integration constraints, or the TA phase
restriction), which under this rubric's weighting is enough to fall below the 80%
threshold even with strong prose throughout. If an expert run scores ≥80%, the task
should be revised to tighten one or more constraints (e.g., a smaller budget cap
relative to itemized needs, or an additional cross-section dependency) until the gate
holds.
