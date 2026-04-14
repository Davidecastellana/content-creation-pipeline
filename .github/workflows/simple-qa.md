---
description: |
  Simple Q&A workflow. Run once to ask a question.
  When user comments with answer, workflow auto-runs again and responds.
on:
  workflow_dispatch:
  issue_comment:
    types: [created]

permissions:
  contents: read
  issues: read
  pull-requests: read

strict: false

safe-outputs:
  create-issue:
    labels: [automated, qa]
  add-comment:
    max: 5

network:
  allowed:
    - defaults
    - api.minimax.io

engine:
  id: claude
  api-target: api.minimax.io
  max-turns: 10

tools:
  github: all
  timeout: 120

timeout-minutes: 5

env:
  ANTHROPIC_API_KEY: "${{ secrets.ANTHROPIC_API_KEY }}"
  ANTHROPIC_BASE_URL: "https://api.minimax.io/anthropic"
  ANTHROPIC_API_TARGET: "api.minimax.io"
  ANTHROPIC_API_BASE_PATH: "/anthropic"
  ANTHROPIC_MODEL: "MiniMax-M2.7"
  CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC: "1"
---

# Simple Q&A Workflow

You are a simple Q&A bot.

## If triggered by workflow_dispatch:
Create Issue #100 with:
- Title: "Quick Question from Bot"
- Body: "What is your favorite color? Please comment with your answer."

## If triggered by issue_comment:
1. Check if the comment is on Issue #100
2. If YES: Read the comment, then add a reply to Issue #100 saying "Your favorite color is: [the color from the comment]"
3. If NO or not on Issue #100: Do nothing, exit silently