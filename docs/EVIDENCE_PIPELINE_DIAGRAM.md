# PacketPuncture Evidence Pipeline Diagram

This document explains the PacketPuncture evidence pipeline from event creation through verification.

It is intended to give developers, researchers, and auditors a quick visual understanding of how PacketPuncture produces deterministic network evidence artifacts.

---

# High-Level Pipeline

```text
┌─────────────────────────────┐
│ 1. Packet / Event Observed  │
│    packetpuncture event     │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│ 2. Canonical Payload Build  │
│    canonical JSON bytes     │
│    UTF-8 no BOM + LF        │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│ 3. Commit Hash Derivation   │
│    SHA-256(payload bytes)   │
│    => commit_hash           │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│ 4. Sign Message Construction│
│    commit.sig.v1 text       │
│    schema / hash / key info │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│ 5. Detached Signature       │
│    ssh-keygen -Y sign       │
│    => .sig artifact         │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│ 6. Local Pledge             │
│    append neverlost.ndjson  │
│    sequence + prev_log_hash │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│ 7. Optional Transport /     │
│    Witness Duplication      │
│    nfl.ingest.v1 envelope   │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│ 8. Verification / Replay    │
│    recompute + verify sig   │
│    verify ledger linkage    │
└─────────────────────────────┘
