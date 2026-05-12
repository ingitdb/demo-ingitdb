# demo-ingitdb

A collection of demo inGitDB databases — each module is an independent example you can explore, copy, or use as a starting point.

[![inGitDB](https://github.com/ingitdb/demo-ingitdb/actions/workflows/ingitdb.yml/badge.svg)](https://github.com/ingitdb/demo-ingitdb/actions/workflows/ingitdb.yml)

## Pick a module

| Module | Size | What it shows |
|--------|------|---------------|
| [`modules/todo`](modules/todo) | 3 collections | Minimal starter — one-record-per-file, dictionary-of-records, foreign keys, a named view. |
| [`modules/geo`](modules/geo) | 1 collection | Multi-language records using `map[locale]string` and locale shortcuts. |
| [`modules/commerce`](modules/commerce) | 15 collections | Real-world CRM/ordering schema — FKs, subcollections, enums, regex, referential integrity. |

Start with `todo` if you're new. Jump straight to `commerce` if you want to see inGitDB on a non-trivial schema.

## How the modules compose

Each module is itself a valid inGitDB database with its own `.ingitdb/` config. The repo-level [`.ingitdb/root-collections.yaml`](.ingitdb/root-collections.yaml) imports them as namespaces:

```yaml
geo.*: modules/geo
todo.*: modules/todo
commerce.*: modules/commerce
```

So when you query this repo, collection IDs look like `todo.tasks`, `geo.countries`, `commerce.orders`. Each module also works standalone — `cd modules/todo && ingitdb validate` validates just that module.

## Run locally

```bash
# Install the CLI (Go required):
go install github.com/ingitdb/ingitdb-cli/cmd/ingitdb@latest

# Validate the whole repo:
ingitdb validate

# Or one module:
ingitdb validate --path modules/todo
```

The repo's [GitHub Actions workflow](.github/workflows/ingitdb.yml) runs `validate` and `materialize` on every push.

## Browsing data on GitHub

Every record is a plain YAML/JSON file. `git blame` and `git log` give you a full audit trail with zero extra infrastructure. For richer UIs, see [DataTug.app](https://datatug.app/#ingitdb=github.com/ingitdb/demo-ingitdb).

## Contributing a new module

1. Create `modules/<name>/.ingitdb/{settings.yaml,root-collections.yaml}`.
2. Add its collections under `modules/<name>/`.
3. Add `<name>.*: modules/<name>` to the root [`.ingitdb/root-collections.yaml`](.ingitdb/root-collections.yaml).
4. Add a row to the table above.
5. Run `ingitdb validate` and open a PR.
