# MEMORANDUM

**Center for Teaching Innovation (CTI) — Ashgrove University**

**To:** Digital Learning Experience Project Manager
**From:** Dr. Elena Vasquez, Director, Center for Teaching Innovation
**Date:** September 2, [current academic year]
**Re:** Pilot project — low-stakes GenAI practice tool for CS1 misconception remediation

---

Thanks for taking this on. Following up on our conversation, here's the brief and the
constraints I need you to design inside — the Associate Dean is releasing Innovation
Fund money for this, but only against a plan that respects all of the following.

**Background.** Prof. Okafor and the CS1 teaching team have flagged a pattern in TA
grading logs and office hours: students are pasting code from AI assistants into
their assignments faster than they're learning to reason about it, and the specific
bugs that result track closely onto the misconception categories our teaching
consultants have documented for years (see the research brief separately). We tried
an in-house fix last year ("DebugBuddy") and it didn't work — I've asked the UX team
to write up why. I don't want to repeat that mistake.

**What I need from you:** a single Project Design & Pilot Plan document I can hand to
the Associate Dean, covering the problem, the tool concept, the GenAI guardrails, the
build/pilot timeline, the budget, the risks, and how we'll know if it worked.

**Hard constraints — please respect all of these:**

1. **Budget:** $8,000 total, one-time, from the CTI Innovation Fund. It does not renew
   next term unless the pilot succeeds. I need it itemized — the Associate Dean will
   ask what each line pays for.
2. **Timeline:** the tool must be built and ready to launch **within 6 weeks** of
   kickoff. We want it live before the Week 8 midterm point of the fall term.
3. **Pilot scope:** a 2-week voluntary pilot in CS1 "Introduction to Programming with
   Python," Section 2 (~45 students). Prof. Okafor has already agreed to this section.
4. **No new LMS/LTI integration.** University IT has a moratorium on new LTI
   integrations this term — they simply don't have the review bandwidth. Whatever we
   build has to be a **standalone web app** students reach via a link, authenticated
   with university SSO. Do not propose an LMS plugin or LTI launch.
5. **GenAI vendor is fixed.** We must use the university's existing enterprise LLM
   agreement (referred to below as "the contracted provider"). CTI already has a
   shared API budget line for this provider capped at **$500/month**, and we cannot
   request additional API funds or a different vendor this fiscal year.
6. **TA time is essentially zero.** The two TAs on CS1 are fully committed to grading.
   They can give **at most 2 hours per week each**, and only **during the 2-week pilot
   window** — not during the 6-week build phase. Don't plan on TA effort before then.
7. **It must stay genuinely low-stakes.** The Faculty Senate passed an "AI-Assisted
   Learning" policy last month: any AI tool used with students must clearly disclose
   that it is *not* a substitute for the department's academic-integrity/AI-disclosure
   policy on graded work, and participation or non-participation **must not affect
   grades** in any way, direct or indirect.
8. **FERPA applies.** Any student interaction data we log needs a privacy/retention
   story we can defend if asked.

I'd like the plan to read as something we could actually greenlight next week — not a
vision statement. Please ground the misconception targeting and the tool design in the
attached materials (research brief, prior-tools audit, student survey, UX heuristics
sheet) rather than starting from scratch.

Thanks,
Elena
