# Patterns Discovered

This file documents recurring code patterns, architectural decisions, and solutions discovered during development. Reference these patterns when implementing similar functionality.

---

## Pattern Template

```markdown
### Pattern Name
**Context**: [When/where this pattern applies]
**Problem**: [What problem does this solve?]
**Solution**: [How to implement it]
**Example**: [Code example]
**Related Files**: [Files that use this pattern]
```

---

## Example Pattern

### Service Initialization Pattern
**Context**: When creating service layer classes that manage collections of data

**Problem**: Services need consistent initialization to avoid null/undefined errors and to ensure predictable behavior in tests and production code.

**Solution**: Initialize services with empty arrays rather than null values. This eliminates the need for null checks throughout the codebase and provides a consistent starting state.

**Example**:
```javascript
// ✅ Good: Initialize with empty array
class TodoService {
  constructor() {
    this.todos = [];  // Always initialized
  }

  getAll() {
    return this.todos;  // Always returns array, never null
  }

  add(todo) {
    this.todos.push(todo);  // No null check required
  }
}

// ❌ Bad: Initialize with null
class TodoService {
  constructor() {
    this.todos = null;  // Requires null checks
  }

  getAll() {
    return this.todos || [];  // Null check required
  }

  add(todo) {
    if (!this.todos) {  // Null check required
      this.todos = [];
    }
    this.todos.push(todo);
  }
}
```

**Related Files**:
- `packages/backend/src/services/todoService.js`
- `packages/backend/__tests__/services/todoService.test.js`

---

## Discovered Patterns

_Add your patterns below._
