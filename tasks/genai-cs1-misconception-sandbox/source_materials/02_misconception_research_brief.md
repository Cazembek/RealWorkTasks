# Internal Research Brief: Common Misconceptions in CS1 (Python)

**Prepared by:** CTI Teaching Consultants Group
**Basis:** coded review of ~500 graded CS1 assignments across the last 3 semesters,
cross-checked against the published literature on novice programming misconceptions
(e.g., work in the tradition of du Boulay's "genetic epistemology of programming" and
more recent empirical taxonomies such as Qian & Lehman's review of novice difficulties).
Percentages below are **our own coded frequency data**, not taken from any external
study — they reflect the share of reviewed assignments in which TAs coded the error as
stemming from this specific misconception (not simply "had a bug").

| # | Misconception category | Plain-language description | Frequency (of coded assignments) |
|---|---|---|---|
| 1 | Reassignment vs. mathematical equality | Students read `x = x + 1` as an equation ("x can't equal x+1") rather than as "update the value stored under the name x." | 42% |
| 2 | Off-by-one / boundary errors | Loop bounds, `range()` endpoints, and index arithmetic are consistently off by one, especially with `range(len(list))` vs. `range(len(list)-1)`. | 38% |
| 3 | Print output vs. return value | Students confuse a function that prints a value with one that returns it, then are surprised when `result = my_func()` is `None`. | 33% |
| 4 | Local/global scope confusion | Students assume a variable assigned inside a function is visible outside it, or vice versa, or attempt to mutate an outer variable without `global`/`nonlocal`. | 30% |
| 5 | Mutable default arguments / aliasing | `def f(x, acc=[])` — students don't realize the default list is created once and shared across calls; more broadly, confusion between "same object" and "equal value" for lists/dicts. | 25% |
| 6 | Recursion base case omission | Recursive functions written without a correct (or any) base case, or with a base case that's unreachable given the recursive step. | 22% |
| 7 | Boolean logic misuse | Redundant comparisons (`if x == True`), incorrect negation of compound conditions (De Morgan's errors), and confusing `and`/`or` short-circuit behavior. | 20% |
| 8 | Floating-point equality | Comparing floats with `==` and being surprised when `0.1 + 0.2 == 0.3` is `False`. | 18% |

**Trend note:** Over the last two semesters (coinciding with wider student adoption of
AI coding assistants), TAs report a *qualitative* shift: the raw bug rate on submitted
assignments has gone down, but in office hours, students are markedly less able to
explain *why* a fix someone (or something) suggested actually works — particularly for
categories 1, 4, and 5, which require a correct mental model of names/references rather
than surface-level syntax knowledge. Categories 2 and 3 remain the most frequent
*first-encounter* misconceptions for students in the first four weeks of the course.
