# Minor Workflow

**Purpose**: Make small, well-defined modifications to specific files or code sections.

> **Use when**: The user has clearly identified what needs to change and where. No research or specification needed - just direct edits to selected files.

## Core Principle: Direct, No Subagents

Minor tasks are simple and fast by definition. The overhead of spawning subagents (context transfer, coordination, result relay) would exceed the cost of the task itself.

- **No subagents** - never delegate to Explore/general-purpose/Plan agents
- **Direct location** - use Read/Grep/Glob directly to locate the target; the user usually already pointed at it
- **Direct edit** - modify in the main conversation, single pass
- **Speed is the feature** - if locating the change requires multi-file exploration, it's not a minor task (escalate to another workflow)

## When to Use

Use this workflow when:
- Adjusting UI elements (colors, spacing, fonts)
- Modifying configuration values
- Updating text/content
- Small code tweaks (renaming, reordering)
- User-specified file modifications

## Workflow Sequence

```
START
  │
  ▼
coding → test → commit → END
```

**Characteristics:**
- No understand phase - user knows what to change
- No spec phase - requirements are clear
- No verify phase - change is straightforward
- No PR - direct commit to branch

## Phase Details

### 1. Coding
```
[Direct modification phase]
```
- Locate the target directly (Read/Grep)
- Edit selected files as specified
- Make the exact changes requested
- No additional refactoring or improvements
- Keep changes minimal and focused

### 2. Test
```bash
/sdlc test
```
**What it checks:**
- lint (code style)
- format (code formatting)
- typecheck (if applicable)

**Note**: No full test suite required for minor changes unless specified

### 3. Commit
```bash
/sdlc commit
```
- Simple commit message
- Reference modified files
- No detailed documentation needed

## Usage Example

```bash
# User selects code and requests minor change
/sdlc start minor "Update button color to blue"

# Step 1: Direct code edit
# → Modify the button color in selected file

# Step 2: Quick validation
/sdlc test
# → Runs lint + format only

# Step 3: Commit
/sdlc commit
# → Simple commit: "style: update button color to blue"

# Done! No PR, no verify, no documentation
```

## When NOT to Use

❌ **Don't use minor for:**
- New features (use `feature`)
- Bug fixes (use `bugfix`)
- Refactoring (use `refactor`)
- Changes that require understanding context (use `quick`)
- Changes where the target location is unknown and needs broad exploration

✅ **Use minor for:**
- "Change this button to blue"
- "Update the config timeout to 30s"
- "Rename this variable"
- "Adjust this margin"

## Notes

- Use `/commit` standalone if not in a workflow
