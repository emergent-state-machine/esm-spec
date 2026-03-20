# Emergent State Machine

The **Emergent State Machine (ESM)** is a deterministic control architecture for systems that must transform observations into decisions while preserving transparency, replayability, and governance.

ESM organizes reasoning into discrete computational frames called **turns**. Each turn transforms observations into signals, constructs a structured state representation, evaluates policy, and produces an authoritative action.

## ESM Core Loop

```text
Environment / Domain
        │
        ▼
Observations
        │
        ▼
Signals
        │
        ▼
State Vector
        │
        ▼
Activation Gate
        │
        ▼
Policy Projection
        │
        ▼
Policy Selection
        │
        ▼
Action
        │
        ▼
State Evolution
        │
        └────────→ next Turn
```

Turn structure: `T_t = (o_t, S_t, x_t, g_t, y_t, a_t)`

Across time: `T_0 → T_1 → T_2 → T_3 → ...`

This makes every state transition inspectable, replayable, and governable.

## Why This Exists

Modern AI and decision systems frequently entangle:

- interpretation
- decision authority
- generative output

This makes systems difficult to:

- audit
- reproduce
- version safely
- govern at scale

The Emergent State Machine addresses this problem by enforcing a strict architectural separation between:

`measurement → interpretation → authority`

Behavioral change may occur only through explicit, versioned policy evolution.

## Scope of This Repository

This repository contains the **normative specification** of the ESM pattern:

- Formal execution model
- Required invariants
- Clarification and ambiguity handling rules
- Versioning guarantees
- Instrumented Deterministic Evolution (IDE)

It does not contain application code.

## Specification

The canonical Emergent State Machine architecture specification is located at:

- [`spec/esm_spec.md`](spec/esm_spec.md)

Current version: `v1.0.0`

The specification defines:

- the ESM execution model
- architectural invariants
- signal and projection structure
- deterministic policy authority
- clarification and ambiguity handling
- Instrumented Deterministic Evolution (IDE)

