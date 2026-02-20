---
description: "Validate that all success criteria for the current step are met"
agent: code-reviewer
tools: ['search', 'read', 'execute', 'web', 'todo']
---

# Validate Step Success Criteria

Check whether all success criteria for a specific step have been met.

## Input Parameters

Step number (REQUIRED): ${input:step-number:Step number to validate (e.g., "5-0", "5-1")}

## Workflow

### 1. Find the Exercise Issue

Use GitHub CLI to find the main exercise issue:
```bash
gh issue list --state open
```

The exercise issue will have **"Exercise:"** in the title.

### 2. Get Issue with All Comments

Retrieve the complete issue including step comments:
```bash
gh issue view <issue-number> --comments
```

### 3. Locate the Target Step

Search through the issue output to find:
```
# Step ${step-number}:
```

For example, if validating step "5-1", look for `# Step 5-1:`.

### 4. Extract Success Criteria

Within that step, find the **Success Criteria** section. It typically includes checkboxes like:

```
**Success Criteria:**
- [ ] All tests pass
- [ ] Feature X is implemented
- [ ] Code follows style guidelines
- [ ] No console.log statements remain
```

### 5. Validate Each Criterion

For each criterion, check the current workspace state:

**Tests passing**:
```bash
cd packages/backend && npm test
cd packages/frontend && npm test
```

**Code quality** (lint errors):
```bash
cd packages/backend && npm run lint
cd packages/frontend && npm run lint
```

**File existence/content**:
Use `read_file` and `grep_search` tools to verify implementations.

**Functionality**:
Review code to confirm features are properly implemented.

### 6. Report Validation Results

Provide a clear checklist showing:

```
✅ All backend tests passing (23 tests)
✅ All frontend tests passing (15 tests)
✅ No lint errors in backend
⚠️  3 lint warnings in frontend (no-console)
✅ Feature X implemented correctly
❌ Feature Y missing implementation

Overall: 4/6 criteria met
```

### 7. Provide Actionable Guidance

For incomplete criteria:

**If tests fail**:
- Show which tests are failing
- Suggest using `/tdd-developer` to fix test failures

**If lint errors exist**:
- Categorize the errors
- Suggest specific fixes
- Use code-reviewer workflow to address systematically

**If features are incomplete**:
- Identify what's missing
- Recommend next steps
- Point to relevant tests or requirements

## Validation Categories

### Code Quality Checks

- **Lint status**: No errors (warnings acceptable in some cases)
- **Test coverage**: All tests passing
- **Code smells**: No obvious anti-patterns
- **Best practices**: Following project conventions

### Functionality Checks

- **Feature completeness**: All activities implemented
- **Correctness**: Code does what requirements specify
- **Integration**: Components work together properly

### Documentation Checks

- **Comments**: Complex code explained
- **README**: Updated if needed
- **API docs**: Endpoints documented (if applicable)

## Commands Reference

**List issues**:
```bash
gh issue list --state open
```

**View issue with comments**:
```bash
gh issue view <issue-number> --comments
```

**Run tests**:
```bash
cd packages/backend && npm test
cd packages/frontend && npm test
```

**Check lint**:
```bash
cd packages/backend && npm run lint
cd packages/frontend && npm run lint
```

## Success Criteria Format

The issue step will typically have success criteria in one of these formats:

**Checkbox format**:
```
**Success Criteria:**
- [ ] Criterion 1
- [ ] Criterion 2
```

**List format**:
```
Success criteria:
1. Criterion 1
2. Criterion 2
```

**Paragraph format**:
```
Success: All tests pass, no lint errors, feature implemented.
```

Parse accordingly and validate each point.

## Output Format

Always provide:
1. **Summary**: "X of Y criteria met"
2. **Details**: Specific pass/fail for each criterion
3. **Next Steps**: What to do for incomplete items
4. **Confidence**: How certain you are about validation results

## Reference

This prompt inherits gh CLI knowledge from [.github/copilot-instructions.md](../copilot-instructions.md).

See the "Workflow Utilities" section for more GitHub CLI commands.
