# ripple-historical-database

A SQL database (Postgres, through Sequelize) meant to be the canonical source of historical data in Ripple.

> **Status: dormant since July 2014.** This is an early sketch from Steven's 2014 Ripple Labs era: a Postgres schema, a first migration and empty spec scaffolding for the models. It never grew a working data layer. Read it as a design record, not a library to depend on.

## What is in here

| Path | What it is |
|---|---|
| `schema.sql` | Postgres schema: `ledgers`, `transactions`, `accounts`, `account_transactions` and `ledger_transactions`, with indexes. It drops and recreates everything when run. |
| `init_db.sh` | Runs `schema.sql` through `psql`. |
| `migrations/20140710103313-create-transactions.js` | A Sequelize migration that creates the `transactions` table (the only table with a migration). |
| `test/models/` | Mocha specs that build each Sequelize model. |
| `index.js` | Empty. |

## Install

Needs Node.js, npm and a local Postgres. The dependencies are from 2014 (`sequelize` ^1.7.9, `sequelize-cli` ^0.2.2, `pg` ^3.3.0), so expect to need an old Node version.

```
npm install
```

## Usage

Create the tables from the schema file:

```
createdb test_db
./init_db.sh
```

`init_db.sh` has its Postgres user, database name and schema file at the top of the script. Edit `PSQL_USER` and `PSQL_DATABASE` first: they are set to the author's own values (`stevenzeiler` and `test_db`).

## Config

There are no environment variables. All settings are the constants at the top of `init_db.sh`.

## How it works

`schema.sql` models ledgers, transactions and accounts as numbered rows, with join tables (`account_transactions`, `ledger_transactions`) so you can ask for the history of one account or one ledger. Hashes are stored as `bytea`. The Sequelize migration describes the `transactions` table (type enum, from account, sequence, ledger sequence, hash, status, raw and meta blobs).

## Status

- `npm test` runs `mocha -R spec test/**/`. The specs require `lib/models/*.js`, which do not exist in the repo, so the tests cannot pass as it stands. Nothing was run in this pass.
- No data is loaded and no code reads from rippled. See [docs/STATUS.md](docs/STATUS.md) for details and what is missing.

## License

ISC, as declared in `package.json`. See [LICENSE](LICENSE).
