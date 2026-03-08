# /sdlc

The main entry point for the SDLC (Software Development Lifecycle) management system.

## Overview

The SDLC skill provides a comprehensive system for managing software development workflows. It coordinates multiple specialized skills to handle different aspects of the development process, from requirements gathering to deployment.

## Usage

```bash
/sdlc [command] [args]
```

## Key Principle: Flexible & Independent

**Each phase can be used independently!** You don't need to follow a strict order.

```bash
# Just run tests - no workflow needed
/sdlc test

# Create a PR - no workflow needed
/sdlc pr

# Run security check - no workflow needed
/sdlc secure

# Or use the full workflow with state tracking
/sdlc start feature "User auth"
/sdlc next
```

The workflow state is **optional** - it only helps if you want to track progress.

## Available Commands

### Core Commands

| Command | Description |
|---------|-------------|
| `/sdlc start <type> [description]` | Start a new workflow |
| `/sdlc status` | Show current workflow status |
| `/sdlc next` | Execute next phase in workflow |
| `/sdlc skip [phase]` | Skip current phase |
| `/sdlc phase <phase_name>` | Jump to specific phase |
| `/sdlc end` | End current workflow |

### Workflow Types

| Type | Description | Workflow |
|------|-------------|----------|
| `feature` | Feature development | research → spec → coding → test → verify → secure → cr → commit → pr → MERGE |
| `bugfix` | Bug fix | debug → coding → test → verify → secure → commit → pr → MERGE |
| `refactor` | Code refactoring | cr → spec → coding → test → verify → secure → cr → commit → pr → MERGE |
| `research` | Research & investigation | research → doc → discuss → END |

### Phase Commands

Execute specific phases directly:

```bash
# Research phase
/sdlc research [topic]

# Specification phase
/sdlc spec [feature_name]

# Coding phase
/sdlc coding [description]

# Test phase
/sdlc test [check_type]

# Verify phase
/sdlc verify [spec_file]

# Security check
/sdlc secure [check_type]

# Code review
/sdlc cr [scope]

# Commit
/sdlc commit [message]

# PR
/sdlc pr [action]

# Debug (bugfix workflow)
/sdlc debug [issue]
```

## Workflow Diagram

```
                    SDLC WORKFLOW v3.2
                    ════════════════

    ┌──────────┐
    │  START   │  ← /sdlc start [type] [description] (optional)
    └────┬─────┘
         │
         ▼
    ┌────────────┐     ┌──────────────┐     ┌─────────────┐
    │  PLANNING  │────▶│ research     │────▶│  spec       │
    └────┬───────┘     └──────────────┘     └─────────────┘
         │
         ▼
    ┌────────────┐     ┌──────────────┐     ┌─────────────┐
    │  DESIGN    │────▶│ Architecture │────▶│  Database   │
    └────┬───────┘     └──────────────┘     └─────────────┘
         │
         ▼
    ┌────────────┐     ┌──────────────┐     ┌─────────────┐
    │ DEVELOPMENT│────▶│  coding      │────▶│  test       │
    └────┬───────┘     └──────────────┘     └─────────────┘
         │
         ▼
    ┌────────────┐     ┌──────────────┐     ┌─────────────┐
    │   REVIEW   │────▶│ verify       │────▶│  secure     │
    └────┬───────┘     └──────────────┘     └─────────────┘
         │                                  ┌─────────────┐
         └─────────────────────────────────▶│  cr         │
                                            └─────────────┘
         │
         ▼
    ┌────────────┐     ┌──────────────┐     ┌─────────────┐
    │   FINALIZE │────▶│  commit      │────▶│  pr         │
    └────┬───────┘     └──────────────┘     └──────┬──────┘
         │                                         │
         ▼                                         ▼
    ┌──────────┐                            ┌──────────┐
    │  MERGE   │◀───────────────────────────│   PR     │
    └──────────┘                            └──────────┘

════════════════════════════════════════════════════════════
                    Quality Gates
════════════════════════════════════════════════════════════

    test    → 代码能跑通吗？  (lint + typecheck + unit + integ + e2e)
    verify  → 功能做对了吗？  (对比 spec 需求)
    secure  → 有安全问题吗？  (漏洞扫描 + 依赖检查)
    cr      → 代码质量好吗？  (最佳实践 + 架构)

════════════════════════════════════════════════════════════
                    State Management
════════════════════════════════════════════════════════════

Optional: Use /sdlc start to enable state tracking
Location: .sdlc/state.json

Without state tracking: All phases work independently
```

