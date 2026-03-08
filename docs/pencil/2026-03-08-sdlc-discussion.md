# SDLC Skills System - Discussion Points

## Design Summary

I've designed a comprehensive SDLC skill system with the following characteristics:

### Architecture
- **7 SDLC Phases**: Planning → Analysis → Design → Implementation → Testing → Deployment → Maintenance
- **5 Entry Points**: Feature, Bugfix, Refactor, Research, Discuss
- **6 Foundation Skills**: pencil, doc, cache, git, code, test
- **40+ Skills** total across all phases

### Key Design Decisions

1. **Hierarchical Organization**: Skills organized by phase under `skills/{phase}/`
2. **Foundation Layer**: Shared skills eliminate duplication
3. **Multiple Entry Points**: Different workflows for different scenarios
4. **Symlink Strategy**: Existing skills like `/pencil` referenced where needed
5. **Progressive Implementation**: 7-week rollout plan

## Questions for Discussion

### 1. Skill Granularity
**Question**: Are the skills too granular or not granular enough?

**Current Design Examples**:
- `/test` vs `/test-unit`, `/test-integ`, `/test-e2e`
- `/deploy` vs `/build`, `/release`, `/monitor`

**Options**:
- A) Keep granular (40+ skills) - Maximum flexibility
- B) Consolidate (20-30 skills) - Simpler to learn
- C) Hybrid - Core skills granular, others consolidated

### 2. Entry Point Behavior
**Question**: How should entry point skills behave?

**Options**:
- A) **Sequential Guide**: Entry point guides through each phase step-by-step
- B) **Smart Jump**: Entry point assesses context and jumps to appropriate phase
- C) **Menu Based**: Entry point shows menu of available actions
- D) **Conversational**: Entry point asks questions to determine workflow

### 3. Foundation Skills Implementation
**Question**: Should foundation skills be:

**Options**:
- A) **Standalone Skills**: Can be called directly (`/doc`, `/code`)
- B) **Internal Only**: Only called by other skills, not directly
- C) **Hybrid**: Some standalone (like `/pencil`), some internal

**Recommendation**: Hybrid - `/pencil`, `/doc`, `/git` as standalone, `/cache`, `/code`, `/test` as internal utilities

### 4. Existing Skills Migration
**Question**: How to handle existing skills in `/commands`?

**Current Existing Skills**:
- `/spec`, `/pencil`, `/pr`, `/codereview`, `/refactor`
- `/git-commit`, `/discuss`, `/research`, `/codeclean`
- `/refactor-go`, `/test-go`, `/refactor-frontend`
- `/review-branch`, `/review-refactor`, `/specreview`
- `/new-command`, `/update-arch`, `/optimize-go-test`

**Options**:
- A) **Move & Replace**: Move all to `skills/`, update commands/ as symlinks
- B) **Duplicate**: Keep in commands/, copy to skills/ (maintain compatibility)
- C) **Gradual Migration**: Move gradually, maintain backward compatibility
- D) **Commands as Interface**: Keep commands/ as user-facing, skills/ as implementation

### 5. Workflow Automation
**Question**: Should skills automatically chain or require user initiation?

**Example**: After `/feature` completes planning phase:

**Options**:
- A) **Auto-Continue**: Automatically suggest and proceed to next phase
- B) **User Prompt**: Ask if user wants to continue to next phase
- C) **Manual**: User must explicitly call next skill
- D) **Configurable**: User preference setting

### 6. Artifact Management
**Question**: How should outputs be organized?

**Current Proposal**:
```
docs/
├── spec/          # Specifications
├── arch/          # Architecture cache
├── pencil/        # Wireframes
├── research/      # Research docs
├── design/        # Design docs
├── test/          # Test plans
└── review/        # Review records
```

**Options**:
- A) **By Phase**: Organize by SDLC phase (as above)
- B) **By Feature**: Organize by feature/project
- C) **By Date**: Organize chronologically
- D) **Hybrid**: Phase structure with feature tags

### 7. Language/Technology Specific Skills
**Question**: Should we have language-specific skills?

**Current**: `/refactor-go`, `/test-go`, `/refactor-frontend`

**Options**:
- A) **Keep Specific**: Maintain language-specific skills
- B) **Generic Only**: Use generic skills with parameters
- C) **Hybrid**: Generic skills with specific variants for common cases

### 8. Skill Discovery
**Question**: How will users discover available skills?

**Options**:
- A) **Index**: Maintain `/skills` index skill
- B) **Help Command**: `/help` or `/skills` command
- C) **Contextual**: Suggest relevant skills based on context
- D) **All**: Combination of above

### 9. Error Handling & Recovery
**Question**: How should skills handle failures?

**Examples**:
- Test fails during implementation
- Deploy fails during deployment
- Merge conflict during review

**Options**:
- A) **Stop & Report**: Stop workflow, report issue, wait for user
- B) **Auto-Retry**: Attempt automatic recovery
- C) **Suggest Fix**: Suggest fix, wait for user
- D) **Smart Recovery**: Context-dependent recovery strategy

### 10. Priority Phases
**Question**: Which phases should we implement first?

**Current Plan**: Foundation → Entry → Planning → Design → Implementation → Testing → Deployment → Review → Maintenance

**Alternative Priority Options**:
- A) **Feature Flow First**: Complete feature workflow end-to-end
- B) **Bugfix Flow First**: Complete bugfix workflow (simpler)
- C) **Foundation First**: All foundation skills, then expand
- D) **Most Used First**: Based on actual usage patterns

## Technical Considerations

### Skill Definition Format
Should we standardize skill definition format?

```markdown
# /skill-name

## Description
Brief description

## Purpose
What it accomplishes

## Usage
/skill-name [args]

## Inputs
- Required inputs
- Optional inputs

## Outputs
- What it produces
- Where files are saved

## Dependencies
- Other skills it uses
- External tools needed

## Workflow
- Step-by-step process

## Examples
Usage examples
```

### Skill Metadata
Should skills include metadata for discovery?
- Tags (phase, technology, complexity)
- Related skills
- Prerequisites
- Estimated time

## Recommendations

### My Recommendations:

1. **Granularity**: Hybrid approach - core workflow skills granular, utility skills consolidated
2. **Entry Points**: Conversational - assess context and guide user
3. **Foundation Skills**: Hybrid - pencil, doc, git as standalone; cache, code, test as internal
4. **Migration**: Gradual - maintain backward compatibility during transition
5. **Automation**: User Prompt - ask before continuing to next phase
6. **Artifacts**: By Phase with feature tagging
7. **Language Skills**: Hybrid - generic skills with specific variants
8. **Discovery**: All approaches - index, help, and contextual
9. **Errors**: Smart Recovery - context-dependent handling
10. **Priority**: Feature Flow First - demonstrate complete workflow

## Next Steps

1. **Review & Discuss**: Review these questions and recommendations
2. **Decide**: Make decisions on each point
3. **Iterate**: Refine design based on decisions
4. **Implement**: Begin phased implementation
5. **Validate**: Test with real workflows

## Questions for You

1. Do you agree with the overall architecture? Any concerns?
2. Which of the 10 discussion points need clarification?
3. Are there missing skills or phases?
4. Any existing skills that don't fit this model?
5. Should we prototype a subset first (e.g., just feature flow)?
6. Timeline - is 7 weeks reasonable? Too long? Too short?
7. Priority - which workflow matters most to you?
