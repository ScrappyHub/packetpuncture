# PacketPuncture Security Model

PacketPuncture focuses on producing verifiable evidence artifacts rather than performing network inspection.

---

# Integrity

Artifact integrity is enforced through SHA-256 hashing.

Every artifact produced by PacketPuncture is hashed and verifiable.

---

# Authenticity

Authenticity is enforced through cryptographic signatures.

OpenSSH signing is used to produce detached signatures.

---

# Append-Only Ledger

Receipt logs are append-only.

Ledger entries include:

- sequence number
- previous log hash
- artifact hashes

This creates a verifiable chain of records.

---

# Independent Verification

Artifacts can be verified without relying on the original system.

Verification requires only:

- the payload
- the signature
- the receipt ledger

---

# Deterministic Outputs

PacketPuncture enforces deterministic serialization rules.

This prevents ambiguity in artifact generation.

Deterministic outputs allow artifacts to be reproduced across machines.
