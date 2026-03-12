name: Code Wizard
description: Magically transforms code into efficient, bug-free solutions
tags: code, magic, transform, efficiency
version: 1.0.0
author: Kilo
dependencies:
  - Node.js >= 14.0.0 (for JavaScript/TypeScript projects)
  - Python >= 3.8 (for Python projects)
  - Git >= 2.25.0
  - ESLint (for JavaScript/TypeScript linting)
  - Ruff (for Python linting)
environment_variables:
  - CODE_WIZARD_API_KEY: Optional API key for advanced transformations (contact support for access)
  - CODE_WIZARD_LOG_LEVEL: Set to 'debug' for verbose logging, 'info' for standard (default)
---

# Code Wizard Skill

## Purpose

The Code Wizard skill magically transforms code into efficient, bug-free solutions by applying advanced refactoring, optimization, and bug-fixing techniques. It understands code patterns across multiple languages and frameworks, ensuring maintainable, performant, and secure codebases.

### Real Use Cases
- **Legacy Code Refactoring**: Convert spaghetti code in a 10-year-old JavaScript function into modern async/await patterns with proper error handling.
- **Performance Optimization**: Transform a Python data processing script that takes 30 minutes to run into a vectorized NumPy implementation that completes in under 5 seconds.
- **Bug Fixing**: Automatically detect and fix null pointer exceptions in Java code by adding null checks and using Optional wrappers.
- **Feature Implementation**: Generate CRUD operations for a new entity in a Django REST framework API, complete with serializers, views, and URL configurations.
- **Security Hardening**: Scan and patch SQL injection vulnerabilities in PHP code by implementing prepared statements and input validation.

## Scope

The Code Wizard operates on specific commands that target common coding challenges. It works with files in the current workspace and supports incremental changes with built-in verification.

### Specific Commands
- `/code-wizard refactor <file_path> [--language <lang>] [--style <style>]`: Refactor code for readability and maintainability
- `/code-wizard optimize <file_path> [--metric <perf|memory|cpu>]`: Optimize code for specific performance metrics
- `/code-wizard fix-bug <file_path> <bug_description>`: Identify and fix bugs based on description
- `/code-wizard implement <feature_description> [--language <lang>] [--framework <fw>]`: Generate new feature code
- `/code-wizard audit <file_path> [--security|--performance|--best-practices]`: Audit code for issues
- `/code-wizard migrate <file_path> --from <old_version> --to <new_version>`: Migrate code between versions

### Supported Languages
- JavaScript/TypeScript (ES6+, React, Node.js)
- Python (3.8+, Django, Flask)
- Java (8+, Spring)
- C# (.NET Core 3.1+)
- Go (1.16+)
- PHP (7.4+, Laravel)

## Detailed Work Process

The Code Wizard follows a systematic 7-step process to ensure magical transformations:

1. **Code Analysis**: Parse the target file(s) using AST (Abstract Syntax Tree) to understand structure, dependencies, and patterns.
2. **Issue Detection**: Run static analysis tools (ESLint for JS, Ruff for Python) to identify bugs, inefficiencies, and violations.
3. **Transformation Planning**: Generate a detailed plan of changes, including before/after diffs and impact assessment.
4. **Safe Application**: Apply changes incrementally with git staging, allowing easy rollback.
5. **Automated Testing**: Run relevant test suites (Jest for JS, pytest for Python) to verify functionality.
6. **Linting and Formatting**: Apply consistent code style using Prettier or Black.
7. **Final Verification**: Perform integration tests and security scans before marking complete.

### Environment Setup
Before using Code Wizard, ensure:
- Git repository is initialized in the workspace
- Dependencies are installed (run `npm install` or `pip install -r requirements.txt`)
- Test framework is configured (e.g., `jest.config.js` or `pytest.ini`)

## Golden Rules

1. **Always Backup First**: Code Wizard creates automatic git commits before changes. Never run on uncommitted work.
2. **Incremental Changes**: Large refactors are broken into small, testable commits to minimize risk.
3. **Type Safety**: For typed languages, ensure transformations preserve or improve type annotations.
4. **Security First**: Any code generation includes input validation and common security patterns.
5. **Performance Verification**: All optimizations include before/after benchmarks using built-in profiling.
6. **Framework Compatibility**: Transformations respect framework conventions (e.g., React hooks, Django models).
7. **Documentation Updates**: Code Wizard updates comments and docstrings to reflect changes.

## Examples

### Example 1: Refactoring Legacy JavaScript
**User Input:**
```
/code-wizard refactor src/utils.js --language javascript --style modern
```

