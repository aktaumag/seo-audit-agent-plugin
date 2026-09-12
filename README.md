# SEO Audit Agent

Тонкий клиентский пакет для полного SEO-аудита в ChatGPT, Codex, Claude и Claude Code. Чек-лист, сценарии, порядок, состояние и критичность приходят с удалённого MCP; пакет обновляется только при изменении протокола подключения.

Готовые ZIP-пакеты версии 0.1.1 опубликованы в [GitHub Releases](https://github.com/aktaumag/seo-audit-agent-plugin/releases/tag/v0.1.1).

## Подключение

Рабочий MCP-адрес: `https://seo-audit.wseo.pw/mcp`.

- [Подключение ChatGPT и Codex](https://seo-audit.wseo.pw/connect/openai/)
- [Подключение Claude и Claude Code](https://seo-audit.wseo.pw/connect/claude/)

После подключения сразу напишите: `Проведи полный SEO-аудит сайта example.com`. Вход не нужен для первого запуска: прогресс временно хранится семь дней. Авторизация предлагается позже, если пользователь решит сохранить накопленный аудит надолго и открывать его в других чатах, ChatGPT, Codex или Claude.

## Состав

- `.codex-plugin/plugin.json` — манифест ChatGPT/Codex;
- `.claude-plugin/plugin.json` — манифест Claude Code;
- `.claude-plugin/marketplace.json` — описание marketplace;
- `.mcp.json` — единый адрес удалённого MCP;
- `skills/seo-audit-agent/SKILL.md` — общий стабильный процесс.

Каталог проверок, исходные Trello/Excel данные и серверные секреты в публичный пакет не входят.
