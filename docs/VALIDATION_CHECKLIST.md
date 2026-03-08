# Validation Checklist

This checklist ensures that PacketPuncture artifacts meet deterministic evidence standards.

---

# Artifact Integrity

Confirm the following:

- payload SHA-256 hash matches recorded hash
- signature file exists
- signature verifies successfully

---

# Receipt Ledger Integrity

Check that:

- sequence numbers increase correctly
- previous log hashes match
- ledger entries are append-only

---

# Transcript Validation

Verify that:

- transcript files exist
- recorded artifact hashes match actual files
- run summary references correct artifacts

---

# Deterministic Properties

Ensure that:

- artifact serialization is canonical
- JSON key ordering is stable
- newline normalization is correct

---

# Independent Verification

Confirm that artifacts can be verified on a separate machine without modification.

---

# Final Evidence Confidence

If all checks pass, the PacketPuncture artifacts can be considered valid deterministic evidence.
