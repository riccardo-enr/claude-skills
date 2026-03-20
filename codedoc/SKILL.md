---
name: codedoc
description: Explain code by adding or updating codedoc.nvim-compatible documentation blocks throughout files. Inserts prose, math, and design rationale in block comments (C-style) or triple-quoted docstrings (Python) at the module, class, and function level. Use when the user asks to explain, document, or annotate code in codedoc format.
disable-model-invocation: true
allowed-tools: Read, Edit, Glob, Grep
---

Add or update documentation in the specified files using codedoc.nvim-compatible format.

## What is codedoc.nvim?

[codedoc.nvim](https://github.com/riccardo/codedoc.nvim) is a Neovim plugin that renders Markdown documentation from code comments side-by-side with the source. Documentation lives entirely in comments and has no effect on the build.

## Format Rules

### C-style languages — C, C++, CUDA, JS, TS, Go, Rust, Java, …

Use `/* ... */` block comments. Single-line `//` comments are **not** rendered by codedoc — always use block comments for documentation prose.

```cpp
/*
# Module Title

Brief description of what this module does and why it exists.

## Key Concepts

Explain the core idea. Use math where helpful:

$$\mathbf{x}_{k+1} = A\mathbf{x}_k + B\mathbf{u}_k$$

## Algorithm

1. Step one — what and why.
2. Step two — what and why.
*/

void my_function(int x) {
    /* Explain what this function computes and why the approach was chosen. */
}
```

### Python

Use triple-quoted strings (`"""` or `'''`) at **module**, **class**, and **function** level. The opening `"""` must be on its own line.

```python
"""
# Module Title

Description of what this module does.

## Design Rationale

Why this approach over alternatives.

$$L(\theta) = \mathbb{E}\left[\sum_t r_t\right]$$
"""

class MyClass:
    """
    ## MyClass

    What this class models and its invariants.
    """

    def my_method(self, x):
        """
        Computes `result` from `x` using the recurrence:

        $$r_n = r_{n-1} + \alpha \cdot x$$
        """
```

### Markdown

The whole file is documentation — no special syntax needed. Ensure headings, lists, and math are well-structured.

## Markdown Content Guidelines

Use rich Markdown inside all documentation blocks:

- `#` / `##` / `###` headings to structure sections.
- `**bold**` for emphasis, `` `backtick` `` for code references.
- Bullet `-` and numbered `1.` lists.
- Fenced code blocks (` ```cpp `, ` ```bash `, …) for examples.
- Inline math `$...$` and display math `$$...$$` (KaTeX).
- Tables for parameter or return-value documentation.

## Documentation Depth

For each file/module, cover at minimum:

1. **Purpose** — what problem this file solves and why it exists.
2. **Key abstractions** — main types, classes, or functions and what they represent.
3. **Algorithm / design** — how it works at a high level; include math where the logic is non-trivial.
4. **Interfaces** — public API, important parameters, return values, side effects.
5. **Rationale** — why this approach was chosen over obvious alternatives.

For each non-trivial function or class, add a doc block that explains:

- What it computes or models.
- Any preconditions or invariants.
- Non-obvious implementation choices.

## Steps

1. Read all target files fully to understand purpose, structure, and algorithm.
2. Identify all module-level, class-level, and function-level documentation opportunities.
3. Write documentation blocks using the correct format for the language (see above).
4. Ensure documentation flows as readable prose — not just a list of parameter names.
5. Add math (KaTeX) wherever the logic involves formulas, recurrences, or optimisation objectives.
6. Do **not** modify any code logic — only add or update documentation comments.
7. Do **not** add inline `//` or `#` comments for prose — only block comments / docstrings.
8. Report a summary of what was documented and any non-obvious design decisions surfaced.

$ARGUMENTS
