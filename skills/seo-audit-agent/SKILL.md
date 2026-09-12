---
name: seo-audit-agent
description: Conduct, resume, recheck, or report on a complete website SEO audit through the SEO Audit Agent MCP. Use when the user asks to audit, inspect, check, diagnose, continue, or report on a site's SEO, technical SEO, performance, on-page SEO, or semantic markup.
---

Use the `seo-audit-agent` MCP as the source of truth for the checklist, order, scenarios, audit state, and severity. Do not reproduce the catalog from memory or start an informal parallel checklist.

For a new audit, call `start_audit` with the public site URL and response language. In the first visible response, show a short **audit created** card containing the returned `audit_url`, retention date, `0 / total_checks`, and the three phases below. The public page is a convenient live viewer, not the only delivery channel: every progress or final report must also be returned as usable Markdown in chat. No account or authorization is used.

Use this execution protocol, which is deliberately visible to the user:

1. **Phase A — autonomous public checks.** HTTP, public search, available SEO tools, and other non-browser work. Before every check returned by `get_next_check`, write a concise operation-log line: `N/total · check_id · title — what is being verified`. After saving it, state the saved status/severity and current completed count. These are factual progress updates, never hidden chain-of-thought.
2. **Phase B — rendered-page checks.** A cloud browser can be useful only to inspect the public rendered DOM after JavaScript, responsive layout, console errors, redirects, and resource loading. It never grants access to the user's computer, server, admin panel, passwords, tokens, Analytics, Search Console, forms, or data changes.
3. **Phase C — authenticated sources, if requested.** Search Console, Analytics, and any private system are a separate optional phase with their own explicit authorization. Never imply that a public-browser permission grants them.

The platform browser-permission UI blocks the chat. Therefore it must never appear as an unexplained interruption:

- For a user who explicitly asks for a **full technical audit now**, give a preflight before opening the first rendered page: name the audited hostname, explain the read-only scope and the DOM/mobile/console purpose, then ask for browser permission early.
- Otherwise use **autonomous-first**: complete everything possible without that browser, save it, call `generate_report`, and show the partial Markdown report and `audit_url`. Only then pause at the exact browser-only check.
- Immediately before a permission request, save that exact check with `status: "needs_input"` and an `access_request` containing the audited hostname, public page URLs, read-only actions, and the concrete reason. Then show the current check ID/title, completed count, what is already done, what remains, and why HTTP output is insufficient **before** invoking a browser tool. The saved checkpoint keeps the page and report truthful if the dialog is unanswered or denied.
- If permission is denied or remains unanswered, do not stall silently and do not invent results. Keep the exact item as `needs_input`, present the partial report in chat, link to the public viewer, and list the browser-only checks still unavailable.

When the user supplies an audit code or link, call `open_audit` first. Preserve the returned `audit_ref` and use it for subsequent tools. A lost link cannot be recovered from a user account.

Work on exactly one check returned by `get_next_check`:

1. Read the current methodology, scenario, scope, required inputs, supplied links, evidence requirements, dependencies, and maturity.
2. Write the visible `N/total` operation-log line before acting. Try to perform the check using HTTP, code, SEO, or other tools already available in the current client. Use the cloud browser only under the Phase B protocol above.
3. If the current client cannot complete it, explain the exact manual steps, give the supplied working or unchecked tool links, and request only the missing URL, measurement, output, screenshot reference, or other evidence. Use `resolved_url` for a site URL template. If browser access is the missing input, use the saved access checkpoint instead of a generic permission request.
4. Never invent access, observations, measurements, tool output, or evidence. Mark unavailable work with the status that best matches the returned scenario.
5. Save the observation, measurement, evidence, confidence, and recommendation through `save_audit_progress`. Do not calculate or override severity outside the MCP. Immediately state the server-returned status, severity, and progress count in the visible operation log.
6. Request the next check. Return to dependency, blocked, and recheck items when the MCP schedules them.

Do not declare the audit complete while an applicable check remains pending, in progress, awaiting input, blocked, or scheduled for recheck. Use `generate_report` for a clearly labeled progress report or after the MCP confirms completion. For a final report, paste the returned full `markdown` into chat with all check IDs, evidence, findings, recommendations, and unresolved items. Then include `audit_url` as an optional interactive view and export location. A completed check can later be marked `recheck`; saving the new result updates the same report.

The audit is available to anyone with its link and is automatically deleted 90 days after the last saved result change. Viewing the page, opening the audit, or exporting the report does not extend that date. There is no manual delete operation, account-based audit list, or link recovery.

Audit only publicly accessible website information. Do not request or store passwords, access tokens, private-panel credentials, or closed files. If the site or required source is not publicly accessible, explain the limitation and save the appropriate unavailable status.

Keep source URLs and measurements exact. Explain the work, questions, and report in the user's language. State when a scenario or severity is provisional. Never delete or silently omit a source link because it is marked `broken`; present it as a historical reference when useful, without claiming that it works unless access succeeds.
