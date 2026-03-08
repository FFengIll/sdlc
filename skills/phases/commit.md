# /commit

/commit creates a git commit following the SDLC workflow, ensuring proper documentation of changes.

**Purpose**: Commit changes with proper message and documentation

## Usage

```
/sdlc commit [message]
```

**Arguments:**
- `message`: Commit message (optional - auto-generates if not provided)

**Examples:**
- `/sdlc commit` - Auto-generate commit message from context
- `/sdlc commit "feat: add user authentication"` - Use custom message

## Pre-commit Checklist

Before committing, verify:

### 1. Code Quality
- [ ] All tests passing (`/sdlc test`)
- [ ] Verification complete (`/sdlc verify`)
- [ ] Security scan passed (`/sdlc secure`)
- [ ] Code review approved (`/sdlc cr`)

### 2. Documentation
- [ ] Spec document exists (if applicable)
- [ ] Test reports saved
- [ ] Verification report saved
- [ ] Security report saved
- [ ] Code review saved

### 3. Files
- [ ] No unintended changes
- [ ] No sensitive data committed
- [ ] No debug console.logs
- [ ] No TODO comments without issues

## Commit Message Format

Follow conventional commits format:

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Types
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting, etc.)
- `refactor`: Code refactoring
- `perf`: Performance improvements
- `test`: Adding or updating tests
- `chore`: Maintenance tasks
- `ci`: CI/CD changes

### Examples

```
feat(auth): add JWT-based authentication

Implement JWT-based authentication system with:
- User registration endpoint
- User login endpoint
- Token refresh mechanism
- Password reset flow

Closes #123
```

```
fix(api): resolve N+1 query in user listing

Use JOIN to prevent N+1 query problem when listing users.
Reduces query count from O(n) to O(1).

Fixes #145
```

```
refactor(auth): extract validation logic

Move user validation logic into separate service class
for better testability and reusability.
```

## Commit Process

### 1. Review Changes
```bash
git status
git diff
```

### 2. Stage Files
Stage relevant files, excluding:
- Debug files
- Sensitive data
- Unrelated changes

### 3. Write Commit Message
- Use conventional commit format
- Be descriptive but concise
- Reference related issues/PRs

### 4. Create Commit
```bash
git commit -m "type(scope): message"
```

## Commit Verification Example

```
━━━ Pre-commit Checklist ━━━

Code Quality:
✓ All tests passing
✓ Verification complete (100% requirements met)
✓ Security scan passed (no critical issues)
✓ Code review approved

Documentation:
✓ Spec document: docs/spec/20260308-user-auth.md
✓ Test report: docs/test/20260308-auth-test-report.md
✓ Verification: docs/verify/20260308-auth-verification.md
✓ Security: docs/secure/20260308-auth-security.md
✓ Code review: docs/cr/20260308-auth-review.md

Files:
✓ No unintended changes
✓ No sensitive data committed
✓ No debug code remaining

━━━ Changes to Commit ━━━

Files: 12 changed, 0 deleted
  src/auth/register.ts       | +45 new lines
  src/auth/login.ts          | +38 new lines
  src/auth/service.ts        | +89 new lines
  src/auth/middleware.ts     | +23 new lines
  src/types/auth.ts          | +15 new lines
  tests/unit/auth.test.ts    | +67 new lines

━━━ Commit Message ━━━

feat(auth): add JWT-based authentication

Implement JWT-based authentication system with:
- User registration endpoint (POST /api/auth/register)
- User login endpoint (POST /api/auth/login)
- Token refresh mechanism (POST /api/auth/refresh)
- Password reset flow (POST /api/auth/reset)

Features:
- bcrypt password hashing (10 rounds)
- JWT tokens (15min access, 7d refresh)
- Email verification
- Rate limiting

Spec: docs/spec/20260308-user-auth.md
Tests: 45/45 passing
Coverage: 87%

Closes #123

━━━ Commit Action ━━━
Ready to commit. Use 'git commit' to finalize.
```

## Best Practices

### Commit Granularity
- **One feature per commit**: Keep commits focused
- **Atomic changes**: Each commit should be self-contained
- **Logical grouping**: Group related files together
- **Small commits**: Easier to review and revert if needed

### Commit Message Tips
- **Use imperative mood**: "Add feature" not "Added feature"
- **Limit subject line**: 50 characters or less
- **Reference issues**: Link to related issue/PR numbers
- **Explain why**: Describe the reason for the change
- **Keep body lines**: 72 characters or less

### What to Include
- Changed source files
- Test files
- Documentation updates
- Configuration changes

### What to Exclude
- Generated files (lock files, build artifacts)
- IDE settings (.vscode, .idea)
- Environment files (.env.local)
- Debug code
- Sensitive credentials

## Commit Output

**Log commits** to track progression:
- Update `docs/commits/YYYYMMDD-[name].md` with commit details
- Include commit hash, message, and related documents

## Completion Conditions

- [ ] All pre-commit checks passed
- [ ] Changes reviewed and staged
- [ ] Commit message follows conventional format
- [ ] Commit created successfully
- [ ] Commit logged to documentation

## State Integration

- **Updates**: `sdlc.phase` = `commit`
- **Creates**: Git commit
- **Creates**: Commit log in `docs/commits/` (optional)
- **Requires**: `cr` phase completed with approval
- **Next**: Proceed to `/sdlc pr` phase

## Related Skills

- `/sdlc cr` - Prerequisite: code review must be approved
- `/sdlc pr` - Next phase: create pull request
- `/sdlc test` - Tests that must pass before committing
