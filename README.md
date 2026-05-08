# Paca Plugins Marketplace Catalog

This repository is the public plugin marketplace source for Paca.

## Purpose

The Paca API reads `catalog/plugins.json` and exposes entries in the web admin marketplace.
Plugin developers publish by opening pull requests that add or update plugin entries.

## Catalog File

- Path: `catalog/plugins.json`
- Format: JSON
- Required artifact URLs per plugin:
  - `backend_tar_gz_url`
  - `frontend_tar_gz_url`
  - `migrations_tar_gz_url`
  - `manifest_tar_gz_url`

## Publish Workflow (PR-based)

1. Create a plugin release in your plugin repository.
2. Upload public tar.gz artifacts for backend, frontend, migrations, and manifest.
3. Update `catalog/plugins.json` with new version and URLs.
4. Open a pull request to this repository.
5. After merge, plugin appears in Paca marketplace UI automatically.

## Artifact Expectations

- `backend.tar.gz` includes `backend.wasm`.
- `frontend.tar.gz` includes frontend assets (for example `assets/remoteEntry.js`).
- `migrations.tar.gz` includes SQL files (for example `0001_create_table.sql`).
- `manifest.tar.gz` includes `plugin.json`.

## Validation Recommendations

- Keep URLs immutable (release assets, not moving branches).
- Keep plugin `name` stable (reverse-DNS identifier).
- Keep `version` semver and aligned with release tag.
- Verify artifact URLs before opening PR.
