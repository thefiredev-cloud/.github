# Security

Thanks for taking security seriously as this project grows.

## Reporting a vulnerability

**Do not** open a public GitHub issue for security bugs.

Email **tanner@meshvault.ai** with:

- What you found and where (repo, file, URL)
- Steps to reproduce
- Impact (read-only vs RCE vs secrets)

We aim to acknowledge within **72 hours** and patch or document mitigations for confirmed issues.

## Scope

| In scope | Out of scope |
|----------|----------------|
| This repository’s code and docs | Social engineering, physical access |
| Obvious secret leaks in git history | Third-party services (report to vendor) |
| Dependency CVEs with exploit path | Generic “scan my whole org” without PoC |

## Safe harbor

Good-faith research that follows this policy and avoids privacy destruction, service disruption, or data exfiltration beyond minimal proof is appreciated.

## Hardening (operators)

- No real API keys, tokens, or `.env` files in git
- Rotate anything accidentally committed immediately
- Prefer private repos for client installs and production monorepos

**MeshVault** — [meshvault.ai](https://meshvault.ai)
