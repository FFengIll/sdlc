---
name: sdlc
description: Software Development Lifecycle management with intelligent intent detection and harness. Routes natural-language requests to workflows (feature, bugfix, refactor, research) and direct actions (understand, spec, test, commit, PR handoff, review, debug, lint, simplify, etc.). Commit requests classify active-task changes into related groups and create focused commits while leaving unrelated work untouched. PR requests are read-only handoffs that produce a title, description, and clickable link for human submission; they never push or create a PR.
---

# /sdlc

Software Development Lifecycle management with intelligent intent detection and routing.

## Usage

```bash
/sdlc [natural language request]  # Smart mode - AI detects intent
/sdlc [command] [args]             # Explicit command
/sdlc commit [message]             # Classify related changes, then commit by group
/sdlc pr [base-branch]             # Write title/content/link for human submission
```

---

# Routing Tables

> For AI execution: match input against Cmd (exact) first, then Intent keywords.
> Always show: `🎯 Detected: <intent>  → Executing: <skill>`

## Actions

| Skill              | File               | Cmd        | Intent keywords                                 |
| ------------------ | ------------------ | ---------- | ----------------------------------------------- |
| action:guard      | action/guard.md    | guard      | safety, before work                             |
| action:plan       | action/plan.md     | plan       | plan, design plan, 规划                         |
| action:understand | action/understand.md | understand | understand, analyze architecture, build context |
| action:cr         | action/cr.md       | cr         | review, check, audit, find issues, 检查         |
| action:spec       | action/spec.md     | spec       | spec, specification, write spec, 规范           |
| action:test       | action/test.md     | test       | test, run tests, 测试                           |
| action:commit     | action/commit.md   | commit     | classify and commit related changes, save changes, 提交 |
| action:pr         | action/pr.md       | pr         | write PR title/content/link, pull request, 提交pr |
| action:debug      | action/debug.md    | debug      | debug, diagnose                                 |
| action:lint       | action/lint.md     | lint       | lint, fix style, check style                    |
| action:simplify   | action/simplify.md | simplify   | simplify, clean up code, 简化                   |
| action:regression | action/regression.md | regression | regression, check regressions                 |
| action:research   | action/research.md | research   | research, investigate, compare, 研究            |
| action:discuss    | action/discuss.md  | discuss    | discuss, talk about                             |
| action:handoff    | action/handoff.md  | handoff    | delegate, handoff                               |
| action:secure     | action/secure.md   | secure     | security, secure                                |
| action:harness    | action/harness.md  | harness    | harness, verification                           |
| action:validate   | action/validate.md | validate   | validate                                        |
| feedback          | action/feedback.md | feedback   | feedback, score, improve                         |

## workflow

| Skill              | File                 | Intent keywords                           | Pipeline                                       |
| ------------------ | -------------------- | ----------------------------------------- | ---------------------------------------------- |
| workflow:bugfix   | workflow/bugfix.md   | fix, bug, issue, error, 修复              | understand→debug→coding→test→validate→secure→commit→pr         |
| workflow:feature  | workflow/feature.md  | add, new feature, implement, 添加, 新功能 | understand→research→spec→coding→test→validate→secure→cr→commit→pr |
| workflow:refactor | workflow/refactor.md | refactor, clean up, 重构                  | understand→spec→coding→test→commit→pr          |
| workflow:research | workflow/research.md | research, investigate, 研究               | understand→research→doc→discuss→END            |
| workflow:minor    | workflow/minor.md    | minor, small change, 小改动               | coding→test→commit                             |

Every `→commit` workflow stage must inventory the whole working tree, classify
active-task changes into coherent groups, and commit those groups separately
when they can be reviewed or reverted independently. Never treat all dirty files
as one group, and never commit unrelated changes merely because they are present.

Every `→pr` workflow stage means a **read-only PR handoff**. It writes the title,
description, and clickable compare/create link for the user. It never pushes a
branch, runs `gh pr create`, calls a PR creation API, or performs another remote
write. Remote publishing requires a separate, explicitly invoked workflow.

---

# Key Behaviors

- `explore/explain/how does` → read and explain inline, no skill invoked
- `understand/analyze architecture` → `action:understand` (creates `.design/arch/` cache)
- `review/check/find issues` → `action:cr` (creates `*.cr.md`)
- `commit/save changes/提交` → `action:commit` (inventory → classify related groups → commit each group → audit leftovers)
- `pr/pull request/提交pr` → `action:pr` (title + content + clickable manual-submission link only; no remote writes)

## Output Structure

```
.design/          # design artifacts — type is the filename suffix
├── {feature}.spec.md
├── {name}.pencil.md
├── arch/         # {scope}-arch.md cache
├── harness/      # {feature}.harness.md
└── archive/
.research/        # {feature}.md research outputs
.sdlc/
└── docs/         # {feature}.{type}.md reports (test/cr/debug/validate/secure/compare/understand)
```

**IMPORTANT:** These folders are placed under the user's coding project path (cwd).

**Filenames never contain dates.** Every generated markdown file records the date in its header frontmatter instead:

```markdown
---
date: 2026-10-26
---
```
