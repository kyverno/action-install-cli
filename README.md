# action-install-cli GitHub Action

This action enables you to install Kyverno CLI.

For a quick start guide on the usage of Kyverno CLI, please refer to https://kyverno.io/docs/kyverno-cli/.

# Usage

This action currently supports GitHub-provided Linux, macOS and Windows runners (self-hosted runners may not work).

Add the following entry to your Github workflow YAML file:

```yaml
uses: kyverno/action-install-cli@main
with:
  release: 'v1.9.5' # optional
```

Example using a pinned version:

```yaml
jobs:
  example:
    runs-on: ubuntu-latest

    permissions: {}

    name: Install Kyverno CLI
    steps:
      - name: Install Kyverno CLI
        uses: kyverno/action-install-cli@main
        with:
          release: 'v1.9.5'
      - name: Check install
        run: kyverno version
```

Example using the default version:

```yaml
jobs:
  example:
    runs-on: ubuntu-latest

    permissions: {}

    name: Install Kyverno CLI
    steps:
      - name: Install Kyverno CLI
        uses: kyverno/action-install-cli@main
      - name: Check install
        run: kyverno version
```

If you want to install Kyverno CLI from its main version by using `go install` under the hood, you can set `release` as `main`.
Once you did that, Kyverno CLI will be installed via `go install` which means that please ensure that go is installed.

Example of installing Kyverno CLI via `go install`:

```yaml
jobs:
  example:
    runs-on: ubuntu-latest

    permissions: {}

    name: Install Kyverno CLI via go install
    steps:
      - name: Install go
        uses: actions/setup-go@v4
        with:
          go-version: '1.20'
          check-latest: true
      - name: Install Kyverno CLI
        uses: kyverno/action-install-cli@main
        with:
          release: 'main'
      - name: Check install
        run: kyverno version
```

### Optional Inputs

The following optional inputs:

| Input | Description |
| --- | --- |
| `release` | `kyverno` version to use instead of the default. |
| `install-dir` | directory to place the `kyverno` binary into instead of the default (`$HOME/.kyverno`). |
| `use-sudo` | set to `true` if `install-dir` location requires sudo privs. Defaults to false. |

## Security

Should you discover any security issues, please refer to Kyverno's [security process](https://github.com/kyverno/kyverno/blob/main/SECURITY.md)