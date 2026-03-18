---
name: create-issue
description: Create a GitHub issue using the gh CLI. Use when the user wants to open, file, or report an issue on the repository.
argument-hint: "<title>"
---

Create a GitHub issue. The issue title or topic is: $ARGUMENTS

## Steps

1. If the user didn't provide a title, ask for one
2. Ask the user for a description if not already given (or infer from context)
3. Ask which labels apply, if any (check available labels with `gh label list`)
4. Create the issue with:

```
gh issue create --title "<title>" --body "<body>" [--label "<label>"] [--assignee "@me"]
```

5. Report back the issue URL returned by the CLI

## Guidelines

- Use a concise, descriptive title (imperative mood preferred, e.g. "Fix crash on startup")
- Body should include: context, expected behavior, actual behavior, and reproduction steps if it's a bug
- For features: motivation and proposed solution
- Use `--web` flag if the user prefers to finish editing in the browser
- Do NOT open the browser unless the user asks for it
