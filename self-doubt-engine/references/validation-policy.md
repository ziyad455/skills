# Validation Policy

Use this file to choose validation depth for coding tasks. The correct level depends on
blast radius, failure cost, and what the environment actually allows.

## Validation Priority

Prefer validation that directly observes the changed behavior:

1. Focused execution of the changed path
2. Relevant automated tests
3. Integration or end-to-end checks
4. Type checking and linting
5. Static inspection and reasoning

Static reasoning is useful, but it is weaker than observed behavior.

## Levels

### Light

Use when:

- the change is local and low-risk
- the behavior is straightforward
- failure would be cheap to correct

Typical checks:

- run one focused test or execution path if available
- inspect for obvious regressions
- confirm inputs and outputs match the request

### Standard

Use for most normal coding tasks.

Typical checks:

- relevant tests for changed modules
- lint and type check when meaningful
- targeted runtime check or spot check
- verify one likely edge case

### Strong

Use when the cost of being wrong is high.

Typical checks:

- primary path plus boundary and failure-path validation
- integration coverage for touched dependencies
- regression checks for adjacent behavior
- explicit review of data safety, security, or side effects

### Constrained

Use when execution is blocked.

Typical checks:

- static contract tracing
- configuration and type inspection
- detailed limitation note describing missing runtime proof

## Validation Triggers By Change Type

- `bug fix`
  Validate the original failure path plus one nearby regression path.
- `feature`
  Validate the main success case plus one meaningful edge or error path.
- `refactor`
  Validate preserved invariants, not only style or compilation.
- `performance`
  Validate with comparative measurement or an explicit proxy, not intuition alone.
- `data mutation or migration`
  Validate selection scope, idempotence or rollback assumptions, and adverse cases.
- `external integration`
  Validate request shape, error handling, and side-effect safety.
- `security-sensitive`
  Validate both allowed and disallowed paths.

## Strong-Signal Failures

Validation is not yet sufficient when:

- only happy-path checks exist for risky logic
- the test run misses the changed path
- build passes but behavior was never exercised
- code was reviewed but not executed where execution was available
- a bug fix was not checked against the original failure signal

## Delivery Honesty Rule

Before finalizing, classify the result:

- `verified`
  The claimed behavior was directly checked.
- `partially verified`
  Some relevant checks ran, but important coverage is missing.
- `unverified`
  The code was written or reviewed but not observed in execution.

Match the delivery language to this classification.
