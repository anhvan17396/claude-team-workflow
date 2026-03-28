---
description: "Run team workflow pipeline: BA → DEV → TEST+DEVOPS → REVIEWER → PM"
---

# STOP. READ THIS FIRST.

You have received a `/team` command. This means you MUST follow the pipeline below.

**YOU ARE FORBIDDEN FROM:**
- Writing any code yourself
- Fixing bugs yourself
- Analyzing requirements yourself
- Doing ANY work directly

**YOU MUST ONLY:**
- Call the Agent tool 6 times (once per role)
- Print headers between each Agent call
- Compile the final TEAM REPORT

If you feel tempted to do the work yourself, STOP and spawn an Agent instead.

---

## Task
$ARGUMENTS

---

## Execute this pipeline NOW. No exceptions.

**STEP 1 — Setup**

Call TodoWrite immediately with these 6 items (all pending):
- "[BA] Analyze requirements"
- "[DEV] Implement"
- "[TEST] Test UI + functionality"
- "[DEVOPS] Check infrastructure"
- "[REVIEWER] Review code"
- "[PM] Verify requirements"

---

**STEP 2 — Spawn BA Agent**

Print exactly:
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  [BA] Business Analyst — Analyzing...
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Then call the Agent tool with:
- description: "[BA] Analyzing requirements for: $ARGUMENTS"
- prompt: "You are a Senior Business Analyst. Task: $ARGUMENTS. Do NOT implement anything. Only analyze. Steps: 1) Read relevant existing code files. 2) Understand current state. 3) Write a detailed BA REPORT containing: Functional Requirements, Files to modify (with exact paths), Ordered subtasks, Acceptance criteria, Edge cases, Risks."

After agent finishes, update TodoWrite: mark [BA] as completed. Print 1-line summary of BA REPORT.

---

**STEP 3 — Spawn DEV Agent**

Print exactly:
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  [DEV] Senior Developer — Implementing...
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Then call the Agent tool with:
- description: "[DEV] Implementing: $ARGUMENTS"
- prompt: "You are a Senior Developer. BA Analysis: <insert full BA REPORT from step 2>. Task: $ARGUMENTS. Implement the changes following project conventions. Output DEV REPORT with: list of files changed, what changed in each file, implementation notes."

After agent finishes, update TodoWrite: mark [DEV] as completed. Print 1-line summary.

---

**STEP 4 — Spawn TEST + DEVOPS in parallel**

Print exactly:
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  [TEST] QA Engineer — Testing...
  [DEVOPS] DevOps — Checking infra...
  (running in parallel)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Call BOTH Agent tools in the SAME message (parallel execution):

Agent 1:
- description: "[TEST] Testing changes"
- prompt: "You are a QA Engineer. Test the recent code changes. Steps: 1) Run git diff to see what changed. 2) If UI changes exist: use mcp__Claude_in_Chrome__tabs_context_mcp to get a tab, use mcp__Claude_in_Chrome__navigate to open the app, use mcp__Claude_in_Chrome__computer with action screenshot to capture UI. 3) Check console errors. 4) Run existing tests (npm test / mvn test) if available. Output TEST REPORT: Status PASS/FAIL, UI checks, console errors, issues found."

Agent 2:
- description: "[DEVOPS] Checking infrastructure"
- prompt: "You are a DevOps Engineer. Steps: 1) Detect project type. 2) Run type-check (npx tsc --noEmit or equivalent). 3) Check if database schema files changed - verify migrations exist. 4) Read Dockerfile, docker-compose.yml, CI config for issues. Output DEVOPS REPORT: build status, migration status, Docker/CI status, verdict OK/ISSUES."

After both finish, update TodoWrite: mark [TEST] and [DEVOPS] as completed. Print 1-line summaries.

If TEST reported FAIL: go back to STEP 3 with specific issues to fix. Max 2 retries.

---

**STEP 5 — Spawn REVIEWER Agent**

Print exactly:
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  [REVIEWER] Code Reviewer — Reviewing...
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Then call the Agent tool with:
- description: "[REVIEWER] Reviewing code changes"
- prompt: "You are a Senior Code Reviewer. Steps: 1) Run git diff to see all changes. 2) Check code quality: readability, DRY, SOLID principles. 3) Check security: SQL injection, XSS, hardcoded secrets, missing auth. 4) Check project conventions from CLAUDE.md. 5) If UI changes: use mcp__Claude_in_Chrome__computer screenshot to verify visually. Output REVIEW REPORT: Status APPROVE or REQUEST_CHANGES, findings list, verdict."

After agent finishes, update TodoWrite: mark [REVIEWER] as completed.
If REQUEST_CHANGES: go back to STEP 3 with specific changes needed. Max 2 retries.

---

**STEP 6 — Spawn PM Agent**

Print exactly:
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  [PM] Product Manager — Verifying...
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Then call the Agent tool with:
- description: "[PM] Verifying requirements"
- prompt: "You are a Product Manager. Original task: $ARGUMENTS. Steps: 1) Read changed files to understand what was built. 2) Check each acceptance criteria from BA REPORT. 3) Verify no requirements were missed. 4) If UI: use Chrome MCP to verify user experience. Output PM REPORT: Acceptance criteria checklist (MET/NOT MET), overall verdict ACCEPTED or REJECTED."

After agent finishes, update TodoWrite: mark [PM] as completed.

---

**STEP 7 — Print TEAM REPORT**

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  TEAM REPORT — Final Summary
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  Task: $ARGUMENTS

  | Role     | Status            | Summary              |
  |----------|------------------|----------------------|
  | BA       | DONE             | <1-line>             |
  | DEV      | DONE             | <1-line>             |
  | TEST     | PASS / FAIL      | <1-line>             |
  | DEVOPS   | OK / ISSUES      | <1-line>             |
  | REVIEWER | APPROVE/CHANGES  | <1-line>             |
  | PM       | ACCEPTED/REJECTED| <1-line>             |

  Overall: ALL PASSED ✓  /  ISSUES REMAIN ✗
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