## Quick Start

### Option 1: Use Individual Phases (No Workflow)

Most common - just run what you need:

```bash
# Run tests
/sdlc test

# Verify implementation
/sdlc verify

# Code review
/sdlc cr

# Create PR
/sdlc pr

# Security check
/sdlc secure
```

### Option 2: Full Workflow with State Tracking

Use when you want to track progress:

```bash
/sdlc start feature "User Authentication System"
/sdlc next  # Proceed through phases
```

### Option 3: Jump to Any Phase

```bash
/sdlc phase test    # Jump directly to test phase
/sdlc phase verify  # Jump directly to verify phase
/sdlc phase commit  # Jump directly to commit phase
```

## State Management

The system maintains workflow state in `.sdlc/state.json`:

```json
{
  "workflow": "feature",
  "current_phase": "spec",
  "completed": ["research"],
  "branch": "feature/user-auth",
  "description": "User Authentication System",
  "started_at": "2026-03-08T10:00:00Z",
  "updated_at": "2026-03-08T14:30:00Z",
  "phase_history": [
    { "phase": "research", "completed_at": "2026-03-08T10:30:00Z" }
  ]
}
```

### State Persistence

State is automatically saved when:
- A workflow starts
- A phase completes
- A phase is skipped
- Branch is created
- Workflow ends

### State Queries

```bash
# Current status
/sdlc status

# View phase history
/sdlc history

# Check what's next
/sdlc next --dry-run
```

## Quality Assurance Phases

| Phase | Purpose | What it Checks |
|-------|---------|----------------|
| **test** | Does the code work? | Lint, typecheck, format, unit tests, integration tests, E2E |
| **verify** | Is the functionality correct? | Requirement coverage, API matching, feature completeness (vs spec) |
| **secure** | Are there security issues? | Vulnerability scanning, dependency checks, secret detection |
| **cr** | Is the code quality good? | Best practices, architecture, maintainability |

## Natural Language Support

All skills support natural language input:

```bash
# Formal
/sdlc start feature "User Authentication System"

# Natural
/sdlc start 我要做一个用户登录功能

# Contextual
/sdlc next
# System understands current phase and executes next step

# Flexible
/sdlc test 帮我跑一下测试
/sdlc verify 检查一下是不是符合需求
```

### Intent Detection

The system automatically detects workflow type from natural language:

**Feature indicators:**
- "做一个...", "实现...", "添加...", "新增..."
- "function", "feature", "add", "implement"

**Bugfix indicators:**
- "修复...", "fix...", "bug...", "问题..."
- "error", "failure", "not working"

**Refactor indicators:**
- "重构...", "优化...", "改进..."
- "code quality", "maintainability"

**Research indicators:**
- "调研...", "研究...", "比较..."
- "solution", "technology selection"

## Branch Management

Auto-create and manage branches:

```bash
# Feature branch
feature/{description}

# Bugfix branch
bugfix/{issue-id-or-description}

# Refactor branch
refactor/{component-name}
```

Example:
```bash
/sdlc start feature "用户认证"
# Creates: feature/user-auth
```

## Output Locations

```
docs/
├── spec/           # Specifications (from /sdlc spec)
├── research/       # Research documents (from /sdlc research)
├── verify/         # Verification reports (from /sdlc verify)
├── pencil/         # Wireframes and designs (from /pencil)
├── arch/           # Architecture cache (from /cache)
└── test/           # Test reports (from /sdlc test)

.sdlc/
├── state.json      # Workflow state
└── history.json    # Phase history
```

## Examples

### Starting a Feature Workflow

```bash
User: /sdlc start feature "User Authentication System"

System:
✓ Created branch: feature/user-auth
✓ Initialized state file
✓ Workflow type: feature

Current phase: research

Next: Execute /sdlc research to start technical research
Or use /sdlc next to automatically enter next phase
```

### Natural Language Input

```bash
User: /sdlc start 我要做一个用户登录功能

System:
Detected intent: feature development
Description: User login functionality

✓ Created branch: feature/user-login
✓ Initialized state file

Current phase: research

Execute /sdlc next to start research, or describe the functionality you want to implement
```

### Continuing Workflow

```bash
User: /sdlc next

System:
Current phase: research

[Executing /sdlc research logic...]

✓ research phase completed
✓ Generated document: ./docs/research/2026-03-08-user-login.md

Next phase: spec
Execute /sdlc next to continue
```

### Skipping Phases

