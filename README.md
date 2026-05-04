# OAP Registry

Append-only public registry of OAP Conformance Receipts. Defined in [RFC 0026](https://github.com/openagentprotocol-OAP/oap-spec/blob/main/rfcs/RFC-0026-registry-protocol.md).

## What this is

This repository is the canonical transparency log for the Open Agent Protocol. Every Conformance Receipt referenced from a publicly listed OAP implementation is anchored here through a Pull Request whose merge commit is the Receipt's anchor.

There is no certification authority. There is no fee. There is no application process. The merge gate is mechanical: signatures must verify, the Manifest must be reachable, peer witnesses (for L4 and L5) must currently themselves hold L4+ Receipts, and the implementation's domain must be at least 30 days old (sybil filter).

## Repository layout

```
implementations/<slug>.json        one file per implementation
revocations/<slug>-<receipt-hash>.json   one file per revocation event
peer-witnesses/<witness-slug>.json       optional witness directory
schemas/implementation.schema.json       JSON Schema for listings
.github/workflows/validate.yml           CI gate (RFC 0026 Section 6)
```

## How to submit

1. Generate a signed Conformance Receipt for your implementation. See the [Certification page](https://openagentprotocol.eu/certification) for the walkthrough.
2. Publish the Receipt at a stable URL on your own domain.
3. Fork this repository.
4. Add `implementations/<your-slug>.json` matching `schemas/implementation.schema.json`.
5. Open a Pull Request. The CI gate runs every check in [RFC 0026 Section 6](https://github.com/openagentprotocol-OAP/oap-spec/blob/main/rfcs/RFC-0026-registry-protocol.md#6-ci-validation-gate).
6. A Maintainer reviews and merges if everything passes. The merge commit is your anchor.
7. Re-submit before `expires_at` (max 90 days) to remain listed.

## Mirror this repository

```
git clone https://github.com/openagentprotocol-OAP/oap-registry
git verify-commit HEAD
```

Mirrors are encouraged. The canonical state is reconstructible from any mirror through standard Git tooling. A Verifier MUST validate against its own clone.

## Maintainers

See `MAINTAINERS.md`. Maintainer rights are recruited from the `oap-spec` Maintainer roster.

## License

* Listings (data): CC0.
* Schemas, workflows, and source code: Apache 2.0.
