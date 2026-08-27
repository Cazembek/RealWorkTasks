# UX Audit: Two Prior AI-Assisted Debugging Tools

**Prepared by:** CTI UX Team
**Purpose:** understand why our one in-house attempt failed, and why a generic
AI-code-fixer approach isn't sufficient, before we design a new tool.
**Method:** heuristic evaluation against Nielsen's 10 usability heuristics (see the
reference sheet), plus usage-log analysis where available.

---

## Tool A: "CodeFix AI" (third-party IDE plugin, trialed informally by ~20 volunteer
students last spring, not university-supported)

CodeFix AI is a general-purpose IDE plugin that detects likely bugs and inserts a
corrected version of the code directly, with a one-line comment describing the change.

**Heuristic findings:**

- **Violates Heuristic 1 (Visibility of system status):** the plugin silently rewrites
  code; students often didn't notice a change had been made until their program's
  *behavior* changed, with no indication of what was altered or why.
- **Violates Heuristic 9 (Help users recognize, diagnose, and recover from errors):**
  because the fix is applied for the student rather than explained as a diagnosis,
  students have no path to recognize the error pattern themselves next time.
- **Usage-log finding:** in a short follow-up quiz, only 32% of students who had used a
  CodeFix AI suggestion could correctly re-explain what the original bug was, and 68%
  could not reproduce an equivalent fix unaided on a similar bug the following week.

**Takeaway:** direct code-fixing tools resolve the symptom, not the misconception, and
actively remove the struggle that leads to learning.

---

## Tool B: "DebugBuddy" (in-house chatbot, piloted in CS1 two semesters ago,
discontinued)

DebugBuddy was a simple chat window bolted onto the course LMS page. Students could
paste code and ask "what's wrong with this?" It used an early general-purpose LLM
integration with no constraints on how it could answer.

**Heuristic findings:**

- **Violates Heuristic 5 (Error prevention):** because DebugBuddy would give a full
  corrected code block on the first ask, there was no design friction discouraging
  copy-paste dependence.
- **Violates Heuristic 8 (Aesthetic and minimalist design) in the *engagement* sense:**
  the tool had no structure, pacing, or sense of session boundaries — students reported
  it felt like "just another chat window," indistinguishable from tools they were
  already using outside class, giving them no reason to prefer it.
- **Usage-log finding:** weekly active use collapsed from 61% of the pilot section in
  week 1 to just **12% by week 3**. Exit-survey respondents most commonly cited "didn't
  feel different from just asking [a general AI assistant]" (44%) and "forgot it
  existed" (29%).
- **Compliance note:** DebugBuddy logged full chat transcripts tied to student login,
  which Legal later flagged as a FERPA retention concern — this was a contributing
  factor in why it was discontinued rather than iterated on.

**Takeaway:** a tool with no distinct pedagogical behavior and no privacy-conscious
logging design will neither engage students nor survive institutional review, no matter
how good the underlying model is.
