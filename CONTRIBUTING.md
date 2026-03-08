# Contributing to PacketPuncture

Thank you for your interest in contributing.

PacketPuncture is a deterministic evidence instrumentation project. Contributions must preserve the core design rules of the system.

---

# Core Development Rules

All contributions must follow these deterministic constraints:

• UTF-8 encoding with **no BOM**  
• **LF newline normalization**  
• deterministic JSON serialization  
• SHA-256 hashing for artifacts  
• append-only receipt logs  
• non-mutating verification behavior  

No contribution may introduce nondeterministic behavior.

---

# Contribution Types

Contributions are currently accepted in the following areas:

• verification tooling  
• deterministic test vectors  
• packet capture ingestion  
• replay validation tools  
• documentation improvements  
• security review  

Feature additions that change artifact structure or evidence models must be discussed before implementation.

---

# Pull Request Process

1. Fork the repository
2. Create a new branch
3. Implement your change
4. Ensure deterministic behavior is preserved
5. Submit a pull request with a clear explanation

Pull requests must not break the deterministic evidence model.

---

# Code Quality Expectations

All code should:

• be readable and minimal  
• avoid hidden side effects  
• maintain deterministic output  
• avoid nondeterministic data structures  

Determinism is more important than convenience.

---

# Reporting Issues

Issues may include:

• verification failures  
• nondeterministic behavior  
• artifact inconsistencies  
• documentation problems  

When reporting issues include:

• system environment  
• reproduction steps  
• relevant artifacts  

---

# Security Concerns

Security issues should be reported according to the guidelines in `SECURITY.md`.
