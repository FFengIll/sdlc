# /sdlc start

**OPTIONAL** - Start a new SDLC workflow with state tracking.

## Guideline

> **You don't need to run this!** Each phase skill works independently.
>
> Use `/sdlc start` only if you want to:
> - Track your progress through a workflow
> - Get automatic phase suggestions
> - See visual progress status
>
> Otherwise, just run the phases you need directly:
> - `/sdlc test`
> - `/sdlc verify`
> - `/sdlc cr`
> - `/sdlc commit`

This skill initializes a new SDLC workflow. It:
1. Creates or resets the workflow state in `.sdlc/state.json`
2. Supports natural language input (Chinese and English)
3. Validates workflow type selection
4. Sets up the initial phase based on workflow type

## Workflow Types

| Type | Description | Initial Phase |
|------|-------------|---------------|
| **feature** | New feature development | research |
| **bugfix** | Bug fixing | debug |
| **refactor** | Code refactoring | cr |
| **research** | Research and documentation | research |

## State Management

The state is stored in `.sdlc/state.json`:

```json
{
  "workflow_type": "feature",
  "current_phase": "research",
  "title": "User authentication system",
  "phases": {
    "research": { "status": "pending", "started_at": null },
    "spec": { "status": "pending", "started_at": null },
    "coding": { "status": "pending", "started_at": null },
    "test": { "status": "pending", "started_at": null },
    "verify": { "status": "pending", "started_at": null },
    "secure": { "status": "pending", "started_at": null },
    "cr": { "status": "pending", "started_at": null },
    "commit": { "status": "pending", "started_at": null },
    "pr": { "status": "pending", "started_at": null }
  },
  "created_at": "2026-03-08T10:00:00Z",
  "updated_at": "2026-03-08T10:00:00Z"
}
```

## Phase Sequences

### FEATURE flow
research → spec → coding → test → verify → secure → cr → commit → pr

### BUGFIX flow
debug → coding → test → verify → secure → commit → pr

### REFACTOR flow
cr → spec → coding → test → verify → secure → cr → commit → pr

### RESEARCH flow
research → doc → discuss

## Input Format

Supports natural language in Chinese and English:

```
/sdlc start feature "用户认证系统"
/sdlc start feature "User authentication"
/sdlc start bugfix "修复登录失败"
/sdlc start bugfix "Fix login issue"
/sdlc start refactor "重构认证模块"
/sdlc start refactor "Refactor auth module"
/sdlc start research "调研新框架"
/sdlc start research "Research new framework"
```

## Output Format

```
╔═══════════════════════════════════════════════════════════╗
║                    SDLC WORKFLOW STARTED                   ║
╠═══════════════════════════════════════════════════════════╣
║  Type:     FEATURE                                         ║
║  Title:    User authentication system                     ║
║  Phase:    research →                                      ║
╠═══════════════════════════════════════════════════════════╣
║                                                           ║
║  💡 Remember: You can jump to any phase anytime!          ║
║                                                           ║
║  Quick start options:                                     ║
║  1. /sdlc next - Auto-proceed through phases              ║
║  2. /sdlc phase <name> - Jump to specific phase           ║
║  3. /sdlc skip - Skip current phase                       ║
║  4. /sdlc status - Check progress                         ║
║                                                           ║
║  Or use phases independently:                             ║
║  /sdlc test, /sdlc verify, /sdlc cr, etc.                ║
║                                                           ║
╚═══════════════════════════════════════════════════════════╝
```

## Error Handling

If a workflow is already active:
```
⚠ Active workflow found: feature "User authentication"
  Use /sdlc status to view current workflow
  Use /sdlc phase <phase> to jump to a specific phase
  Or confirm to reset and start new workflow
```

## Completion Conditions

- [ ] Workflow type selected
- [ ] Title provided
- [ ] State file created
- [ ] Initial phase set
- [ ] Next steps communicated
