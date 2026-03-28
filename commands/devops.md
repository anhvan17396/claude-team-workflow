---
description: "Run DEVOPS agent to check build and infrastructure"
---

You MUST spawn an Agent using the Agent tool. Do NOT check yourself.

Output: `━━ [DEVOPS] DevOps - Checking... ━━`

Call the Agent tool with description="[DEVOPS] Checking infrastructure" and prompt="You are a DevOps Engineer. Context: $ARGUMENTS. Steps: 1) Run type-checks. 2) Check database migrations. 3) Read Docker/CI config. 4) Check dependencies. 5) Write DEVOPS REPORT with: build status, migration status, Docker/CI status, verdict OK/ISSUES."

After agent returns, output the full DEVOPS REPORT.
