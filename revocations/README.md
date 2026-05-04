# Revocations

Append-only directory of revoked Conformance Receipts. Defined in [RFC 0026 Section 5](https://github.com/openagentprotocol-OAP/oap-spec/blob/main/rfcs/RFC-0026-registry-protocol.md#5-revocation-format).

## File naming

Each file MUST be named `<slug>-<receipt-sha256>.json` so that revocations are addressable by both implementation slug and the exact Receipt bytes they invalidate. The CI revocation evaluator enforces the filename pattern.

## Schema

Every file in this directory is validated against [`schemas/revocation.schema.json`](../schemas/revocation.schema.json) by the `schema` job in `.github/workflows/validate.yml`.

## Two valid signing paths

A revocation is accepted only if at least one of the following holds:

1. **Self-revocation.** `signature.value` verifies, using Ed25519, against a `verificationMethod` published in the DID Document of `revoked_by_did`. For self-revocation, `revoked_by_did` MUST equal the listing's `tool_did`.

2. **Forced (Quorum) revocation.** `peer_witness_signatures` contains at least three entries that meet ALL of:
   - Three or more distinct `witness_did` values.
   - Three or more distinct controller domains (derived from `did:web` hostnames).
   - Each witness DID is currently a live L4+ implementation in this Registry.
   - Each witness signature verifies against a `verificationMethod` in that witness DID's DID Document.

The revocation evaluator job in CI enforces both paths.

## Effect

Once a revocation file with a `revoked_at` timestamp in the past is merged, the CI revocation evaluator additionally checks every entry in `implementations/`. Any listing whose `conformance_receipt_sha256` matches the `revoked_receipt_sha256` of an effective revocation fails the validation gate and cannot be re-merged until the implementation publishes a new Receipt at a new URL and updates the listing.

## Allowed reasons

- `key_compromise`: the implementation's signing key has been disclosed or its custody can no longer be verified.
- `manifest_non_conformance`: the live Manifest no longer matches the claims in the Receipt.
- `superseded`: the implementation has issued a newer Receipt and is voluntarily withdrawing the older one.
- `voluntary_withdrawal`: the implementation is leaving the Registry.
- `dispute_resolved_against`: a community dispute has resolved against the implementation.
