# Task Overview (Author's Notes)

**Task family:** Digital project management for computer science education
**Domain synthesis:** novice-programmer misconceptions research, GenAI-in-education design guardrails, UX heuristics, low-stakes experiential learning

## Task idea

A teaching-innovation office at a university wants to pilot a browser-based tool that
lets intro programming students get AI help on their bugs *without* the AI just handing
them fixed code — because faculty have noticed students pasting AI-generated fixes they
don't understand, which entrenches rather than resolves classic CS1 misconceptions
(off-by-one errors, mutable-default-argument aliasing, scope confusion, etc.).

The model being evaluated plays a **Digital Learning Experience Project Manager** who
must turn a packet of internal materials (a director's memo with hard constraints, a
misconceptions research brief with frequency data, an audit of two prior tools that
failed, a student survey, and a UX heuristics reference sheet) into a single, coherent,
funding-ready **Project Design & Pilot Plan**.

## Why this scenario

It naturally forces integration of all four of the stated interest areas:

1. **Programming misconceptions** — the plan must prioritize *specific* misconception
   categories from real internal data, not generic "students make mistakes" language.
2. **GenAI in education** — the plan must design a guardrail (Socratic questioning,
   turn limits, no direct fixes) that prevents the exact over-reliance failure mode
   documented in the prior-tools audit.
3. **UX design principles** — the plan must apply *named* heuristics to *specific*
   design decisions, not just assert the tool will be "intuitive."
4. **Low-stakes experiential learning** — the tool must remain explicitly ungraded and
   voluntary, consistent with a (fictional) Faculty Senate AI policy, while still
   driving real engagement (the prior in-house tool collapsed to 12% weekly active use
   by week 3 — the new plan has to visibly avoid repeating that).

## What makes it gradable

The source packet embeds ~15 hard, checkable constraints (dollar figures, week counts,
staffing caps, a named vendor lock-in, a no-new-integrations IT moratorium, FERPA, a
non-punitive AI-use policy). A shallow answer will sound polished and cover the "soft"
pedagogy/UX content well while quietly violating several of the operational constraints
(budget doesn't sum, TA hours assigned during the wrong phase, proposes a new LTI
integration or a new LLM vendor, treats the survey completion incentive as touching
grades, etc.). This is what pulls fluent-but-shallow answers below the 80% gate.

## Files in this package

- `source_materials/01_directors_memo.md` — the commissioning memo with all hard constraints
- `source_materials/02_misconception_research_brief.md` — internal misconception data (public/created)
- `source_materials/03_prior_tools_audit.md` — UX heuristic audit of two failed prior tools
- `source_materials/04_student_survey_results.md` — quantitative + qualitative survey data
- `source_materials/05_ux_heuristics_reference.md` — Nielsen's 10 heuristics, given as reference only
- `task_prompt.md` — the exact prompt given to the model under evaluation
- `golden_answer.md` — the complete, professional reference solution
- `rubric.md` — the weighted evaluation rubric (15 criteria, weights sum to 100)
- `difficulty_and_gate.md` — what makes the task hard + the difficulty gate statement
