---
name: self-doubt-engine
description: >
  Evidence-gated control layer for tool-using agents. Use this skill whenever an
  answer, recommendation, code result, code change, data result, or external action
  depends on retrieval, execution, validation, or real-world state. It classifies
  risk, freshness, ambiguity, readiness, and evidence needs; routes work into the
  right research, coding, or verification funnel; decides when to clarify, deepen
  work, implement, validate, or stop; and makes the final output explicit about what
  was checked, what is inferred, and what remains uncertain.
compatibility: >
  Portable across GitHub Copilot, GitHub CLI gh skill, Codex, Claude Code, Cursor,
  Gemini CLI, and similar agent hosts. Full benefit assumes repository inspection and
  optional code execution for validation-heavy tasks.
---

# Self-Doubt Engine: Evidence Control For Tool-Using Agents

Self-Doubt Engine is not a tone setting. It is an evidence-control system for agents
that use tools, browse, inspect state, execute code, analyze data, or take actions.

Its governing question is:

**Before I answer or act, do I have enough support for this exact task at this level
of risk?**

If the answer is yes, move quickly. If the answer is no, deepen the work, narrow the
claim, or escalate. Do not replace missing support with confident prose or nervous
hedging.

## Use This Skill

Invoke this skill whenever at least one of these is true:

- The response depends on external retrieval, internal retrieval, code execution, data
  analysis, state inspection, or tool output.
- The task asks the agent to write, modify, refactor, debug, review, or deliver code.
- The user asked for the latest, current, live, today, recent, or environment-specific
  state.
- The agent is making a recommendation, comparison, or synthesis rather than repeating
  one source.
- The task could trigger an irreversible or costly action.
- The request is ambiguous enough that the answer or action could change materially.
- The task is high-stakes, compliance-sensitive, money-sensitive, safety-sensitive, or
  operationally important.

Do not use this skill for purely creative tasks, casual brainstorming with no factual
stakes, or simple transformations where the user supplied all required content.

## Mission

Convert vague confidence into explicit evidence-backed behavior:

- Choose the right workflow for the task instead of using one generic search pattern.
- Decide whether a coding task is ready to implement or still needs clarification.
- Distinguish stable facts from freshness-sensitive state.
- Prefer direct evidence over intuition.
- Verify proportionally to the cost of being wrong.
- Stop when the evidence is sufficient, not when the agent is tired of searching.
- Surface ambiguity and conflict explicitly instead of smoothing them away.
- Produce outputs that separate findings, inference, uncertainty, and next actions.

## Core Loop

Run this loop before answering or acting:

1. Classify the task on the axes below.
2. Route to the matching funnel in [references/research-funnels.md](references/research-funnels.md)
   or [references/coding-funnels.md](references/coding-funnels.md).
3. Gather the minimum decisive evidence needed for that funnel.
4. Test whether the evidence is sufficient.
5. Apply proportional verification based on risk and reversibility.
6. Return, act, defer, or escalate with an explicit evidence account.

Do not skip routing. Many failures come from using a fast lookup workflow on a deep
research task, or a reasoning-only workflow on a state-dependent task.

## Task Classification

Classify each task across these axes before choosing depth:

- `task shape`
  Fast fact, freshness check, research synthesis, code or data validation,
  coding patch, feature implementation, bug diagnosis, refactor, recommendation,
  internal-knowledge lookup, action request, conflict resolution, or expert deep dive.
- `evidence source`
  Model memory, internal documents, external sources, structured system state,
  executable validation, or user-provided material.
- `readiness state`
  Ready, conditional, or blocked by ambiguity.
- `freshness sensitivity`
  Stable, time-sensitive, or live-state dependent.
- `risk of error`
  Low, medium, or high impact if wrong.
- `reversibility`
  Easy to undo, costly to undo, or irreversible.
- `ambiguity`
  Low, moderate, or high ambiguity in the request, definitions, or success criteria.

If the answer depends on current reality, prefer runtime evidence over memory. If the
answer depends on how something behaves, prefer direct execution or state inspection
over explanation-only reasoning.

## Routing Rules

Use this fast router. Read the detailed funnel only after selecting it.

- If the user needs a bounded fact and the claim is likely stable, use `fast factual
  lookup`.
- If the task is about latest, current, today, recent, live state, or changing rules,
  use `freshness-critical retrieval`.
- If the answer requires combining multiple sources, tradeoffs, or broader context, use
  `deep research synthesis`.
- If the task involves code behavior, calculations, transformations, queries, or data
  outputs, use `code and data validation`.
- If the task asks the agent to write, modify, debug, refactor, review, or deliver
  code, add the coding overlay and route through
  [references/coding-funnels.md](references/coding-funnels.md).
- If the user wants a recommendation, ranking, or comparison, use `recommendation and
  comparison analysis`.
- If the task would send, write, delete, modify, publish, purchase, or otherwise act on
  the world, use `irreversible action gating`.
- If the request could plausibly mean multiple materially different things, use
  `ambiguity resolution`.
- If the answer depends on local files, workspace state, internal docs, or
  organization-specific knowledge, use `internal knowledge lookup`.
- If retrieved evidence disagrees on a central claim, use `multi-source conflict
  resolution`.
- If the user explicitly wants thoroughness or the problem remains hard after the first
  pass, use `expert-mode deep dive`.

## Non-Negotiable Policy

- Treat confidence as a hint, not as evidence.
- Prefer direct observation, execution, or authoritative sources over summaries.
- Mark claims internally as `observed`, `derived`, or `assumed`. Do not present assumed
  claims as observed facts.
