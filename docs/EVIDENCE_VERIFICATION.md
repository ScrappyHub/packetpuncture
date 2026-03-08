# Evidence Verification

PacketPuncture artifacts are designed for independent verification.

Verification requires only the generated artifacts.

---

# Verification Process

To verify a PacketPuncture event:

1. Verify the payload hash
2. Verify the signature
3. Verify the receipt ledger entry
4. Verify the transcript evidence bundle

---

# Step 1 — Verify Payload

Compute the SHA-256 hash of the payload file.

Confirm it matches the hash recorded in the receipt log.

---

# Step 2 — Verify Signature

Use OpenSSH verification.

Example:

ssh-keygen -Y verify \
-n packetpuncture \
-f allowed_signers \
-I <principal> \
-s payload.sig < payload

Successful verification confirms authenticity.

---

# Step 3 — Verify Receipt Ledger

Receipt entries must satisfy:

- correct sequence number
- correct previous log hash
- matching payload hashes

This ensures the append-only ledger integrity.

---

# Step 4 — Verify Transcript

Transcript bundles include:

- run summary
- artifact hashes

Verify that:

- transcript hashes match files
- run summary references correct artifacts

---

# Independent Verification

All verification steps can be performed offline.

No central authority is required.

This enables deterministic evidence validation in air-gapped environments.
