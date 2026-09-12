# Changelog

## 0.2.2

- Standardized every audit iteration around new colored check lines, one audit link, and conditional stop/continuation details.
- Removed separately displayed access codes and technical audit references from user-facing output.
- Continue automatically after every non-blocking saved result; do not request Work Mode when tools already work.
- Added concise, localized progress Markdown and separated unverified items from checked results without exposing internal status names.

## 0.2.1

- Added a visible per-check operation log with server-backed `N / total` progress.
- Added persisted, read-only cloud-browser checkpoints: hostname, public pages, exact reason, and permitted inspection actions are visible before a blocking permission dialog.
- Added an explicit autonomous-first / full-technical-now protocol so a paused browser dialog never becomes the only audit outcome.
- Added a live public report timeline and current-check snapshot; the full Markdown report remains available directly in chat.

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
