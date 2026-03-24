# Emergent State Machine (ESM)

## Architectural Specification (v1.5.0)

> Note: This version refines the architecture by differentiating invariant requirements from variations that may be necessary in practical implementations.

## 1. Overview

The Emergent State Machine (ESM) is a deterministic architectural framework for systems that transform observations into governed outcomes while preserving transparency, auditability, and control.

The architecture separates four responsibilities:

- Measurement — extracting signals from observations
- Interpretation — constructing a coherent system state
- Relevance Determination — deciding whether a situation warrants evaluation
- Authority — selecting outcomes through deterministic policy

This separation ensures that probabilistic or statistical interpretation mechanisms cannot directly authorize consequential actions. All authority remains governed by explicit, versioned policy.

The system operates through discrete turns, each representing a bounded reasoning frame.

## 2. Architectural Principles

### 2.1 Invariant Requirements (MUST)

- Authority MUST be deterministic
- Each turn MUST expose a complete reasoning chain
- Interpretation MUST NOT authorize outcomes
- All governing artifacts MUST be versioned
- Evaluation MUST be conditionally triggered (not continuous action)

### 2.2 Permitted Variations (MAY)

- Interpretation MAY use statistical or learned models
- Systems MAY operate in advisory-only mode
- Systems MAY include confidence or uncertainty annotations

## 3. Core Concepts

### Turn

#### 3.1 Invariant Requirements (MUST)

A turn MUST:

- incorporate observations
- construct a coherent state
- produce a projected representation
- evaluate relevance
- produce an outcome

A turn MUST be:

- bounded
- inspectable
- replayable

#### 3.2 Permitted Variations (MAY)

- Turns MAY begin from initialized state (not empty)
- Turns MAY include additional diagnostic artifacts

#### 3.3 Implementation Notes

The turn is both:

- the atomic reasoning unit
- the temporal unit of system evolution

Each turn:

- incorporates new observations
- constructs a coherent state
- determines whether the situation warrants evaluation
- conditionally produces an outcome

A turn is a bounded, replayable decision frame.

#### 3.4 Turn Outcomes

##### Invariant Requirements (MUST)

Each turn MUST produce an outcome.

The outcome MUST be explicitly represented, even if no action occurs.

##### Permitted Variations (MAY)

Outcome types MAY include:

- no-op
- local_action
- escalation
- handoff
- request_clarification

Implementations MAY define additional outcome types.

##### Implementation Notes

“No-op” SHOULD be explicitly recorded to preserve auditability.

### 5. Observations

#### Invariant Requirements (MUST)

- Observations MUST be identifiable inputs at time  
  𝑡  
  t
- Observations MUST be sufficient to reconstruct signal computation

#### Permitted Variations (MAY)

- Observations MAY be stored inline or referenced externally
- Observations MAY be partial or incomplete

#### Implementation Notes

Missing observations SHOULD be represented explicitly, not silently defaulted.

### 6. Signals

#### Invariant Requirements (MUST)

Signals MUST be:

- explicitly defined
- bounded
- independently testable
- versioned

Signals MUST be computable from observations.

#### Permitted Variations (MAY)

- Signals MAY be derived, aggregated, or transformed
- Signals MAY include model-assisted outputs
- Signals MAY include confidence or uncertainty

#### Implementation Notes

Model-assisted signals MUST NOT directly authorize outcomes.

### 7. Coherent State (State Vector)

#### Invariant Requirements (MUST)

The state vector MUST:

- represent a fully constructed interpretation
- be reproducible from signals
- be independent of policy

#### Permitted Variations (MAY)

- State MAY include derived features
- State MAY include uncertainty representations

#### Implementation Notes

State MUST be “decision-ready” — ambiguity should not be deferred past this layer.

### 8. Projection

#### Invariant Requirements (MUST)

Projection MUST:

- map  
  𝑥  
  𝑡  
  →  
  𝑦  
  𝑡  
  x  
  t  
  →y  
  t

- be explicitly represented
- be distinct from state construction and policy

Projection MUST NOT:

- introduce new semantic meaning
- resolve ambiguity

#### Permitted Variations (MAY)

- Projection MAY be linear, rule-based, or learned
- Projection MAY include normalization or scaling
- Projection MAY reduce dimensionality

#### Implementation Notes

Projection is where coarse-graining occurs for decision-making.

### 9. Relevance Determination (Gating)

#### Invariant Requirements (MUST)

- Relevance MUST evaluate  
  𝑦  
  𝑡  
  y  
  t

- Relevance MUST produce a gating result
- Policy MUST NOT execute if gating is false

#### Permitted Variations (MAY)

- Gating MAY be binary or multi-state
- Gating MAY incorporate temporal logic
- Gating MAY include uncertainty thresholds

#### Implementation Notes

Gating defines the authorization boundary.

### 10. Policy (Authority)

#### Invariant Requirements (MUST)

- Policy MUST be deterministic
- Policy MUST be the sole source of authority
- Policy MUST operate only when gating allows

#### Permitted Variations (MAY)

- Policy MAY be rule-based or table-driven
- Policy MAY include escalation logic
- Policy MAY output no-op

#### Implementation Notes

Policy determines outcomes—not interpretation layers.

### 11. Action and Outcome

#### Invariant Requirements (MUST)

- Actions MUST be distinguishable from outcomes
- Outcomes MUST be recorded even if no action occurs

#### Permitted Variations (MAY)

- Actions MAY be internal or external
- Outcomes MAY include non-action results

### 12. Control State

