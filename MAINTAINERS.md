# OAP Registry Maintainers

Maintainers of `oap-registry` are recruited from the [`oap-spec` Maintainer roster](https://github.com/openagentprotocol-OAP/oap-spec/blob/main/governance/MAINTAINERS.md). The procedure to become a Maintainer is the same: open a Pull Request adding your handle to the table below, link to your contributions in either repository, and wait for confirmation by at least three current Maintainers from at least three distinct organizations.

| GitHub handle | Organization | Term started |
|---|---|---|
| `@till-fengler` | BEEP Technologies UG | 2026-05 |

## Bootstrap

While the active Maintainer count is below three, the bootstrap quorum is the existing roster plus one approving review from a recognised independent contributor (defined in the README of the `oap-spec/governance/` directory).

## Responsibilities

* Review Pull Requests after CI passes.
* Merge listings and revocations that meet every check in [RFC 0026 Section 6](https://github.com/openagentprotocol-OAP/oap-spec/blob/main/rfcs/RFC-0026-registry-protocol.md#6-ci-validation-gate).
* Reject listings that fail any check, with a link to the failing check.
* Periodically prune expired listings.

Maintainers do NOT have authority to override CI failures. Branch protection on `main` requires CI to pass.
