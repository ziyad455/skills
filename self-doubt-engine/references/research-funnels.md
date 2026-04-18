# Research Funnels

Use this file to choose and execute the right evidence workflow. Do not use every
funnel on every task. Pick the shallowest funnel that can still support the required
quality bar.

## Quick Router

| Funnel | Trigger | Minimum decisive evidence | Stop when | Escalate when |
| --- | --- | --- | --- | --- |
| Fast factual lookup | Bounded stable fact | One strong direct or authoritative source | The answer is directly supported and low-risk | The fact is stale, ambiguous, or unexpectedly disputed |
| Freshness-critical retrieval | Latest, current, live, recent, today's | Current state from live or current-date sources | Date-sensitive claim is grounded in current evidence | Sources are stale, status is changing, or time zone matters |
| Deep research synthesis | Multi-source explanation or synthesis | Multiple high-quality sources that cover the main subquestions | Major subquestions are answered or bounded | Key dimensions remain unsupported |
| Code and data validation | Code behavior, queries, calculations, outputs | Direct execution, tests, spot checks, or state inspection | Behavior is observed and matches the claim | Validation environment is missing or inconsistent |
| Recommendation and comparison analysis | Best option, ranking, tradeoffs | Evidence per criterion for the leading candidates | A defensible top choice or shortlist is clear | User criteria are underspecified and change the result |
| Irreversible action gating | Send, write, delete, modify, publish, purchase | Verified target, scope, permissions, and consequences | Preconditions are checked and action is safe to take | Target or scope remains ambiguous |
| Ambiguity resolution | Multiple plausible interpretations | A resolved interpretation or bounded assumption set | One interpretation is justified enough to proceed | Different interpretations lead to materially different outcomes |
| Internal knowledge lookup | Workspace, local files, internal docs, org policy | Canonical internal source or direct environment state | The local truth source is identified and checked | Internal sources conflict or are stale |
| Multi-source conflict resolution | Central sources disagree | Ranked evidence showing why one reading wins or why conflict remains | Conflict is resolved or clearly bounded | No source can be shown superior |
| Expert-mode deep dive | Complex, contentious, high-value, or explicitly thorough work | Structured evidence map across subquestions | Marginal new search returns little new decision value | Core questions remain open after a strong pass |

## 1. Fast Factual Lookup

### Trigger

- The question is narrow and answerable with one or two claims.
- The subject is likely stable over time.
- The cost of being wrong is low to moderate.

### Sequence

1. Rewrite the question into the exact claim to verify.
2. Check whether the claim is stable or actually freshness-sensitive.
3. Retrieve one strong direct or authoritative source.
4. If the source directly answers the claim and there are no red flags, answer.
5. Add one corroborating source only if the first source is indirect, surprising, or
   medium-stakes.

### Sufficient Evidence

- The main claim is directly supported by a strong source.
- Definitions and units match the user's question.
- No overlooked ambiguity changes the answer.

### Stop Signals

- Additional searching is only finding paraphrases of the same fact.
- New sources add no decision-relevant detail.

### Escalate

- The user implicitly needs current information.
- The top source is weak, stale, or secondary.
- The answer changes depending on definition or jurisdiction.

## 2. Freshness-Critical Retrieval

### Trigger

- The user asked for latest, current, live, today, recent, now, or a status that could
  change.
- The task involves laws, prices, schedules, product versions, personnel, incidents, or
  anything that can drift.

### Sequence

1. Anchor the task to the current date, time, and relevant time zone.
2. Prefer live system state or current official sources over memory or old summaries.
3. Gather the freshest direct evidence available.
4. Cross-check one more source when the first source is not canonical or when the task
   is high-stakes.
5. State the relevant date or timestamp in the output.

### Sufficient Evidence

- Evidence is current enough for the claim.
- The answer references the relevant date or live state.
- A stale source is not carrying the core claim.

### Stop Signals

- The answer is grounded in the most authoritative current source available.
- Any remaining uncertainty is caused by the source itself being in flux, not by search
  shallowness.

### Escalate

- Sources disagree because the situation is actively changing.
- The only available evidence is stale relative to the task.
- Time zone or cutoff rules could flip the answer.

## 3. Deep Research Synthesis

### Trigger

- The user wants explanation, synthesis, or a structured overview across multiple
  dimensions.
- One source cannot answer the whole task.

### Sequence

1. Decompose the task into a small set of answer-bearing subquestions.
2. Decide what source type is strongest for each subquestion.
3. Retrieve strategically; do not gather sources without a role.
4. Build a compact evidence map: subquestion, source, claim, confidence, open gaps.
5. Synthesize only after the main subquestions are covered.
6. Preserve unresolved gaps instead of inventing coherence.

### Sufficient Evidence

- The answer's major claims are each supported by at least one strong source.
- Important counterevidence or disagreement has been checked.
- The synthesis adds value beyond repeating a single source.

### Stop Signals

- Remaining gaps are peripheral rather than central.
- New sources repeat known claims without changing the synthesis.

### Escalate

- The task is too broad to answer well without narrowing scope.
- One major dimension is still weakly supported.
- The user likely needs a recommendation or action plan rather than a survey.

## 4. Code And Data Validation

### Trigger

- The answer depends on how code behaves, whether a query works, what a calculation
  produces, or whether a transformation succeeded.

### Sequence

1. Identify the exact artifact to validate: function behavior, file change, query, test,
   metric, or transformed output.
2. Prefer direct execution, tests, linting, schema validation, or spot checks over
   reasoning-only review.
3. Check representative and edge cases that could flip the conclusion.
4. If full validation is impossible, say precisely what was not executed or observed.

### Sufficient Evidence

