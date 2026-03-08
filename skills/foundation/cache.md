# Cache Skill

The `/cache` skill manages SDLC workflow state and cached data, including architecture knowledge and workflow metadata.

## Usage

```
/cache [action] [key] [value?]
```

**Actions:**
- `get` - Retrieve cached value by key
- `set` - Store a value with associated key
- `clear` - Remove cached value by key (or clear all if no key)
- `list` - List all cached keys and metadata
- `invalidate` - Mark cache entry as stale

**Keys:**
- `workflow.state` - Current SDLC phase and status
- `workflow.phase` - Active phase name
- `architecture` - Project architecture cache
- `branch` - Current working branch
- `config` - SDLC configuration settings
- Custom keys for project-specific data

**Values:**
- Simple values: strings, numbers, booleans
- Complex values: JSON objects for structured data

**Examples:**
- `/cache set workflow.phase implementation` - Set current phase
- `/cache get workflow.state` - Get current workflow state
- `/cache list` - List all cached entries
- `/cache clear workflow.state` - Clear workflow state
- `/cache set config '{"timeout": 300, "retries": 3}'` - Store JSON config

## Guidelines

### When to Use
- **Workflow State Management**: Track current SDLC phase and progress
- **Architecture Caching**: Store and reuse project architecture understanding
- **Session Context**: Maintain context across multiple sessions
- **Configuration Storage**: Store SDLC configuration and settings
- **Progress Tracking**: Cache progress for long-running workflows
- **Data Persistence**: Store computed data for reuse

### Cache Storage

Cache data is stored in: `./.sdlc/cache/`

File structure:
```
.sdlc/
├── cache/
│   ├── workflow-state.json      # Current workflow state
│   ├── architecture.json        # Cached architecture data
│   ├── config.json              # SDLC configuration
│   └── [custom-keys].json       # Project-specific cache
└── meta/
    └── cache-metadata.json      # Cache metadata and timestamps
```

### JSON Storage Format

For complex data, use JSON format:

```json
{
  "key": "workflow.state",
  "value": {
    "phase": "implementation",
    "status": "in_progress",
    "startedAt": "2026-03-08T10:00:00Z",
    "completedSteps": ["planning", "design"],
    "currentStep": "implementation",
    "metadata": {
      "feature": "user-auth",
      "branch": "feature/user-auth"
    }
  },
  "createdAt": "2026-03-08T10:00:00Z",
  "updatedAt": "2026-03-08T10:30:00Z",
  "ttl": 86400
}
```

### Cache Metadata

Track cache freshness with metadata:

```json
{
  "entries": {
    "workflow.state": {
      "created": "2026-03-08T10:00:00Z",
      "updated": "2026-03-08T10:30:00Z",
      "accessed": "2026-03-08T11:00:00Z",
      "size": 1024,
      "stale": false
    }
  },
  "version": "1.0"
}
```

### Cache Structure

```markdown
# [Project/Module Name] Architecture

**Last Updated**: [YYYY-MM-DD]
**Version**: [semantic version if applicable]

---

## Overview

[Brief description of the project/module - what it does, who uses it, key goals]

---

## Technology Stack

| Layer | Technology | Version | Purpose |
|-------|-----------|---------|---------|
| Frontend | [React/Vue/etc] | [version] | [purpose] |
| Backend | [Go/Node/etc] | [version] | [purpose] |
| Database | [PostgreSQL/MongoDB/etc] | [version] | [purpose] |
| Cache | [Redis/etc] | [version] | [purpose] |
| Message Queue | [RabbitMQ/Kafka/etc] | [version] | [purpose] |

---

## Architecture Diagram(s)

[Include ASCII diagrams or describe key architectural patterns]

---

## Directory Structure

```
project-root/
├── src/
│   ├── frontend/          # Frontend application code
│   ├── backend/           # Backend application code
│   └── shared/            # Shared utilities/types
├── docs/
│   ├── spec/             # Specification documents
│   └── arch/             # Architecture documents
└── tests/
    ├── unit/             # Unit tests
    ├── integration/      # Integration tests
    └── e2e/              # End-to-end tests
