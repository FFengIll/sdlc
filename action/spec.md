# Specification Phase Skill

Creates detailed technical specification documents based on research findings and requirements.

## Usage

```
/sdlc spec [title]
```

## Guideline

**ALWAYS follow this sequence:**

### Phase 1: Propose (Requirement-Driven)

1. **Understand First, Design Before Action**
   - Read the user's request and understand the intent
   - Review any existing research findings
   - Think about the problem before jumping to solution
   - Design the approach in your head first

2. **Read Architecture Cache**
   - Check `./.design/arch/` for existing architecture cache
   - Priority order: component → module → project overview
   - Use cached architecture info to reduce code searching and reading
   - If no relevant cache exists, generate it first with `/sdlc understand [scope]`

3. **Present Motivation + Proposal**
   - Write a brief **Motivation** section: *why* this feature/change is needed
   - Write a **Proposal** section: *what* will be built at a high level (1-3 paragraphs)
   - Use `pencil` skill to show a text-based diagram if it helps clarify the design
   - Use `AskUserQuestion` to confirm direction with the user before proceeding
   - **Do not write the full spec yet** — wait for user confirmation

### Phase 2: Expand (Full Spec)

4. **Write the Spec Document**
   - Only after user confirms the proposal direction
   - Save to `./.design/{feature}.spec.md`
   - Expand the proposal into a full spec with all relevant sections
   - Keep specs key-focused and guiding-oriented
   - Pay attention to model definitions and file/module/function abstractions
   - **IMPORTANT**: After creating file, display the path to user:
     ```
     ✅ Spec file created: `.design/recording-impl.spec.md`
     ```

5. **Output the Design**
   - After writing the spec, present the design to the user
   - **Always include file path in output** for easy reference
   - Use `askUserQuestion` tool to communicate with the user
   - **Include file path in AskUserQuestion options/descriptions** when relevant
   - Use `pencil` skill to show design in text-based graph if helpful

## Architecture Cache

Architecture cache speeds up spec creation by reusing existing understanding.

### Reading Cache

Priority order (most specific first):
```bash
.design/arch/[module]-[sub]-[comp]-arch.md  # Component (~3 days)
.design/arch/[module]-[sub]-arch.md          # Sub-module (~7 days)
.design/arch/[module]-arch.md                # Module (~14 days)
.design/arch/overview-arch.md                # Project (~30 days)
```

**Note**: Arch files use simplified format `scope-arch.md` because the directory is already isolated.

### Cache Freshness

TTL values are reference guidelines:
- Project level: ~30 days
- Module level: ~14 days
- Component level: ~7 days

If cache is expired or missing, regenerate using `/sdlc understand [scope]`.

**See also**: `.design/arch/ARCH_CACHE_SYSTEM.md` for full documentation

## Output Format

Spec files are saved to `.design/{feature}.spec.md`

**Filename format**: `{feature}.spec.md` under `.design/` (date goes in frontmatter)
- `category` - Module/category (e.g., `auth`, `payment`, `user`)
- `feature` - Feature description in kebab-case (e.g., `user-login`, `oauth-integration`)
- `date` - Date in frontmatter `date: YYYY-MM-DD`
- `type` - Document type (`spec` for specifications)

**Examples**:
- `auth-user-login.spec.md`
- `payment-stripe-checkout.spec.md`
- `user-profile-edit.spec.md`

Include:
- Overview and scope
- Requirements (functional and non-functional)
- User stories/use cases
- Data structures and schemas
- API endpoints and contracts
- Component interfaces
- State management approach
- Error handling strategy
- Security considerations
- Testing strategy
- Dependencies
- Implementation phases
- Open questions
- Alternatives considered

## Frontend Notes

- Use the same tech stack, components, theme, and design patterns
- Understand user intent and implement good design
- Replacement solutions are allowed for locale and text

## Backend Notes

- Pay attention to current file structure
- List directories with limited depth
- Write necessary tests following language conventions
- Handle special test cases carefully

## IMPORTANT

- You can use `askUserQuestion` to communicate with the user or let them choose
- You can use `pencil` skill to show design in text-based graph
- DO NOT make spec documents too long and verbose; keep them key-focused
- **ALWAYS display the file path after creating/updating the spec document**
- **Include file path in AskUserQuestion when asking user to review or approve**
- Format: `✅ Spec file: `.design/{feature}.spec.md``

## Examples

### Example 1: Feature with Existing Cache

```bash
/sdlc spec "Add OAuth to Auth"
# Reads .design/arch/auth-arch.md for context
# Writes .design/auth-oauth-integration.spec.md
```

### Example 2: Feature Requiring New Cache

```bash
/sdlc understand auth/providers    # Create cache first
/sdlc spec "Add SAML Provider"     # Then write spec as auth-saml-provider.spec.md
```

## Integration

**Workflow Position:** Research → **Spec** → Coding

The spec phase translates research findings and architecture understanding into a concrete implementation plan.

---

**Version**: 1.2.0 | **Updated**: 2026-04-12