- The key claim about behavior or output is directly observed.
- Validation covers the most likely failure mode, not only the happy path.
- The answer distinguishes "I changed it" from "I verified it works."

### Stop Signals

- The validated result matches the claim and no higher-risk edge case remains obvious.
- Additional runs would be redundant given the requested scope.

### Escalate

- The required runtime, dependencies, permissions, or fixtures are unavailable.
- The observed result is inconsistent across environments or runs.
- The request implies production safety that local checks cannot establish.

## 5. Recommendation And Comparison Analysis

### Trigger

- The user asks what is best, better, worth choosing, or how options compare.

### Sequence

1. Extract or infer decision criteria.
2. If criteria are missing and the choice is sensitive to them, ask or present a
   conditional recommendation.
3. Build a candidate set broad enough to be credible but narrow enough to evaluate.
4. Evaluate candidates against the criteria using evidence rather than vibes.
5. Produce a recommendation, shortlist, or decision tree with tradeoffs.

### Sufficient Evidence

- The top recommendation is tied to explicit criteria.
- Tradeoffs are grounded in evidence, not trendiness.
- Excluded candidates were excluded for a reason.

### Stop Signals

- The top options separate cleanly under the user's constraints.
- Further search mostly adds more of the same candidates.

### Escalate

- Unknown user constraints dominate the choice.
- The market is changing quickly and current availability matters.
- Evidence is mostly marketing or anecdote.

## 6. Irreversible Action Gating

### Trigger

- The agent is about to send, write, delete, merge, publish, purchase, alter state, or
  trigger an external workflow.

### Sequence

1. Restate the proposed action in concrete terms: target, scope, payload, and effect.
2. Verify the target and scope against actual state, not memory.
3. Confirm permissions, prerequisites, and side effects.
4. Prefer dry run, preview, or simulation when available.
5. If ambiguity remains on a critical field, stop and clarify.
6. Only execute once the preconditions are satisfied.

### Sufficient Evidence

- The exact target is confirmed.
- The intended scope matches the user's likely intent.
- The action is safe, permitted, and appropriately timed.

### Stop Signals

- All critical preconditions are explicitly verified.
- There is no live ambiguity about object, audience, amount, or scope.

### Escalate

- The action is destructive or public and the target is not explicit.
- A preview or direct confirmation is unavailable.
- The agent cannot inspect the relevant state before acting.

## 7. Ambiguity Resolution

### Trigger

- The request contains ambiguous entities, vague success criteria, or multiple plausible
  meanings.

### Sequence

1. List the interpretations that would materially change the answer or action.
2. Resolve from context if one interpretation is clearly dominant and low-risk.
3. If low-risk and answerable, proceed with a bounded assumption and state it.
4. If high-risk or action-bearing, ask one concise clarification question or provide
   clearly separated branches.

### Sufficient Evidence

- One interpretation is supported strongly enough to proceed, or the output clearly
  branches.

### Stop Signals

- Further analysis is not reducing ambiguity without new user input.

### Escalate

- Different interpretations change the outcome materially.
- An irreversible action depends on the ambiguous field.

## 8. Internal Knowledge Lookup

### Trigger

- The answer depends on workspace files, internal docs, project conventions, policies,
  repositories, or local environment state.

### Sequence

1. Identify the most canonical internal source.
2. Prefer direct file, configuration, schema, or environment inspection over memory.
3. Check neighboring artifacts when the canonical source might be stale or partial.
4. Distinguish local truth from assumptions based on common patterns.

### Sufficient Evidence

- The answer points to the local source of truth or observed state.
- Environment-specific claims are based on actual inspection.

### Stop Signals

- The relevant local artifact has been checked directly.
- Additional internal search is only duplicating the same signal.

### Escalate

- Internal docs conflict with runtime state.
- No canonical source exists for the question.

## 9. Multi-Source Conflict Resolution

### Trigger

- Strong sources disagree on a claim that matters to the answer.

### Sequence

1. Identify the exact point of disagreement.
2. Rank the sources by directness, authority, recency, scope, and relevance.
3. Check whether the conflict is actually caused by different definitions, dates, or
   jurisdictions.
4. Prefer the source that best matches the user's scope and the current state.
5. If no clean winner exists, preserve the disagreement explicitly.

### Sufficient Evidence

- The conflict is resolved with a defensible reason, or it is clearly bounded.
- The final answer does not flatten genuine disagreement into a false consensus.

### Stop Signals

- Further sources are weaker than the sources already compared.
- The residual disagreement is inherent rather than caused by shallow search.

### Escalate

- The conflict sits between equally strong sources.
- The answer would be high-stakes if the wrong side were chosen.

## 10. Expert-Mode Deep Dive

### Trigger

- The user explicitly requests a thorough investigation.
- The problem is complex, contentious, high-value, or still unresolved after the first
  appropriate funnel.

### Sequence

1. Frame the end product: decision memo, technical brief, recommendation, failure
   analysis, or research synthesis.
2. Break the problem into subquestions and dependencies.
3. Use the best funnel for each subquestion rather than one monolithic search stream.
4. Track an evidence ledger so claims do not detach from support.
5. Revisit the question after the first pass and identify the highest-value remaining
   gap.
6. Stop when the next search step is unlikely to change the conclusion materially.

### Sufficient Evidence

- Core claims are covered by strong evidence.
- The remaining uncertainty is explicitly bounded.
- The report shows synthesis rather than accumulation.

### Stop Signals

- New effort is yielding only marginal refinements.
- The user would gain little from additional retrieval relative to the delay.

### Escalate

- Solving the remaining gaps requires unavailable expertise, data, or permissions.
- The user should narrow the problem before further work is efficient.
