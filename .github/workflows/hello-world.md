---
description: Simple Hello World Pipeline
on:
  workflow_dispatch:

permissions:
  contents: read

strict: false

network:
  allowed:
    - defaults
    - api.minimax.io

engine:
  id: claude
  max-turns: 5

tools:
  github: all
  timeout: 120

timeout-minutes: 5

env:
  ANTHROPIC_BASE_URL: "https://api.minimax.io/anthropic"
  ANTHROPIC_AUTH_TOKEN: "${{ secrets.ANTHROPIC_API_KEY }}"
  ANTHROPIC_MODEL: "MiniMax-M2.7"
  CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC: "1"
---

# Hello World Pipeline

Execute a simple hello world task.

## Task
Say hello world and confirm the MiniMax API connection works.
