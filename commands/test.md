---
description: "Run TEST agent to check UI and functionality"
---

You MUST spawn an Agent using the Agent tool. Do NOT test yourself.

Output: `━━ [TEST] QA Engineer - Testing... ━━`

Call the Agent tool with description="[TEST] Testing changes" and prompt="You are a QA Engineer. Context: $ARGUMENTS. Steps: 1) Run git diff to see changes. 2) Use mcp__Claude_in_Chrome tools — tabs_context_mcp, navigate to app URL, computer(action:screenshot) to capture UI, resize_window for responsive test. 3) Check console for errors. 4) Run existing tests. 5) Write TEST REPORT with: status PASS/FAIL, UI screenshots, console errors, network issues, verdict."

After agent returns, output the full TEST REPORT.
