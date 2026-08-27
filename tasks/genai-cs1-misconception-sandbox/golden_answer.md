# Project Design & Pilot Plan: "Duck Check" — A Low-Stakes GenAI Debugging Sandbox for CS1

**Prepared for:** Dr. Elena Vasquez, Director, Center for Teaching Innovation
**Prepared by:** Digital Learning Experience Project Manager
**Status:** For Associate Dean review / Innovation Fund release

---

## 1. Executive Summary

We propose **Duck Check**, a standalone web sandbox that lets CS1 students describe a
bug and get *questions*, not fixes, from our contracted LLM provider — modeled on
rubber-duck debugging rather than autocomplete. It targets the four misconception
categories most linked to AI-fix dependency in our own data (reassignment vs. equality,
off-by-one errors, print-vs-return confusion, and scope confusion), directly correcting
the two failure modes that killed our two prior tools: silent/direct fixes (CodeFix AI)
and undifferentiated, unbounded chat (DebugBuddy). It is built and ready to launch in 6
weeks, piloted voluntarily and ungraded for 2 weeks in CS1 Section 2 (~45 students),
for $7,940 against the $8,000 cap, using only the contracted LLM vendor within the
$500/month API line, with no new LMS/LTI integration and at most 2 hours/week per TA
during the pilot only. Success is measured by session completion rate, a pre/post
misconception diagnostic, System Usability Scale (SUS) score, and week-over-week active
use — none of which touch grades.

---

## 2. Problem Statement & Misconception Targeting

TA-coded review of ~500 CS1 assignments over three semesters shows eight recurring
misconception categories (research brief, §2). Two trends make this urgent now:
AI-assistant adoption is high (71% of surveyed students use one weekly), and 54% of
students say they don't understand *why* an AI-suggested fix works. TAs report this is
concentrated in the misconceptions that require a correct mental model of names,
references, and control flow — not surface syntax.

We will prioritize the tool's detection and questioning logic around the four
highest-value categories:

