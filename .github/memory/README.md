# Working Memory System

## Purpose

This memory system tracks patterns, decisions, and lessons learned during development to improve AI-assisted workflows. It provides a structured way to capture and reference knowledge across development sessions.

## Two Types of Memory

### Persistent Memory
**Location**: `.github/copilot-instructions.md`

Contains foundational principles and workflows that define how development work is approached in this project. These are stable, rarely-changed rules that apply universally across all sessions.

**Examples:**
- Development principles (TDD, incremental changes)
- Testing scope and approach
- Workflow patterns (TDD, code quality, integration)
- Agent usage guidelines
- Git workflow conventions

### Working Memory
**Location**: `.github/memory/`

Contains discoveries, patterns, and context accumulated during development. This memory grows and evolves as the project matures, capturing specific patterns, decisions, and lessons learned.

## Directory Structure

### `session-notes.md` (Committed to Git)
**Purpose**: Historical record of completed development sessions

Contains dated summaries of what was accomplished in each session. This provides context for future work and helps understand the evolution of the codebase.

**When to use:**
- At the end of a development session
- When wrapping up a major feature or bug fix
- To document significant decisions or discoveries

**What to include:**
- Session name and date
- What was accomplished
- Key findings and decisions
- Outcomes (tests passing, features completed, issues resolved)

This file is a **historical record** and should be committed to git.

---

### `patterns-discovered.md` (Committed to Git)
**Purpose**: Accumulated code patterns and solutions

Documents recurring patterns, solutions to common problems, and architectural decisions discovered during development. These patterns inform future development and help maintain consistency.

**When to use:**
- When you discover a pattern that should be followed consistently
- After solving a tricky problem that might recur
- When you identify best practices specific to this codebase

**What to include:**
- Pattern name and context
- Problem description
- Solution approach
- Code example
- Related files

This file is an **accumulated reference** and should be committed to git.

---

### `scratch/working-notes.md` (NOT Committed - Active Session Only)
**Purpose**: Active development notes for the current session

A scratchpad for capturing thoughts, approaches, findings, and decisions during active development. This is ephemeral memory that gets summarized into `session-notes.md` at the end of each session.

**When to use:**
- Throughout active development
- When debugging issues
- When making decisions that need to be remembered during the session
- When tracking blockers or next steps

**What to include:**
- Current task description
- Approach being taken
- Key findings as they emerge
- Decisions made during the session
- Blockers encountered
- Next steps to take
- General notes and observations

This file is **not committed to git** (see `scratch/.gitignore`) and serves as active working memory.

---

## Workflow Integration

### During TDD Workflow
**Write or fix tests → Run → Fail → Implement → Pass → Refactor**

1. **Before starting**: Review `patterns-discovered.md` for relevant patterns
2. **During work**: Track decisions in `scratch/working-notes.md`
3. **After refactor**: Document new patterns in `patterns-discovered.md`
4. **End of session**: Summarize findings into `session-notes.md`

**Example:**
```
Working on: Add validation to TODO creation endpoint
Pattern found: Service layer should validate input before calling repository
Decision: Use express-validator middleware for consistency
→ Document in patterns-discovered.md
→ Note in scratch/working-notes.md
→ Summarize in session-notes.md at end
```

### During Code Quality Workflow
**Run lint → Categorize issues → Fix systematically → Re-validate**

1. **Before fixing**: Check `patterns-discovered.md` for coding standards
2. **During fixes**: Note any patterns in `scratch/working-notes.md`
3. **After fixes**: Document recurring lint issues and solutions in `patterns-discovered.md`
4. **End of session**: Add summary to `session-notes.md`

**Example:**
```
Fixing: ESLint errors across backend
Finding: Consistent pattern of missing semicolons in async functions
Decision: Configure editor to auto-format on save
→ Document in patterns-discovered.md
→ Note in scratch/working-notes.md
→ Summarize in session-notes.md at end
```

### During Debugging Workflow
**Identify issue → Debug → Test → Fix → Verify**

1. **During debugging**: Capture findings in `scratch/working-notes.md`
2. **After fix**: Document root cause and solution in `patterns-discovered.md`
3. **End of session**: Add to `session-notes.md`

**Example:**
```
Bug: Tests failing due to undefined service methods
Root cause: Service not initialized in test setup
Solution: Call initializeService() in beforeAll hook
→ Document in patterns-discovered.md
→ Track in scratch/working-notes.md
→ Summarize in session-notes.md at end
```

---

## How AI Reads and Applies Memory

### When Starting a Task
1. **Reads persistent memory** (`.github/copilot-instructions.md`) for foundational principles
2. **Reads patterns-discovered.md** for known patterns relevant to the task
3. **Reads session-notes.md** for recent context and decisions
4. **References scratch/working-notes.md** if in active session

### During Development
1. **Suggests solutions** based on documented patterns
2. **Maintains consistency** with previous decisions
3. **Avoids repeating** known issues or anti-patterns
4. **Reminds** of relevant findings when applicable

### When Making Suggestions
1. **Cites patterns** from `patterns-discovered.md`
2. **References previous decisions** from `session-notes.md`
3. **Maintains context** from `scratch/working-notes.md`
4. **Proposes updates** to memory when new patterns emerge

**Example:**
```
User: "How should I initialize the TODO service?"
AI: Based on patterns-discovered.md, services in this project should be 
initialized with empty arrays rather than null values. See the 
"Service Initialization Pattern" for the standard approach.
```

---

## Session Workflow Summary

### At Start of Session
1. Review `session-notes.md` for recent context
2. Review `patterns-discovered.md` for relevant patterns
3. Create/update `scratch/working-notes.md` with current task

### During Session
1. Capture findings in `scratch/working-notes.md`
2. Reference patterns from `patterns-discovered.md`
3. Add new patterns to `patterns-discovered.md` as discovered

### At End of Session
1. Review `scratch/working-notes.md`
2. Extract key findings and decisions
3. Add session summary to `session-notes.md`
4. Update `patterns-discovered.md` with any new patterns
5. Clear or archive `scratch/working-notes.md` for next session

---

## Best Practices

### Do
- ✅ Update `scratch/working-notes.md` frequently during active development
- ✅ Summarize completed sessions in `session-notes.md`
- ✅ Document patterns when they become clear
- ✅ Reference memory files when making decisions
- ✅ Keep patterns concise and actionable

### Don't
- ❌ Commit `scratch/working-notes.md` to git
- ❌ Let patterns-discovered.md become a dumping ground
- ❌ Document every tiny decision
- ❌ Forget to review memory at session start
- ❌ Skip session summaries

---

## Benefits

1. **Continuity**: Resume work with full context from previous sessions
2. **Consistency**: Apply patterns uniformly across the codebase
3. **Learning**: Build institutional knowledge in the codebase
4. **Efficiency**: Avoid repeating past mistakes or rediscovering solutions
5. **AI Context**: Provide AI with rich, project-specific context for better suggestions

---

## Getting Started

1. **For your first session:**
   - Read this README
   - Review the example in `session-notes.md`
   - Review the example in `patterns-discovered.md`
   - Create your first entry in `scratch/working-notes.md`

2. **For ongoing sessions:**
   - Review `session-notes.md` for recent work
   - Check `patterns-discovered.md` for relevant patterns
   - Update `scratch/working-notes.md` as you work
   - Summarize to `session-notes.md` when done

3. **For AI assistance:**
   - Reference memory files in prompts: "Check patterns-discovered.md for the service pattern"
   - Ask AI to update memory: "Document this pattern in patterns-discovered.md"
   - Request summaries: "Summarize today's work for session-notes.md"
