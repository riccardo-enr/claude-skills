---
name: simplify
description: Review recently changed code for unnecessary complexity, duplication, and inefficiency, then fix the issues. Use when the user asks to simplify, clean up, or improve changed code.
disable-model-invocation: true
allowed-tools: Bash(git diff*), Bash(git status*), Read, Edit, Glob, Grep
---

Review and simplify the code changed in the current working tree.

## Steps

1. Run `git diff HEAD` to see what has changed. If nothing, check `git status` for untracked files.
2. Read the changed files in full to understand the broader context.
3. For each changed area, look for:
   - **Duplication**: extract shared logic into a helper only if it's used 3+ times and the abstraction is clearer than repetition
   - **Dead code**: unused variables, unreachable branches, commented-out blocks
   - **Unnecessary complexity**: overly nested conditions, redundant intermediate variables, manual loops replaceable by standard library calls
   - **Inefficiency**: repeated expensive operations inside loops, allocations that could be avoided
4. Apply only the improvements that are clearly better — do not refactor for its own sake. Three similar lines are often better than a premature abstraction.
5. Do not add comments, docstrings, or type annotations to code you didn't touch.
6. Report what you changed and why.

$ARGUMENTS
