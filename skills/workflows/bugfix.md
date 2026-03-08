# Bug Fix Workflow

**Purpose**: Fix bugs efficiently with proper testing and verification.

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
debug → coding → test → verify → secure → commit → pr → MERGE
```

## Phase Details

### 1. Debug
```bash
/sdlc debug "Analyze bug root cause"
```
- Reproduce the bug
- Identify root cause
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

### 4. Verify
```bash
/sdlc verify
```
**What it checks:**
- Bug is actually fixed
- No regressions introduced
- Edge cases covered
- Fix matches issue description

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

## Usage Example

```bash
# Start bugfix workflow
/sdlc start bugfix "Fix user session timeout"

# Debug phase
/sdlc debug "Session expires after 5 minutes instead of 24h"
# → Found: Missing refresh token logic in session middleware

# [Manual coding - implement fix]

# Run tests
/sdlc test

# Verify fix
/sdlc verify

# Security check
/sdlc secure

# Commit fix
/sdlc commit

# Create PR
/sdlc pr

# [Merge after review]
```

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

## Navigation Commands

```bash
# Move to next phase
/sdlc next

# Skip phase (with reason)
/sdlc skip "No security impact for this fix"

# Check current status
/sdlc status

# Jump to specific phase
/sdlc goto <phase>
```

## Completion Checklist

- [ ] Bug root cause identified
- [ ] Fix implemented
- [ ] Regression tests added
- [ ] All tests passing
- [ ] Bug verified fixed
- [ ] No regressions
- [ ] Security scan clean
- [ ] Committed with issue reference
- [ ] PR created and merged

## Key Differences from Feature Workflow

| Feature | Bugfix |
|---------|--------|
| Start with research | Start with debug |
| Create full spec | Document bug/fix |
| extensive coding | Minimal changes |
| Full verify | Regression focused |
| Initial CR needed | CR after fix |

## Notes

- Bugfix workflow is **faster** than feature workflow
- Skips research and spec phases (uses debug instead)
- Focus on minimal, targeted changes
- Always add regression tests
- Consider hotfix process for production bugs
- Use `/doc`, `/cache` for documentation needs
