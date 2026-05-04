# Submitting an OAP implementation listing

## Checklist

- [ ] I have generated an Ed25519 keypair, published the public key in my `/.well-known/did.json`, and signed my Conformance Receipt with the corresponding private key.
- [ ] My implementation publishes a valid OAP Manifest at `/.well-known/oap-tool.json` and the manifest's `tool.did` matches the listing's `tool_did`.
- [ ] My Conformance Receipt is reachable at the URL in `conformance_receipt_uri` and its SHA-256 matches `conformance_receipt_sha256`.
- [ ] My Receipt's signature value is NOT a placeholder. Placeholder signatures (RFC 0019 Section 7.3) are rejected by the CI gate.
- [ ] My Receipt's `validity.not_after` is in the future and at most 90 days after `issued_at`.
- [ ] (L4 only) My Receipt carries at least one peer-witness signature from another currently-conformant L4+ implementation listed in this Registry.
- [ ] (L5 only) My Receipt carries at least three independent peer-witness signatures, no two from the same controlling organization.
- [ ] My DID's domain is at least 30 days old, OR I have set `provisional: true`.

## Notes for the reviewer

(describe anything unusual here)

## Re-issuance? Revocation?

If this PR is re-issuing an existing listing, link the PR that added the previous Receipt. If this PR is revoking a Receipt, follow the revocation format in RFC 0026 Section 5 instead and submit under `revocations/`.
