# AGENTS.md

Guidance for AI agents working in this repo. Humans: see [README.md](README.md).

## What this is

A dormant 2014 sketch (profile: `legacy`, baseline tier) of a Postgres/Sequelize database for Ripple ledger history. See [docs/STATUS.md](docs/STATUS.md) for the current state.

## Stack

- Node.js with npm. `package.json` pins nothing for the engine. The dependencies are 2014 versions: `sequelize` ^1.7.9, `sequelize-cli` ^0.2.2, `pg` ^3.3.0. mocha is used by the test script but is not listed in `package.json`.
- PostgreSQL for `schema.sql`.

## Layout

- `schema.sql`, `init_db.sh`: schema and loader script.
- `migrations/`: one Sequelize migration (`transactions`).
- `test/models/`: model specs. They require `lib/models/*.js`, which does not exist.
- `index.js`: empty.

## Commands

- Install: `npm install` (old dependency tree, may fail on a current Node).
- Test: `npm test` runs `mocha -R spec test/**/`. Known not to work today: mocha is not a declared dependency and the specs require missing `lib/models` files.
- Run: there is no application. `./init_db.sh` loads the schema into a local Postgres after you edit its user and database constants.

## Rules

- Add or update tests with every change.
- Never commit secrets (database passwords, connection strings, keys).
- Use Conventional Commits (`docs:`, `fix:`, `feat:`, `chore:`).
- Keep `docs/STATUS.md` current when behaviour or status changes.

## What agents may and may not do

- May: fix docs, add the missing baseline files listed in `docs/STATUS.md`, open pull requests.
- May not, without Steven: archive or delete the repo, publish a package, rewrite git history, change the license, or merge their own pull requests.
