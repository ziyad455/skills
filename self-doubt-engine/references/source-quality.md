# Source Quality Policy

Use this file when the task depends on factual grounding, synthesis, conflict
resolution, or verification. The goal is to judge evidence quality explicitly instead of
treating every retrieved artifact as equal.

## Evidence Hierarchy

Prefer evidence in roughly this order, adjusted for task type:

1. Direct environment state
   Filesystem state, API response, system status, database row, test output, compiled
   result, or observed runtime behavior.
2. Primary or official source
   Vendor documentation, original paper, standards body text, government record, first
   party announcement, product changelog, or canonical policy.
3. Canonical internal source
   Repository code, internal spec, schema, owned documentation, or organization policy
   that is treated as the local source of truth.
4. High-quality secondary source
   A reputable synthesis that cites primary material accurately.
5. Tertiary commentary or anecdote
   Blog summaries, forum posts, unsourced claims, or hearsay.
6. Model memory
   Useful for hypotheses and orientation, not for freshness-sensitive or high-stakes
   claims.

Use stronger evidence when the claim is volatile, high-stakes, technical, or easily
checkable.

## Directness Levels

Label the support behind important claims:

- `observed`
  Directly seen in tool output, code execution, state inspection, or a source that
  states the fact explicitly.
- `derived`
  Computed or inferred from observed facts with a short, checkable reasoning step.
- `assumed`
  Plausible but not verified in the current environment or evidence set.

Do not phrase assumed claims as observed facts. If an answer depends on an assumption,
either verify it or bound it clearly.

## Recency Rules

- Stable topics can rely on older authoritative sources if the subject genuinely does
  not drift.
- Freshness-sensitive topics require current evidence. Include the relevant date or
  timestamp in the answer.
- If the user uses relative time words such as today, tomorrow, latest, or current, map
  them to an explicit date or state check.
- If a source is undated or obviously stale relative to the task, demote it sharply.

## Primary Vs Secondary Use

- For technical, legal, policy, scientific, or standards-heavy work, prefer primary
  sources.
- Use secondary sources for orientation, triangulation, or plain-language context, not
  as the sole support for central high-stakes claims.
- If secondary sources disagree with primary material, the primary material wins unless
  the scope differs.

## Corroboration Rules

- `low risk, stable`
  One strong direct source can be enough.
- `medium risk or surprising`
  Use one strong source plus one corroborating source, or direct execution plus a
  supporting reference.
- `high risk, volatile, or action-bearing`
  Prefer direct state plus corroboration, or multiple strong independent sources if
  direct state is unavailable.

Corroboration is not source counting. Two weak summaries do not outweigh one strong
primary source.

## Detecting Shallow Support

Support is shallow when any of these are true:

- The source is a paraphrase of another source rather than an independent basis.
- The claim appears only in marketing, commentary, or generated summaries.
- The evidence is adjacent to the question but not directly on point.
- A source is current in publication date but cites stale underlying data.
- The answer depends on one brittle inference step that was not checked.
- The agent gathered many sources but most trace back to the same original claim.

If support is shallow, deepen quality before deepening quantity.

## Conflict Resolution Policy

When sources disagree:

1. Compare scope. They may be talking about different versions, dates, entities, or
   jurisdictions.
2. Compare directness. Prefer the source closest to the fact.
3. Compare authority. Prefer canonical owners of the underlying truth.
4. Compare recency. Prefer the source current for the claim in question.
5. Compare completeness. Prefer the source that addresses the actual user question.

If the conflict remains unresolved, say so explicitly. Do not synthesize a false
consensus.

## Environment State Beats Memory

If the runtime can directly inspect the relevant state, that observation outranks model
memory and generic knowledge. Examples:

- Run the code instead of guessing behavior.
- Inspect the repository instead of assuming framework defaults.
- Check the API or database state instead of reasoning from old docs.
- Look at the live page or structured record instead of using cached descriptions.

## Outdated Or Missing Evidence

If evidence is weak, stale, or unavailable:

- Narrow the claim to what is actually supported.
- State the missing piece that blocks stronger confidence.
- Ask for the specific input or permission that would resolve it.
- Abstain from high-stakes certainty or irreversible action.

## False Synthesis Traps

Avoid these failure patterns:

- Treating volume of sources as evidence of truth.
- Picking the nicest phrasing rather than the strongest support.
- Merging incompatible definitions into one answer.
- Treating consensus among copied summaries as corroboration.
- Mistaking a plausible explanation for a verified mechanism.
