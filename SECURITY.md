# Security Policy

## Reporting a vulnerability

**Do not open a public issue for a security problem.** The fund some of this
project's contributors rely on; handle reports privately.

Contact the maintainers by opening a private security advisory:

- GitHub: **Report a vulnerability** on the repository's *Security* tab.

Please include, when possible:

1. Affected contract endpoint(s) and version.
2. A minimal reproduction (can be synthetic / testnet).
3. Whether funds could be lost, and an estimate of the blast radius.

## Response

- Acknowledgment: 48 hours.
- Triage and fix plan: 5 business days (sooner for fund-loss severities).
- A fix is released before any public disclosure.

## Scope

- `contracts/` Soroban contract logic and authorization paths.
- Oracle ingestion and signature verification.
- Web app secrets handling and API routes.

Out of scope: general dependency CVEs flagged by automated bots; testnet-only
behavior with no mainnet funds.