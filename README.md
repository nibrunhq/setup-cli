# Set up the nibrun CLI

Install and cache `nib` in a GitHub Actions workflow:

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

Replace `<commit-sha>` with a reviewed commit from this repository. `version` is
required and takes an exact [CLI release tag](https://github.com/ilbertt/nibrun/releases),
including its `cli-v` prefix.

The Action passes the version to the [nibrun installer](https://nibrun.com/install.sh)
as `NIB_VERSION` and adds its installation directory to `PATH`. The cache contains
only the CLI executable and is keyed by release tag, operating system and
architecture. The installer checks the installed version after restoring the
cache and downloads the binary when needed.

Supported runners are Linux x64, Linux ARM64 and macOS ARM64. The Action only
sets up the CLI; invoke `nib` in subsequent workflow steps.
