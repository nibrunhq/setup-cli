# Set up the nibrun CLI

Install `nib` in a GitHub Actions workflow:

```yaml
jobs:
  example:
    runs-on: ubuntu-latest
    steps:
      - uses: nibrunhq/setup-cli@v1
        with:
          version: 2026.10.13-1
      - run: nib --version
```

`@v1` follows updates in the Action's v1 release series.

| Input | Type | Required | Default | Meaning |
| --- | --- | --- | --- | --- |
| `version` | string | No | `latest` | An exact CLI version (bare, `v`-prefixed or `cli-v`-prefixed), or `latest` for the newest CLI release. |

`2026.10.13-1`, `v2026.10.13-1` and `cli-v2026.10.13-1` select the same
[CLI release](https://github.com/ilbertt/nibrun/releases).

Omit `version` or set it to `latest` to let the official installer select the
newest release. Empty values also use the installer's default. These selections
are not cached, so later runs can receive newer releases.

For exact versions, the cache contains the CLI executable and is keyed by
the supplied version, operating system and architecture. An exact cache hit
skips fetching the installer when the executable is present. A cache miss or incomplete cache
runs the [official installer](https://raw.githubusercontent.com/ilbertt/nibrun/main/packages/cli/install.sh)
with the selected release in `NIB_VERSION` and its directory in `NIB_INSTALL_DIR`.
The Action adds that directory to `PATH` for subsequent steps.

Supported runners are Linux x64, Linux ARM64 and macOS ARM64. The Action only
sets up the CLI; invoke `nib` in subsequent workflow steps.
