# Policy Packs for GhostGuard

**Pre-written, behavior-tested governance rule sets for agent jobs** — in
GhostGuard's real policy format, each shipped with a test suite that proves
every rule fires as designed, run against the real GhostGuard engine, not a
description of it.

A policy *engine* is not a policy. Writing good rules is the hard part:
tier semantics (strictest verdict wins), fail-closed edges, locked
team-layer rules, initiator discipline. These packs are ours, already
written and proven, so an agent can post, shop, or triage an inbox safely
without its operator learning the policy language first.

By **Ghost Developer Studio**. Part of the
[GhostGuard](https://github.com/littlestjames82-sys/ghostguard) family.
MIT licensed. Pricing (in `PLAN.md`) is **DRAFT**.

## The catalog — 8 packs, 89 behavior checks, all green

| Pack | Governs | Locked "never" rules |
| --- | --- | --- |
| `packs/social-poster/` | An agent that reads, drafts, and posts to a social account | spending |
| `packs/inbox-assistant/` | An email/chat triage agent | deletes |
| `packs/shopping-agent/` | A purchasing/research agent (checkout asks, over-cap hands off) | subscriptions, gift cards |
| `packs/research-agent/` | A web-research agent | spend, delete |
| `packs/coding-agent/` | A coding agent (push/merge ask, deploy hands off) | secrets access, force-push, branch delete |
| `packs/agency-client-work/` | An agency agent working across client projects | cross-client data access |
| `packs/marketplace-seller/` | A marketplace seller agent | listing deletes, payout/bank changes |
| `packs/home-assistant/` | A home-assistant agent (non-owner initiators held stricter) | locks/security changes, recording deletes |

Each pack is a directory with exactly the same shape:

```
packs/<pack-name>/
  policy.json     the policy document — GhostGuard PolicyDoc format, data not code
  README.md       what it governs, the classification map, tuning knobs
  test/run.ts     behavior tests against the real engine
```

The same `policy.json` document is evaluated identically by the GhostGuard
engine (TypeScript) and by Agent Seatbelt's governor (Python) — one file
serves both runtimes.

## Running the tests

The suites import the GhostGuard engine source and run under the core
repo's `tsx`, so this repo expects the core as a sibling checkout — see
the layout note at the bottom of this README. Then:

```sh
npm test    # runs all eight pack suites in sequence
```

See `PLAN.md` for the pack format definition and `REPORT.md` for the
Oct 10, 2026 build report with per-pack results.

## Repository layout note

This add-on imports the GhostGuard core engine from a **sibling checkout**:
`../../ghostguard/dist/index.js` (its source and/or tests do; nothing in the
core is modified). To run it, clone the core next to this repo so both folders
share a parent directory:

```sh
git clone https://github.com/littlestjames82-sys/ghostguard
git clone https://github.com/littlestjames82-sys/policy-packs
# build the core once so dist/ exists:
cd ghostguard && npm run build && cd ..
cd policy-packs && npm test
```

Part of the GhostGuard family by **Ghost Developer Studio**.
