# PacketPuncture Architecture

PacketPuncture is built as a deterministic evidence instrument.

The system converts packet-related events into cryptographically verifiable artifacts that can be independently validated.

The architecture is intentionally simple and deterministic.

---

# Evidence Pipeline

PacketPuncture follows a strict artifact pipeline.

Packet Event
    ↓
Canonical Message Generation
    ↓
Commitment Creation
    ↓
Detached Signature
    ↓
Append-Only Pledge Log
    ↓
Evidence Transcript Bundle

Each stage produces deterministic artifacts that can be verified independently.

---

# Core Components

## Event Input

PacketPuncture receives packet-derived events from:

- packet capture systems
- IDS/IPS engines
- network monitoring systems
- manual evidence creation

PacketPuncture itself does not need to perform packet inspection to produce evidence artifacts.

---

## Commitment Engine

The commitment engine:

- canonicalizes event data
- generates a signing message
- produces a commitment hash

This ensures event integrity.

---

## Signing Layer

Commitments are signed using:

OpenSSH `ssh-keygen -Y sign`

Detached signatures are generated to allow independent verification.

---

## Pledge Ledger

Each commitment is appended to a local receipt ledger.

Ledger characteristics:

- append-only
- deterministic JSON
- SHA-256 verifiable
- reproducible across systems

---

## Evidence Transcripts

Each full run generates an evidence transcript bundle.

Example:

proofs/transcripts/pp_full_green_v1/

This contains:

- summary evidence
- artifact hashes
- execution results

These transcripts allow reproducible validation of the run.

---

# Deterministic Guarantees

PacketPuncture enforces strict deterministic rules:

- UTF-8 encoding with no BOM
- LF newline normalization
- canonical JSON serialization
- SHA-256 artifact hashing
- append-only receipt logs

These rules guarantee reproducibility across machines.

---

# Standalone Operation

PacketPuncture is designed to operate fully standalone.

The instrument does not require:

- network access
- centralized services
- external verification systems

Optional ecosystem integrations may exist but are not required for core operation.

---

# Future Integration

PacketPuncture may later integrate with:

- governed operating systems
- IDS/IPS systems
- network security platforms

However the standalone deterministic instrument is always the primary design goal.
