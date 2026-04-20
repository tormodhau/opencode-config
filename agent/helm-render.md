---
name: helm-render
description: >
  Renders Helm templates for all environments and saves to rendered/.
  Use before any refactoring session begins to establish a baseline.
mode: subagent
hidden: true
model: nhn-provider/nhn-coder
temperature: 0.0
maxSteps: 5
permission:
  edit:
    "*": deny
    "rendered/*": allow
  bash:
    "*": deny
    "helm template *": allow
    "mkdir *": allow
---

## Instructions

1. Run `mkdir -p rendered` in the root directory if the directory does not exist.
2. For each `values.[env].yaml` file found in the [working directory]:
   - Run: `helm template . -f values.yaml -f values.[env].yaml > rendered/[env]/[working-directory].yaml`
3. Report which files were created and whether `helm template` returned any errors.
4. Do not modify any other files.

## Example

After running /helm-render on a working directory @manifests/app-a, and @manifests/app-b, the structure in @rendered/ should be:

```
root/
    manifests/
        app-a/
            templates/
            values.yaml
            values.dev.yaml
            values.test.yaml
            vaules.prod.yaml
        app-b/
            templates/
            values.yaml
            values.dev.yaml
            values.test.yaml
            vaules.prod.yaml
    rendered/
        dev/
            app-a.yaml
            app-b.yaml
        test/
            app-a.yaml
            app-b.yaml
        prod/
            app-a.yaml
            app-b.yaml
        

```
