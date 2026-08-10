# Refactor Workflow

**Purpose**: Improve code structure without changing functionality.

## When to Use

Use this workflow when:
- Improving code quality
- Reducing technical debt
- Optimizing performance
- Restructuring for maintainability
- Updating to new patterns/architecture

## Workflow Sequence

```
START
  │
  ▼
understand → spec → coding → test → DONE
```

## Core Phases

### 1. Understand (Required)
```bash
/sdlc understand [scope]
```
Map current architecture before changing it:
- Current dependencies and relationships
- Integration points
- Data flow
- Potential impact areas

### 2. Spec (Required)
```bash
/sdlc spec "Design refactoring approach"
```
Define the refactoring plan:
- Refactoring goals
- New structure
- Migration strategy
- Breaking changes (if any)

### 3. Coding (Manual)
```
[Implement refactoring]
```
- Maintain existing behavior
- Update related tests
- Keep changes incremental

### 4. Test (Required)
```bash
/sdlc test
```
Verify behavior unchanged:
- All tests pass
- No regressions
- Performance maintained

## Optional Tools

Use these when needed, not by default:

### Code Review
```bash
/sdlc cr
```
- Get architecture feedback
- Review code quality improvements

### Security Scan
```bash
/sdlc secure
```
- Check for new vulnerabilities
- Verify dependencies

### Commit & PR
```bash
/sdlc commit
/sdlc pr
```
- When ready to integrate changes

## Refactoring Categories

### Code Quality
- Reduce complexity
- Improve naming
- Extract methods
- Remove duplication

### Architecture
- Separate concerns
- Introduce patterns
- Restructure modules
- Update dependencies

### Performance
- Optimize algorithms
- Reduce memory usage
- Improve caching

### Maintainability
- Add type safety
- Improve testing
- Update documentation

## Key Principles

1. **Understand First**: Never refactor without understanding the current system
2. **Preserve Behavior**: Refactoring should not change external behavior
3. **Small Steps**: Make incremental changes that can be tested
4. **Test Coverage**: Ensure tests pass before and after

---

**Version**: 2.0.0 | **Updated**: 2026-03-26
