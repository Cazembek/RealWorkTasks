# Evaluation Rubric

Weights sum to 100. Score each criterion 0–1 (0 for missing, 0.5 for partially there, and 1 for fully there), multiply by weight, sum.
"Cites/references" requires a specific, checkable reference to the source packet —
generic restatement without the underlying data/number/name does not satisfy a
criterion that requires it.

| # | Criterion | Weight | What full credit requires |
|---|---|---|---|
| 1 | Executive summary | 5 | Present as its own section, ≤200 words, and accurately previews every other section (timeline, budget figure, vendor/integration constraints, evaluation approach) without introducing claims absent from the rest of the document. |
| 2 | Misconception prioritization | 9 | Identifies ≥4 of the 8 categories from the research brief by name/description, uses the frequency data (or the brief's trend note) to justify *why* those specific categories were prioritized over the others — not just a list of all 8 with no selection logic. |
| 3 | Prior-tool lessons applied | 6 | Names a specific failure from at least one of CodeFix AI or DebugBuddy (e.g., silent fixes, no base case for diagnosis, engagement collapse, FERPA transcript issue), ties it to a named heuristic or concrete metric from the audit, and explains concretely how the new design avoids repeating it. |
| 4 | Tool concept & IA concreteness | 9 | Describes a specific information architecture or interaction flow (nameable screens/steps a reviewer could picture and later wireframe) — not only adjectives like "intuitive" or "engaging." |
| 5 | UX heuristics applied concretely | 8 | Names ≥3 distinct Nielsen heuristics from the reference sheet and ties each to a specific design decision in the tool (not a bare restatement of the heuristic's definition). |
| 6 | GenAI guardrail: no direct answers | 10 | Explicitly designs a mechanism preventing the tool from returning a fixed/corrected code block (e.g., Socratic questioning, turn limits, output filtering), and explicitly connects this to preventing the over-reliance failure mode documented in the prior-tools audit. |
| 7 | Cost containment & vendor constraint | 7 | Explicitly ties a cost-control mechanism (rate limiting, tiered model use, caching, or equivalent) to the stated $500/month cap, and uses only the contracted/existing LLM vendor — does not propose a new vendor or additional API budget. |
| 8 | No new LTI/LMS integration | 5 | Explicitly designs the tool as a standalone web app reached via a link with university SSO, and does not propose an LMS plugin, LTI launch, or new integration with the LMS. |
| 9 | Timeline consistency | 8 | Provides a build timeline with distinct weekly milestones fitting within 6 weeks, plus a separate 2-week pilot window, with no internal contradiction (e.g., an accessibility audit or other prerequisite scheduled after the launch it's supposed to gate). |
| 10 | Budget itemization | 8 | Budget is broken into line items, the stated total is ≤$8,000, arithmetic is correct, and every line item is traceable to a role/task described elsewhere in the plan (no unexplained or orphan costs). |
| 11 | TA constraint respected | 4 | TA involvement is capped at ≤2 hours/week per TA and occurs only during the pilot window, not the 6-week build phase. |
| 12 | Risk register | 6 | Lists ≥4 distinct, plausible risks (not generic "something could go wrong"), each with an assessed likelihood/impact and a concrete, specific mitigation. |
| 13 | Evaluation plan | 7 | Defines ≥2 distinct learning-outcome metrics and ≥2 distinct engagement/UX metrics, each with a stated data-collection method, and explicitly states that no metric affects student grades. |
| 14 | Accessibility & equity | 4 | States a concrete accessibility target (e.g., WCAG 2.1 AA) and addresses at least one equity consideration grounded in the survey data (e.g., low-bandwidth access, opt-out of gamification). |
| 15 | Privacy & policy compliance | 4 | Addresses FERPA-relevant data handling (e.g., anonymization, retention limit) for logged interactions, and explicitly upholds the Faculty Senate's non-punitive/disclosure requirement (participation/non-participation does not affect grades; tool is not a substitute for the graded-work AI-disclosure policy). |

**Total: 100**

## Scoring notes for graders

- A response that satisfies the "soft" pedagogy/UX criteria (2–5, 12–14) well but
  silently violates one or more hard operational constraints (6–11, 15) — e.g., an
  over-budget or unitemized budget, a timeline that doesn't fit 6 weeks, TA hours
  assigned during the build phase, a new LTI integration, or a new LLM vendor — should
  lose full credit on each violated criterion regardless of overall polish. These
  constraint violations are the primary intended discriminator between fluent-but-
  shallow and genuinely correct responses.
- Criteria 2, 3, 5, and 6 require a *specific, checkable* tie back to the source
  packet (a named category, a named heuristic, a named prior-tool failure). Vague or
  generic references without the specific supporting detail should receive partial
  (not full) credit.
