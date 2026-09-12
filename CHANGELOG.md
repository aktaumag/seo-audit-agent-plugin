# Changelog

## 0.2.0

- Replaced accounts and OAuth with permanent access-by-link behavior.
- Added shareable 16-character audit codes and public noindex report pages.
- Added `open_audit` for continuing work from the same link across supported clients.
- Added Markdown and JSON downloads from the public report page.
- Changed retention to 90 days after the last saved result change; views do not extend it.
- Removed `list_audits`, `claim_audit`, and `delete_audit` from the MCP interface.

## 0.1.0

- Added the shared SEO audit workflow skill.
- Added the remote Streamable HTTP MCP connection for ChatGPT, Codex, and Claude Code.
- Added full-audit state, deterministic severity, evidence capture, rechecks, and Markdown/JSON reporting through the MCP server.
