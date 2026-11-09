# .github

Default community health files for repositories owned by [thefiredev-cloud](https://github.com/thefiredev-cloud), the home of Kodros and TheFireDev.

GitHub uses a file from this repository when a repository does not have its own copy:

- [SECURITY.md](SECURITY.md): how to report a vulnerability privately
- [CONTRIBUTING.md](CONTRIBUTING.md): how to propose changes

The profile page itself lives in [thefiredev-cloud/thefiredev-cloud](https://github.com/thefiredev-cloud/thefiredev-cloud).

<!-- arch:begin -->
## Architecture

Organization defaults: security and contributing policy, plus a reusable gitleaks secret-scan workflow.

```mermaid
flowchart LR
  caller{{"Any org repo<br/>calls the workflow"}}:::ext
  wf["Reusable workflow<br/>gitleaks scan"]:::job
  cfg[("Shared gitleaks.toml<br/>repo-local file wins")]:::store
  policy["SECURITY + CONTRIBUTING<br/>org defaults"]:::doc
  reporter(["Reporter / contributor"]):::actor
  caller -->|"workflow_call"| wf
  wf -->|"reads"| cfg
  reporter -->|"reads"| policy
  classDef actor fill:#fde68a,stroke:#b45309,color:#111827
  classDef doc fill:#fed7aa,stroke:#c2410c,color:#0b1220
  classDef ext fill:#e5e7eb,stroke:#4b5563,color:#0b1220,stroke-dasharray:4 3
  classDef job fill:#fbcfe8,stroke:#be185d,color:#0b1220
  classDef store fill:#bbf7d0,stroke:#15803d,color:#0b1220
```

[Full architecture](docs/ARCHITECTURE.md) · Hi-res: [SVG](docs/architecture/whiteboard.svg) · [PNG 3x](docs/architecture/whiteboard@3x.png) · [dark PNG](docs/architecture/whiteboard.dark@3x.png) · [Explorable (Archify)](docs/architecture/dot-github.archify.html) · [Graphify report](docs/architecture/graphify/GRAPH_REPORT.md)
<!-- arch:end -->

## Secret scan

Call the reusable workflow from a repo's workflow file:

```yaml
jobs:
  gitleaks:
    uses: thefiredev-cloud/.github/.github/workflows/gitleaks-reusable.yml@main
```

- Optional input `gitleaks-version`: plain `x.y.z`, default `8.21.2`.
- A repo-local `.gitleaks.toml` replaces the shared `gitleaks/gitleaks.toml`.
- Pull requests scan the base..head range. Other events scan full history.
- Local hook: install `pre-commit`, copy `gitleaks/pre-commit-config.example.yaml` to `.pre-commit-config.yaml`, then run `pre-commit install`. It needs `gitleaks` on PATH.

## License

All rights reserved. See [LICENSE](LICENSE). Licensing questions and contact: [tanner@kodros.ai](mailto:tanner@kodros.ai).
