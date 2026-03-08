# Threat Model

PacketPuncture focuses on evidence integrity rather than packet analysis security.

---

# Threats Considered

- artifact tampering
- signature forgery
- receipt log manipulation
- evidence replay attacks

---

# Mitigations

SHA-256 hashing ensures artifact integrity.

Detached signatures ensure authenticity.

Append-only ledgers prevent record rewriting.

Deterministic artifacts allow independent verification.

---

# Threats Out of Scope

PacketPuncture does not attempt to prevent:

- network intrusion
- packet spoofing
- traffic interception

Those are responsibilities of network security systems.

PacketPuncture instead provides evidence artifacts.
