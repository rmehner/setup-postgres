# setup-postgres

Faster than fast setup for postgresql in a Github action.

# Features

- [x] Installs postgresql binaries (in PATH) for use in steps, fast!
- [x] Starts a postgresql server in fast-mode*, fast!
- [x] Configures environment variables for use in steps, fast!
- [x] It's fast! >10x faster install and setup than other actions, complete in ~1-2 seconds!

See our `Test action.yml` steps [here](https://github.com/bmizerany/setup-postgres/actions) for comparison.

# Usage

```yaml
steps:
  # ...
  - uses: bmizerany/setup-postgres@v3
  - run: psql 'SELECT 1'
```

That's it!

## Supported OSs and Architectures

This action supports all OSs and architectures that Github actions supports; at
the time of writing.

## Supported Versions

A version may be specified in the form of `X.Y.Z` where `X`, `Y`, and `Z` are
integers. The version must be a valid version of postgresql that is available
from the [embedded postgres project](https://github.com/zonkyio/embedded-postgres).

A list of supported versions can be found [here](https://repo1.maven.org/maven2/io/zonky/test/postgres/embedded-postgres-binaries-linux-amd64/).

## Environment variables

The action will set the following environment variables for subsequent steps:

| Name | Description |
| --- | --- |
| `PGHOST` | The host to connect to (default: `localhost`) |
| `PGPORT` | The port to connect to (default: `5432`) |
| `PGUSER` | The user to connect as (default: `postgres`) |
| `PGPASSWORD` | The password to connect with (default: `postgres`) |
| `PGDATABASE` | The database to connect to (default: `postgres`) |
| `PGDATA` | The data directory for the running postgres instance |
| `DATABASE_URL` | The DSN that can be used to connect to the database |

> NOTE: `DATABASE_URL` is in the DSN form (e.g. `dbname=postgres user=postgres
> ...`) which is accepted my most postgresql clients, drivers, ORMs, etc. It
> was chosen over an actual URL because it is more flexible, and easier to
> override settings by simply appending new settings to the string.
>
> Users that want a URL can build one like: `postgresql://$PGUSER:$PGPASSWORD@$PGHOST:$PGPORT/$PGDATABASE`


## Inputs

| Name | Description | Default |
| --- | --- | --- |
| `version` | The version of postgresql to install | `17.2.0` |

## Outputs

Outputs are provided for use in configuring other steps in a workflow. It is
assumed most users will not need them for normal use, and instead can rely on
the environment variables set by this action.

| Name | Description |
| --- | --- |
| `dsn` | The DSN that can be used to connect to the database |
| `data` | The data directory for the running postgres instance |

## Fast-mode

This action runs postgresql in "fast-mode" which is a mode that disables `fsync`
and `full_page_writes`. This is not recommended for production use, but is great
for CI/CD environments where you want to get up and running quickly, and for
tests to run lightning fast.

# Credits

This is possible thanks to the [embedded postgres project](https://github.com/zonkyio/embedded-postgres)
which provides pre-built binaries for many versions of postgresql. Please
consider supporting them if you find this action useful.

This is obviously most possible because of the hard work of the postgresql
community. Thank you!

# Contributing

Please open an issue for any feature requests, bugs, or questions. Large PRs
(e.g. new features) should be discussed in an issue first. Small PRs for bug
fixes, typos, etc are welcome without an issue.

Also, be nice, or else.
