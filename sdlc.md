# /sdlc

Software Development Lifecycle management with intelligent intent detection and routing.

## Usage

```bash
/sdlc [natural language request]  # Smart mode - AI detects intent
/sdlc [command] [args]             # Explicit command
```

---

# Routing Tables

> For AI execution: match input against Cmd (exact) first, then Intent keywords.
> Always show: `🎯 Detected: <intent>  → Executing: <skill>`

## Actions

| Skill              | Cmd        | Intent keywords                                 |
| ------------------ | ---------- | ----------------------------------------------- |
| actions:guard      | guard      | safety, before work                             |
| actions:plan       | plan       | plan, design plan, 规划                         |
| actions:understand | understand | understand, analyze architecture, build context |
| actions:cr         | cr         | review, check, audit, find issues, 检查         |
| actions:spec       | spec       | spec, specification, write spec, 规范           |
| actions:coding     | coding     | implement, code, write, build, 实现             |
| actions:test       | test       | test, run tests, 测试                           |
| actions:commit     | commit     | commit, save changes, 提交                      |
| actions:pr         | pr         | pull request, 提交pr                            |
| actions:debug      | debug      | debug, diagnose                                 |
| actions:lint       | lint       | lint, fix style, check style                    |
| actions:simplify   | simplify   | simplify, clean up code, 简化                   |
| actions:regression | regression | regression, check regressions                   |
| actions:research   | research   | research, investigate, compare, 研究            |
| actions:discuss    | discuss    | discuss, talk about                             |
| actions:handoff    | handoff    | delegate, handoff                               |
| actions:secure     | secure     | security, secure                                |
| actions:harness    | harness    | harness, verification                           |
| actions:validate   | validate   | validate                                        |
| feedback           | feedback   | feedback, score                                 |

## Workflows

| Skill              | Intent keywords                           | Pipeline                                       |
| ------------------ | ----------------------------------------- | ---------------------------------------------- |
| workflows:bugfix   | fix, bug, issue, error, 修复              | understand→debug→coding→test→commit→pr         |
| workflows:feature  | add, new feature, implement, 添加, 新功能 | understand→research→spec→coding→test→commit→pr |
| workflows:refactor | refactor, clean up, 重构                  | understand→spec→coding→test→commit→pr          |
| workflows:research | research, investigate, 研究               | understand→research→doc→END                    |
| workflows:minor    | minor, small change, 小改动               | coding→test→commit                             |


---

# Key Behaviors

- `explore/explain/how does` → read and explain inline, no skill invoked
- `understand/analyze architecture` → `actions:understand` (creates `.sdlc/arch/` cache)
- `review/check/find issues` → `actions:cr` (creates `*.cr.md`)

## Output Structure

```
.sdlc/
├── docs/      # category-feature-date.type.md
├── harness/   # verification harnesses
└── arch/      # architecture cache
```

**IMPORTANT:** `.sdlc` folder should be placed under the user's coding project path.
