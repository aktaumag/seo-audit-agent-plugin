---
name: seo-audit-agent
description: Conduct, resume, recheck, or report on a complete website SEO audit through the SEO Audit Agent MCP. Use when the user asks to audit, inspect, check, diagnose, continue, or report on a site's SEO, technical SEO, performance, on-page SEO, or semantic markup.
---

Use the `seo-audit-agent` MCP as the source of truth for the checklist, order, scenarios, audit state, and severity. Do not reproduce the catalog from memory or start an informal parallel checklist.

For a new audit, call `start_audit` with the public site URL and response language. Immediately show the returned `audit_url` and explain that it opens the web report and can be pasted into ChatGPT, Codex, Claude, or another supported client to continue the same audit. No account or authorization is used.

When the user supplies an audit code or link, call `open_audit` first. Preserve the returned `audit_ref` and use it for subsequent tools. A lost link cannot be recovered from a user account.

Work on exactly one check returned by `get_next_check`:

1. Read the current methodology, scenario, scope, required inputs, supplied links, evidence requirements, dependencies, and maturity.
2. Try to perform the check using browsing, HTTP, code, SEO, or other tools already available in the current client.
3. If the current client cannot complete it, explain the exact manual steps, give the supplied working or unchecked tool links, and request only the missing URL, measurement, output, screenshot reference, or other evidence. Use `resolved_url` for a site URL template.
4. Never invent access, observations, measurements, tool output, or evidence. Mark unavailable work with the status that best matches the returned scenario.
5. Save the observation, measurement, evidence, confidence, and recommendation through `save_audit_progress`. Do not calculate or override severity outside the MCP.
6. Request the next check. Return to dependency, blocked, and recheck items when the MCP schedules them.

Do not declare the audit complete while an applicable check remains pending, in progress, awaiting input, blocked, or scheduled for recheck. Use `generate_report` for a clearly labeled progress report or after the MCP confirms completion. A completed check can later be marked `recheck`; saving the new result updates the same report.

The audit is available to anyone with its link and is automatically deleted 90 days after the last saved result change. Viewing the page, opening the audit, or exporting the report does not extend that date. There is no manual delete operation, account-based audit list, or link recovery.

Audit only publicly accessible website information. Do not request or store passwords, access tokens, private-panel credentials, or closed files. If the site or required source is not publicly accessible, explain the limitation and save the appropriate unavailable status.

Keep source URLs and measurements exact. Explain the work, questions, and report in the user's language. State when a scenario or severity is provisional. Never delete or silently omit a source link because it is marked `broken`; present it as a historical reference when useful, without claiming that it works unless access succeeds.
