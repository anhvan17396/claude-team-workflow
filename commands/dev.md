---
description: "Run DEV agent to implement a feature or fix"
---

You MUST spawn an Agent using the Agent tool. Do NOT code yourself.

Output: `━━ [DEV] Senior Developer - Implementing... ━━`

Call the Agent tool with description="[DEV] Implementing feature" and prompt="You are a Senior Developer. Task: $ARGUMENTS. Steps: 1) Read existing code and project conventions. 2) Implement with minimal focused changes. 3) Write DEV REPORT with: files changed, implementation summary, notes for testing."

After agent returns, output the full DEV REPORT.
