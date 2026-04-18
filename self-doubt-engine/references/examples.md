# Examples

Use these examples to calibrate depth and output quality.

## Example 1: Freshness-Critical Retrieval

User request:
"What is the latest release of framework X?"

Weak behavior:

- Answers from memory or an old blog post.
- Omits the checked date.

Upgraded behavior:

- Routes to `freshness-critical retrieval`.
- Checks the current official release source.
- States the release and the date checked.
- Notes uncertainty only if the release feed itself is lagging or inconsistent.

## Example 2: Code And Data Validation

User request:
"I changed the parser. Does it work now?"

Weak behavior:

- Reviews the diff and says it looks correct.

Upgraded behavior:

- Routes to `code and data validation`.
- Runs the relevant tests or a focused execution path.
- Reports the observed result and any untested edge case.

## Example 3: Recommendation And Comparison

User request:
"Which database should our small team use?"

Weak behavior:

- Names a popular option with generic pros and cons.

Upgraded behavior:

- Extracts criteria such as scale, ops burden, cost, and workload type.
- Compares a small candidate set against those criteria.
- Recommends one option or a shortlist tied to the stated constraints.

## Example 4: Irreversible Action Gating

User request:
"Delete the old customer records."

Weak behavior:

- Proceeds after identifying a likely table or file.

Upgraded behavior:

- Restates target and scope precisely.
- Verifies what "old" means and which records are in scope.
- Checks whether deletion is reversible and whether a preview exists.
- Stops for clarification if the cutoff or scope is ambiguous.

## Example 5: Conflict Resolution

User request:
"These two sources disagree on the deadline. Which one is right?"

Weak behavior:

- Picks one source without explaining why.

Upgraded behavior:

- Identifies the exact disagreement.
- Compares authority, scope, and recency.
- Resolves the conflict if possible or preserves the unresolved conflict clearly.

## Example 6: Routine Patch

User request:
"Add trimming to this helper before validation."

Weak behavior:

- Asks unnecessary questions about architecture or future extensibility.

Upgraded behavior:

- Routes to `fast patch`.
- Makes the local change.
- Runs a focused check on the helper behavior.

## Example 7: Material Ambiguity In Coding

User request:
"Add export support for reports."

Weak behavior:

- Starts coding without knowing format, destination, or scope.

Upgraded behavior:

- Routes to `clarification-first`.
- Identifies that output format and delivery path change implementation materially.
- Asks only the minimum questions needed.

## Example 8: Bug Fix

User request:
"The parser crashes on some files. Fix it."

Weak behavior:

- Guesses a likely cause and patches the code without anchoring the failure.

Upgraded behavior:

- Routes to `bug diagnosis and fix`.
- Uses failing input, stack trace, or test evidence to localize the bug.
- Rechecks the failing path after the fix.
