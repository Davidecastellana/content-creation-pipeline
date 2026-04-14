# Workspace — Entry Point

This workspace uses the meta-pipeline plugin for orchestration.

## Pipelines
| Pipeline | Stages | Purpose |
|----------|--------|---------|
| content-creation-pipeline | 001 → 002 → 003 → 004 | Social media content creation workflow |

## Pipeline Routing
content-creation-pipeline reads from: User inputs and competitive research
content-creation-pipeline outputs to: Final formatted content ready for publishing

## Commands
- Initialize: pipeline_init content-creation-pipeline {project}
- Status: pipeline_status content-creation-pipeline
- Current: pipeline_current content-creation-pipeline
- Approve: pipeline_approve content-creation-pipeline

## How It Works
1. Plugin (.opencode/plugins/meta-pipeline.js) handles orchestration
2. State files (.state.json) track progress per stage
3. Skills in each stage define the work
4. Human approval required for INTERACTIVE and HYBRID stages

## Content Types Supported
- LinkedIn posts and articles
- Twitter/X threads
- Instagram captions
- Social media content calendars
