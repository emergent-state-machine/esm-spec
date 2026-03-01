# Emergent State Machine (ESM)

The Emergent State Machine (ESM) is a normative turn-based control architecture that structurally separates descriptive state representation from authoritative action selection.

Within ESM, all state mutation occurs exclusively through a **Controlled Mutation Layer (CML)** — a deterministic, versioned, and instrumented boundary governing how authoritative state may evolve.

ESM formalizes structural separation between:

- Descriptive state representation  
- Deterministic, versioned authority  
- Optional schema-constrained generative instrumentation  

It is designed for engineers building systems where probabilistic interpretation and consequential action must coexist — without sacrificing auditability, replayability, or policy control.

---

## Why This Exists

Modern AI systems frequently entangle:

- Interpretation  
- Decision authority  
- Generative output  

This entanglement makes systems difficult to:

- Audit  
- Reproduce  
- Version safely  
- Govern at scale  

ESM addresses this by enforcing a strict architectural separation between descriptive projection and authoritative mutation.

Behavioral change may occur only through explicit, versioned state transitions mediated by the Controlled Mutation Layer (CML) — never through implicit drift.

---

## Scope of This Repository

This repository contains the **normative specification** of the ESM pattern:

- Formal execution model  
- Required invariants  
- Clarification and ambiguity handling rules  
- Versioning guarantees  
- Instrumented Deterministic Evolution (IDE)  

It does not contain application code.

---

## White Paper

- *ESM: A Turn-Based Control Architecture (v0.9)*  
  [Download PDF](paper/ESM_Turn_Based_Control_Architecture_v0.9.pdf)

---

## Engineering Specification

Canonical engineering specification:

[spec/esm_spec.md](spec/esm_spec.md)

An implementation must satisfy this specification to be considered ESM-compliant.

---

## Reference Implementation

The Digital Learning Companion (DLC) is one implementation of the ESM pattern:

https://github.com/ih8scargo/dlc

Additional implementations are welcome.

---

## Join the Conversation

If you are building systems that require:

- Deterministic authority boundaries  
- Explicit policy control  
- Structured ambiguity handling  
- Safe, versioned evolution  

We invite collaboration and discussion.
