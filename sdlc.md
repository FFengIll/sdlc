# /sdlc

Software Development Lifecycle management with intelligent intent detection.

## Usage

```bash
/sdlc [natural language request]  # Smart mode - AI detects intent
/sdlc [command] [args]             # Explicit command
```

## Quick Start

```bash
# Smart mode - just describe what you want
/sdlc understand the codebase       # → /sdlc understand
/sdlc fix the login bug             # → bugfix workflow
/sdlc add user authentication       # → feature workflow
/sdlc run tests                     # → /sdlc test
/sdlc commit my changes             # → /sdlc commit

# Explicit commands
/sdlc understand
/sdlc spec "Add OAuth"
/sdlc coding
/sdlc test
/sdlc commit
```

## Intent Detection

| Your Request              | Detected Action          | Creates Files?        |
| ------------------------- | ------------------------ | --------------------- |
| "understand the codebase" | `/sdlc understand`       | ✅ Yes (arch cache)    |
| "explore payment module"  | Quick explore (no skill) | ❌ No                  |
| "how does auth work?"     | Quick explain (no skill) | ❌ No                  |
| "write a spec for auth"   | `/sdlc spec`             | ✅ Yes                 |
| "implement login"         | `/sdlc coding`           | ✅ Yes                 |
| "run tests"               | `/sdlc test`             | ❌ No                  |
| "review my changes"       | `/sdlc cr`               | ✅ Yes (review report) |
| "check for bugs"          | `/sdlc cr`               | ✅ Yes (review report) |
| "fix the login bug"       | bugfix workflow          | ✅ Yes                 |
| "add user API"            | feature workflow         | ✅ Yes                 |

> **Note**: "explore" and "how does" questions are answered directly without creating files. Use "understand" to build reusable architecture cache.
| "修复登录bug" | bugfix workflow (中文) |

## Commands

| Command                  | Description                                                     |
| ------------------------ | --------------------------------------------------------------- |
| `/sdlc guard [task]`     | Establish safety guardrails before proceeding with work         |
| `/sdlc understand`       | Build context, explore codebase, discuss architecture           |
| `/sdlc cr [scope]`       | Code review - find issues, check quality (staged/files/folders) |
| `/sdlc spec [title]`     | Write specification                                             |
| `/sdlc harness [title]`  | Write verification harness (invariants, flows, constraints)      |
| `/sdlc coding [desc]`    | Write code based on spec                                        |
| `/sdlc test [type]`      | Run tests (lint + unit + e2e)                                   |
| `/sdlc validate [target]`| Validate against harness or user goal                            |
| `/sdlc commit [msg]`     | Commit changes                                                  |
| `/sdlc pr [action]`      | Create/manage PR                                                |
| `/sdlc debug [issue]`    | Debug bugs                                                      |
| `/sdlc research [topic]` | Research solutions                                              |
| `/sdlc status`           | Show current workflow progress                                  |
| `/sdlc resume`           | Browse and resume recent work from `.sdlc/docs/`                |

## Workflows

| Type       | Description         | Workflow                                                            |
| ---------- | ------------------- | ------------------------------------------------------------------- |
| `minor`    | Minor modifications | coding → test → commit                                              |
| `quick`    | Small changes       | understand → spec → coding → test → commit → pr                     |
| `feature`  | New features        | understand → research → spec → coding → test → verify → commit → pr |
| `bugfix`   | Bug fixes           | understand → debug → coding → test → verify → commit → pr           |
| `research` | Research            | understand → research → doc → END                                   |

## Natural Language Flow Control

Workflow progression is handled through natural language:

```bash
/sdlc 做个登录功能          # Start feature workflow
继续 / 下一步                # Proceed to next phase
跳过测试                     # Skip current phase
到哪了？                     # Check status
/sdlc status                # Show detailed progress
```

Workflows are created implicitly when you first describe what you want to do.

## Examples

