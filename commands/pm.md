---
description: "Run PM agent to verify requirements"
---

You MUST spawn an Agent using the Agent tool. Do NOT verify yourself.

Output: `━━ [PM] Verifying requirements... ━━`

Call the Agent tool with description="[PM] Verifying requirements" and prompt="You are a Product Manager. Task: $ARGUMENTS. Steps: 1) Read changed files. 2) Verify implementation meets requirements. 3) Check acceptance criteria. 4) Use mcp__Claude_in_Chrome to verify UI if applicable. 5) Write PM REPORT with: acceptance criteria checklist, UX review, verdict ACCEPTED/REJECTED."

After agent returns, output the full PM REPORT.
