# Feature Development Workflow

**Purpose**: Develop new features from research to production deployment.

> **Critical**: Always start with `/sdlc understand` and `/sdlc spec` before any coding. This ensures you understand the existing codebase architecture and have a clear specification before implementation.

## When to Use

Use this workflow when:
- Adding a new feature to the codebase
- Implementing new functionality
- Creating new capabilities or services
- Building new user-facing features

## Workflow Sequence

```
START
  │
  ▼
understand → research → spec → coding → test → validate → secure → cr → commit → pr → MERGE
```

## Phase Details

### 0. Understand (Required First Step)
```bash
/sdlc understand [scope]
```
- Build context of the codebase architecture
- Create or reuse architecture cache in `.design/arch/`
- Identify relevant components and integration points
- Understand existing patterns and conventions
- **Do not skip this step!**

### 1. Research
```bash
/sdlc research "Investigate technology options"
```
- Research technical approaches
- Evaluate libraries and frameworks
- Document findings
- Identify potential risks

### 2. Spec (Required Before Coding)
```bash
/sdlc spec "Design feature specification"
```
- Define requirements
- Design APIs and interfaces
- Document data structures
- Create implementation plan
- **Must be completed before coding starts**

### 3. Coding
```
[Manual coding phase]
```
- Implement the feature based on spec
- Write code following project conventions
- Add inline documentation
- **Only start after understand + spec are complete**

### 4. Test
```bash
/sdlc test
```
**What it checks:**
- lint (code style)
- typecheck (type validation)
- format (code formatting)
- unit (unit tests)
- integ (integration tests)
- e2e (end-to-end tests)
- coverage (test coverage)

**Question answered**: "Can the code run?"

### 5. Validate
```bash
/sdlc validate [target] [criteria]
```
**What it checks:**
- Harness-based validation (invariants, flows, constraints)
- Goal-based validation (user goals achievable)
- Active testing of behavior
- Dependency chain verification

**Question answered**: "Does it work correctly?"

### 6. Secure
```bash
/sdlc secure
```
**What it checks:**
- Vulnerability scanning
- Dependency security
- Secret detection

### 7. Code Review
```bash
/sdlc cr
```
**What it checks:**
- Best practices
- Architecture design
- Code maintainability
- Style consistency

### 8. Commit
```bash
/sdlc commit
```
- Create structured commit message
- Reference spec document
- Link to issue/ticket

### 9. Pull Request
```bash
/sdlc pr
```
- Create PR with description
- Include test results
- Request review

### 10. Merge
```
[Merge PR after approval]
```
- Merge to main branch
- Update changelog
- Deploy to production

## Notes

- The **coding** phase is manual - all other phases are automated
- Use `/doc`, `/pencil`, `/cache` anytime during workflow
- Can skip later phases with documented reason (but not understand + spec)
