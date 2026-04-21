---
name: helm-conventions
description: >
  Kubernetes and Helm refactoring conventions: when to use values files,
  when to inline, helper template rules, environment split patterns.
  Load this when planning or executing Helm refactors.
---

## Code guidelines

1. values.[env].yaml should contain ONLY values that differ between environments
2. values.yaml should be empty
3. _helpers.tpl functions are only justified when they remove >3 instances of duplication
4. Remove all Helm code that exists only for chart sharing
5. templates should not use static default values

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
