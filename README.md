# RDC Cloud Actions

Install the [RDC Cloud CLI](https://docs.redredgroup.com/docs/rdc-cloud/cli-commands) (`rdc`) in GitHub Actions and add it to `PATH`.

## Usage

```yaml
steps:
  - uses: actions/checkout@v7

  - uses: redredgroup/rdc-cloud-actions@v1
    with:
      version: 0.0.4

  - run: rdc secret runtime --workspace <workspace-uuid> --group backend --environment production -- node server.js
    env:
      RDC_TOKEN: ${{ secrets.RDC_TOKEN }}
```

## Inputs

| Name | Default | Description |
| --- | --- | --- |
| `version` | `latest` | CLI version to install. Pin an exact version for reproducible builds. |
| `node-version` | `24` | Node.js version used to run the CLI. |

## Outputs

| Name | Description |
| --- | --- |
| `version` | Installed CLI version. |

## Authentication

Create an access token from **Access Token** in RDC Console and store it as a repository or environment secret. Pass it to steps that run `rdc` through the `RDC_TOKEN` environment variable. No `rdc login` is needed, and the CLI never saves this token.

The token's permissions, expiry and workspace IP access policies apply. GitHub-hosted runners do not use fixed IP addresses; if your workspace restricts secret access by IP, use a runner with a fixed outbound IP.

Keep the token out of command output and shell tracing (`set -x`).

## Notes

- This action runs `actions/setup-node`, so later steps in the same job use the selected Node.js version. Run your own `actions/setup-node` afterward if the job needs a different version.
- The CLI is installed from the public npm registry without running package install scripts.
- Supported on Linux, macOS and Windows runners.

## License

[MIT](LICENSE)
