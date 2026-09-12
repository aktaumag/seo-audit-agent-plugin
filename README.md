# SEO Audit Agent

Тонкий клиентский пакет для полного SEO-аудита в ChatGPT, Codex, Claude и Claude Code. Чек-лист, сценарии, порядок, состояние и критичность приходят с удалённого MCP; пакет обновляется только при изменении протокола подключения.

## Подключение

1. Добавьте сервер из `.mcp.json` в поддерживаемый ИИ-клиент.
2. Войдите через защищённую страницу SEO Audit Agent.
3. Разрешите `audit:read` и `audit:write`.
4. Напишите: `Проведи полный SEO-аудит сайта example.com`.

Подробные инструкции будут доступны на публичном сайте SEO Audit Agent после выпуска 0.1.

## Состав

- `.codex-plugin/plugin.json` — манифест ChatGPT/Codex;
- `.claude-plugin/plugin.json` — манифест Claude Code;
- `.claude-plugin/marketplace.json` — описание marketplace;
- `.mcp.json` — единый адрес удалённого MCP;
- `skills/seo-audit-agent/SKILL.md` — общий стабильный процесс.

Каталог проверок, исходные Trello/Excel данные и серверные секреты в публичный пакет не входят.
