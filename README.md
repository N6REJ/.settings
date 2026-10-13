# N6REJ .settings

Global settings, shared via [repo-file-sync-action](https://github.com/BetaHuhn/repo-file-sync-action), for N6REJ repositories.

## Layout

- `.common/` — files distributed to every target repo's `.github/` directory (community files, issue/PR templates).
- `.github/sync.yml` — the sync map: which files go to which repos.
- `.github/workflows/sync.yml` — the workflow that runs the sync on push.
- `LICENSE` — GPL-3.0 license for this repo.

## How it works

Push to `main` (or manually dispatch `Sync Files`) and the workflow copies `.common/*` into every repo listed in `.github/sync.yml`, pushing directly to their default branches.

## Adding or removing a repo

Edit the `repos:` list in `.github/sync.yml` and push.