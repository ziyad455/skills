# Clarification Policy

Use this file to decide whether to ask questions before coding. The goal is not to ask
more questions. The goal is to avoid wrong implementation caused by material ambiguity.

## Ask Before Building When

- Different reasonable interpretations produce different code, interfaces, or tests.
- The environment, framework version, runtime, or deployment target changes the design.
- The request leaves success criteria too vague to validate.
- The agent would have to choose a product behavior, policy, or UX decision.
- Edge-case handling could change real-world correctness or safety.
- The user asked for production readiness, but the non-functional constraints are absent.

## Do Not Ask When

- The task is standard and conventions are dominant.
- The missing detail can be satisfied by a safe default.
- The assumption can be isolated cleanly and changed later with low cost.
- The user clearly wants a prototype, example, or draft.
- Clarification would not meaningfully reduce wrong-build risk.

## Material Ambiguity Test

An ambiguity is material only if resolving it would likely change one of:

- architecture
- interface
- data contract
- validation strategy
- security posture
- performance profile
- user-visible behavior

If it would not change one of these in a meaningful way, proceed.

## Question Quality Rules

When clarification is needed:

- Ask the smallest number of questions that will unblock correct implementation.
- Prefer concrete either-or questions when appropriate.
- Tie each question to why it changes the code.
- Avoid asking for information that can be discovered from the codebase or environment.

## Repository-First Resolution

Before asking, try to resolve ambiguity from:

- existing code patterns
- tests
- types and interfaces
- configuration
- documentation and comments
- neighboring modules

Only ask the user when the repository cannot answer the question reliably.

## Safe Assumption Policy

Proceed with a bounded assumption only when all of these are true:

- the task is low-risk
- the assumption follows strong local convention
- changing it later would be cheap
- the assumption is disclosed in the delivery note if it still matters

## Stop Conditions

Stop and ask before coding when:

- implementation would lock in a product decision
- the agent would otherwise invent a contract
- the wrong assumption would create costly rework
- validation cannot be defined without the missing information
