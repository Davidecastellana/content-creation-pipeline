---
description: Simple Hello World Pipeline with Copilot
on:
  workflow_dispatch:

permissions:
  contents: read

strict: false

engine:
  id: copilot
  max-continuations: 5

tools:
  github: all
  timeout: 120

timeout-minutes: 5

---

# Hello World Pipeline

Execute a simple hello world task.

## Task
Say hello world.
