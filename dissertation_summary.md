# Dissertation Study Summary — For Discussion

## Study Title
Comparative Study of Code-Tracing Learning Approaches

## Original Design

A three-condition randomized experiment in CS 105 (Introduction to Computer Science) at UIUC, comparing instructional approaches for teaching code tracing to introductory programming students.

**Conditions:**

- **Control Group (~40 students):** 10 code-tracing questions, all at the "How to Trace" level (building tracing tables for variables, conditionals, loops, functions, lists, etc.). Feedback limited to correctness only.

- **Treatment Group A (~40 students):** A three-stage progressive curriculum — Stage 1: HOW to Trace (foundational tracing-table skills), Stage 2: WHY to Trace (using tracing to find discrepancies and debug), Stage 3: WHAT to Trace (strategic tracing — deciding which variables to track and how to build trace tables for analysis). Feedback is static/correctness-based.

- **Treatment Group B (~20 students):** Same three-stage curriculum as Treatment A, supplemented with automated LLM-generated feedback. Smaller group size to support qualitative analysis of student–LLM interactions.

**Procedure:** Pre-test → learning activities (single session, ~90–180 min) → post-test → survey.

**Target enrollment:** ~100 completed participants (120 on IRB to allow buffer).

## Current Recruitment Situation

- ~300 students enrolled in CS 105 this term (vs. ~500 last term)
- 17 sign-ups after ~10 days of recruitment
- Last term: 50–60 sign-ups from 500 students, only 20–30 completions (data not usable due to separate issues)
- Projected completions this term: likely 20–30 students, well short of the ~100 needed for the original three-condition design

**Constraints:** Cannot extend data collection to another term (graduation timeline). No comparable course to recruit from. Committee is expected to be flexible on redesign as long as the study remains sound.

## Revised Options Under Consideration

### Option A: Two Groups — Treatment A vs. Treatment B (Mixed-Methods)

Split participants into Treatment A (3-stage, no LLM) and Treatment B (3-stage, with LLM). Drop the control group entirely.

*Strengths:* Preserves a comparison. Can examine how LLM feedback changes the learning process across the three stages. Mixed-methods framing allows qualitative analysis to carry the main contribution, with quantitative pre/post results reported as exploratory.

*Limitations:* Small N per group (~10–15 each). Loses the ability to evaluate the 3-stage curriculum itself against a baseline. Quantitative comparisons will be underpowered.

### Option B: Single Group — Everyone Gets Treatment B (Qualitative Deep Dive)

All participants experience the full 3-stage curriculum with LLM feedback. Focus entirely on qualitative analysis of student interactions.

*Strengths:* Maximizes data richness per student. Enables deep analysis of how students interact with LLM feedback at each stage — what questions they prioritize, whether they try to game the system, whether feedback helps at different stages of the curriculum. Coherent narrative.

*Limitations:* No comparison group. Cannot make any claims about the effectiveness of the 3-stage design relative to alternatives, or about LLM feedback vs. no feedback.

## Questions for Discussion

1. Which revised option is more defensible as a dissertation study?
2. Would supplementary analyses (e.g., from prior term data or secondary datasets) strengthen the dissertation, even if the data comes from a different course context?
3. Are there other feasible strategies to boost recruitment in the remaining window?
4. What is the minimum number of completions needed for the chosen design to be viable?
