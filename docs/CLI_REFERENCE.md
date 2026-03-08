# CLI Reference

PacketPuncture provides command-line scripts for generating and verifying evidence artifacts.

---

# Full Runner

_RUN_pp_full_green_v1.ps1

Runs the full deterministic pipeline:

- signing selftest
- event commitment
- pledge ledger entry
- transcript evidence generation

Successful execution prints:

PP_FULL_GREEN_OK

---

# Commit Command

pp_commit_v1.ps1

Creates a commitment for a packet-derived event.

Parameters include:

- event type
- device identifier
- session identifier
- signing key path

Outputs include:

- commitment payload
- signature message
- detached signature

---

# Local Pledge

pp_pledge_local_v1.ps1

Appends the commitment to the receipt ledger.

This creates an append-only record of the event.

---

# Verification Tools

Verification tools will allow investigators to:

- verify signatures
- verify commitment hashes
- verify receipt chain integrity
- verify transcript artifacts

---

# Usage Philosophy

Commands are intentionally simple and deterministic.

Each command should produce artifacts that can be independently verified.
