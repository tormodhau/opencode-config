---
name: helm-plan
description: >
  Analyse the current Helm chart and produce a structured PLAN.md refactoring table.
  Uses the reasoning model. No files are modified (read-only analysis).
agent: helm-plan
subtask: false
---

Read all files in the current directory:

- values.yaml
- values.*.yaml
- templates/
- _helpers.tpl (if present)
- Chart.yaml

See the helm-conventions skill for the underlying philosophy and conventions.

Write PLAN.md with a numbered TODO table (columns: #, Area, What to change, Risk, Effort).
Stop after writing PLAN.md. Do not implement any changes.
