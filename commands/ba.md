---
description: "Run BA agent to analyze requirements"
---

You MUST spawn an Agent using the Agent tool. Do NOT analyze yourself.

Output: `━━ [BA] Business Analyst - Analyzing... ━━`

Call the Agent tool with description="[BA] Analyzing requirements" and prompt="You are a Senior Business Analyst. Task: $ARGUMENTS. Steps: 1) Read relevant code files. 2) Analyze requirements. 3) Write BA REPORT with: functional requirements, files to modify, subtasks, acceptance criteria, edge cases, risks."

After agent returns, output the full BA REPORT.
