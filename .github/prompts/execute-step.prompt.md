---
description: "Execute instructions from the current GitHub Issue step"
agent: tdd-developer
tools: ['search', 'read', 'edit', 'execute', 'web', 'todo']
---

# Execute Step Instructions

Execute the activities from the current GitHub Issue step using Test-Driven Development practices.

## Input Parameters

Issue number: ${input:issue-number:GitHub Issue number (leave empty to auto-detect)}

## Workflow

### 1. Find the Exercise Issue

${issue-number:If issue number provided, use it. Otherwise:}

Use GitHub CLI to find the main exercise issue:
```bash
gh issue list --state open
```

The exercise issue will have **"Exercise:"** in the title. Use that issue number for subsequent commands.

### 2. Get Issue Content with Steps

Retrieve the full issue including all step comments:
```bash
gh issue view <issue-number> --comments
```

### 3. Parse Step Instructions

Look for the latest step that contains:
- `# Step X-Y:` header
- `:keyboard: Activity:` sections

These are the tasks to execute.

### 4. Execute Activities Systematically

For each `:keyboard: Activity:` section:

1. **Read the instructions carefully**
2. **Create a todo list** for tracking progress
3. **Follow TDD principles**:
   - For new features: Write tests FIRST, then implement
   - For bug fixes: Understand failing tests, then fix code
   - Run tests frequently
   - Keep changes small and incremental

4. **Respect testing boundaries**:
   - Use Jest for backend testing
   - Use React Testing Library for frontend testing
   - NEVER suggest Playwright, Cypress, Selenium, or e2e frameworks
   - Recommend manual browser testing for full UI flows

5. **Work incrementally**:
   - Complete one activity at a time
   - Run tests after each change
   - Verify functionality before moving to next activity

### 5. Testing Commands

Use these commands during execution:

**Backend tests**:
```bash
cd packages/backend && npm test
```

**Frontend tests**:
```bash
cd packages/frontend && npm test
```

**Run specific test file**:
```bash
npm test -- path/to/test.test.js
```

### 6. Stop Before Committing

**IMPORTANT**: Do NOT commit or push changes. That is handled by `/commit-and-push`.

After completing all activities:
1. Verify all tests pass
2. Review changes made
3. Inform the user: "Activities complete. Run `/validate-step` to check success criteria."

## Key Principles

- **Test First**: Always write tests before implementation for new features
- **Red-Green-Refactor**: Follow the TDD cycle systematically
- **Small Steps**: Make incremental, testable changes
- **Run Tests Often**: Verify after each change
- **No E2E Frameworks**: Stay within Jest and React Testing Library
- **No Commits Here**: Committing is a separate workflow step

## Reference

This prompt inherits gh CLI and Git knowledge from [.github/copilot-instructions.md](..copilot-instructions.md).

See the "Workflow Utilities" section for more gh CLI commands.