```bash
# Understanding
/sdlc understand the codebase
/sdlc explore the payment module
/sdlc how does the auth system work

# Code Review (find issues)
/sdlc review my changes
/sdlc check for bugs in src/auth
/sdlc audit the payment code for security issues

# Specification
/sdlc write a spec for user authentication
/sdlc create specification for OAuth

# Implementation
/sdlc implement the login feature
/sdlc write code for user profile

# Testing & Debugging
/sdlc run all tests
/sdlc debug the login timeout issue

# Commit & PR
/sdlc commit my changes
/sdlc create a pull request

# Workflows
/sdlc fix the login bug           # → bugfix workflow
/sdlc add user API endpoints      # → feature workflow
/sdlc refactor the auth module    # → refactor workflow
```

## Output Locations

```
.sdlc/
├── state.json             # Workflow state
├── docs/                  # Working documents (flat structure)
│   ├── auth-user-login-20240115.spec.md
│   ├── auth-user-login-20240116.coding.md
│   ├── auth-oauth-integration-20240116.research.md
│   ├── payment-stripe-checkout-20240201.cr.md
│   └── user-profile-edit-20240205.test.md
├── harness/               # Verification harnesses (separate level)
│   ├── auth-flow-invariants-20240115.harness.md
│   └── payment-constraints-20240201.harness.md
└── arch/                  # Architecture cache (separate level)
    ├── overview-20240115.arch.md
    └── auth-20240115.arch.md
```

### Directory Structure

| Directory | Purpose | Structure |
|-----------|---------|-----------|
| `docs/` | Working documents (spec, cr, test, etc.) | Flat, `category-feature-date.type.md` |
| `harness/` | Verification harnesses | Flat, `category-feature-date.harness.md` |
| `arch/` | Architecture cache | Flat, `[scope]-date.arch.md` |

### File Naming Convention

**Format**: `category-feature-date.type.md` (or `[scope]-date.type.md` for arch)

| Part | Description | Example |
|------|-------------|---------|
| category/scope | Module/Category (lowercase) | `auth`, `payment`, `user`, `overview` |
| feature | Feature description (kebab-case) | `user-login`, `stripe-checkout`, `flow-invariants` |
| date | Date (YYYYMMDD) | `20240115` |
| type | Document type | `spec`, `coding`, `test`, `cr`, `research`, `harness`, `arch` |

**Document Types**:
- `spec` - Specification documents (in `docs/`)
- `coding` - Implementation guidance (in `docs/`)
- `test` - Test reports (in `docs/`)
- `validate` - Validation reports (in `docs/`)
- `cr` - Code review reports (in `docs/`)
- `secure` - Security review reports (in `docs/`)
- `debug` - Debug reports (in `docs/`)
- `research` - Research documents (in `docs/`)
- `understand` - Understanding reports (in `docs/`)
- `commit` - Commit logs (in `docs/`)
- `pr` - PR logs (in `docs/`)
- `guard` - Guardrail reports (in `docs/`)
- `harness` - Verification harnesses (in `harness/`)
- `arch` - Architecture cache (in `arch/`)

## Best Practices

1. **Use the flat structure for working docs** - All documents in `.sdlc/docs/` with consistent naming
2. **Harnesses are special** - Verification harnesses go in `.sdlc/harness/` (separate level)
3. **Filter by type** - Use `*.spec.md`, `*.cr.md`, etc. to find document types
4. **Filter by category** - Use `auth-*.md` to find all auth-related documents
5. **Always start with `/sdlc understand`** - Build context and create architecture cache
6. **Always write specs with `/sdlc spec`** - Document what you're doing
7. **Use smart mode for convenience** - Let AI detect the workflow
8. **Use explicit commands for precision** - When you know exactly what phase you need

## Migration Notes

| Old Command   | New Command                 |
| ------------- | --------------------------- |
| `/spec`       | `/sdlc spec`                |
| `/git-commit` | `/commit` or `/sdlc commit` |
| `/codereview` | `/sdlc cr`                  |

**`/commit` and `/pr` are now standalone** - use anytime without starting an SDLC workflow.

---

# Internal: Intent Detection & Routing

> This section is for model execution. The simplified documentation above is for users.

## Intent Detection Process

When `/sdlc` is invoked with arbitrary input:

1. **Check for explicit commands first**
   - If input matches `guard|understand|spec|harness|coding|test|validate|commit|pr|debug|research|cr|secure`
   - Execute the corresponding phase skill directly

