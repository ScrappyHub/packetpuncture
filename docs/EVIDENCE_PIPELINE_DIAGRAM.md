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
Artifact Flow
packet-derived event
        │
        ▼
commit.payload.<commit_hash>.json
        │
        ├── sha256(payload) = commit_hash
        │
        ▼
commit.sigmsg.<commit_hash>.txt
        │
        ▼
commit.sigmsg.<commit_hash>.txt.sig
        │
        ▼
neverlost.ndjson append-only pledge record
        │
        ▼
nfl.ingest.<commit_hash>.json   (optional duplication / witness handoff)
PacketPuncture Tier-0 Standalone Flow

PacketPuncture is Tier-0 standalone first.

That means the core valid pipeline is:

event
  -> canonical payload
  -> commit hash
  -> detached signature
  -> local append-only pledge
  -> deterministic receipt

NFL duplication and later GOS integration are downstream surfaces, not prerequisites for PacketPuncture correctness.

Commit Construction Diagram
Input fields
  producer_instance
  event_type
  device_id
  session_id
  watchtower_commit_hash
  content_ref
  strength
  policy_tags
  notes_ref
        │
        ▼
ordered payload object
        │
        ▼
canonical JSON serialization
        │
        ▼
SHA-256
        │
        ▼
commit_hash
Signature Construction Diagram
commit_hash
principal
key_id
producer
        │
        ▼
commit.sig.v1 message text
        │
        ▼
ssh-keygen -Y sign -n commitment
        │
        ▼
detached signature file
Local Pledge Ledger Model

Each local pledge appends one new canonical NDJSON line.

previous neverlost.ndjson bytes
        │
        ▼
sha256(previous log bytes)
        │
        ▼
local_prev_log_hash
        │
        ▼
new pledge record:
  schema
  time_utc
  action
  ok
  commit_hash
  local_sequence_number
  local_prev_log_hash
  payload.path
  payload.sha256
  producer_sig.path
  producer_sig.sha256
        │
        ▼
append to neverlost.ndjson

This creates an append-only local chain.

Verification Model

Verification must be non-mutating.

payload file
  -> recompute sha256
  -> compare to expected commit hash

signature file
  -> verify detached signature against sig message

pledge log
  -> validate append-only linkage
  -> validate sequence continuity
  -> validate prev_log_hash chain

Verification must never repair or rewrite artifacts.

Any repair must be a separate explicit action with its own receipts.

Deterministic Evidence Outputs

PacketPuncture aims to produce the following stable evidence outputs:

canonical payload JSON

canonical sign message text

detached signature file

append-only pledge ledger record

optional transport envelope

transcript summary

sha256sums manifest over evidence pack

These outputs allow independent review and replay.

Standalone vs Ecosystem Boundary
Standalone Tier-0 boundary

PacketPuncture must stand on its own as:

a deterministic packet/network evidence instrument

a signing and receipt-producing system

a non-mutating verifier surface

a reproducible evidence generator

Post-Tier-0 ecosystem boundary

After PacketPuncture is fully proven standalone, it can integrate with:

GOS IPS / IDS layers

witness systems

transport layers

policy/governance systems

broader verification meshes

These integrations must not redefine PacketPuncture’s standalone correctness.

Competitive Positioning Diagram
Traditional packet tools
  -> inspect traffic
  -> decode protocols
  -> assist operators

PacketPuncture
  -> convert packet-derived events into evidence
  -> sign artifacts
  -> preserve append-only proof
  -> support deterministic verification

PacketPuncture is therefore not merely a packet viewer.

It is an evidence-oriented network instrumentation system.

Research Value

PacketPuncture can be used to explore:

deterministic packet evidence generation

reproducible network event documentation

append-only security evidence ledgers

offline signature-based validation of network artifacts

stronger evidentiary workflows for security operations

Summary

PacketPuncture turns packet-derived events into deterministic evidence artifacts.

The core pipeline is:

observe
  -> canonicalize
  -> hash
  -> sign
  -> pledge
  -> verify

That pipeline is the foundation for both:

standalone PacketPuncture as a serious security research and evidence tool

future integration into GOS security systems after Tier-0 completion
