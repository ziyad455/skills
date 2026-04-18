# Output Contracts

Use these patterns when the answer needs to be stronger, clearer, or more auditable.
Adapt the amount of structure to the task. Do not add headings mechanically when a short
answer is enough.

## General Grounded Answer

Use when the task is factual, analytical, or validation-heavy.

Output shape:

1. Direct answer to the user's actual question.
2. Short support summary: what was checked or what evidence carries the conclusion.
3. Narrow uncertainty statement only if it materially affects the answer.
4. Next action only if it helps the user move forward.

Good properties:

- The conclusion appears first.
- Support is specific, not generic.
- Uncertainty is bounded, not theatrical.

## High-Stakes Or Action-Gated Answer

Use when the output could trigger money, safety, legal, operational, or destructive
impact.

Output shape:

1. `status`
   Ready, blocked, or needs confirmation.
2. `verified facts`
   The key preconditions or observations that were actually checked.
3. `open risk or blocker`
   The one or two missing facts that still matter.
4. `recommended next step`
   Proceed, clarify, approve, or stop.

Good properties:

- The user can tell whether action is safe right now.
- The answer does not blur checked facts with assumptions.

## Conflicting-Evidence Answer

Use when strong sources disagree on a central claim.

Output shape:

1. Best-supported reading.
2. What the sources disagree about.
3. Why one reading currently looks stronger, or why no winner exists.
4. What would resolve the conflict if the answer must become more certain.

Good properties:

- No false consensus.
- No unexplained source dumping.

## Recommendation Or Comparison Answer

Use when the user asks what to choose.

Output shape:

1. Recommendation or shortlist.
2. Decision criteria used.
3. Tradeoffs that matter most.
4. Constraint-sensitive caveat if a different user priority would change the result.

Good properties:

- Recommendation is tied to criteria.
- Caveats are about decision boundaries, not generic uncertainty.

## Research Synthesis Answer

Use when the answer integrates multiple sources or subquestions.

Output shape:

1. Synthesis conclusion.
2. Key findings grouped by theme or subquestion.
3. Live disagreements or open gaps.
4. Practical takeaway.

Good properties:

- The answer sounds integrated, not pasted together.
- The user can see what was checked without reading a source dump.

## Code Or Data Validation Answer

Use when reporting software, query, calculation, or transformation results.

Output shape:

1. What changed, ran, or was checked.
2. Observed result.
3. Remaining limitation, if any.

Good properties:

- Distinguishes implementation from verification.
- Makes clear whether the result was observed or only reasoned about.

## Coding Clarification Answer

Use when a coding task is not yet ready to build.

Output shape:

1. What is unclear.
2. Why it changes implementation or validation.
3. The smallest question or questions needed.

Good properties:

- The question set is minimal.
- Each question is tied to a concrete coding consequence.

## Coding Delivery Answer

Use when code was written, modified, or reviewed.

Output shape:

1. What was implemented or changed.
2. What was validated.
3. Important assumptions.
4. Remaining risk or unverified area, only if material.

Good properties:

- The user can distinguish code changes from confirmed behavior.
- Assumptions are visible rather than buried.

## High-Risk Change Report

Use when the code change affects data, auth, payments, migrations, concurrency, or
other high-blast-radius behavior.

Output shape:

1. Status: ready, conditionally ready, or blocked.
2. Critical checks completed.
3. Remaining blocker or safety concern.
4. Recommended next step.

## Style Rules

- Answer the real problem, not just the narrow literal phrasing.
- Prefer short, high-information prose over performative structure.
- Mention validation steps when the user cannot see them.
- Keep speculation clearly marked and brief.
- State observed validation before inferred confidence.
- If the task is simple, compress aggressively.
