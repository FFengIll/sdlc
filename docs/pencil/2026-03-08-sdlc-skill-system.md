# SDLC Skill System Architecture

## Overview
A comprehensive skill system supporting the complete Software Development Life Cycle with multiple entry points and shared foundational capabilities.

## Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                          SDLC SKILL SYSTEM                                      │
├─────────────────────────────────────────────────────────────────────────────────┤
│                                                                                 │
│  ┌─────────────────────────────────────────────────────────────────────────┐   │
│  │                         ENTRY POINTS                                    │   │
│  │  /feature   /bugfix   /refactor   /research   /discuss                  │   │
│  └───────────────────────────┬─────────────────────────────────────────────┘   │
│                              │                                                   │
│                              ▼                                                   │
│  ┌─────────────────────────────────────────────────────────────────────────┐   │
│  │                      FOUNDATIONAL SKILLS (Shared)                        │   │
│  │  ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐      │   │
│  │  │ pencil │ │  doc   │ │ cache  │ │  git   │ │  code  │ │  test  │      │   │
│  │  └────────┘ └────────┘ └────────┘ └────────┘ └────────┘ └────────┘      │   │
│  └───────────────────────────┬─────────────────────────────────────────────┘   │
│                              │                                                   │
│                              ▼                                                   │
│  ┌─────────────────────────────────────────────────────────────────────────┐   │
│  │                         SDLC PHASES                                      │   │
│  │                                                                          │   │
│  │  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐               │   │
│  │  │  PLANNING    │───▶│   ANALYSIS   │───▶│    DESIGN    │               │   │
│  │  │              │    │              │    │              │               │   │
│  │  │ /spec        │    │ /research    │    │ /pencil      │               │   │
│  │  │ /arch        │    │ /analyze     │    │ /prototype   │               │   │
│  │  │ /estimate    │    │ /discuss     │    │ /review-des  │               │   │
│  │  └──────────────┘    └──────────────┘    └──────────────┘               │   │
│  │         │                                      │                          │   │
│  │         └──────────────────┬───────────────────┘                          │   │
│  │                            │                                              │   │
│  │                            ▼                                              │   │
│  │  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐               │   │
│  │  │IMPLEMENTATION│───▶│   TESTING    │───▶│  DEPLOYMENT  │               │   │
│  │  │              │    │              │    │              │               │   │
│  │  │ /code        │    │ /test        │    │ /build       │               │   │
│  │  │ /implement   │    │ /test-unit   │    │ /deploy      │               │   │
│  │  │ /refactor    │    │ /test-integ  │    │ /release     │               │   │
│  │  │ /codeclean   │    │ /test-e2e    │    │ /monitor     │               │   │
│  │  └──────────────┘    └──────────────┘    └──────────────┘               │   │
│  │         │                                      │                          │   │
│  │         └──────────────────┬───────────────────┘                          │   │
│  │                            │                                              │   │
│  │                            ▼                                              │   │
│  │  ┌──────────────┐    ┌──────────────┐                                     │   │
│  │  │  MAINTENANCE │◀───│   REVIEW     │                                     │   │
│  │  │              │    │              │                                     │   │
│  │  │ /monitor     │    │ /codereview  │                                     │   │
│  │  │ /debug       │    │ /pr          │                                     │   │
│  │  │ /optimize    │    │ /approve     │                                     │   │
│  │  │ /update-doc  │    │ /merge       │                                     │   │
│  │  └──────────────┘    └──────────────┘                                     │   │
│  └─────────────────────────────────────────────────────────────────────────┘   │
│                                                                                 │
└─────────────────────────────────────────────────────────────────────────────────┘

WORKFLOW EXAMPLES:

Feature Flow:
/feature → /spec → /research → /pencil → /implement → /test → /review → /merge

Bug Fix Flow:
/bugfix → /analyze → /debug → /test → /codereview → /commit

Refactor Flow:
/refactor → /analyze → /refactor-go → /test-go → /codereview → /commit

Research Flow:
/research → /doc → /discuss → /spec → /pencil → /prototype
```

## Skill Categories

### 1. Entry Point Skills
```
/feature    - Start a new feature development workflow
/bugfix     - Start a bug fix workflow
/refactor   - Start a refactoring workflow
/research   - Start a research/investigation workflow
/discuss    - Start a discussion/consultation workflow
```

### 2. Foundational Skills (Shared)
```
/pencil     - Wireframe & UI/UX design visualization
/doc        - Documentation generation & management
/cache      - Architecture knowledge caching & retrieval
/git        - Git operations & version control
/code       - Code generation & modification
/test       - Test generation & execution
```

### 3. Phase-Specific Skills

**Planning Phase:**
```
/spec       - Requirements specification
/arch       - Architecture design
/estimate   - Effort estimation
```

**Analysis Phase:**
```
/research   - Technical research
/analyze    - Code/issue analysis
/discuss    - Stakeholder discussion
```

**Design Phase:**
```
/pencil     - UI/UX wireframing
/prototype  - Prototype generation
/review-des - Design review
```

**Implementation Phase:**
```
/code       - Code generation
/implement  - Feature implementation
/refactor   - Code refactoring
/codeclean  - Code cleanup
```

**Testing Phase:**
```
/test       - Test coordination
/test-unit  - Unit testing
/test-integ - Integration testing
/test-e2e   - End-to-end testing
```

**Deployment Phase:**
```
/build      - Build configuration
/deploy     - Deployment automation
/release    - Release management
/monitor    - Monitoring setup
```

**Review Phase:**
```
/codereview - Code review
/pr         - Pull request management
/approve    - Approval workflow
/merge      - Merge coordination
```

**Maintenance Phase:**
```
/monitor    - Application monitoring
/debug      - Debugging assistance
/optimize   - Performance optimization
/update-doc - Documentation updates
```

## Integration Points

1. **Horizontal Integration**: Skills can call other skills as needed
2. **Vertical Integration**: Foundational skills support all phase-specific skills
3. **Entry Point Flexibility**: Multiple paths to reach the same phase
4. **Skip Capability**: Phases can be skipped based on context

## Data Flow

```
User Request → Entry Point → Phase Skills → Foundational Skills → Output
     ↓              ↓              ↓                ↓              ↓
  Context       Workflow      Specific Task    Shared Tools    Artifact
```

## Key Design Principles

1. **Composability**: Skills combine to form complete workflows
2. **Reusability**: Foundational skills eliminate duplication
3. **Flexibility**: Multiple entry points for different scenarios
4. **Traceability**: Each phase produces documented artifacts
5. **Efficiency**: Cache architecture knowledge to reduce overhead
