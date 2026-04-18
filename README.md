# Self-Doubt Engine

A skill for AI agents that makes them stop and verify before they act.

## What It Does

Most agents answer too fast. They guess, hallucinate, or skip validation.

The **Self-Doubt Engine** adds a control layer that asks one question before every response:

> *Do I have enough evidence to answer, code, or act on this — at this level of risk?*

If yes, it proceeds. If not, it retrieves more, flags uncertainty, or escalates.

## Install

Clone the repo and copy the skill folder into your project:

```bash
git clone https://github.com/ziyad455/skills.git
cp -r skills/self-doubt-engine ./self-doubt-engine
```

Or download just the skill folder using `degit` (no git history):

```bash
npx degit ziyad455/skills/self-doubt-engine self-doubt-engine
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

## Adding More Skills

Each skill lives in its own folder:

```
self-doubt-engine/
another-skill/
```



## License

MIT