2. **Analyze for workflow-level intents**
   - Bug fix: `fix|bug|issue|error|problem|修复|调试`
   - Feature: `add|new feature|implement|feature|添加|新功能|实现`
   - Refactor: `refactor|clean up|restructure|重构`

3. **Analyze for phase-level intents**
   - Understand (creates architecture cache): `understand|analyze architecture|map codebase|build context|create arch cache`
   - Explore/Read (lightweight, no cache): `explore|show me|how does|explain|walk through|what is|read code`
   - Review/CR (finds issues): `review|check|audit|assess|inspect|find issues|find problems|look for bugs|审查|检查`
   - Spec: `spec|specification|document requirements|write spec|规范|规格|文档`
   - Research: `research|investigate|compare|best practices|研究|调研|比较`
   - Coding: `implement|code|write|build|create|develop|实现|编写|开发`
   - Test: `test|run tests|verify|check|validate|测试|运行测试`
   - Commit: `commit|save changes|提交|保存`
   - PR: `pull request|pr|submit|提交pr`

4. **Analyze for flow control intents** (natural language only)
   - Continue/Next: `continue|next|proceed|go on|继续|下一步`
   - Skip: `skip|bypass|not doing this|跳过|略过`
   - Status: `status|progress|where am i|what's next|状态|进度|到哪了`
   - Jump to phase: `go to|jump to|switch to|去|转到|切换到` + phase name

4. **Extract context**
   - Git status (uncommitted changes?)
   - Current branch name
   - Active workflow state
   - Recent specs

5. **Route and execute**
   - Show detected intent
   - Execute appropriate skill or workflow

## Routing Map

```python
# Pseudo-code for routing
if is_explicit_command(input):
    execute_phase_skill(input)
elif has_flow_control_intent(input):
    # Natural language flow control
    if wants_to_continue(input):
        advance_to_next_phase()
    elif wants_to_skip(input):
        skip_current_phase()
    elif wants_status(input):
        execute_status_skill()
    elif wants_to_jump(input):
        jump_to_phase(extract_phase_name(input))
elif has_bugfix_intent(input):
    execute_workflow('bugfix', extract_description(input))
elif has_feature_intent(input):
    execute_workflow('feature', extract_description(input))
elif has_refactor_intent(input):
    execute_workflow('refactor', extract_description(input))
else:
    # Phase-level intents
    intent = detect_phase_intent(input)
    if intent:
        execute_phase_skill(intent)
    else:
        ask_for_clarification()
```

## Skill Invocations

When routing to a specific phase, invoke:
- `/sdlc guard` → read `skills/phases/guard.md`
- `/sdlc understand` → read `skills/phases/understand.md`
- `/sdlc cr` → read `skills/phases/cr.md`
- `/sdlc spec` → read `skills/phases/spec.md`
- `/sdlc harness` → read `skills/phases/harness.md`
- `/sdlc coding` → read `skills/phases/coding.md`
- `/sdlc test` → read `skills/phases/test.md`
- `/sdlc validate` → read `skills/phases/validate.md`
- `/sdlc commit` → read `skills/phases/commit.md`
- `/sdlc pr` → read `skills/phases/pr.md`

When routing to a workflow, invoke:
- bugfix → read `skills/workflows/bugfix.md`
- feature → read `skills/workflows/feature.md`
- refactor → read `skills/workflows/refactor.md`
- research → read `skills/workflows/research.md`

## Skill Behavior Summary

| Skill          | Creates Files                            | Purpose                                    |
| -------------- | ---------------------------------------- | ------------------------------------------ |
| `understand`   | ✅ Yes (`.sdlc/docs/arch/`, `.sdlc/docs/*.understand.md`) | Architecture cache, reusable documentation |
| `cr`           | ✅ Yes (`.sdlc/docs/*.cr.md`)             | Code review report with findings           |
| `explore/read` | ❌ No                                     | Quick inspection, no artifacts             |

### When to use which

- **User says "explore/show me/how does/explain/walk through"** → Just read and explain, **do not** invoke understand skill
  - This is a lightweight conversation, no artifacts needed
  - Just use Read/Glob tools and explain

