# Bug Fix Workflow

**Purpose**: Fix bugs efficiently with proper testing and verification.

> **Critical**: Always start with `/sdlc understand` before debugging. Understanding the existing code architecture helps identify root causes faster and prevents introducing new bugs.

## When to Use

Use this workflow when:
- Fixing a reported bug
- Resolving an issue in production
- Patching a defect
- Correcting unexpected behavior

## Workflow Sequence

```
START
  │
  ▼
understand → debug → coding → test → validate → secure → commit → pr → MERGE
```

## Phase Details

### 0. Understand (Required First Step)
```bash
/sdlc understand [scope]
```
- Build context of the codebase architecture
- Understand how the affected components currently work
- Identify related code and integration points
- Check architecture cache for relevant context
- **Do not skip! Trying to debug without understanding causes more bugs**

### 1. Debug
```bash
/sdlc debug "Analyze bug root cause"
```
- Reproduce the bug
- Identify root cause (now easier with context from understand)
- Document bug behavior
- Create minimal reproduction

### 2. Coding
```
[Manual coding phase]
```
- Implement the fix
- Make minimal changes
- Add regression tests
- Document the fix

### 3. Test
```bash
/sdlc test
```
**What it checks:**
- lint (code style)
- typecheck (type validation)
- format (code formatting)
- unit (unit tests including regression)
- integ (integration tests)
- e2e (end-to-end tests)
- coverage (test coverage)

**Question answered**: "Does the fix work?"

### 4. Validate
```bash
/sdlc validate [target] [criteria]
```
**What it checks:**
- Bug is actually fixed (active testing)
- No regressions introduced
- Edge cases covered
- Related harness invariants still hold

**Question answered**: "Is the bug truly resolved?"

### 5. Secure
```bash
/sdlc secure
```
**What it checks:**
- Vulnerability scanning
- Dependency security
- Secret detection
- Fix doesn't introduce security issues

### 6. Commit
```bash
/sdlc commit
```
- Create structured commit message
- Reference issue/ticket
- Document the fix approach
- Note any breaking changes

### 7. Pull Request
```bash
/sdlc pr
```
- Create PR with description
- Include before/after evidence
- Link to original issue
- Request review

### 8. Merge
```
[Merge PR after approval]
```
- Merge to main branch
- Update issue tracker
- Notify stakeholders

## Bug Report Template

```
Bug: [Brief description]

Reproduction Steps:
1.
2.
3.

Expected Behavior:
[What should happen]

Actual Behavior:
[What actually happens]

Environment:
- Version:
- OS/Browser:
- Other relevant info:

Root Cause:
[Analysis after debug phase]

Fix:
[Description of the fix]
```

## Key Differences from Feature Workflow

| Aspect | Feature | Bugfix |
|--------|---------|--------|
| **Start with** | understand → research → spec | **understand → debug** |
| **Spec phase** | Full specification required | Brief bug/fix documentation |
| **Coding approach** | Extensive new code | Minimal targeted changes |
| **Verification** | Full spec compliance | Regression focused (validate) |
| **Code review** | CR during implementation | CR after fix is complete |

## Notes

- Consider hotfix process for production bugs
- Use `/doc`, `/cache` for documentation needs
