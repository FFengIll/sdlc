# Feature Development Workflow

**Purpose**: Develop new features from research to production deployment.

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
research → spec → coding → test → verify → secure → cr → commit → pr → MERGE
```

## Phase Details

### 1. Research
```bash
/sdlc research "Investigate technology options"
```
- Research technical approaches
- Evaluate libraries and frameworks
- Document findings
- Identify potential risks

### 2. Spec
```bash
/sdlc spec "Design feature specification"
```
- Define requirements
- Design APIs and interfaces
- Document data structures
- Create implementation plan

### 3. Coding
```
[Manual coding phase]
```
- Implement the feature based on spec
- Write code following project conventions
- Add inline documentation

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

### 5. Verify
```bash
/sdlc verify
```
**What it checks:**
- Requirements coverage
- API contract matching
- Data structure correctness
- Business logic completeness

**Question answered**: "Did we build the right thing?"

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

## Usage Example

```bash
# Start feature workflow
/sdlc start feature "User authentication"

# Execute research phase
/sdlc research "Evaluate auth libraries: NextAuth vs Clerk vs custom"

# Create specification
/sdlc spec "Define auth endpoints, session management, and security"

# [Manual coding - implement the feature]

# Run tests after coding
/sdlc test

# Verify implementation matches spec
/sdlc verify

# Security check
/sdlc secure

# Code review
/sdlc cr

# Commit changes
/sdlc commit

# Create pull request
/sdlc pr

# [Merge after review approval]
```

## Navigation Commands

```bash
# Move to next phase
/sdlc next

# Skip current phase (with reason)
/sdlc skip "Phase not applicable for this feature"

# Check current status
/sdlc status

# Jump to specific phase
/sdlc goto <phase>
```

## Completion Checklist

- [ ] Research documented
- [ ] Spec approved
- [ ] Code implemented
- [ ] All tests passing
- [ ] Spec requirements verified
- [ ] Security scan clean
- [ ] Code review approved
- [ ] Committed with proper message
- [ ] PR created and merged

## Notes

- The **coding** phase is manual - all other phases are automated
- Use `/doc`, `/pencil`, `/cache` anytime during workflow
- Each phase validates specific quality aspects
- Can skip phases with documented reason
- Test phase includes multiple check types
