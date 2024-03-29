# GitHub Action to install and setup goose

This github actions installs and sets up the [Goose](https://github.com/pressly/goose) migration tool binary.

## Example usage

```yaml
name: Migrate

on:
  push:
    branches: ['main']

jobs:
  migrate:
    name: Migrate
    runs-on: ubuntu-latest
    steps:
      - uses: actions/setup-go@v5
        with:
          go-version: '1.20.x'

      - uses: actions/checkout@v3

      - uses: mscno/setup-goose@v1

      - run: goose up
```

That's it! This workflow will run your migrations using goose.

The action works on Linux and macOS runners. If you'd like support for Windows runners, let us know!

## Select goose version to install
By default, pressly/setup-goose installs the latest released version of goose.

You can select a version with the version parameter:

```yaml
- uses: mscno/setup-goose@v1
  with:
    version: v0.14.1
```

To build and install goose from source using go install, specify version: `tip`.

## Running Migrations

goose is a database migration tool. You manage your database schema by creating incremental SQL or Go scripts.

After installing goose with this action, you can run your migrations with goose up:

```yaml
- uses: mscno/setup-goose@v1
- run: goose up
```


You can also run specific migrations with goose up-to <version>, roll back migrations with goose down, and more. See the goose documentation for more information.

## A note on versioning
The @v0.X in the uses statement refers to the version of the action definition in this repo.

Regardless of what version of the action definition you use, pressly/setup-goose will install the latest released version of goose unless otherwise specified with version:.
