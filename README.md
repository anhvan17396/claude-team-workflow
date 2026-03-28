# Claude Team Workflow Plugin

Multi-agent team workflow plugin for Claude Code. Simulates a development team with 6 roles working in pipeline.

## Pipeline

```
BA → DEV → TEST + DEVOPS (parallel) → REVIEWER → PM
```

| Role | Description |
|------|-------------|
| **BA** | Business Analyst — Analyze requirements, write specs |
| **DEV** | Senior Developer — Implement features, fix bugs |
| **TEST** | QA Engineer — Test UI (Chrome screenshots), check console, responsive |
| **DEVOPS** | DevOps Engineer — Type-check, migrations, Docker, CI |
| **REVIEWER** | Code Reviewer — Code quality, security, UI verification |
| **PM** | Product Manager — Verify requirements, acceptance criteria |

## Usage

### Full pipeline (all 6 roles)
```
/team <task description>
```

### Individual roles
```
/ba <task>        # Only BA analysis
/dev <task>       # Only DEV implementation
/test <context>   # Only TEST verification
/devops <context> # Only DEVOPS check
/review <context> # Only code review
/pm <task>        # Only PM verification
```

## Installation

```bash
# Clone to Claude Code plugins directory
git clone https://github.com/anhvan17396/claude-team-workflow.git ~/.claude/plugins/team-workflow

# Restart Claude Code — commands are available immediately
```

## Features

- Each role runs as a separate subagent with its own context
- TEST + DEVOPS run in parallel for speed
- TEST and REVIEWER can use Chrome MCP to screenshot and verify UI
- Auto fix loop: if TEST fails or REVIEWER requests changes, DEV fixes and re-tests (max 2 iterations)
- TodoWrite progress tracking across all roles
- Final TEAM REPORT summarizes all results

## Requirements

- Claude Code (Desktop App, CLI, or Web)
- Chrome MCP extension (optional, for UI testing)
