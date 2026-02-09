# /commit

/commit guides the process of creating git commits with proper file selection and separation of concerns.

## Usage

```
/commit [message]
```

**Parameters:**
- `message` (optional): Commit message (if not provided, will prompt based on changes)

## Guidelines

### File Selection Principles

1. **Only Commit Related Files**
   - Commit files that are logically related to each other
   - Each commit should have a single, coherent purpose
   - Group files that implement the same feature/fix together

2. **Never Commit**
   - Secrets: `.env`, `.env.local`, credentials.json, `.pem`, `.key` files
   - IDE/Editor files: `.idea/`, `.vscode/`, `*.swp`, `*.swo`
   - Build artifacts: `node_modules/`, `dist/`, `build/`, `*.lockb`
   - OS files: `.DS_Store`, `Thumbs.db`
   - Test/Temp files: test files with `test-` prefix unless explicitly requested
   - Log files: `*.log`, `npm-debug.log`, `yarn-error.log`

3. **Separate Different Changes**
   - Different features → separate commits
   - Bug fixes vs new features → separate commits
   - Refactoring vs functional changes → separate commits
   - Docs vs code → separate commits (unless doc change directly relates to code change)
   - Different modules/packages → separate commits if logically independent

### Commit Process

1. **Check Status**
   - Run `git status` to see all untracked and modified files
   - Run `git diff` to see actual changes

2. **Group Related Changes**
   - Identify logical groups among changed files
   - Plan multiple commits if changes fall into distinct categories

3. **Stage Files Selectively**
   - Use `git add <specific-files>` NOT `git add .` or `git add -A`
   - Stage only the files for the current commit
   - Double-check: do these files all relate to the same change?

4. **Write Commit Message**
   - Follow project's commit style (see `/pr` command for prefixes)
   - Format: `[prefix]: [brief description]`
   - Lowercase prefix and description
   - Keep it focused on what changed and why

5. **Verify and Commit**
   - Run `git status` to verify staged files
   - Run `git diff --staged` to review changes
   - Create commit with `git commit -m "message"`
   - Repeat for remaining changes if applicable

### Commit Message Prefixes

- `bugfix:` - Bug fixes
- `feat:` - New features
- `command:` - Command-related changes
- `chore:` - Chores/maintenance
- `mv:` - File/directory moves
- `doc:` - Documentation changes
- `perf:` - Performance improvements

### Examples

**Scenario 1: Single focused change**
```
# Changed files: auth.go, auth_test.go, login.html
# All related to login feature
→ Single commit: "feat: add user login functionality"
```

**Scenario 2: Multiple unrelated changes**
```
# Changed files:
# - user.go, user_test.go (new feature)
# - auth.go (bugfix)
# - README.md (docs)
# - .env.local (should be ignored!)

→ Commit 1: "bugfix: fix token validation in auth"
→ Commit 2: "feat: add user profile management"
→ Commit 3: "doc: update README with new features"
```

**Scenario 3: With suspicious files**
```
# Changed files:
# - api.go (feature)
# - .env (NEVER COMMIT)
# - test-api.sh (test file, skip unless asked)

→ Commit: "feat: add new API endpoints"
→ Ignore .env and test files
```

## Tips

- Always review what you're staging before committing
- When in doubt, ask: "Do these changes belong together?"
- It's better to have multiple small commits than one large mixed commit
- Use `git status` between commits to track remaining changes
- If you see `.env`, credentials, or lock files, warn the user and skip them
