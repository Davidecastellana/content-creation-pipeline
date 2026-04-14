---
description: |
  FAAW Pipeline Orchestrator - Sequential Stage Execution
  Reads from: content-creation-pipeline/CLAUDE.md for pipeline config
  Executes stages in order, passing data via files
on:
  workflow_dispatch:
    inputs:
      mode:
        description: "Execution mode (auto/hybrid)"
        required: true
        default: "auto"
      start-stage:
        description: "Stage to start from (001/002/003/004)"
        required: false
        default: "001"
  schedule:
    - cron: "daily"

permissions:
  contents: read
  issues: read
  pull-requests: read

strict: false

network:
  allowed:
    - defaults
    - api.minimax.io

engine:
  id: claude
  api-target: api.minimax.io
  max-turns: 50

tools:
  github: all
  timeout: 180

timeout-minutes: 60

env:
  ANTHROPIC_API_KEY: "${{ secrets.ANTHROPIC_API_KEY }}"
  ANTHROPIC_BASE_URL: "https://api.minimax.io/anthropic"
  ANTHROPIC_API_TARGET: "api.minimax.io"
  ANTHROPIC_API_BASE_PATH: "/anthropic"
  ANTHROPIC_MODEL: "MiniMax-M2.7"
  CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC: "1"
  
  PIPELINE_ROOT: "content-creation-pipeline"
  STAGE_OUTPUTS: "content-creation-pipeline/stages"

safe-outputs:
  create-issue:
    title-prefix: "[faaw] "
    labels: [faaw-pipeline, automated]
    max: 5
    close-older-issues: true
  add-comment:
    max: 20

---

# FAAW Pipeline Orchestrator

Execute the FAAW content-creation-pipeline with sequential stage execution.

## Pipeline Configuration

Read `content-creation-pipeline/CLAUDE.md` for:
- Stage order: 001 → 002 → 003 → 004
- Stage types (AUTO/HYBRID/INTERACTIVE)
- Skills mapping per stage

## Execution Modes

### Mode: auto
All AUTO stages execute sequentially in one agent call. HYBRID/INTERACTIVE stages pause for human input.

### Mode: hybrid
Each stage runs as a separate workflow, chained via `dispatch-workflow`.

## Stage Execution Order

### Stage 001: RESEARCH (AUTO if no brief needed)

1. Read `content-creation-pipeline/001-RESEARCH/CLAUDE.md`
2. Read `content-creation-pipeline/001-RESEARCH/skills/` if exists
3. Execute research tasks:
   - Competitor analysis
   - Trend research
   - Content intelligence
4. Write outputs to `content-creation-pipeline/001-RESEARCH/outputs/`
   - `research-findings.json` - structured findings
   - `competitor-analysis.md` - markdown report
   - `trend-report.md` - trends analysis
5. Create/update status issue with progress

### Stage 002: INTAKE (INTERACTIVE - requires human)

1. Read `content-creation-pipeline/002-INTAKE/CLAUDE.md`
2. If mode=auto and human brief exists in issue:
   - Parse brief from trigger issue or previous outputs
   - Execute planning tasks
3. If mode=hybrid or no brief:
   - Create issue asking for brief
   - Wait for human response
4. Write outputs to `content-creation-pipeline/002-INTAKE/outputs/`
   - `content-brief.json` - structured brief
   - `topic-definitions.md` - topics for content

### Stage 003: CREATE (AUTO)

1. Read `content-creation-pipeline/003-CREATE/CLAUDE.md`
2. Read previous stage outputs (001 + 002)
3. Execute content creation:
   - LinkedIn posts
   - Twitter threads
   - Instagram captions
   - Content calendar
4. Write outputs to `content-creation-pipeline/003-CREATE/outputs/`
   - `linkedin-posts.md` - draft LinkedIn content
   - `twitter-threads.md` - draft Twitter content
   - `instagram-captions.md` - draft Instagram content
   - `content-calendar.md` - scheduled content

### Stage 004: OUTPUT (AUTO)

1. Read `content-creation-pipeline/004-OUTPUT/CLAUDE.md`
2. Read 003 outputs
3. Execute formatting:
   - Platform-specific formatting
   - Hashtag optimization
   - Timing recommendations
4. Write final outputs to `content-creation-pipeline/004-OUTPUT/outputs/`
   - `final-content.md` - all formatted content
   - `publish-schedule.md` - posting schedule
   - `performance-metrics.md` - expected metrics

## Data Passing Between Stages

Each stage reads from previous stage outputs:

```
001-RESEARCH/outputs/
├── research-findings.json    → 002 reads
├── competitor-analysis.md   → 002 reads
└── trend-report.md          → 002 reads

002-INTAKE/outputs/
├── content-brief.json       → 003 reads
└── topic-definitions.md     → 003 reads

003-CREATE/outputs/
├── linkedin-posts.md         → 004 reads
├── twitter-threads.md        → 004 reads
└── content-calendar.md       → 004 reads

004-OUTPUT/outputs/
└── final-content.md         → Final deliverable
```

## Task Execution Structure

For each stage, the AI executes these tasks in order:

```
Task [N]: Execute Stage [XXX]
  1. Read stage CLAUDE.md for context
  2. Read skill files for instructions
  3. Execute defined tasks
  4. Write outputs to stage/outputs/
  5. Create status comment on issue
  6. Signal completion or blocker
```

## Final Output

When all stages complete, create a summary issue with:
- Pipeline run summary
- Links to all stage outputs
- Final content for publishing
- Next recommended actions

## Error Handling

If any stage fails:
1. Create issue with error details
2. Include last successful outputs
3. Recommend recovery steps
4. Allow manual restart from failed stage