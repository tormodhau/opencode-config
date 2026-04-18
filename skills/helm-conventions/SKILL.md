---
name: helm-conventions
description: >
  Kubernetes and Helm refactoring conventions: when to use values files,
  when to inline, helper template rules, environment split patterns.
  Load this when planning or executing Helm refactors.
---

## When a value belongs in values.yaml vs values.[env].yaml

- `values.yaml`: default values shared across ALL environments (image repository, port, annotations)
- `values.[env].yaml`: ONLY values that are different in that environment (replicas, resource limits, ingress host, env-specific secrets)
- A value that is the same in all three env files should be moved to `values.yaml` and removed from all env files

## When _helpers.tpl is justified

- Justified: a label block, selector, or name template used in 4+ places
- Not justified: a single-use helper, a helper that wraps a single value, a helper used only in one template

## Semantic vs cosmetic diff changes

Cosmetic (safe to ignore):

- Whitespace and blank lines
- YAML comment changes
- Key ordering changes (same values)
- Reformatting of equivalent YAML

Semantic (must ask user):

- Any change to `spec:` fields
- Any change to resource requests/limits
- Any change to image tag or repository
- Added or removed Kubernetes resources
- Changes to environment variables
- Changes to securityContext, serviceAccount, RBAC

## Chart sharing anti-patterns to remove

- `alias:` dependencies used only to share templates between internal charts
- `library:` charts with no external consumers
- `requirements.yaml` / `dependencies:` entries that are only used by one chart in the monorepo