#### Invariant Requirements (MUST)

- Control state MUST evolve deterministically

#### Permitted Variations (MAY)

Control state MAY include:

- timers
- counters
- workflow stages

#### Implementation Notes

Control state enables temporal behavior without breaking determinism.

### 13. Turn Execution Flow

#### Invariant Requirements (MUST)

Each turn MUST execute:

- observations
- signals
- state construction
- projection
- relevance determination
- policy (conditional)
- outcome
- control update

### 14. Instrumentation (Turn Record)

#### Invariant Requirements (MUST)

Each turn record MUST include:

- observations
- signals
- state  
  𝑥  
  𝑡  
  x  
  t
- projection  
  𝑦  
  𝑡  
  y  
  t
- relevance result
- outcome

#### Permitted Variations (MAY)

Turn records MAY include:

- action
- control state
- confidence
- uncertainty
- volatility
- provenance metadata
- version identifiers

#### Implementation Notes

Replayability depends on recording sufficient information, but the spec defines only the minimum.

### 15. Temporal Dynamics

#### Invariant Requirements (MUST)

- Temporal behavior MUST be explicit and reproducible

#### Permitted Variations (MAY)

Temporal logic MAY include:

- persistence
- aggregation
- decay
- trend detection

### 16. Layered ESMs

#### Invariant Requirements (MUST)

- Each ESM MUST operate independently after initialization

#### Permitted Variations (MAY)

- ESMs MAY initialize downstream systems
- ESMs MAY operate hierarchically

### 17. Instrumented Deterministic Evolution (IDE)

#### Invariant Requirements (MUST)

- All governing artifacts MUST be versioned

#### Permitted Variations (MAY)

Artifacts MAY include:

- signals
- projection
- relevance
- policy
- control logic

### 18. Architectural Boundaries

#### Invariant Requirements (MUST)

- Interpretation MUST NOT authorize outcomes
- All outcomes MUST be deterministic

#### Permitted Variations (MAY)

- Probabilistic systems MAY assist interpretation

### 19. Domain Adaptation

#### Invariant Requirements (MUST)

Implementations MUST define:

- signals
- state
- projection
- relevance
- policy

#### Permitted Variations (MAY)

- Domain-specific extensions MAY be added

### 20. Summary

The ESM defines a minimal, invariant architecture for transforming observations into governed outcomes.

All implementations must preserve:

- layered reasoning
- explicit state
- deterministic authority

All additional capabilities are extensions, not replacements.

### 21. Compliance Checklist

This checklist defines the minimum conditions required for an implementation to be considered a valid Emergent State Machine (ESM).

An implementation MUST satisfy all items in Core Compliance.

#### 21.1 Core Compliance (Required)

Turn Structure

- The system operates in discrete, identifiable turns
- Each turn represents a complete reasoning cycle
- Each turn produces an explicit outcome

Layer Representation

Each turn MUST include explicit representations of:

- Observations (  
  𝑜  
  𝑡  
  o  
  t  
  )
- Signals (  
  𝑆  
  𝑡  
  S  
  t  
  )
- Coherent state (  
  𝑥  
  𝑡  
  x  
  t  
  )
- Projection (  
  𝑦  
  𝑡  
  y  
  t  
  )
- Relevance determination (  
  𝑔  
  𝑡  
  g  
  t  
  )
- Outcome (  
  𝑟  
  𝑡  
  r  
  t  
  )

Layer Separation

- Interpretation layers (signals, state, projection) are separated from authority
- Projection is implemented as a distinct step (not merged with state or policy)
- Relevance determination occurs before policy execution

Deterministic Authority

- Policy decisions are deterministic
- Identical inputs under fixed versions produce identical outcomes
- No probabilistic component directly authorizes outcomes

Conditional Policy Execution

- Policy is executed only when relevance conditions are satisfied
- When relevance is not satisfied, policy is not evaluated

Inspectable Reasoning

- Each turn exposes a complete reasoning chain from observations to outcome
- Intermediate representations (signals, state, projection) are inspectable

#### 21.2 Turn Record Compliance (Required)

Each turn record MUST include:

- Observations
- Signals
- State (  
  𝑥  
  𝑡  
  x  
  t  
  )
- Projection (  
  𝑦  
  𝑡  
  y  
  t  
  )
- Relevance result (  
  𝑔  
  𝑡  
  g  
  t  
  )
- Outcome

#### 21.3 Strongly Recommended (Non-Blocking)

These are not required for validity but are recommended for robust implementations.

Reproducibility and Replay

- Version identifiers for signals, projection, relevance, and policy
- Sufficient data to replay a turn deterministically

Outcome Clarity

- No-op outcomes are explicitly recorded
- Outcome types are clearly defined

Handling Uncertainty

- Missing or ambiguous inputs are explicitly represented
- Confidence or uncertainty is recorded where relevant

Temporal Logic

- Temporal features (e.g., persistence, trends) are explicit and reproducible

Model-Assisted Components

- Use of models is documented and bounded to non-authoritative layers
- Model outputs are treated as signals or projection inputs, not decisions

Initialization and Handoff

- Initial state or upstream inputs are explicitly recorded
- Source of initialization is identifiable

#### 21.4 Non-Compliance Indicators

An implementation is NOT a valid ESM if any of the following occur:

- Outcomes are produced without explicit projection or relevance steps
- Policy decisions are influenced directly by probabilistic outputs
- Intermediate reasoning layers are not inspectable
- The system operates as a continuous black-box transformation
- Turn boundaries are not defined or reconstructible