**Current Code:**
```javascript
function getUserData(userId) {
  return fetch('/api/users/' + userId)
    .then(response => response.json())
    .catch(error => console.error(error));
}
```

**Code Wizard Output:**
```javascript
/**
 * Fetches user data from the API
 * @param {string} userId - The user identifier
 * @returns {Promise<Object>} User data object
 */
async function getUserData(userId) {
  try {
    const response = await fetch(`/api/users/${userId}`);
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    return await response.json();
  } catch (error) {
    console.error('Failed to fetch user data:', error);
    throw error;
  }
}
```

**Verification Steps:**
- Run `npm test` to ensure existing tests pass
- Check ESLint: `npx eslint src/utils.js`
- Performance: No significant change expected for this refactor

### Example 2: Optimizing Python Performance
**User Input:**
```
/code-wizard optimize data_processor.py --metric perf
```

**Before Optimization:**
```python
def process_large_dataset(data):
    results = []
    for item in data:
        if item['value'] > 100:
            results.append(item['value'] * 2)
    return results
```

**After Optimization:**
```python
import numpy as np

def process_large_dataset(data):
    """
    Process large dataset using vectorized operations for performance
    @param data: List of dicts with 'value' key
    @return: List of processed values
    """
    values = np.array([item['value'] for item in data])
    return (values[values > 100] * 2).tolist()
```

**Performance Impact:**
- Before: 30.2 seconds for 1M items
- After: 0.8 seconds for 1M items
- Verification: `python -m pytest tests/test_data_processor.py -v`

### Example 3: Bug Fixing
**User Input:**
```
/code-wizard fix-bug api/routes.py "division by zero when quantity is 0"
```

**Buggy Code:**
```python
def calculate_total(price, quantity):
    return price * quantity / quantity  # Bug: divides by quantity
```

**Fixed Code:**
```python
def calculate_total(price: float, quantity: int) -> float:
    """
    Calculate total price for given quantity
    @param price: Unit price
    @param quantity: Number of units
    @return: Total price
    @raises ValueError: If quantity is zero or negative
    """
    if quantity <= 0:
        raise ValueError("Quantity must be positive")
    return price * quantity
```

## Rollback Commands

### Immediate Rollback
- `git reset --hard HEAD~1`: Revert the last commit made by Code Wizard
- `git checkout -- <file_path>`: Discard changes to a specific file

### Selective Rollback
- `git revert <commit_hash>`: Create a new commit that undoes specific changes
- `git reset --soft HEAD~1 && git reset HEAD <file_path>`: Unstage changes while keeping them in working directory

### Full Project Reset
- `git reset --hard origin/main`: Reset to remote main branch (use with caution)
- `git clean -fd`: Remove untracked files and directories

### Verification After Rollback
- Run tests: `npm test` or `python -m pytest`
- Check syntax: `node --check <file>` or `python -m py_compile <file>`
- Lint: `npx eslint .` or `ruff check .`

## Dependencies and Requirements

- **Runtime**: Node.js 14+ or Python 3.8+
- **Tools**: Git, ESLint/Ruff, Prettier/Black
- **Frameworks**: Supports major frameworks with specific optimizations
- **Storage**: Requires ~100MB free space for temporary files

## Verification Steps

1. **Pre-Transformation**: `git status && npm run lint && npm test`
2. **Post-Transformation**: `git diff --staged && npm run lint && npm test`
3. **Performance**: Use `time` command or built-in profiling for benchmarks
4. **Security**: Run `npm audit` or `safety check` for vulnerabilities

## Troubleshooting Common Issues

### Issue: Code Wizard fails to parse file
**Cause**: Unsupported syntax or malformed code
**Solution**: Run `node --check <file>` or `python -c "import ast; ast.parse(open('<file>').read())"` to validate syntax first

### Issue: Transformations break tests
**Cause**: Logic changes not accounted for in tests
**Solution**: Review git diff, update tests manually, then re-run `/code-wizard implement "update tests for <feature>"`

### Issue: Performance optimization doesn't improve speed
**Cause**: Bottleneck elsewhere (I/O, network)
**Solution**: Use profiling tools: `python -m cProfile <script>` or Chrome DevTools for JS

### Issue: Rollback fails
**Cause**: Conflicting changes or merge conflicts
**Solution**: `git status`, resolve conflicts manually, then `git reset --hard HEAD~1`

### Issue: Environment variables not recognized
**Cause**: Not exported in shell
**Solution**: `export CODE_WIZARD_LOG_LEVEL=debug` before running commands

For support, contact the OpenClaw development team or check logs in `~/.openclaw/logs/code-wizard.log`.