- Do not cite weak evidence as if it were decisive support.
- Do not average away contradictions. Explain them or preserve them.
- Do not browse endlessly. Stop when the funnel's sufficiency criteria are met.
- Do not stop early when a central claim is still supported only by one weak or stale
  source.
- Do not confuse plausible code with working code.
- Do not hide material product or interface assumptions inside implementation details.
- Do not perform high-impact actions until preconditions are checked against actual
  state.

## Coding Overlay

When the task includes code authoring, debugging, refactoring, or delivery, add this
overlay on top of the core policy:

- Decide whether the task is `ready`, `conditional`, or `blocked` before coding.
- Clarify only when ambiguity would materially change the implementation, validation
  plan, or user-visible behavior.
- Prefer repository inspection and direct runtime evidence over generic framework
  assumptions.
- Choose the smallest implementation that satisfies the request and keeps assumptions
  visible.
- Validate at the strongest practical level before claiming the result works.
- Distinguish `implemented`, `partially verified`, and `verified` outcomes in the final
  answer.

Load:

- [references/coding-funnels.md](references/coding-funnels.md)
  for coding-task workflow selection
- [references/clarification-policy.md](references/clarification-policy.md)
  when deciding whether to ask before coding
- [references/validation-policy.md](references/validation-policy.md)
  when deciding how much validation is required before delivery

## Sufficiency Test

Evidence is sufficient only when all of the following hold:

- The evidence directly addresses the user's real question, not a nearby one.
- The strongest available source type for the task has been checked when practical.
- The answer is stable enough for the task's freshness and risk profile.
- Any central inference is short, explicit, and supported by visible premises.
- Remaining uncertainty would not materially change the answer, or it is clearly called
  out.

If any of these fail, deepen the work, narrow the claim, or escalate.

## Verification Ladder

Match verification effort to risk.

- `low risk`
  Re-read against the request, confirm no obvious omissions, and verify any easy
  factual dependency.
- `medium risk`
  Add at least one strong external check, execution check, or corroborating source.
  Confirm edge conditions that could flip the answer.
- `high risk or hard-to-undo`
  Validate against direct state or primary evidence, confirm critical preconditions, dry
  run when possible, and do not hide unresolved blockers.
- `irreversible action`
  Verify target, scope, permissions, and consequences immediately before acting. If any
  critical input is ambiguous, stop and ask or defer.

## Escalation Rules

Escalate, abstain, or ask for clarification when any of these holds:

- A high-stakes answer depends on unavailable or untrusted evidence.
- An action request has ambiguous target, scope, or intent.
- Central sources conflict and the conflict cannot be resolved with better evidence.
- The environment needed for validation is unavailable.
- The user asked for certainty that the evidence does not support.
- The cost of a wrong action is high and confirmation is cheap but missing.

When escalating, state:

- what is known
- what is still uncertain
- why the uncertainty matters
- what exact check, input, or approval would unlock progress

## Output Contract

Every final answer should reflect the quality of the evidence, not just the raw
conclusion.

- Answer the real task first.
- Separate findings from inference when the distinction matters.
- Mention what was checked when the user cannot see the validation steps.
- Bound uncertainty tightly. Do not use vague disclaimers.
- If evidence is conflicting, present the best-supported reading and the live conflict.
- If the task is action-oriented, state whether the action is ready, blocked, or needs
  confirmation.

For reusable response patterns, load
[references/output-contracts.md](references/output-contracts.md).

## Progressive Disclosure

Keep this file as the control layer. Load only the references needed for the task:

- [references/research-funnels.md](references/research-funnels.md)
  Read when routing the task or when the initial approach is too shallow.
- [references/coding-funnels.md](references/coding-funnels.md)
  Read when the task includes code implementation, debugging, refactoring, or delivery.
- [references/clarification-policy.md](references/clarification-policy.md)
  Read when deciding whether a coding task is clear enough to build.
- [references/validation-policy.md](references/validation-policy.md)
  Read when selecting the right validation depth for code changes.
- [references/source-quality.md](references/source-quality.md)
  Read for factual work, conflicting evidence, freshness-sensitive tasks, technical
  claims, or high-stakes outputs.
- [references/output-contracts.md](references/output-contracts.md)
  Read when the answer needs stronger structure, clearer uncertainty handling, or action
  gating language.
- [references/runtime-portability.md](references/runtime-portability.md)
  Read when the runtime lacks standard tools or uses unfamiliar tool names.
- [references/examples.md](references/examples.md)
  Read when the right depth or funnel choice is unclear.
- [references/evaluation-rubric.md](references/evaluation-rubric.md)
  Read when auditing the skill, benchmarking its behavior, or refining failures.

## Failure Modes To Actively Avoid

- Returning a polished answer that rests on one weak source.
- Treating old information as current because it matches model memory.
- Confusing correlation, default behavior, or convention with direct confirmation.
- Claiming synthesis while merely paraphrasing one source.
- Running more searches without improving source quality or decision relevance.
- Asking for clarification on low-risk ambiguity that can be resolved with a bounded
  assumption.
- Building immediately from an underspecified coding request.
- Declaring a bug fixed or a feature complete without validating the relevant behavior.
- Taking an irreversible action after verifying only the general idea, not the exact
  target or scope.

## Minimal Completion Standard

The skill has done its job only if the agent can answer:

- Which funnel did I use, and why?
- What is the strongest evidence behind the main claim?
- What would most likely make this answer wrong?
- Did I verify proportionally to the risk?
- If code changed, was the task actually ready to implement and what validation directly
  supports the claimed behavior?
- Is the output explicit about what was observed, inferred, and still open?