```bash
User: /sdlc skip research

System:
Confirm: Skip research phase?
Reason: [optional]

User: yes

System:
✓ Skipped research phase
Current phase: spec

Execute /sdlc next to continue
```

### Quick Actions

```bash
# Run tests
/sdlc test

# Verify implementation
/sdlc verify

# Check code quality
/sdlc test lint typecheck

# Security scan
/sdlc secure

# Generate documentation
/doc api User Authentication API
```

## Status Output Format

```
═══════════════════════════════════════════════════════════
  SDLC Workflow Status
═══════════════════════════════════════════════════════════

Workflow:    feature
Description: User Authentication System
Phase:       spec
Completed:   ✓ research

Branch:      feature/user-auth
Started:     2026-03-08 10:00
Updated:     2026-03-08 14:30

═══════════════════════════════════════════════════════════
  Progress
═══════════════════════════════════════════════════════════

research  ████████████████████  ✓ Complete
spec      ██████████████░░░░░░  ⚠ In Progress
coding    ░░░░░░░░░░░░░░░░░░░░  → Pending
test      ░░░░░░░░░░░░░░░░░░░░  → Pending
verify    ░░░░░░░░░░░░░░░░░░░░  → Pending
secure    ░░░░░░░░░░░░░░░░░░░░  → Pending
cr        ░░░░░░░░░░░░░░░░░░░░  → Pending
commit    ░░░░░░░░░░░░░░░░░░░░  → Pending
pr        ░░░░░░░░░░░░░░░░░░░░  → Pending

═══════════════════════════════════════════════════════════
  Next Steps
═══════════════════════════════════════════════════════════

Execute /sdlc next to continue spec phase

Tips:
- Confirm spec document completeness
- Use /pencil to create design diagrams
- Execute /sdlc next to enter coding phase when ready
```

## Integration with Other Skills

The SDLC system integrates with specialized skills:

- **Flow skills**: start, status, next, skip, phase, end
- **Phase skills**: research, spec, coding, test, verify, secure, cr, commit, pr, debug
- **Foundation skills**: doc, pencil, cache, git

## Best Practices

1. **Independent usage is OK**: Each phase skill works standalone
2. **Workflow tracking is optional**: Use `/sdlc start` only if you want state tracking
3. **Skip freely**: Use `/sdlc skip` to bypass any phase - you know what you're doing
4. **Jump around**: Use `/sdlc phase <name>` to go directly to any phase
5. **Use verify**: Always run `/sdlc verify` to ensure implementation matches spec
6. **Quick actions**: Most common use case is running individual phases

## Troubleshooting

### State Issues

**Problem**: State not persisting
```
Solution:
1. Check .sdlc/ directory permissions
2. Run /sdlc status to validate state
3. Reinitialize if needed: /sdlc start
```

**Problem**: Lost work
```
Solution:
1. Check /sdlc history
2. View phase history in state file
3. Documents are saved in docs/ directory
```

### Phase Transition Issues

**Problem**: Cannot advance phase
```
Solution:
1. Check /sdlc status for blockers
2. Complete required tasks in current phase
3. Use /sdlc skip if appropriate
```

**Problem**: Wrong phase
```
Solution:
1. /sdlc phase [correct-phase]
2. Or /sdlc end to start over
```

## Related Skills

- **/sdlc research** - Technical research and solution evaluation
- **/sdlc spec** - Write specifications and design documents
- **/sdlc coding** - Coding guidance and implementation
- **/sdlc test** - Test validation (lint + typecheck + format + unit + integ + e2e)
- **/sdlc verify** - Verify implementation matches spec requirements
- **/sdlc secure** - Security checks
- **/sdlc cr** - Code review
- **/sdlc commit** - Commit code
- **/sdlc pr** - PR management
- **/sdlc debug** - Debug issues (bugfix workflow)
- **/doc** - Documentation generation
- **/pencil** - Wireframe and design diagrams
- **/cache** - Architecture knowledge caching
- **/git** - Git operations assistance

## Migration from Old Skills

| Old Skill | New Location |
|-----------|--------------|
| `/spec` | `/sdlc spec` |
| `/pr` | `/sdlc pr` |
| `/codereview` | `/sdlc cr` |
| `/git-commit` | `/sdlc commit` |
| `/research` | `/sdlc research` |
| `/test-go` | `/sdlc test` |
| `/codeclean` | `/sdlc test` (lint check) |
| `/refactor-go` | `/sdlc cr` |
| `/update-arch` | `/cache` |
