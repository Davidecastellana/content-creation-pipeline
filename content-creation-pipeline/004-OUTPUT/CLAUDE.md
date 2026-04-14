# 004-OUTPUT — Pipeline Stage

## Stage Info
- **Type**: AUTO
- **Purpose**: Format and package content for each platform
- **Pipeline**: content-creation-pipeline
- **Stage Path**: ./content-creation-pipeline/004-OUTPUT/

## Routing (Layer 2)
- **Reads from previous stages**: ../003-CREATE/outputs
- **Skips**: N/A

## Skills
Skills for this stage are in `./skills/`

## State
State is managed via `.state.json`
