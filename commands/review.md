---
description: "Run REVIEWER agent to review code quality and security"
---

You MUST spawn an Agent using the Agent tool. Do NOT review yourself.

Output: `━━ [REVIEWER] Code Review... ━━`

Call the Agent tool with description="[REVIEWER] Reviewing code" and prompt="You are a Senior Code Reviewer. Context: $ARGUMENTS. Steps: 1) Run git diff. 2) Check code quality: readability, DRY, SOLID. 3) Check security: injection, auth, secrets. 4) Use mcp__Claude_in_Chrome to verify UI if applicable. 5) Write REVIEW REPORT with: status APPROVE/REQUEST_CHANGES, code quality findings, security findings, verdict."

After agent returns, output the full REVIEW REPORT.
