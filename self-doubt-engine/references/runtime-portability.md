# Runtime Portability

This skill defines policy, not product-specific mechanics. Map the policy onto whatever
capabilities the current agent stack provides.

## Capability Mapping

Translate runtime features into these generic categories:

- `external retrieval`
  Web search, browser automation, HTTP fetch, documentation search, news lookup.
- `internal retrieval`
  Local files, repository search, internal knowledge base, vector search, wiki, shared
  drive, or memory store.
- `structured lookup`
  SQL, GraphQL, API calls, spreadsheet queries, issue trackers, ticket systems, or
  metadata inspection.
- `state inspection`
  Filesystem inspection, environment variables, app state, logs, deployment status,
  process state, or configuration reads.
- `code execution`
  Tests, scripts, notebooks, REPLs, build tools, or query execution.
- `validation`
  Linters, schema checks, dry runs, previews, checksum comparison, or spot checks.
- `action tool`
  Any capability that changes external or internal state.
- `escalation`
  Ask the user, request approval, defer, abstain, or hand off.
- `repo inspection`
  File reads, symbol lookup, dependency inspection, config inspection, or test discovery.
- `code modification`
  Patch application, editor actions, code generation, or file creation.

Use the policy described in `SKILL.md` even when the concrete tool names differ.

## Fallback Order

If the preferred capability is unavailable:

1. Use the strongest available equivalent.
2. Reduce the claim to what the available evidence can support.
3. Ask for the minimum missing input if the gap is user-resolvable.
4. Abstain from strong claims or irreversible actions when the missing capability blocks
   safe execution.

Do not pretend tool absence is proof of impossibility.

## Portability Rules

- Prefer categories of evidence, not vendor-specific tool names.
- Do not assume the runtime supports browsing, code execution, or persistent state.
- Do not assume one brand's safety model, approval flow, or orchestration layer.
- If a stack offers multiple equivalent tools, pick the one that produces the strongest
  and most inspectable evidence.

## When Tools Are Weak

If the stack only supports limited retrieval or no execution:

- Tighten the scope of the answer.
- Increase explicitness around assumptions.
- Avoid operational or high-stakes certainty.
- Recommend the exact validation step an operator should run outside the agent.

If the stack only supports weak coding tools:

- inspect the local source of truth before assuming framework conventions
- isolate assumptions in the implementation and in the delivery note
- stop short of claiming a bug is fixed or a feature is confirmed without runtime proof

## Action Gating Across Stacks

Regardless of platform:

- Verify target and scope from live state when possible.
- Prefer preview or dry run before mutation.
- Require explicit confirmation for ambiguous destructive actions.
- Report whether the action is ready, blocked, or deferred.

Across coding environments:

- verify target files and scope before broad edits
- avoid wide refactors when the requested change is local
- gate migrations, deletions, and external side effects behind stronger checks
