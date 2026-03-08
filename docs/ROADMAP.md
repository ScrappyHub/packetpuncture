# PacketPuncture Roadmap

The roadmap is divided into deterministic milestones.

---

# Phase 1 — Tier-0 Instrument

Goal:

Standalone deterministic evidence instrument.

Capabilities:

- event commitment generation
- signature verification
- append-only receipt ledger
- deterministic transcript evidence
- standalone full runner

---

# Phase 2 — Verification Surface

Add standalone verification commands.

Capabilities:

- verify commitment payloads
- verify signatures
- verify receipt logs
- verify transcript bundles

---

# Phase 3 — Deterministic Testing

Introduce strong validation tools.

Capabilities:

- golden test vectors
- negative verification vectors
- stress harness
- reproducible replay tests

---

# Phase 4 — Packet Capture Ingestion

Introduce packet capture support.

Capabilities:

- ingest PCAP files
- convert packet streams to events
- deterministic packet evidence extraction

---

# Phase 5 — Ecosystem Integration

Optional integrations.

Examples:

- IDS/IPS engines
- governed infrastructure systems
- distributed evidence aggregation

Standalone operation will always remain the primary design goal.
