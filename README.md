# Emergent State Machine

The **Emergent State Machine (ESM)** is an architectural framework for deterministic, interpretable decision systems.

It defines how systems transform observations into governed outcomes while preserving:

- transparency
- replayability
- auditability
- explicit control over decision authority

## Core Execution Model

ESM organizes reasoning into discrete computational frames called turns.

Each turn:

- incorporates observations
- derives signals
- constructs a coherent state
- re-expresses that state in decision coordinates
- determines whether evaluation is warranted
- conditionally produces an outcome

## ESM Core Loop

```text
Environment / Domain
        │
        ▼
Observations (o_t)
        │
        ▼
Signals (S_t)
        │
        ▼
Coherent State (x_t)
        │
        ▼
Projection (y_t = P(x_t))
        │
        ▼
Relevance Determination (g_t = G(y_t))
        │
        ▼
Policy Evaluation (π)
        │
        ▼
Outcome / Action (a_t)
        │
        ▼
Control State Update (m_t)
        │
        └────────→ next Turn
```

Turn structure: `T_t = (o_t, S_t, x_t, y_t, g_t, a_t, m_t)`

Across time: `T_0 → T_1 → T_2 → ...`

This makes every state transition inspectable, replayable, and governable.

## Architectural Separation

ESM enforces strict separation between:

- Measurement → signals from observations
- Interpretation → coherent state construction
- Relevance Determination → whether a situation warrants evaluation
- Authority → deterministic policy selection

This separation ensures:

- probabilistic or generative systems may assist interpretation,
- but cannot directly authorize outcomes.

## Key Concepts

### Coherent State

Signals are organized into a fully resolved, internally consistent state representation.

This state contains all semantic content required for decision-making.

### Projection

Projection re-expresses the coherent state in policy-relevant coordinates.

Projection introduces no new semantic content.

It is a structured re-representation of an already interpreted state.

### Relevance Determination (Gating)

Relevance determination defines:

- the authorization boundary for decision-making

It determines whether the current situation warrants policy evaluation.

### Policy (Authority)

Policy is the exclusive source of authority.

All outcomes must be selected:

- deterministically
- explicitly
- under versioned rules

## Why This Exists

Modern AI and decision systems often entangle:

- interpretation
- decision authority
- generative output

This leads to systems that are:

- difficult to audit
- difficult to reproduce
- unsafe to evolve
- hard to govern

The Emergent State Machine addresses this by:

- making state construction explicit
- separating interpretation from authority
- enforcing a governed decision boundary
- enabling replayable system evolution

Behavior changes only through:

- explicit, versioned modification of architectural artifacts

## Scope of This Repository

This repository contains the canonical specification of the ESM architecture.

It defines:

- the execution model
- architectural invariants
- coherent state construction
- projection semantics
- relevance determination
- deterministic policy authority
- Instrumented Deterministic Evolution (IDE)

This repository does not contain application implementations.

## Specification

The canonical Emergent State Machine architecture specification is located at:

- [`spec/esm_spec.md`](spec/esm_spec.md)

### Latest Spec Draft

#### ESM Spec v1.5.0

The specification has been updated to align with the current architecture paper and governance framing.

This draft clarifies the architectural boundary between signals, projection, and authority, and reflects the current formulation of ESM as a framework for interpretable situational reasoning and controlled state mutation.

See ESM Spec v1.5.0: [`spec/esm_spec.md`](spec/esm_spec.md)

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

**v1.5.0 — Interpretable Situational Reasoning & Projection Formalization**

The latest version of the Emergent State Machine architecture sharpens its core contribution:
making situational reasoning explicit, inspectable, and governable.

This release clarifies how systems move from raw observations to meaningful decisions by formalizing projection as an explicit transformation from measurable state into policy-relevant structure.

Key highlights:

- Projection defined as explicit coarse-graining into decision space
- Stronger framing of ESM as a system for situational reasoning
- Clearer articulation of the decision boundary (policy as authority)
- Continued emphasis on determinism, replayability, and auditability

This version represents the most complete and accessible articulation of the architecture to date.