For systems that require a deterministic and instrumented mutation boundary, the ESM architecture can be implemented using a **[Controlled Mutation Layer (CML)](https://github.com/controlled-mutation-layer)**.

## Governance Framework (Draft)

A draft ESM Governance Framework is available for early review.

The document outlines how Emergent State Machine systems can remain inspectable, auditable, and operationally accountable as they evolve through structured state mutation and policy-driven decision loops.

This draft focuses on practical governance mechanisms, including:

- mutation boundaries
- policy traceability
- replayable decision history
- controlled system evolution

The framework is still evolving and community feedback is welcome.

See the draft here:

- [`governance/esm_governance.md`](governance/esm_governance.md)

## Papers

### Latest Paper Release

**Emergent State Machine: A Deterministic Architecture for Situational Reasoning in Complex Systems — v1.1.0**

A revised version of the formal architecture paper has been released.

Version 1.1.0 introduces a clearer mathematical framing of the Emergent State Machine (ESM) as a turn-based control architecture. The revision improves conceptual clarity while preserving the original formal structure.

Key updates:

- Turn formalization: the architecture is now explicitly defined around the concept of a Turn, a bounded reasoning frame containing observations, signals, state construction, projection, and policy evaluation.
- Clearer state construction model: signals derived during a turn are formally organized into a state vector, providing an interpretable representation of the system's current situation.
- Improved projection framing: projection is clarified as a transformation of the state vector into policy-relevant coordinates, aligning the architecture with state-space formulations in control theory.
- Instrumented Deterministic Evolution (IDE): the paper now introduces a formal section defining IDE, the mechanism by which ESM systems evolve through explicit versioned changes to detectors, projection logic, and policy artifacts.
- Expanded theoretical grounding: the Related Work section situates the architecture within traditions including control theory and state-space modeling, dynamical systems, situation awareness research, software architectural separation, and AI interpretability and governance.

Scope of the paper:

This paper focuses on the mathematical architecture of the Emergent State Machine. Operational governance topics such as policy modularity and generative assistance constraints are addressed in the broader ESM specification.

Location:

- [PDF](papers/esm-architecture/esm_architecture_v1.1.0.pdf)

### Previous Architecture Paper Release

**Emergent State Machine: A Turn-Based Control Architecture — v1.0.0**

This release updates the architecture paper to align with the ESM specification v1.0.0.

Major clarifications include:

- explicit separation of **Signal**, **Projection**, and **Authority** layers
- introduction of **primitive detectors** and **signals** as the measurement interface
- formalization of **control state** within the policy decision boundary
- clarification of the **authority boundary** separating interpretation from action
- expanded definition of **Instrumented Deterministic Evolution (IDE)**

Paper available in:

- [PDF](papers/esm-architecture/esm_architecture_v1.0.0.pdf)

### Designing the Digital Learning Companion

Design narrative describing how the Emergent State Machine architecture emerged.

- [PDF](papers/dlc-design-narrative/Designing_the_Digital_Learning_Companion_v0.9.0.pdf)

## Reference Implementation

The Digital Learning Companion (DLC) is one implementation of the ESM pattern:

- [Digital Learning Companion](https://github.com/Digital-Learning-Companion)

Additional implementations are welcome.

## Release History

### v1.1.0 — Update to Strengthen Control-Theoretic Formulation

This update introduces the first standalone Emergent State Machine Specification (`esm_spec`) document.

The specification defines the architectural structure of the ESM independent of any specific implementation or application domain.

Highlights:

- Formal definition of the Turn as the fundamental unit of ESM reasoning
- Clear separation of measurement, interpretation, and authority within the architecture
- Definition of signals, state vectors, projection, and policy as explicit system artifacts
- Introduction of control state for deterministic multi-turn system behavior
- Specification of Instrumented Deterministic Evolution (IDE) as the mechanism governing system evolution
- Clarification of architectural boundaries that prevent interpretive mechanisms from directly authorizing consequential actions

Purpose of the specification:

The goal of the ESM specification is to provide a domain-agnostic architectural reference that can support implementations across multiple domains, including:

- decision support systems
- operational monitoring
- AI-assisted reasoning systems
- governance-sensitive automated systems

The specification is intended to evolve alongside the mathematical paper and reference implementations.

Relationship to the math paper:

The mathematical paper describes the formal structure of the architecture. The specification provides an implementation-oriented description of the system components and execution model. Both documents will evolve in parallel as the architecture develops.

### v1.0.0 — First Public Release

First public release of the Emergent State Machine (ESM) architectural specification.

This release clarifies:

- the separation of Signal, Projection, and Authority layers
- primitive detectors, signals, and feature vectors
- deterministic policy as the exclusive mutation authority
- the placement of probabilistic interpretation within the Projection Layer
- hierarchical composition of nested ESMs
- norm ladders as staged operational or learning progressions

See:

- [`spec/esm_spec.md`](spec/esm_spec.md)
- [GitHub Release: v1.0.0](https://github.com/emergent-state-machine/esm-spec/releases/tag/v1.0.0)

### v0.9.1 — Late Pre-Release Draft

Late pre-release draft of the Emergent State Machine architectural specification.

This version is retained as a historical reference point immediately prior to the first stable public release.

Contents at this tag included:

- draft specification at `spec/esm_spec.md`
- accompanying draft paper and LaTeX sources

See:

- [GitHub Release: v0.9.1](https://github.com/emergent-state-machine/esm-spec/releases/tag/v0.9.1)

## Citation

If you reference the Emergent State Machine architecture in research or technical work, please cite:

**Emergent State Machine (ESM) Architectural Specification v1.0.0**  
Emergent State Machine Project  
[https://github.com/emergent-state-machine/esm-spec](https://github.com/emergent-state-machine/esm-spec)

## Join the Conversation

If you are building systems that require:

- deterministic authority boundaries
- explicit policy control
- structured ambiguity handling
- safe, versioned evolution

We invite collaboration and discussion.
