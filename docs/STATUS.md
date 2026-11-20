# Status

Last reviewed: 2026-11-20 (github-audit pass 02, from the files and git log; nothing was executed).

## What works

- `schema.sql` is a complete, readable schema for five tables with indexes. **(inference)** It is probably loadable with `psql`, but it was not run.
- `init_db.sh` is a small wrapper around `psql -f schema.sql`.

## What's broken or unknown

- `npm test` cannot pass: the five specs require `lib/models/*.js`, and there is no `lib/` directory.
- `mocha` is not in `package.json` dependencies.
- Only `transactions` has a Sequelize migration. The other four tables exist only in `schema.sql`.
- `index.js` is empty, so `require('ripple-historical-database')` exports nothing.
- `init_db.sh` hard-codes the author's Postgres user and a `test_db` database name.
- `package.json` has an empty `author` field. The dependency versions are from 2014 and have not been checked against current security advisories.

## What's next

Nothing is planned. If Steven wants to revive it: add the models in `lib/models`, align the migration with `schema.sql`, move to a current Sequelize and Node, and decide whether this is still wanted now that rippled and its ecosystem have changed.

## Not yet from the standard

Remaining baseline items:

- CONTRIBUTING.md
- SECURITY.md
- `.editorconfig`
- `.github` issue and pull request templates
- Dependabot configuration
- `ci.yml` with gitleaks
- Rename the default branch from `master` to `main`
- CloudEvents catalog
- Product ONE-PAGER

Added in this pass: README.md, AGENTS.md, CLAUDE.md, docs/STATUS.md and LICENSE (ISC, matching the `license` field already in `package.json`).
