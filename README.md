# Paca Plugins Marketplace Catalog

This repository is the public plugin marketplace source for Paca.

## Purpose

The Paca API reads `catalog/plugins.json` and exposes entries in the web admin marketplace.
Plugin developers publish by opening pull requests that add or update plugin entries.

## Catalog File

- Path: `catalog/plugins.json`
- Format: JSON
- Artifact URLs per plugin:
  - `manifest_tar_gz_url` — required.
  - `backend_tar_gz_url`, `frontend_tar_gz_url`, `migrations_tar_gz_url` — optional, include when your plugin has that surface.
  - `mcp_tar_gz_url` — optional, include when your plugin's manifest declares an `mcp` section.
  - `skills_tar_gz_url` — optional, include when your plugin's manifest declares a `skills` section (see [skills-plugin-system.md](https://github.com/Paca-AI/paca/blob/master/docs/plugins/skills-plugin-system.md)).

## Publish Workflow (PR-based)

1. Create a plugin release in your plugin repository.
2. Upload public tar.gz artifacts for every surface your plugin ships — manifest is always required; backend, frontend, migrations, mcp, and skills are each uploaded only if your plugin.json declares that section.
3. Update `catalog/plugins.json` with new version and URLs.
4. Open a pull request to this repository.
5. After merge, plugin appears in Paca marketplace UI automatically.

## Artifact Expectations

- `backend.tar.gz` includes `backend.wasm`.
- `frontend.tar.gz` includes frontend assets (for example `assets/remoteEntry.js`).
- `migrations.tar.gz` includes SQL files (for example `0001_create_table.sql`).
- `manifest.tar.gz` includes `plugin.json`.
- `mcp.tar.gz` includes the MCP entry bundle referenced by `plugin.json`'s `mcp.remoteEntryUrl`.
- `skills.tar.gz` includes one directory per skill named in `plugin.json`'s `skills.names`, each containing a `SKILL.md` (e.g. `paca-my-skill/SKILL.md`) — required whenever `plugin.json` has a `skills` section, otherwise the declared skills can never be fetched at install time.

## Validation Recommendations

- Keep URLs immutable (release assets, not moving branches).
- Keep plugin `name` stable (reverse-DNS identifier).
- Keep `version` semver and aligned with release tag.
- Verify artifact URLs before opening PR.
