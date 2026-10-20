# N6REJ .settings

Global settings, shared via [repo-file-sync-action](https://github.com/BetaHuhn/repo-file-sync-action), for N6REJ repositories.

## Layout

- `.common/` — source files distributed to target repos' `.github/` directory (community files, issue/PR templates).
- `.github/sync.yml` — the sync map: which files go to which repos.
- `.github/workflows/sync.yml` — the workflow that runs the sync on push.
- `LICENSE` — GPL-3.0 license for this repo.

## How it works

Push to `main` (or manually dispatch `Sync Files`) and the workflow copies the
files listed in `.github/sync.yml` from `.common/` into every listed repo,
pushing directly to their default branches.

## Adding a common file

1. Add the file under `.common/`.
2. Add an explicit entry to the common group in `.github/sync.yml`:

   ```yaml
   - source: .common/example.md
     dest: .github/example.md
   ```

Files are listed explicitly on purpose. Syncing the whole `.common` directory
would push any new file to every repo automatically, which is easy to do by
accident. Add entries deliberately.

## Repository-owned files

Some files are intentionally **not** in `.common/` because each repo should own
its version. The sync never touches files it does not list, so these are safe:

- `.github/ISSUE_TEMPLATE/config.yml` — each repo links its own security policy
  and contact links.

To keep a repo from receiving a common file, either leave the file out of the
common group or add the repo to a `repos:` list that excludes it.

## Adding or removing a repo

Edit the `repos:` list in `.github/sync.yml` and push.