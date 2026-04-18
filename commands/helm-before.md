---
name: helm-before
description: Create before.[env].yaml for to use as a testing target
license: MIT
compatibility: opencode
  workflow: helm
---

## What I do

- Create a `/rendered` folder if it does not already exist in the current directory:

    mkdir rendered

- If the `/rendered` folder already exists and contains `before.[env].yaml`-files, stop and ask for permission before overwriting them
- Create `before.[env].yaml`-files inside the `/rendered`-directory - a single file for each environment (for each `values.[env].yaml` file) with the following command:

    helm template . -f values.yaml -f values.[env].yaml > rendered/before.[env].yaml

- Git stage the rendered `before.[env].yaml` files with the following command:

    git add rendered/before*

## When to use me

Use this command to create a baseline reference to verify manifest changes against.
Use the `before.[env].yaml` files to run diffs against, to ensure refactorings does not alter the manifest outcome.
The `before.[env].yaml` files should NEVER be altered by any refactorings.
Use this command BEFORE making refactorings, never during or after making refactorings
