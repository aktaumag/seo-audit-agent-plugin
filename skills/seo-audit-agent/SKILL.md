---
name: seo-audit-agent
description: Conduct or resume a complete website SEO audit using the SEO Audit Agent MCP. Use when the user asks to audit, inspect, check, diagnose, or report on a site's SEO, technical SEO, performance, on-page SEO, or semantic markup.
---

Use the `seo-audit-agent` MCP as the source of truth for the checklist, order, scenarios, state, and severity.

For a new audit, call `start_audit` with the user's site and response language. Sign-in is not required to begin. For a request to resume or find an account audit, call `list_audits`; this is when authentication may be requested. Do not reproduce the catalog from memory or begin an informal parallel checklist.

Treat storage behavior returned by MCP as part of the workflow:

- A temporary audit is saved on the server for seven days. Briefly explain the `storage_notice` returned at the start, the first pause, and before the final report. Do not repeat it when the MCP does not return a notice.
- Explain that account saving keeps the accumulated progress and enables continuation in another chat or supported client.
- Call `claim_audit` only after the user chooses permanent saving or asks to continue the audit elsewhere. The login happens then; do not ask the user to re-enter results already stored in the temporary audit.
- Preserve the exact `audit_id` while an audit is temporary. Do not imply that temporary data is permanently saved.

Work on exactly one check returned by `get_next_check`:

1. Read the current methodology, scenario, scope, required inputs, supplied links, evidence requirements, dependencies, and maturity.
2. Try to perform the check using browsing, HTTP, code, SEO, or other tools already available in the current client.
3. If the current client cannot complete it, explain the exact manual steps, give the supplied working or unchecked tool links, and request only the missing URL, measurement, output, screenshot reference, or other evidence. Use `resolved_url` for a site URL template.
4. Never invent access, observations, measurements, tool output, or evidence. Mark unavailable work with the status that best matches the returned scenario.
5. Save the observation, measurement, evidence, confidence, and recommendation through `save_audit_progress`. Do not calculate or override severity outside the MCP.
6. Request the next check. Return to dependency, blocked, and recheck items when the MCP schedules them.

Do not declare the audit complete while an applicable check remains pending, in progress, awaiting input, blocked, or scheduled for recheck. Use `generate_report` for a clearly labeled progress report or after the MCP confirms completion.

If the user explicitly asks to remove the current temporary audit, call `delete_audit` with its preserved `audit_id`; sign-in is not required. Account audit listing and permanent attachment require authorization.

Keep source URLs and measurements exact. Explain the work, questions, and report in the user's language. State when a scenario or severity is provisional so the user can distinguish a draft rule from an owner-reviewed rule.

Never delete or silently omit a source link because it is marked `broken`. Present it as a historical reference when it helps the user review that check, but do not claim that it currently works or use it as evidence unless access succeeds.
