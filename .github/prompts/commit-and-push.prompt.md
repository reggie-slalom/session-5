---
description: "Analyze changes, generate commit message, and push to feature branch"
tools: ['read', 'execute', 'todo']
---

# Commit and Push Changes

Analyze workspace changes, generate a conventional commit message, and push to a feature branch.

## Input Parameters

Branch name (REQUIRED): ${input:branch-name:Feature branch name (e.g., feature/add-todo-crud)}

## Workflow

### 1. Validate Branch Name

Ensure the branch name follows the pattern: `feature/<descriptive-name>`

If the user didn't provide a branch name, STOP and ask for it.

### 2. Analyze Changes

Review what has changed in the workspace:
```bash
git status
git diff
```

Understand:
- Which files were modified
- What functionality was added/changed
- Whether this is a feature, fix, or other change type

### 3. Generate Commit Message

Use **conventional commit format**:

```
<type>: <brief description>

<optional body with more details>
```

**Common types**:
- `feat:` - New feature
- `fix:` - Bug fix
- `test:` - Adding or updating tests
- `refactor:` - Code refactoring without behavior change
- `chore:` - Build, tooling, dependencies
- `docs:` - Documentation changes
- `style:` - Code formatting (not style sheets)

**Example**:
```
feat: add CRUD operations for todo items

- Implement POST /todos endpoint
- Add tests for todo creation
- Update frontend to handle new todos
```

### 4. Create or Switch to Feature Branch

Check if the branch exists:
```bash
git branch --list ${branch-name}
```

If it doesn't exist, create it:
```bash
git checkout -b ${branch-name}
```

If it exists, switch to it:
```bash
git checkout ${branch-name}
```

**CRITICAL**: NEVER commit to `main` or any other branch. ONLY use the user-provided branch name.

### 5. Stage All Changes

```bash
git add .
```

Verify what will be committed:
```bash
git status
```

### 6. Commit with Generated Message

```bash
git commit -m "<your generated commit message>"
```

For multi-line messages, use:
```bash
git commit -m "<title>" -m "<body paragraph 1>" -m "<body paragraph 2>"
```

### 7. Push to Remote

```bash
git push origin ${branch-name}
```

If this is the first push of a new branch:
```bash
git push -u origin ${branch-name}
```

### 8. Confirm Success

Report to the user:
- Branch name used
- Commit message generated
- Number of files changed
- Push status (success/failure)

## Safety Checks

✅ Branch name follows `feature/<name>` pattern
✅ Changes staged before committing
✅ Commit message follows conventional format
✅ Pushing to feature branch, NOT main
✅ All files included in commit

❌ NEVER commit directly to `main`
❌ NEVER force push unless explicitly requested
❌ NEVER commit without analyzing changes first

## Git Workflow Best Practices

- Use descriptive branch names
- Write clear, concise commit messages
- Commit related changes together
- Push regularly to backup work
- Keep commits focused (single purpose)

## Reference

This prompt inherits Git workflow knowledge from [.github/copilot-instructions.md](../copilot-instructions.md).

See the "Git Workflow" section for conventional commit standards.