| Priority | Category | Frequency | Why it's prioritized |
|---|---|---|---|
| 1 | Reassignment vs. equality (#1) | 42% | Highest frequency; foundational to every later category. |
| 2 | Off-by-one / boundary errors (#2) | 38% | Highest frequency *first-encounter* misconception (weeks 1–4), where a low-stakes practice space has the most leverage before habits form. |
| 3 | Print vs. return value (#3) | 33% | High frequency and, per TA notes, one of the categories most likely to be "fixed" by AI without the student noticing the distinction. |
| 4 | Local/global scope confusion (#4) | 30% | Explicitly flagged in the brief as one of the categories (with #1 and #5) where AI-assisted "fixes" have made students *less* able to explain the underlying model. |

We are deliberately **not** attempting to cover all 8 categories in the 6-week build;
categories 5–8 (aliasing, recursion, boolean logic, floating point) are lower-frequency
or more advanced and are the natural target list for a term-two expansion if the pilot
succeeds, per the memo's note that Innovation Fund renewal depends on pilot outcomes.

---

## 3. Lessons from Prior Tools

Two prior attempts inform the design directly (prior-tools audit):

- **CodeFix AI** silently rewrote code (violating Heuristic 1, Visibility of system
  status) and gave students no diagnostic path of their own (violating Heuristic 9).
  Result: only 32% of users could re-explain the original bug, and 68% couldn't
  reproduce an equivalent fix unaided a week later. **Design response:** Duck Check
  never edits or outputs corrected code. It only asks targeted questions, and every
  turn is visibly labeled as a "hint," not a fix.
- **DebugBuddy** gave full corrected code on first ask (violating Heuristic 5, Error
  prevention) and had no structural distinctiveness from a general chat window,
  collapsing from 61% to 12% weekly active use by week 3, with "didn't feel different
  from just asking [AI]" as the top exit-survey reason. It also logged full transcripts
  tied to student identity, which drew a FERPA concern. **Design response:** Duck Check
  is structured as short, bounded *sessions* (max 6 exchanges) with a visible
  progress/hint meter, ends in a mandatory one-line self-explanation, and logs only
  anonymized session data with a 30-day retention limit (see §9).

---

## 4. Tool Concept & UX Design

**Concept:** a single-purpose, single-task web app. A student pastes a code snippet and
picks "I'm stuck" or "Check my thinking." Duck Check never returns a fix — it returns a
Socratic question tied to a detected misconception category, up to 6 exchanges, ending
in a short self-explanation the student writes themselves.

**Information architecture / key screens:**

1. **Landing & consent screen** — one paragraph stating, in plain language, that this
   tool is not graded, is not visible to instructors, and is not a substitute for the
   course's AI-disclosure policy on graded assignments (see §9). SSO login via
   university credentials (no new account/password).
2. **Code input screen** — a single paste box and a one-line prompt ("What do you
   expect this to do, and what's it doing instead?") — capturing the student's own
   framing before any AI response, which also gives the classifier a stronger signal.
3. **Socratic exchange screen** — a turn-limited chat (max 6 exchanges) with a visible
   **hint meter** ("Hint 2 of 6") and a persistent "Not graded / not visible to your
   instructor" banner.
4. **Mandatory reflection screen** — before the session can close, the student writes
   1–2 sentences explaining what the bug was in their own words. This is stored (see
   §9) but never scored.
5. **Optional badge screen** — a lightweight, dismissible collection of category badges
   ("Boundary Bug Spotted"). Fully opt-out via a single toggle on first login, in direct
   response to survey comments rejecting a "whole gamification layer" (39% found badges
   motivating, but a comparable share pushed back — see §4a below).

**UX heuristics applied:**

- **Heuristic 1 (Visibility of system status):** the hint-meter and persistent
  "not graded" banner directly correct CodeFix AI's silent-change failure and address
  the 45% of students who avoid AI help near deadlines out of integrity anxiety.
- **Heuristic 5 (Error prevention) / Heuristic 9 (Help users recognize, diagnose, and
  recover from errors):** the 6-turn Socratic structure structurally prevents the
  "first-ask full fix" pattern that made DebugBuddy a dependency risk, replacing it
  with diagnosis-oriented prompting.
- **Heuristic 6 (Recognition rather than recall):** misconception categories are
  surfaced to students in plain language ("this looks like a boundary/off-by-one
  issue") rather than requiring them to recall or self-diagnose CS terminology.
- **Heuristic 8 (Aesthetic and minimalist design):** the core flow is a single task per
  screen with no dashboard, score, or leaderboard on the main path — directly
  responding to the survey comment rejecting leaderboard-style gamification; badges are
  opt-in and tucked behind a separate, optional screen.

**4a. Gamification decision.** Survey data is split (39% motivated by badges, 31%
neutral, 30% opposed, with unprompted comments specifically rejecting leaderboards). We
resolve this by making badges opt-out-by-default-visible but fully togglable, and by
never using competitive/comparative elements (no leaderboard, no rank) — consistent
with keeping the tool low-stakes for every student, not just those who like game
mechanics.

---

## 5. GenAI Guardrail Design

Duck Check uses the university's contracted LLM provider exclusively, within the
existing $500/month CTI API budget line — no new vendor or procurement.

**Behavioral guardrails (system-level, not user-configurable):**

- The model is instructed, and the response is server-side validated, to never emit a
  runnable corrected code block. Any output resembling a full corrected function is
  rejected and replaced with a fallback Socratic question template for the detected
  category.
- Sessions are hard-capped at 6 exchanges, after which the mandatory reflection screen
  is forced regardless of whether the student feels "done" — this bounds both cost and
  over-reliance risk.
- Question phrasing is drawn from a rotating bank per misconception category (not a
  single fixed script), so that screenshots/answers shared between students age quickly
  and don't function as an answer key.

**Cost containment (to stay inside $500/month):**

- **Tiered model use:** a lightweight/cheaper model call classifies the likely
  misconception category from the pasted code and the student's framing; only the
  Socratic-question generation step uses the more capable (costlier) tier, minimizing
  expensive calls per turn.
- **Hard rate limit:** 3 sessions per student per day, 6 exchanges per session, capped
  input/output length per turn — bounding worst-case monthly volume for a 45-student,
  2-week pilot to a small, predictable fraction of the $500 line, with the API
  dashboard's built-in spend alert set at 80% of the monthly cap as an early warning
  (see Risk Register, §7).
- **Response caching:** the four prioritized misconception categories map to a small
  set of common question patterns; near-duplicate code submissions reuse cached
  classification results rather than re-invoking the classifier.

**Academic-integrity guardrail:** the persistent banner and landing-screen consent text
explicitly state that Duck Check is not a substitute for the department's AI-disclosure
policy on graded assignments and does not report usage (or non-usage) to instructors —
directly answering the 45% of students who report avoiding AI help out of integrity
anxiety, and complying with the Faculty Senate's non-punitive requirement (§9).

---

## 6. Project Plan

### Timeline (6-week build, then 2-week pilot)

| Week | Milestone |
|---|---|
| 1 | Finalize misconception-to-feature mapping (§2); wireframe the 5 screens. |
| 2 | Finalize UX flow and copy (banners, consent text); draft Socratic question banks and classifier prompts for the 4 priority categories. |
| 3 | Build core sandbox UI; integrate contracted-provider API with tiered-model routing, rate limits, and guardrail validation. |
| 4 | Internal QA; external accessibility audit (WCAG 2.1 AA) and remediation. |
| 5 | TA orientation (30 min, asynchronous-friendly materials — does not count against the pilot-window TA hour cap); soft-launch usability test with 8–10 volunteer students outside Section 2. |
| 6 | Refine based on usability test findings; finalize; confirm SSO access for Section 2 roster. |
| 7–8 | **Pilot window:** voluntary, ungraded use in CS1 Section 2. TAs mention the tool once in section (≤2 hrs/week each, pilot weeks only) and are available for troubleshooting questions only — no grading or monitoring role. |
| 9 | Analyze pilot data; write outcomes report to the Associate Dean; recommend renew/iterate/discontinue. |

This satisfies the memo's requirement of build-ready within 6 weeks and a live tool
before the Week 8 midterm point.

### Roles

| Role | Source | Time commitment | New cost? |
|---|---|---|---|
| Project Manager (this role) | Existing CTI FTE | Ongoing oversight | No |
| CTI Director | Existing FTE | ~1 hr/week, advisory | No |
| UX/front-end contractor | New, contracted | 6 weeks × 10 hrs/week | Yes |
| Prompt engineering / backend contractor | New, contracted | 6 weeks × 6 hrs/week | Yes |
| External accessibility auditor | New, contracted | Flat-fee engagement, Week 4 | Yes |
| CS1 TAs (2) | Existing course staff | ≤2 hrs/week each, **pilot weeks (7–8) only** | No new hours |
| Prof. Okafor | Existing faculty | One in-class mention, Week 7 | No |

### Budget (itemized, total $7,940 of $8,000 cap)

| Line item | Basis | Cost |
|---|---|---|
| Contracted-provider API usage | $500/month shared line × 2 months (build testing + pilot) | $1,000 |
| UX/front-end contractor | 6 weeks × 10 hrs/week × $60/hr | $3,600 |
| Prompt engineering / backend contractor | 6 weeks × 6 hrs/week × $60/hr | $2,160 |
| Accessibility audit (external, flat fee) | Week 4 engagement | $400 |
| Post-pilot survey incentive | $10 e-gift card × 50 respondents (survey completion only, not tool usage) | $500 |
| Contingency (~3.5%) | Unplanned/rounding buffer | $280 |
| **Total** | | **$7,940** |

Every line traces to a task above: no orphan costs, and no line requests funds beyond
the $8,000 cap or the $500/month API sub-cap.

---

## 7. Risk Register

| # | Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|---|
| 1 | Over-reliance recurrence: students screenshot/share Socratic hints as an answer key. | Medium | Medium | Rotating question bank per category; mandatory self-explanation gates session close; hints reference the student's own code, reducing reusability. |
| 2 | API cost overrun beyond $500/month. | Medium | High | Hard per-student rate limits, tiered model routing, cached classification, and an 80%-of-cap spend alert on the provider dashboard. |
| 3 | Low adoption, repeating DebugBuddy's collapse to 12% weekly use by week 3. | High | High | Short (≤10 min) bounded sessions, one in-class mention from Prof. Okafor in Week 7, opt-in badges — kept to a 2-week pilot window so engagement is measured before novelty fades. |
| 4 | Accessibility gaps exclude students with disabilities or limited bandwidth (18% report unreliable home internet). | Low | High | Budgeted external WCAG 2.1 AA audit in Week 4 with remediation time before launch; lightweight, low-asset UI (no animation-heavy screens). |
| 5 | Student data handling raises a FERPA concern, as it did with DebugBuddy. | Low | High | Anonymized session IDs only, no full transcript tied to identity, 30-day auto-deletion (§9). |

---

## 8. Evaluation & Success Metrics

**Learning-outcome metrics:**

- **Pre/post misconception diagnostic:** an 8-item voluntary quiz (one item per
  category from the research brief) administered before Week 7 and after Week 8,
  measuring change in students' ability to correctly identify each misconception in a
  short code sample.
- **Recurrence rate in graded work:** TAs already code assignment errors by category as
  part of normal grading (per the research brief's methodology); we compare
  misconception-category recurrence rates in Section 2 (pilot) against a
  non-pilot CS1 section over the same weeks, using existing TA coding practice — no new
  grading burden.

**Engagement/UX metrics:**

- **Session completion rate:** percent of started sessions reaching the mandatory
  reflection screen; target ≥70%.
- **System Usability Scale (SUS):** administered voluntarily post-pilot; target ≥68
  (the standard "above average" SUS benchmark), for direct comparison against the
  qualitative collapse we saw with DebugBuddy.
- **Weekly active use trend across the 2-week pilot,** explicitly tracked against
  DebugBuddy's failure curve (61%→12% by week 3) as the comparison baseline we're
  trying to avoid repeating.

**Non-grading statement:** per the Faculty Senate policy and the memo's constraint, no
metric above is used for, or visible in, any student's grade. Participation is entirely
voluntary; the only incentive offered anywhere in this plan is the $10 gift card for
completing the *optional post-pilot survey*, not for using the tool itself.

---

## 9. Accessibility, Equity & Privacy

- **Accessibility:** target WCAG 2.1 AA, verified by the budgeted external audit in
  Week 4 with remediation before Week 6 launch readiness.
- **Bandwidth equity:** 18% of surveyed students report unreliable home internet
  (hotspot/lab-only access). The UI avoids heavy animation or large media assets and is
  usable on a low-bandwidth connection.
- **Gamification equity:** badges are opt-out by a single toggle, directly responding
  to survey comments rejecting mandatory gamification, so the tool doesn't
  disadvantage or alienate students who find game mechanics distracting or patronizing.
- **FERPA / data retention:** sessions are logged under anonymized, non-reversible
  session identifiers, not student names or IDs; raw session transcripts (code pasted,
  chat exchanges) are auto-deleted after 30 days; only aggregated, de-identified metrics
  (§8) are retained beyond that window for the outcomes report.
- **Policy compliance:** consistent with the Faculty Senate's AI-Assisted Learning
  policy, the landing screen explicitly discloses that this tool does not substitute
  for the course's graded-work AI-disclosure policy, and no aspect of participation,
  non-participation, or performance within the tool is shared with instructors or
  factored into grades.