```

---

## Key Components

### Frontend Components

| Component | File | Purpose | Key Props/State |
|-----------|------|---------|-----------------|
| [ComponentName] | [path] | [purpose] | [key props/state] |

### Backend Services/Modules

| Service/Module | File | Purpose | Key Methods/Endpoints |
|----------------|------|---------|----------------------|
| [ServiceName] | [path] | [purpose] | [key methods/endpoints] |

---

## Data Models

### [Model Name]
```typescript
// or Go struct, SQL schema, etc.
type [ModelName] struct {
    ID          string    `json:"id"`
    [Field1]    [Type]    `json:"[field1]"`
    [Field2]    [Type]    `json:"[field2]"`
}
```
**Purpose**: [what this model represents]
**Key Relationships**: [related models]

---

## API Endpoints

### [Resource Name]

| Method | Endpoint | Description | Request | Response |
|--------|----------|-------------|---------|----------|
| GET | `/api/v1/resource` | List items | - | `Item[]` |
| POST | `/api/v1/resource` | Create item | `CreateItemRequest` | `Item` |

---

## State Management

### Frontend State
- **Global State**: [what's managed globally]
- **Local State**: [what's managed locally]
- **Server State**: [how data is fetched/cached]

### Backend State
- **Session Management**: [how sessions are handled]
- **Caching Strategy**: [what's cached and where]
- **Database Connection**: [pooling, transactions]

---

## Key Patterns & Conventions

### Architectural Patterns
- [Pattern 1]: [description and where it's used]

### Code Conventions
- **Naming**: [naming conventions]
- **Error Handling**: [how errors are handled]
- **Logging**: [logging strategy]
- **Testing**: [testing patterns]

---

## Integration Points

### External Services
| Service | Purpose | Integration Method | Fallback Strategy |
|---------|---------|-------------------|-------------------|
| [Service 1] | [purpose] | [REST/GraphQL/SDK] | [fallback] |

### Internal APIs
| API | Consumer | Data Flow |
|-----|----------|-----------|
| [API Name] | [who consumes it] | [data flow description] |

---

## Security Considerations

- **Authentication**: [method - JWT, session, OAuth, etc.]
- **Authorization**: [RBAC, ABAC, middleware]
- **Data Protection**: [encryption at rest/transit]
- **Input Validation**: [validation strategy]
- **Rate Limiting**: [how rate limiting is implemented]

---

## Performance Considerations

- **Database Optimization**: [indexes, query optimization]
- **Caching Strategy**: [what's cached, TTL, invalidation]
- **Frontend Optimization**: [code splitting, lazy loading]
- **Monitoring**: [what's monitored - APM, metrics, logs]

---

## Known Technical Debt

| Issue | Impact | Proposed Solution | Priority |
|-------|--------|-------------------|----------|
| [debt 1] | [impact] | [solution] | [High/Medium/Low] |

---

## References

- **Related Specs**: [links to relevant spec docs]
- **External Documentation**: [links to external docs]
- **Design Decisions**: [links to ADRs or design discussions]
```

## Process

### Get Operation (`/cache get [key]`)

1. Check if cache directory exists
2. Look up key in cache files
3. Parse JSON if complex value
4. Return value with metadata (age, size)
5. Warn if cache is stale

**Error Handling:**
- Key not found: Return null or default value
- Invalid JSON: Return raw value with warning
- Cache directory missing: Create and return null

### Set Operation (`/cache set [key] [value]`)

1. Ensure cache directory exists
2. Parse value as JSON if possible
3. Create or update cache file
4. Update metadata (timestamp, size)
5. Return success confirmation

**Error Handling:**
- Invalid JSON: Store as string value
- Write permission error: Report and suggest fix
- Disk space: Check before write

### Clear Operation (`/cache clear [key?]`)

1. If key provided: delete specific cache file
2. If no key: confirm then clear all cache
3. Update metadata to reflect changes
4. Return summary of cleared items

**Error Handling:**
- Key not found: Inform and continue
- File lock: Retry or report
- Partial failure: Report what was cleared

### List Operation (`/cache list`)

1. Read all cache files
2. Extract metadata for each entry
3. Display in formatted table
4. Show key, size, age, staleness status

**Output Format:**
```
Cache Entries:
┌─────────────────┬──────────┬──────────┬────────┐
│ Key             │ Size     │ Age      │ Stale  │
├─────────────────┼──────────┼──────────┼────────┤
│ workflow.state  │ 1.2 KB   │ 2m ago   │ No     │
│ architecture    │ 45.6 KB  │ 1h ago   │ No     │
│ config          │ 0.8 KB   │ 1d ago   │ Yes    │
└─────────────────┴──────────┴──────────┴────────┘
```

### Invalidate Operation (`/cache invalidate [key]`)

1. Mark cache entry as stale in metadata
2. Optionally delete cache file
3. Update metadata timestamp
4. Return confirmation

## Cache Invalidation Strategies

### TTL (Time To Live)
- Set expiration time when storing
- Auto-invalidate after TTL expires
- Configurable per key type

### Manual Invalidation
- Explicit invalidate command
- Useful when data becomes stale
- Prevents using outdated cache

### Dependency Tracking
- Track dependencies between cache entries
- Invalidate dependent entries when parent changes
- Example: architecture cache invalidates when code changes

## Integration with Other Skills

### Used By
- **doc**: Cache architecture knowledge for context
- **git**: Store workflow state and branch info
- **phases**: Track phase completion status
- **workflows**: Maintain workflow execution state

### State Management Example

```json
{
  "key": "workflow.state",
  "value": {
    "currentPhase": "implementation",
    "phases": {
      "planning": {
        "status": "completed",
        "completedAt": "2026-03-08T09:00:00Z"
      },
      "design": {
        "status": "completed",
        "completedAt": "2026-03-08T10:00:00Z"
      },
      "implementation": {
        "status": "in_progress",
        "startedAt": "2026-03-08T11:00:00Z",
        "tasks": ["task1", "task2"]
      },
      "testing": {
        "status": "pending"
      },
      "deployment": {
        "status": "pending"
      }
    },
    "metadata": {
      "feature": "user-auth",
      "branch": "feature/user-auth",
      "assignee": "developer"
    }
  }
}
```

## Dependencies

- **doc**: Create architecture documentation from cached data
- **git**: Update branch info in workflow state
- **phases**: Update phase completion in workflow state

## Completion Criteria

- [ ] Cache directory structure created
- [ ] Value stored successfully with key
- [ ] JSON values properly parsed and formatted
- [ ] Metadata tracked for all entries
- [ ] Staleness detection working
- [ ] Integration with other skills functional
- [ ] Error handling comprehensive
- [ ] List operation displays all entries
- [ ] Clear operation works for single and all entries
- [ ] TTL support implemented
