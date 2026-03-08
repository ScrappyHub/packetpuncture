# PacketPuncture Evidence Model

PacketPuncture converts packet-related events into deterministic evidence artifacts.

Each event produces a chain of verifiable artifacts.

---

# Artifact Types

PacketPuncture generates the following artifacts.

## Event Payload

The canonical representation of the packet-related event.

Example contents:

- event type
- timestamp
- device identifier
- session identifier
- metadata

---

## Signature Message

A canonical message generated from the event payload.

This message is the exact content signed by the signing key.

---

## Detached Signature

The signature produced by OpenSSH signing.

This allows verification without modifying the original payload.

---

## Commitment Hash

A SHA-256 hash derived from the canonical payload.

This serves as the unique identifier for the commitment.

---

## Receipt Log Entry

A JSON entry appended to the pledge ledger.

The ledger provides an append-only record of commitments.

---

## Transcript Evidence

Evidence bundles generated during deterministic runs.

These bundles include:

- execution summary
- artifact hashes
- verification outputs

---

# Independent Verification

Anyone with access to the artifacts can verify:

- the payload
- the commitment hash
- the signature
- the receipt log integrity

No central authority is required.

---

# Deterministic Reproduction

Given identical inputs and signing keys, PacketPuncture should produce identical artifacts.

This property allows reproducible validation of network evidence.
