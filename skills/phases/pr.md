# /pr

/pr manages the pull request process, creating PRs, managing reviews, and handling merge requirements.

**Purpose**: Create and manage pull requests for code integration

## Usage

```
/sdlc pr [action]
```

**Actions:**
- No argument: Create a new PR
- `status` - Check PR status
- `update` - Update PR with new commits
- `merge` - Merge PR (when ready)

**Examples:**
- `/sdlc pr` - Create a new pull request
- `/sdlc pr status` - Check current PR status
- `/sdlc pr merge` - Merge the PR when approved

## PR Creation Process

### 1. Prepare PR Content

#### Title
Follow conventional commit format:
```
<type>(<scope>): <subject>
```

#### Description Template
```markdown
## Overview
[Brief description of the change]

## Changes
- [Change 1]
- [Change 2]
- [Change 3]

## Type of Change
- [ ] Bug fix (non-breaking change)
- [ ] New feature (non-breaking change)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work)
- [ ] Refactor (code quality improvement)
- [ ] Documentation update

## Testing
- [ ] Unit tests added/updated
- [ ] Integration tests added/updated
- [ ] E2E tests added/updated
- [ ] All tests passing

## Documentation
- [ ] Spec document linked
- [ ] API documentation updated
- [ ] README updated (if applicable)
- [ ] Changelog updated

## Checklists
- [ ] Code follows project style guidelines
- [ ] Self-review completed
- [ ] Code is self-contained (no incomplete features)
- [ ] No unnecessary files included
- [ ] Comments added to complex code

## Related
- Spec: `docs/spec/YYYYMMDD-title.md`
- Test Report: `docs/test/YYYYMMDD-title-test-report.md`
- Verification: `docs/verify/YYYYMMDD-title-verification.md`
- Security: `docs/secure/YYYYMMDD-title-security.md`
- Code Review: `docs/cr/YYYYMMDD-title-review.md`

Closes #[issue_number]
```

### 2. Create PR
Using GitHub CLI or web interface:
```bash
gh pr create --title "feat(auth): add JWT authentication" --body "..."
```

## PR Review Process

### Review Categories

#### 1. Code Review
- Implementation correctness
- Code quality and style
- Best practices adherence
- Performance considerations

#### 2. Testing Review
- Test coverage adequate
- Tests are meaningful
- Edge cases covered
- Integration tests included

#### 3. Documentation Review
- Code is documented
- API docs updated
- README updated (if needed)
- Changelog updated

#### 4. Design Review
- Architecture appropriate
- Design patterns consistent
- No breaking changes (unless intentional)
- Migration path for breaking changes

## PR Status Check

```
━━━ Pull Request Status ━━━

PR: #45 - feat(auth): add JWT authentication
Branch: feature/user-auth → main
Status: Ready for review

━━━ Checks ━━━
✓ CI/CD Pipeline: Passing
  - Lint: ✓
  - Type Check: ✓
  - Unit Tests: ✓ (45/45)
  - Integration Tests: ✓ (12/12)
  - E2E Tests: ✓ (8/8)

✓ Code Coverage: 87% (target: 80%)
✓ Security Scan: No vulnerabilities

━━━ Review Status ━━━
Required reviewers: 2
✓ @alice - Approved
  ⚠ "Consider adding rate limiting per IP"
✓ @bob - Approved
  ✓ "Looks good to me"

━━━ Files Changed ━━━
12 files changed, +277 lines, -15 lines
  src/auth/          (+195 lines)
  tests/             (+82 lines)

━━━ Merge Readiness ━━━
✓ All checks passed
✓ Required approvals received
✓ No merge conflicts
✓ Up to date with main

━━━ Action ━━━
Ready to merge! Use `/sdlc pr merge` to complete.
```

## Merge Requirements

Before merging, ensure:

### Required Checks
- [ ] All CI/CD checks passing
- [ ] Code coverage threshold met
- [ ] Security scan clean
- [ ] No merge conflicts

### Required Approvals
- [ ] Minimum number of approvals received
- [ ] No outstanding review objections
- [ ] Reviewer feedback addressed

### Final Checks
- [ ] PR description complete
- [ ] Related spec linked
- [ ] Test reports linked
- [ ] Breaking changes documented

## Merge Process

### 1. Final Review
Review all:
- Conversation threads
- Review comments
- Suggested changes

### 2. Update if Needed
Apply any final changes based on feedback

### 3. Merge
```bash
gh pr merge --merge --delete-branch
```

### 4. Post-Merge
- [ ] Verify deployment
- [ ] Update project tracking
- [ ] Notify stakeholders
- [ ] Close related issues

## Best Practices

### PR Hygiene
- **Keep PRs focused**: One feature or fix per PR
- **Keep PRs small**: Easier to review and merge
- **Use draft PRs**: For work in progress
- **Reference issues**: Link to related issue numbers

### PR Communication
- **Be responsive**: Address review comments promptly
- **Be descriptive**: Explain why changes were made
- **Be respectful**: Consider all feedback
- **Document decisions**: Explain non-obvious choices

### Review Tips
- **Be thorough**: Review all changed files
- **Be constructive**: Provide helpful feedback
- **Be timely**: Review PRs promptly
- **Be clear**: Explain suggestions

## PR Output

**Log PR details** to `docs/pr/YYYYMMDD-[name].md`:
- PR number and title
- Branch information
- Review status
- Merge status
- Related documents

## Completion Conditions

### For PR Creation
- [ ] PR title follows format
- [ ] PR description complete with template
- [ ] All related documents linked
- [ ] PR created successfully

### For PR Merge
- [ ] All required approvals received
- [ ] All checks passing
- [ ] No merge conflicts
- [ ] PR merged successfully
- [ ] Branch deleted (if applicable)
- [ ] PR logged to documentation

## State Integration

- **Updates**: `sdlc.phase` = `pr`
- **Creates**: Pull request
- **Creates**: PR log in `docs/pr/`
- **Requires**: `commit` phase completed
- **Next**: After merge, workflow complete

## Related Skills

- `/sdlc commit` - Prerequisite: commits must exist to create PR
- `/sdlc cr` - Code review that happens before PR review
- `/sdlc test` - Tests that must pass for PR checks
