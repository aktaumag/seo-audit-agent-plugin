---
name: seo-audit-agent
description: Conduct, resume, recheck, or report on a complete website SEO audit through the SEO Audit Agent MCP. Use when the user asks to audit, inspect, check, diagnose, continue, or report on a site's SEO, technical SEO, performance, on-page SEO, or semantic markup.
---

Use the `seo-audit-agent` MCP as the source of truth for the checklist, order, scenarios, audit state, display lines, and severity. Keep this Skill as workflow guidance; do not copy the rules catalog or calculate severity locally.

For a new audit, call `start_audit`. Show its `user_message_markdown`, including the complete clickable `audit_url`, then immediately call `get_next_check`. Never show the embedded access code or a technical `audit_ref` separately. When the user provides an existing audit link, call `open_audit` and continue with that complete URL. A legacy bare code is accepted by the server but must not be echoed to the user.

Process one check at a time:

1. Read the returned scenario, evidence requirements, dependencies, and supplied links.
2. Use browsing, HTTP, code, SEO, and connected tools already available in the conversation. Never request Work Mode or another client mode as a generic prerequisite while tool calls already work.
3. Never invent an observation, measurement, tool result, access, or evidence. If a concrete input is missing, ask only for that input. If a required browser action actually reports unavailable permission, save `needs_input` with the exact read-only `access_request` before asking the user to grant it. Do not run an initial browser preflight.
4. Save every result with `save_audit_progress`. Use its `display_result` for user-facing status; never calculate or rename severity.
5. After every non-blocking save, immediately call `get_next_check` and continue in the same run. Do not stop merely to narrate progress or ask whether to continue.

Collect `display_result` values saved since the previous user-facing response. When the run ends, use this structure:

```markdown
**Проверил:**

🟢 Название проверенного пункта
🟡 Название проверенного пункта
🟠 Название проверенного пункта
🔴 Название проверенного пункта

**Подробности:** [Открыть аудит](https://seo-audit.wseo.pw/audit/....)

**Примечание:** Короткая дополнительная информация, только если она полезна.

**Почему остановился:** Точная причина остановки.

**Чтобы продолжить:** Конкретное действие пользователя.
```

Each line under `Проверил:` contains only the server-provided colored circle and check title. Use `Не проверено:` for returned results whose `display_result.section` is `not_checked`. Do not expose internal enum names such as `manual_review`. Do not repeat check lines already shown in the conversation unless the user asks for complete progress; then call `generate_report` and use its `progress_markdown`.

Omit `Примечание` by default. Add it only for useful context that does not belong to a check line, the audit link, the stop reason, or the continuation action, and keep it to one short paragraph.

Include `Почему остановился` and `Чтобы продолжить` only when the run actually has to end because a concrete user input is missing, an attempted required tool reports unavailable access or permission, the audit is complete, or the platform ends the run. If the platform ends the run while the audit can continue, write that the audit is not blocked and tell the user to send `Продолжай аудит`. Otherwise continue autonomously.

Do not declare completion while an applicable check remains pending, in progress, awaiting input, blocked, or scheduled for recheck. Use `generate_report` after completion or when the user asks for the full current progress. Keep source URLs and measurements exact and respond in the user's language.

Anyone with the audit link can view and continue it. The audit is automatically deleted 90 days after its last saved result change; viewing it does not extend retention. Audit only public website information and never request passwords, access tokens, private-panel credentials, or closed files.
