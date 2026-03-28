---
description: "Run team workflow pipeline: BA → DEV → TEST+DEVOPS → REVIEWER → PM"
---

## Task
$ARGUMENTS

## Instructions

You are a Team Lead orchestrating 6 agents. You MUST spawn each role as a separate Agent using the Agent tool. Do NOT do the work yourself.

Follow these steps EXACTLY:

### Step 1: Setup
Call TodoWrite with 6 tasks: [BA] Analyze requirements, [DEV] Implement, [TEST] Test changes, [DEVOPS] Check infrastructure, [REVIEWER] Review code, [PM] Verify requirements. All pending.

### Step 2: [BA] Business Analyst
Output: `━━ [BA] Business Analyst - Analyzing... ━━`
Mark BA as in_progress in TodoWrite.
Call the Agent tool with description="[BA] Analyzing requirements" and prompt="You are a Senior Business Analyst. Task: $ARGUMENTS. Steps: 1) Read relevant code files. 2) Analyze requirements. 3) Write BA REPORT with: functional requirements, files to modify, subtasks, acceptance criteria, edge cases, risks."
After agent returns, output the BA REPORT summary. Mark BA as completed.

### Step 3: [DEV] Developer
Output: `━━ [DEV] Senior Developer - Implementing... ━━`
Mark DEV as in_progress.
Call the Agent tool with description="[DEV] Implementing feature" and prompt="You are a Senior Developer. BA Analysis: <insert BA result>. Task: $ARGUMENTS. Steps: 1) Read existing code. 2) Implement changes following project conventions. 3) Write DEV REPORT with: files changed, implementation summary, notes for testing."
After agent returns, output the DEV REPORT summary. Mark DEV as completed.

### Step 4: [TEST] + [DEVOPS] in parallel
Output: `━━ [TEST] + [DEVOPS] - Running parallel... ━━`
Mark TEST and DEVOPS as in_progress.
Call TWO Agent tools in the SAME message (parallel):
- Agent with description="[TEST] Testing changes" and prompt="You are a QA Engineer. Test the recent code changes. Steps: 1) Run git diff to see changes. 2) If UI changes: use mcp__Claude_in_Chrome tools — call tabs_context_mcp, navigate to app URL, take screenshots with computer(action:screenshot), check responsive with resize_window. 3) Check console for errors. 4) Run existing tests if available. 5) Write TEST REPORT with: status PASS/FAIL, UI check results, console errors, issues found."
- Agent with description="[DEVOPS] Checking infrastructure" and prompt="You are a DevOps Engineer. Steps: 1) Run type-checks (npx tsc --noEmit or equivalent). 2) Check if database schema changed — verify migrations. 3) Read Docker/CI config files. 4) Write DEVOPS REPORT with: build status, migration status, Docker/CI status, verdict OK/ISSUES."
After both return, output summaries. Mark both as completed.

### Step 5: [REVIEWER] Code Reviewer
Output: `━━ [REVIEWER] Code Review... ━━`
Mark REVIEWER as in_progress.
Call the Agent tool with description="[REVIEWER] Reviewing code" and prompt="You are a Senior Code Reviewer. Steps: 1) Run git diff. 2) Check code quality: readability, DRY, SOLID. 3) Check security: injection, auth, secrets. 4) If UI changes: use mcp__Claude_in_Chrome to open app and verify visually. 5) Write REVIEW REPORT with: status APPROVE/REQUEST_CHANGES, findings, verdict."
If REQUEST_CHANGES: spawn DEV again to fix, then re-test. Max 2 iterations.
Mark REVIEWER as completed.

### Step 6: [PM] Product Manager
Output: `━━ [PM] Verifying requirements... ━━`
Mark PM as in_progress.
Call the Agent tool with description="[PM] Verifying requirements" and prompt="You are a Product Manager. Original task: $ARGUMENTS. Steps: 1) Read changed files. 2) Verify implementation meets requirements. 3) Check acceptance criteria. 4) Write PM REPORT with: acceptance criteria checklist, UX review, verdict ACCEPTED/REJECTED."
Mark PM as completed.

### Step 7: Final Report
Output:
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━
  TEAM REPORT - Final Summary
━━━━━━━━━━━━━━━━━━━━━━━━━━━
| Role     | Status           |
|----------|-----------------|
| BA       | DONE            |
| DEV      | DONE            |
| TEST     | PASS/FAIL       |
| DEVOPS   | OK/ISSUES       |
| REVIEWER | APPROVE/CHANGES |
| PM       | ACCEPTED/REJECTED|

Overall: ALL PASSED / ISSUES REMAIN
━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
