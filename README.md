# HarvestShield

**Parametric crop-loss insurance for Stellar Soroban** — when a verified drought,
flood, or heat wave hits an enrolled field, the smart contract pays the farmer
automatically. No adjusters, no paperwork, no waiting.

HarvestShield gives smallholder cooperatives the tools to launch their own
index-based insurance products: onboard farmers, subscribe to weather and yield
oracles, define payout schedules, and let claims settle themselves.

Think of it as a crop-insurance vending machine for the parts of the world that
traditional insurers do not serve.

## Why HarvestShield

A single dry season can wipe out a smallholder's entire income. Conventional
insurance costs more to administer than it pays out, so farmers stay
uninsured. Parametric insurance inverts that economics:

- **Index triggers over claims adjusters** — a payout fires when an on-chain
  oracle value (rainfall deficit, heat degree-days, flood water level) crosses
  a contract threshold. Nothing for the farmer to prove.
- **Automatic settlement** — payout eligibility and amounts are computed on
  chain from verifiable data. Claims settle in minutes, not months.
- **Transparent by construction** — every policy, every oracle reading, and
  every payout is public on the ledger.
- **Cooperative-owned** — any cooperative can deploy its own policy registry,
  choose its own oracles, and set its own rates.

## Repository layout

```
harvest-shield/
├── contracts/            # Soroban contracts (policy registry, orchard, oracle adapter)
│   ├── policy-registry/  # create policies, enroll fields, settle payouts
│   ├── orchard/          # insurance-relevant crop data & thresholds
│   └── oracle-adapter/   # timestamped off-chain data ingestion & root hashing
├── apps/
│   ├── dashboard/        # cooperative / insurer admin dashboard (Next.js)
│   └── farmer-app/       # mobile-first farmer enrollment + claim view
├── oracles/              # data feed workers (weather APIs, index computation)
├── docs/                 # architecture, roadmap, API, deployment
├── CONTRIBUTING.md       # how to pick up an issue and ship it
└── .github/ISSUE_TEMPLATE/
```

## Quick start

### Prerequisites

- Rust stable + `wasm32-unknown-unknown` target
- Node.js 20+ and pnpm
- `soroban-cli` (for testnet deploys, optional)

### Build and test the contracts

```bash
cargo build --release --target wasm32-unknown-unknown -p policy-registry
cargo test --workspace
```

### Run the dashboard

```bash
pnpm install
pnpm --filter dashboard dev
```

Open http://localhost:3000 to see the cooperative admin view.

## Contribute

HarvestShield is explicitly built to be contributed to. Look for issues labeled
`good-first-issue` or `help-wanted`, or pick a roadmap item from
[`docs/ROADMAP.md`](docs/ROADMAP.md). Every issue follows a strict template
(problem → context → implementation → verification) so you always know what
"done" means. See [`CONTRIBUTING.md`](CONTRIBUTING.md).

## Community

- [Issues](https://github.com/chainNG/harvest-shield/issues) — bugs, features, bounty work
- [Discussions](https://github.com/chainNG/harvest-shield/discussions) — questions and product ideas
- [Stellar / Soroban](https://stellar.org) — the network this runs on

## License

MIT License. See [`LICENSE`](LICENSE).