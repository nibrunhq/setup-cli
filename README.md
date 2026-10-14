# Set up the nibrun CLI

Install `nib` in a GitHub Actions workflow:

```yaml
jobs:
  example:
    runs-on: ubuntu-latest
    steps:
      - uses: nibrunhq/setup-cli@<commit-sha>
        with:
          version: cli-v2026.10.13-1
      - run: nib --version
```

Replace `<commit-sha>` with a reviewed commit from this repository.

| Input | Type | Required | Default | Meaning |
| --- | --- | --- | --- | --- |
| `version` | string | No | `latest` | An exact [CLI release tag](https://github.com/ilbertt/nibrun/releases), including its `cli-v` prefix, or `latest` for the newest CLI release. |

Omit `version` or set it to `latest` to let the official installer select the
newest release. Empty values also use the installer's default. These selections
are not cached, so later runs can receive newer releases.

For exact release tags, the cache contains the CLI executable and is keyed by
release tag, operating system and architecture. An exact cache hit skips fetching
the installer when the executable is present. A cache miss or incomplete cache
runs the [official installer](https://raw.githubusercontent.com/ilbertt/nibrun/main/packages/cli/install.sh)
with the selected release in `NIB_VERSION` and its directory in `NIB_INSTALL_DIR`.
The Action adds that directory to `PATH` for subsequent steps.

Supported runners are Linux x64, Linux ARM64 and macOS ARM64. The Action only
sets up the CLI; invoke `nib` in subsequent workflow steps.
