# Self-Doubt Engine Skills Repository

This repository is organized as a GitHub-compatible Agent Skills repository with one
published skill:

- `self-doubt-engine`

The repository layout now matches the Agent Skills model used by GitHub’s `gh skill`
command and the open Agent Skills specification: each skill lives in its own directory,
and the directory name matches the `name` field in `SKILL.md`.

## Repository Layout

```text
.
├── README.md
└── self-doubt-engine/
    ├── SKILL.md
    ├── references/
    │   ├── clarification-policy.md
    │   ├── coding-funnels.md
    │   ├── evaluation-rubric.md
    │   ├── examples.md
    │   ├── output-contracts.md
    │   ├── research-funnels.md
    │   ├── runtime-portability.md
    │   ├── source-quality.md
    │   └── validation-policy.md
    └── scripts/
        └── validate_skill.py
```

## GitHub Compatibility

This repo is organized for GitHub’s new `gh skill` workflow and for the broader Agent
Skills ecosystem.

Key compatibility choices:

- The skill is in its own folder: `self-doubt-engine/`
- The folder contains a required `SKILL.md`
- The frontmatter `name` is `self-doubt-engine`, which matches the folder name
- Optional resources are kept in standard `references/` and `scripts/` directories
- All file references in `SKILL.md` are relative to the skill root

That structure matters because:

- the Agent Skills specification defines a skill as a directory containing `SKILL.md`
- the spec requires the `name` field to match the parent directory name
- GitHub’s skills documentation expects each skill to live in its own subdirectory
- `gh skill install OWNER/REPOSITORY SKILL` is designed around repos that expose one or
  more named skill directories

## Install With GitHub CLI

Once this repository is published on GitHub, the intended install shape is:

```bash
gh skill install OWNER/REPOSITORY self-doubt-engine
```

You can also target a specific host:

```bash
gh skill install OWNER/REPOSITORY self-doubt-engine --agent codex
gh skill install OWNER/REPOSITORY self-doubt-engine --agent claude-code
gh skill install OWNER/REPOSITORY self-doubt-engine --agent cursor
```

If you publish tagged releases, the same repo layout also supports versioned installs:

```bash
gh skill install OWNER/REPOSITORY self-doubt-engine@v1.0.0
gh skill install OWNER/REPOSITORY self-doubt-engine --pin v1.0.0
```

## What The Skill Does

`self-doubt-engine` is a unified control layer for tool-using agents.

It combines:

- evidence-gated research and factual verification
- freshness-sensitive retrieval policy
- coding-task readiness control
- proportional validation and action gating
- explicit conflict, ambiguity, and escalation handling
- output contracts that keep findings, inference, and uncertainty separate

Its central question is:

> Before I answer, implement, or act, do I have enough support for this exact task at
> this level of risk?

## Skill Architecture

The skill package is split into one control file and a set of focused references.

### `self-doubt-engine/SKILL.md`

This is the control plane.

It defines:

- when the skill should trigger
- the main control loop
- task classification axes
- routing rules
- the coding overlay
- sufficiency, verification, escalation, and output expectations
- progressive disclosure rules for loading references only when needed

### Research Reference Layer

- `self-doubt-engine/references/research-funnels.md`
  Main non-coding workflows such as fast factual lookup, freshness-critical retrieval,
  deep research synthesis, conflict resolution, recommendation analysis, and
  irreversible action gating
- `self-doubt-engine/references/source-quality.md`
  Evidence ranking, recency rules, corroboration policy, and weak-support detection

### Coding Reference Layer

- `self-doubt-engine/references/coding-funnels.md`
  Coding workflows such as fast patch, clarification-first, bug diagnosis and fix,
  feature implementation, refactor with invariants, and high-risk change gating
- `self-doubt-engine/references/clarification-policy.md`
  Rules for deciding when ambiguity is material enough to block implementation
