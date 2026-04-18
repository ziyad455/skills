# Self-Doubt Engine

A skill for AI agents that makes them stop and verify before they act.

## What It Does

Most agents answer too fast. They guess, hallucinate, or skip validation.

The **Self-Doubt Engine** adds a control layer that asks one question before every response:

> *Do I have enough evidence to answer, code, or act on this — at this level of risk?*

If yes, it proceeds. If not, it retrieves more, flags uncertainty, or escalates.

## Install

```bash
gh skill install ziyad455/skills self-doubt-engine
```

Target a specific agent:

```bash
gh skill install ziyad455/skills self-doubt-engine --agent claude-code
gh skill install ziyad455/skills self-doubt-engine --agent codex
gh skill install ziyad455/skills self-doubt-engine --agent cursor
```

Pin to a version:

```bash
gh skill install ziyad455/skills self-doubt-engine@v1.0.0
```

## What's Inside

```
self-doubt-engine/
├── SKILL.md               ← Main control file (start here)
└── references/
    ├── research-funnels.md      ← When and how to look things up
    ├── coding-funnels.md        ← When and how to write or change code
    ├── source-quality.md        ← How to rank evidence
    ├── clarification-policy.md  ← When to ask before building
    ├── validation-policy.md     ← How much to verify, based on risk
    ├── output-contracts.md      ← How to format responses
    ├── runtime-portability.md   ← How to adapt to any agent runtime
    ├── evaluation-rubric.md     ← How to score skill performance
    └── examples.md              ← Before/after behavior examples
```

## How It Works

1. **Classify** the task (research, code, action)
2. **Pick a funnel** — the right workflow for that task type
3. **Gather evidence** — the minimum needed to be confident
4. **Check sufficiency** — is this enough, given the risk?
5. **Verify** — proportionally, not uniformly
6. **Respond** — with clear labels: `observed`, `derived`, or `assumed`

## Validate the Package

```bash
python3 self-doubt-engine/scripts/validate_skill.py
```

## Adding More Skills

Each skill lives in its own folder:

```
self-doubt-engine/
another-skill/
```



## License

MIT
