# Dev Workflow Skill

A structured 6-phase development sprint: **Think → Plan → Build → Review → Test → Ship**. Role-based subagents at each phase. Inspired by [Garry Tan's gstack](https://github.com/garrytan/gstack).

Works with any [Agent Skills](https://agentskills.io) compatible tool: Claude Code, OpenAI Codex, Trae, Cursor, Gemini CLI, and more.

## What This Is

[gstack](https://github.com/garrytan/gstack) is Garry Tan's (CEO of Y Combinator) open-source software factory for Claude Code — 15 specialist roles and 6 power tools that turn Claude Code into a virtual engineering team.

This skill takes gstack's core insight — **structured roles beat generic prompting** — and packages it as a portable Agent Skill that works across 20+ AI coding tools, not just Claude Code.

**What we kept from gstack:**
- The Think → Plan → Build → Review → Test → Ship workflow
- Role-based subagent spawning (YC Coach, Eng Manager, Staff Engineer, QA Lead, Release Engineer)
- Design doc as the central artifact that flows between phases
- Paranoid review culture

**What we changed:**
- Simplified from 15 skills to 6 phases (most people don't need all 15)
- Made it tool-agnostic via Agent Skills standard
- Focused on solo dev / small team use case
- Added model selection guidance per phase

## Phases

| # | Phase | Role | Spawns | Output |
|---|-------|------|--------|--------|
| 1 | **Think** | YC Office Hours Coach | Sonnet | `DESIGN.md` |
| 2 | **Plan** | Eng Manager | Sonnet | `PLAN.md` |
| 3 | **Build** | Implementer | Haiku/Sonnet | Code + Tests |
| 4 | **Review** | Staff Engineer | Sonnet | Review Report |
| 5 | **Test** | QA Lead | Sonnet | Bug Report + Fixes |
| 6 | **Ship** | Release Engineer | Haiku | PR / Deploy |

## Install

### Via npm
```bash
npm install -g @jahonn/agentskills-cli
agentskills install ./dev-workflow-skill -t all
```

### Via ClawHub (OpenClaw)
```bash
clawhub install gstack-workflow
```

### Manual
Copy the skill directory to your tool's skill folder:
```bash
# Claude Code
cp -r dev-workflow-skill ~/.claude/skills/dev-workflow

# Codex
cp -r dev-workflow-skill ~/.codex/skills/dev-workflow
```

## Usage

### Full sprint
```
"Build me a [feature]" → runs all 6 phases
"Run dev-workflow on [description]"
```

### Partial sprint
```
"Just review and ship this branch" → Review → Ship
"I have DESIGN.md, skip to Plan"
```

### Single phase
```
"/think [idea]"
"/review"
"/ship"
```

## How It Works

Each phase spawns a focused subagent with a specialized prompt. The subagent works in isolation, produces a structured artifact, and passes it to the next phase.

```
User idea → DESIGN.md → PLAN.md → Code → Review → Tests → PR
           (Think)     (Plan)    (Build) (Review) (Test)  (Ship)
```

Key principle: **no code until the plan is approved**. Challenge scope ruthlessly.

## Frameworks Used

- **YC Office Hours** — reframing problems before solving them
- **Amazon Working Backwards** — press release before PRD
- **INVEST** — user story quality criteria
- **RICE** — feature prioritization

## Credit

Built on the ideas from [gstack](https://github.com/garrytan/gstack) by [Garry Tan](https://x.com/garrytan). gstack is MIT licensed. This skill is an independent implementation inspired by gstack's philosophy, not a fork.

## Related

- [gstack](https://github.com/garrytan/gstack) — the original (15 skills for Claude Code)
- [PM Agent Skill](https://github.com/jahonn/pm-agent-skill) — product management workflow
- [Agent Skills Spec](https://agentskills.io/specification) — the open standard

## License

MIT