- `self-doubt-engine/references/validation-policy.md`
  Rules for light, standard, strong, and constrained validation

### Output And Portability Layer

- `self-doubt-engine/references/output-contracts.md`
  Response patterns for grounded answers, coding delivery, and high-risk change reports
- `self-doubt-engine/references/runtime-portability.md`
  Maps the policy onto generic capabilities such as retrieval, repo inspection,
  execution, validation, code modification, and action gating

### Quality Layer

- `self-doubt-engine/references/evaluation-rubric.md`
  Scores routing, evidence quality, stopping behavior, coding readiness, validation
  honesty, and action safety
- `self-doubt-engine/references/examples.md`
  Shows weak versus upgraded behavior across research and coding tasks

### Validation Script

- `self-doubt-engine/scripts/validate_skill.py`
  Checks structure, required content, link integrity, metadata alignment, and now also
  enforces that the frontmatter `name` matches the skill directory name

## How The Skill Works

At runtime, the skill follows this pattern:

1. Classify the task.
2. Choose the right research or coding funnel.
3. Gather the minimum decisive evidence.
4. Test whether that evidence is sufficient.
5. Verify proportionally to risk and reversibility.
6. Return, implement, act, or escalate with explicit support.

This prevents the common failure mode of using one shallow workflow for every task.

## Research Coverage

The skill includes ten research funnels:

1. Fast factual lookup
2. Freshness-critical retrieval
3. Deep research synthesis
4. Code and data validation
5. Recommendation and comparison analysis
6. Irreversible action gating
7. Ambiguity resolution
8. Internal knowledge lookup
9. Multi-source conflict resolution
10. Expert-mode deep dive

Each funnel defines:

- when it triggers
- the operating sequence
- what counts as sufficient evidence
- when to stop
- when to escalate

## Coding Coverage

The skill also includes a coding-specific overlay with eight implementation funnels:

1. Fast patch
2. Clarification-first
3. Bug diagnosis and fix
4. Feature implementation
5. Refactor with invariants
6. High-risk change gating
7. Validation and delivery check
8. Limited-validation fallback

The coding layer exists to reduce:

- wrong-first-build implementations
- hidden assumptions becoming code structure
- untested code being presented as confirmed
- superficial checks being mistaken for real validation

## Evidence Model

The skill explicitly ranks evidence. In general it prefers:

1. direct environment state
2. primary or official sources
3. canonical internal sources
4. high-quality secondary sources
5. tertiary commentary or anecdote
6. model memory

It also requires important claims to be treated as:

- `observed`
- `derived`
- `assumed`

That distinction is central to the project. It is how the skill prevents polished but
weakly supported outputs.

## Validation Model

The skill uses proportional validation rather than uniform validation.

For general tasks:

- low risk
- medium risk
- high risk or hard-to-undo
- irreversible action

For coding tasks:

- light
- standard
- strong
- constrained

The goal is strategic validation, not maximum validation.

## Local Validation

Validate the skill package from the repository root with:

```bash
python3 self-doubt-engine/scripts/validate_skill.py
```

This validator checks the package structure expected by the repository and the spec.

## Publishing Guidance

If you publish this repo for GitHub skill installation:

- keep `self-doubt-engine/` as the stable skill directory
- tag releases if you want reproducible installs
- avoid renaming the skill directory unless you also change the frontmatter `name`
- keep `SKILL.md` references relative and one level deep
- validate before publishing or tagging

## Extending The Repo

If you later add more skills, the correct pattern is:

```text
.
├── README.md
├── self-doubt-engine/
│   └── SKILL.md
└── another-skill/
    └── SKILL.md
```

Each additional skill should:

- live in its own lowercase hyphenated directory
- contain its own `SKILL.md`
- keep its internal resources inside that skill directory
- keep its `name` field aligned with the directory name

## Current State

This repository currently contains one GitHub-compatible skill directory:

- `self-doubt-engine`
