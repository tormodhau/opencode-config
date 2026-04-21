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
    "*": ask
    "helm template *": allow
    "helm lint *": allow
    "difft *": allow
    "diff *": allow
    "git diff *": allow
    "git show *": allow
    "git log *": allow
    "git add rendered/*": allow
    "mkdir rendered": allow
    "cat *": allow
    "grep *": allow
    "head *": allow
    "ls *": allow
---

## Instructions

1. Run `mkdir -p rendered` in the root directory, and `rendered/dev`, `rendered/test` and `rendered/prod` if theses directories do not exist.
2. For each `values.[env].yaml` file found in the $1 directory:
   - Run: `helm template $1 -f values.yaml -f values.[env].yaml > rendered/[env]/[app].yaml`
3. Report which files were created and whether `helm template` returned any errors.
4. Do not modify any other files.

## Example

Running "/helm-render @manifests/apps/app-a" should generate the following file structure:

```
root/
    .git
    manifests/
        apps/
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
