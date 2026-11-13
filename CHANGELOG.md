# Changelog

All notable changes to Markmap Skills are documented in this file.

## Unreleased

- Reworded the plugin description in every manifest and `package.json` to match the FINOLABS brand copy and the shared `finolabs/plugins` catalog.

## 0.2.0 - 2026-11-03

**Breaking for installs from this repository's catalogs.** Markmap Skills is now listed in the shared [`finolabs/plugins`](https://github.com/finolabs/plugins) catalog, and the repository no longer serves a marketplace of its own. Existing `markmap-skills@fioenix-plugins` (Claude Code, Codex) and `markmap-skills@Finolabs` (Codex) installs need the migration steps in the [README](README.md#2-openai-codex).

- Removed `.claude-plugin/marketplace.json` and `.agents/plugins/marketplace.json`; install with `markmap-skills@finolabs` after `marketplace add finolabs/plugins`.
- Replaced the root `plugin.json` with the Antigravity manifest `.antigravity-plugin/plugin.json` (`agy plugin install https://github.com/finolabs/markmap-skills`); `scripts/sync_version.sh` and `tests/validate.sh` follow.
- Moved manifest, policy and issue-template URLs from `fioenix/markmap-skills` to `finolabs/markmap-skills`.
- Made the plugin description and keywords identical in the Claude Code, Codex, Antigravity and legacy Codex manifests, matching the shared catalog.