- [PDF](papers/esm-architecture/esm_architecture_v1.5.0.pdf)

### Previous Architecture Paper Release

**v1.4.0 — Architectural Framework & Governance Boundary**

This release formalizes the Emergent State Machine as an architectural framework for interpretable situational reasoning, with a clear and enforceable boundary between interpretation and authority.

Key advancements:

- Clarifies the architecture as Signal → State → Projection → Authority (CML)
- Establishes the governance boundary: only policy may authorize state mutation
- Refines the role of projection as explicit, inspectable coarse-graining into policy space
- Strengthens the framing of ESM as a decision system architecture, not a model or pipeline

This version represents the current canonical framing of ESM as a system for governed, auditable decision-making in complex environments.

- [PDF](papers/esm-architecture/esm_architecture_v1.4.0.pdf)

**v1.3.0 — Architectural Reframing & Interpretability Emphasis**

This release transitions the language of ESM from a control-system framing toward a broader architectural interpretation of situational reasoning systems.

Key advancements:

- Reframes ESM as an architectural framework, not just a control loop
- Strengthens emphasis on interpretability, auditability, and governance
- Clarifies projection as the mechanism that makes situations visible, not predicted
- Refines narrative around human–AI collaboration at the decision boundary

This version bridges the earlier mathematical formulation and the current governance-oriented architecture.

- [PDF](papers/esm-architecture/esm_architecture_v1.3.0.pdf)

**v1.2.0 — Projection Clarity & Policy-Space Reasoning**

This release sharpens the role of projection into policy space as a central architectural component.

Key advancements:

- Defines projection as explicit transformation into decision-relevant coordinates
- Distinguishes projection from prediction and inference
- Clarifies how policy operates over structured situational dimensions
- Strengthens the separation between state representation and decision logic

This version marks the point where projection becomes clearly identifiable as a novel architectural contribution.

- [PDF](papers/esm-architecture/esm_architecture_v1.2.0.pdf)

**v1.1.0 — Deterministic State-Space Formulation & IDE**

This release introduces the formal structure of the ESM as a deterministic state-space system with explicit reasoning steps.

Key advancements:

- Defines the turn as the atomic unit of reasoning
- Formalizes the transformation chain: observations → signals → state → projection → action
- Introduces Instrumented Deterministic Evolution (IDE) as the mechanism for system change
- Establishes replayability, auditability, and failure localization as core properties

This version provides the first fully developed mathematical and architectural articulation of the system.

- [PDF](papers/esm-architecture/esm_architecture_v1.1.0.pdf)

**v1.0.0 — Initial Formalization of the ESM Architecture**

This release represents the first complete formal draft of the Emergent State Machine architecture.

Key contributions:

- Establishes the turn-based reasoning loop
- Introduces signals, state vectors, and deterministic policy selection
- Frames the architecture as an alternative to opaque, model-centric decision systems
- Begins formalizing the relationship to control theory and state-space systems

This version provides the first end-to-end articulation of the system’s structure.

- [PDF](papers/esm-architecture/esm_architecture_v1.0.0.pdf)

**v0.9.1 — Foundational Architecture: Turn-Based Control**

This release captures the earliest formal articulation of the Emergent State Machine as a turn-based control architecture.

Key contributions:

- Establishes the turn-based execution model
- Introduces explicit construction of state from signals
- Frames the problem of entangled interpretation and action in AI systems
- Motivates separation between descriptive reasoning and authoritative decision-making

While later versions refine layering and governance boundaries, this release contains the core insight:
making the construction of state from signals explicit as the foundation of interpretable decision systems.

📄 [PDF](papers/esm-architecture/ESM_Turn_Based_Control_Architecture_v0.9.pdf)

### Designing the Digital Learning Companion

Design narrative describing how the Emergent State Machine architecture emerged.

- [PDF](papers/dlc-design-narrative/Designing_the_Digital_Learning_Companion_v0.9.0.pdf)

## Reference Implementation

The Digital Learning Companion (DLC) is one implementation of the ESM pattern:

- [Digital Learning Companion](https://github.com/Digital-Learning-Companion)

Additional implementations are welcome.

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