- **User says "understand/analyze architecture/map codebase/build context"** → Invoke `/sdlc understand`
  - Creates architecture cache in `.sdlc/docs/arch/`
  - Generates understanding report as `.sdlc/docs/category-feature-date.understand.md`
  - For reuse across multiple tasks

- **User says "review/check/audit/assess/find issues"** → Invoke `/sdlc cr`
  - Creates code review report as `.sdlc/docs/category-feature-date.cr.md`
  - Finds bugs, security issues, quality problems

## Context Extraction

```bash
# Get git status
git_status=$(git status --porcelain)

# Get current branch
current_branch=$(git branch --show-current)

# Check for active workflow
if [ -f .sdlc/state.json ]; then
    active_workflow=$(jq -r '.workflow' .sdlc/state.json)
    current_phase=$(jq -r '.phase' .sdlc/state.json)
fi

# Get latest spec
latest_spec=$(find .sdlc/docs -name "*.spec.md" -type f -printf '%T@ %p\n' | sort -n | tail -1 | cut -f2- -d" ")
```

## Execution Feedback

Always show what was detected before executing:

```
🎯 Detected intent: <intent>
📋 Scope: <extracted_scope>
→ Executing: <command or workflow>
```

---

# Related Skills

The SDLC system is composed of the following skills organized under `sdlc/`:

## Phase Skills (`skills/sdlc/phases/`)

| Skill         | Description                                   | File                   |
| ------------- | --------------------------------------------- | ---------------------- |
| `/guard`      | Establish safety guardrails before work       | `phases/guard.md`      |
| `/understand` | Build architecture cache and explore codebase | `phases/understand.md` |
| `/cr`         | Code review - find issues and check quality   | `phases/cr.md`         |
| `/spec`       | Write specifications                          | `phases/spec.md`       |
| `/harness`    | Write verification harnesses (invariants)     | `phases/harness.md`    |
| `/coding`     | Write code based on specs                     | `phases/coding.md`     |
| `/test`       | Run tests (lint + unit + e2e)                 | `phases/test.md`       |
| `/validate`   | Validate against harness/goal (active testing)| `phases/validate.md`   |
| `/commit`     | Commit changes                                | `phases/commit.md`     |
| `/pr`         | Create and manage pull requests               | `phases/pr.md`         |
| `/debug`      | Debug and fix bugs                            | `phases/debug.md`      |
| `/research`   | Research solutions and best practices         | `phases/research.md`   |
| `/secure`     | Security review and analysis                  | `phases/secure.md`     |

## Workflow Skills (`skills/sdlc/workflows/`)

| Skill      | Description                       | File                    |
| ---------- | --------------------------------- | ----------------------- |
| `minor`    | Minor modifications workflow      | `workflows/minor.md`    |
| `feature`  | New features development workflow | `workflows/feature.md`  |
| `bugfix`   | Bug fixes workflow                | `workflows/bugfix.md`   |
| `refactor` | Code refactoring workflow         | `workflows/refactor.md` |
| `research` | Research workflow                 | `workflows/research.md` |

## Flow Control Skills (`skills/sdlc/flow/`)

| Skill          | Description            | File             |
| -------------- | ---------------------- | ---------------- |
| `/sdlc status` | Show workflow progress | `flow/status.md` |
| `/sdlc resume` | Browse and resume work | `flow/resume.md` |

## Foundation Skills (`skills/sdlc/foundation/`)

| Skill         | Description                  | File                        |
| ------------- | ---------------------------- | --------------------------- |
| `archive`     | Archive documentation        | `foundation/archive.md`     |
| `cache`       | Manage architecture cache    | `foundation/cache.md`       |
| `discuss`     | Discussion and collaboration | `foundation/discuss.md`     |
| `doc`         | Documentation management     | `foundation/doc.md`         |
| `git`         | Git operations               | `foundation/git.md`         |
| `git-resolve` | Resolve git conflicts        | `foundation/git-resolve.md` |
| `handoff`     | Handoff between contexts     | `foundation/handoff.md`     |
| `pencil`      | Quick note-taking            | `foundation/pencil.md`      |
