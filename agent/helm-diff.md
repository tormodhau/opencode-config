---
name: helm-diff
description: >
  Compares current helm template output against the baseline in rendered/.
  Reports whether any non-cosmetic (semantic) differences were found.
mode: subagent
hidden: true
model: qwen/qwen3-coder-next-fp8
temperature: 0.0
maxSteps: 5
permission:
  edit:
    "*": deny
    "rendered/diff-*": allow
  bash:
    "*": deny
    "helm template *": allow
    "difft *": allow
    "diff *": allow
---

## Instructions

1. Find all `rendered/[env].yaml` files.
2. If none found, stop and report.
3. For each env, run:
   - `helm template . -f values.yaml -f values.[env].yaml | difft rendered/[env].yaml -`
   - If `difft` is unavailable: `helm template . -f values.yaml -f values.[env].yaml | diff rendered/[env].yaml -`
4. Save each diff to `rendered/diff-[env].txt`.
5. Classify each diff: cosmetic only (whitespace, comments, ordering) vs semantic (value changes, added/removed resources, spec changes).
6. Return a summary table:

| Env | Diff file | Semantic changes? | Details |
|-----|-----------|-------------------|---------|

If semantic changes are found, show the relevant diff lines.
