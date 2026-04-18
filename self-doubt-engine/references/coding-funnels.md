# Coding Funnels

Use these funnels when the task includes writing, modifying, debugging, refactoring, or
delivering code. Do not use the same workflow for a small patch, bug fix, feature,
refactor, or high-risk system change.

## Quick Router

| Funnel | Trigger | First move | Minimum evidence before delivery | Stop when | Escalate when |
| --- | --- | --- | --- | --- | --- |
| Fast patch | Narrow, low-risk change | Inspect target code path | Focused sanity check or targeted validation | Main behavior is confirmed or low-risk assumption is isolated | Hidden dependency or unclear contract appears |
| Clarification-first | Material ambiguity | Resolve the smallest critical unknown | Clear enough request and testable success criteria | Ambiguity no longer changes implementation materially | Different answers produce different code |
| Bug diagnosis and fix | Reported failure, flaky behavior, failing test | Reproduce or inspect failure evidence | Fix is tied to a verified failure path and retested | The failure path is explained and checked | Failure cannot be localized or reproduced safely |
| Feature implementation | New or changed behavior | Define behavior, interface, and success checks | Changed behavior is validated on the main path | Core feature works and key edge cases are bounded | Product decisions remain implicit |
| Refactor with invariants | Structural change with behavior preservation | Identify invariants | Tests, snapshots, or equivalent checks preserve behavior | Invariants still hold after change | Invariants are unknown or untested |
| High-risk change gating | Data, auth, payments, migrations, concurrency, external effects | Verify scope and blast radius first | Strong validation plus precondition checks | Critical risk points are checked | Safe verification is unavailable |
| Validation and delivery check | Code exists but confidence is weak | Inventory what was actually verified | Strongest available evidence is gathered and reported honestly | Delivery claim matches validation scope | Claimed confidence exceeds evidence |
| Limited-validation fallback | Runtime checks unavailable | Narrow claim and do best static verification | Static evidence plus explicit limitations | Unsupported areas are clearly bounded | Unverified risk remains too high to imply readiness |

## 1. Fast Patch

### Trigger

- Small, localized change
- Clear desired behavior
- Low blast radius

### Sequence

1. Inspect the current implementation and surrounding call sites.
2. Confirm the patch scope is truly narrow.
3. Implement the simplest change that addresses the request.
4. Run the cheapest check that would catch the most likely regression.

### Sufficient Evidence

- The changed path is clearly targeted.
- A focused check supports the claimed behavior.

### Escalate

- The patch touches broader behavior than expected.
- The requested outcome depends on unspecified edge cases.

## 2. Clarification-First

### Trigger

- Missing output contract
- Unclear interface shape
- Unknown environment or version constraint
- Multiple materially different implementation choices

### Sequence

1. Identify the smallest set of unresolved questions that changes the build.
2. Resolve from repository evidence if possible.
3. Ask only the questions that unblock correct implementation.
4. Restate success criteria before coding.

### Sufficient Evidence

- The agent can describe the target behavior concretely.
- Competing implementations are no longer equally plausible.

### Escalate

- The request hides a product decision rather than a coding detail.
- The user-provided direction still leaves the main contract undefined.

## 3. Bug Diagnosis And Fix

### Trigger

- Failing test
- Reported defect
- Flaky or inconsistent behavior

### Sequence

1. Capture the failure signal: reproduction, stack trace, test output, or code path.
2. Determine the likely class of failure before patching.
3. Fix the most supported cause, not the first plausible one.
4. Re-run the failing path and a nearby regression check.

### Sufficient Evidence

- The bug was reproduced or otherwise anchored to evidence.
- The fix is validated against the relevant failure path.

### Escalate

- Failure evidence is too weak to target safely.
- The issue reproduces inconsistently across environments.

## 4. Feature Implementation

### Trigger

- New behavior
- Changed user-visible logic
- New endpoint, component, job, or data flow

### Sequence

1. Translate the request into concrete input, output, and behavior expectations.
2. Identify the minimum viable implementation path.
3. Define the main success case and one or two meaningful edge or failure cases.
4. Implement in a way that is easy to test and explain.
5. Validate the primary path before polishing.

### Sufficient Evidence

- Core behavior is exercised directly or by relevant tests.
- The implementation matches the intended contract.

### Escalate

- Feature scope is drifting during implementation.
- The requested behavior depends on unresolved product policy.

## 5. Refactor With Invariants

### Trigger

- The goal is cleaner structure, maintainability, or reuse without intentionally
  changing behavior.

### Sequence

1. State the invariants that must remain true.
2. Identify the public contracts, outputs, or side effects that must not move.
3. Refactor incrementally when possible.
4. Validate against invariants, not just code style.

### Sufficient Evidence

- Behavior-preserving checks exist and pass.
- The refactor did not silently widen scope into feature work.

### Escalate

- The original behavior is poorly specified or untested.
- The refactor would require product-level decisions.

## 6. High-Risk Change Gating

### Trigger

- Auth
- Payments
- Security-sensitive logic
- Data mutation or migration
- Concurrency
- External side effects

### Sequence

1. Identify blast radius and failure cost.
2. Check preconditions, rollback considerations, and safety boundaries.
3. Prefer explicit guards, tests, and narrow scope over broad rewrites.
4. Validate the risky path and at least one adverse or boundary condition.

### Sufficient Evidence

- The critical path is checked directly.
- The main failure mode has been considered or tested.

### Escalate

- Verification cannot safely cover the critical risk.
- The change relies on implicit system guarantees not confirmed locally.

## 7. Validation And Delivery Check

### Trigger

- Code exists but the agent is about to overclaim confidence.
- The main question is whether the result is ready to present or ship.

### Sequence

1. Inventory what was actually observed, executed, or tested.
2. Compare that evidence to the delivery claim.
3. Add the highest-value missing check if feasible.
4. Narrow the delivery statement to match the evidence.

### Sufficient Evidence

- The final answer is aligned with the real validation scope.

### Escalate

- Delivery readiness depends on checks that cannot be performed.

## 8. Limited-Validation Fallback

### Trigger

- No runnable environment
- Missing dependencies
- Restricted permissions
- Partial repository access

### Sequence

1. Perform the best static analysis available: code inspection, type reasoning, schema
   inspection, contract tracing.
2. Identify the specific runtime checks that remain missing.
3. Narrow the claim and recommended next step accordingly.

### Sufficient Evidence

- The answer does not imply runtime confirmation that never happened.

### Escalate

- The missing validation is central to safety or correctness.
