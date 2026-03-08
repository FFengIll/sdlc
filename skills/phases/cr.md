# /cr

/cr performs code review to assess code quality, maintainability, and adherence to best practices.

**Purpose**: Ensure high-quality, maintainable code

## Usage

```
/sdlc cr [files_or_directories]
```

**Arguments:**
- `files_or_directories`: Specific files or directories to review (optional - reviews changes if not provided)

**Examples:**
- `/sdlc cr` - Review current changes
- `/sdlc cr src/auth` - Review auth module
- `/sdlc cr src/auth/login.ts src/auth/register.ts` - Review specific files

## Review Categories

### 1. Best Practices
**Purpose**: Verify adherence to coding best practices

**Checks**:
- Error handling implementation
- Input validation presence
- Resource cleanup (connections, file handles)
- Async/await proper usage
- Memory leak prevention

**Output example**:
```
━━━ Best Practices ━━━
✓ Error handling implemented
✓ Input validation present
⚠ Consider adding rate limiting to auth endpoints
⚠ Missing timeout on database queries
```

### 2. Code Style
**Purpose**: Ensure consistent, readable code

**Checks**:
- Naming conventions
- Code formatting
- Comment quality
- File organization
- Import structure

**Output example**:
```
━━━ Code Style ━━━
✓ Follows project conventions
✓ Naming is consistent
✓ Proper comments and documentation
⚠ Some functions are too long
  - authenticateUser(): 67 lines (target: <50)
```

### 3. Architecture
**Purpose**: Assess structural design

**Checks**:
- Separation of concerns
- Coupling between modules
- Abstraction levels
- Design pattern usage
- Module boundaries

**Output example**:
```
━━━ Architecture ━━━
✓ Separation of concerns
✓ No tight coupling
⚠ Service layer could be extracted for better testability
✓ Clear module boundaries
```

### 4. Maintainability
**Purpose**: Evaluate long-term maintainability

**Checks**:
- Code complexity
- Function length
- Duplication
- Test coverage
- Documentation

**Output example**:
```
━━━ Maintainability ━━━
✓ Code is well commented
✓ Functions are focused
⚠ authenticateUser() is too long (67 lines, target: <50)
⚠ Some duplicated validation logic
✓ Good test coverage
```

### 5. Performance
**Purpose**: Identify performance concerns

**Checks**:
- Algorithm efficiency
- Database query optimization
- Caching opportunities
- Unnecessary re-renders
- Bundle size impact

**Output example**:
```
━━━ Performance ━━━
⚠ N+1 query problem in user listing
✓ Efficient pagination implementation
⚠ Missing indexes on frequently queried fields
✓ Appropriate use of caching
```

## Full Code Review Report Example

```
Code Review Results:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

━━━ Files Reviewed ━━━
- src/auth/login.ts
- src/auth/register.ts
- src/auth/service.ts
- src/auth/middleware.ts

━━━ Best Practices ━━━
✓ Error handling implemented
✓ Input validation present
⚠ Consider adding rate limiting to auth endpoints
⚠ Missing timeout on database queries
✓ Proper async/await usage
✓ Resources cleaned up properly

━━━ Code Style ━━━
✓ Follows project conventions
✓ Naming is consistent (camelCase for vars, PascalCase for types)
✓ Proper comments and documentation
⚠ Some functions are too long
  - authenticateUser(): 67 lines (target: <50)
  - registerUser(): 58 lines (target: <50)

━━━ Architecture ━━━
✓ Separation of concerns (routes → controller → service → repository)
✓ No tight coupling between modules
⚠ Service layer could be extracted for better testability
  -建议: Move business logic from controller to AuthService
✓ Clear module boundaries
✓ Dependency injection pattern used

━━━ Maintainability ━━━
✓ Code is well commented
✓ Functions are focused on single responsibility
⚠ authenticateUser() is too long (67 lines, target: <50)
⚠ Some duplicated validation logic
  -建议: Extract to validateUserCredentials() helper
✓ Good test coverage (87%)
✓ Clear variable names

━━━ Performance ━━━
⚠ N+1 query problem in user listing
  -建议: Use JOIN or data loader
✓ Efficient pagination implementation
⚠ Missing indexes on frequently queried fields
  -建议: Add index on users.email, users.created_at
✓ Appropriate use of caching (Redis for sessions)

━━━ Security ━━━
✓ Passwords hashed with bcrypt
✓ SQL injection prevention (parameterized queries)
✓ XSS prevention (input sanitization)
⚠ Consider adding CSRF protection
✓ Rate limiting on auth endpoints

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Suggestions:
Priority - HIGH:
1. Fix N+1 query in user listing
   - Use JOIN or data loader pattern

2. Add database indexes
   - users.email (for login lookups)
   - users.created_at (for sorting)

Priority - MEDIUM:
3. Refactor long functions
   - Break down authenticateUser() into smaller functions
   - Break down registerUser() into smaller functions

4. Extract validation logic
   - Create validateUserCredentials() helper

5. Add CSRF protection
   - Implement CSRF tokens for state-changing operations

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Overall: APPROVED with suggestions ✓
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Strengths:
- Good separation of concerns
- Solid error handling
- Strong security practices
- Good test coverage

Areas for Improvement:
- Function length (some >50 lines)
- Query optimization (N+1 problem)
- Code duplication (validation logic)
```

## Code Review Output

**Always save code review reports** to `docs/cr/YYYYMMDD-[name]-review.md` where:
- `YYYYMMDD` - Current date timestamp
- `[name]` - Feature or component name

## Best Practices

### Conducting Reviews
- **Be constructive**: Focus on improvement, not criticism
- **Explain why**: Provide context for suggestions
- **Prioritize**: Mark issues as high/medium/low priority
- **Be specific**: Point to exact code locations

### What to Look For
- **Correctness**: Does the code do what it's supposed to?
- **Readability**: Is the code easy to understand?
- **Maintainability**: Will this be easy to change later?
- **Performance**: Are there obvious performance issues?
- **Security**: Are there security vulnerabilities?

### Review Process
1. **Understand the context**: Read the spec or PR description
2. **Review the code**: Check each category systematically
3. **Test the code**: Run tests, verify functionality
4. **Provide feedback**: Clear, actionable suggestions

## Completion Conditions

- [ ] All review categories assessed
- [ ] Code review report saved to `docs/cr/`
- [ ] Suggestions prioritized
- [ ] Either:
  - [ ] Code approved (PASS), or
  - [ ] Issues documented with action plan (FAIL with fixes required)

## State Integration

- **Updates**: `sdlc.phase` = `cr`
- **Creates**: Code review report in `docs/cr/`
- **Requires**: `secure` phase completed
- **Next**: Proceed to `/sdlc commit` phase

## Related Skills

- `/sdlc secure` - Prerequisite: security checks completed
- `/sdlc coding` - The code being reviewed
- `/sdlc commit` - Next phase after approval
- `/sdlc test` - Tests that should pass
