# Emergent State Machine (ESM)

## Architectural Specification (v1.1.0)

**Note:** This update introduces the first standalone Emergent State Machine Specification (`esm_spec`) document.

## 1. Overview

The Emergent State Machine (ESM) is a deterministic control architecture for systems that must transform observations into actions while preserving transparency, auditability, and governance.

The architecture separates three responsibilities:

- Measurement -- extracting signals from observations
- Interpretation -- constructing a structured representation of system state
- Authority -- selecting actions through explicit deterministic policy

This separation prevents probabilistic interpretation mechanisms from directly authorizing consequential actions. Instead, authoritative decisions remain governed by explicit policy rules.

The architecture operates through a sequence of turns, each representing a bounded reasoning frame.

## 2. Architectural Principles

The ESM architecture is governed by several core principles.

### 2.1 Deterministic Authority

Authoritative actions must be selected by deterministic policy functions. Identical system state must produce identical decisions under fixed policy versions.

### 2.2 Inspectable Reasoning

Every decision must be traceable through an explicit reasoning chain linking actions to underlying observations.

### 2.3 Separation of Description and Authority

Interpretation mechanisms may describe system conditions but cannot directly authorize actions.

### 2.4 Versioned Evolution

Changes to system behavior must occur through explicit revision of versioned artifacts rather than implicit model drift.

## 3. Core Concepts

### 3.1 Turn

A turn is the fundamental unit of reasoning within an Emergent State Machine.

Each turn processes new observations and produces an authoritative action.

A turn contains the following stages:

- observation intake
- signal extraction
- state construction
- projection into policy space
- policy evaluation
- action selection

Turns provide a bounded computational frame that supports replayability and auditability.

### 3.2 Observations

Observations represent measurable information about the environment.

Observations may originate from:

- sensors
- user input
- external systems
- historical records

Observations are denoted:

`o_t`

where `t` indicates the current turn.

### 3.3 Signals

Signals are structured measurements derived from observations.

Signals may be:

- direct signals -- direct measurements
- derived signals -- deterministic transformations of observations or other signals

Signals must satisfy the following properties:

- explicit definition
- bounded output range
- independent testability
- versioned implementation

Signals extracted during a turn form the signal set:

`S_t = { s1, s2, ..., sn }`

### 3.4 State Vector

Signals are organized into a structured representation called the state vector.

The state vector describes the system's current situation in a form suitable for policy evaluation.

`x_t = [ s1, s2, ..., sn ]`

Each component corresponds to a signal derived during the current turn.

Unlike latent representations used in many machine learning systems, the ESM state vector remains explicitly interpretable.

## 4. Projection

The state vector alone does not determine which actions should occur.

The system therefore projects the state vector into policy space, where dimensions correspond to decision-relevant conditions.

Projection is represented as:

`y_t = P(x_t)`

where:

- `x_t` is the state vector
- `P` is the projection function
- `y_t` is the policy-space representation

Projection may be implemented through deterministic algorithms or statistical models, but the resulting representation must remain structured and reproducible.

Projection does not authorize action.

## 5. Policy

Policy governs authoritative action selection.

The policy function maps projected state into actions:

`a_t = π(y_t)`

where:

- `π` is the policy function
- `y_t` is the policy-space representation
- `a_t` is the selected action

Policy rules may include:

- threshold logic
- escalation rules
- persistence requirements
- cooldown constraints
- routing logic

Policy must satisfy four requirements:

- determinism
- explicit definition
- versioning
- exclusive decision authority

Only policy may authorize actions that affect external systems.

## 6. Action

An action represents the authoritative decision produced by the system during a turn.

Examples include:

- triggering an alert
- routing a request
- escalating a workflow
- requesting clarification
- performing system updates

The action set is defined as:

`A = { a1, a2, ..., ak }`

## 7. Control State

An Emergent State Machine maintains internal operational state across turns.

Control state may include:

- workflow stage
- escalation level
- cooldown timers
- persistence counters
- active objectives

Control state is denoted:

`m_t`

Control state evolves deterministically:

`m_{t+1} = f(m_t, y_t, a_t)`

This update function is explicit and versioned.

## 8. Turn Execution Flow

At each turn the system executes the following pipeline:

- receive observations
- compute signals
- construct state vector
- project state into policy space
- evaluate policy
- select action
- update control state

This pipeline ensures that authoritative decisions always pass through explicit policy.

## 9. Clarification and Partial Observability

In some situations available signals may not uniquely determine a valid action.

When policy cannot determine a unique action, the system may select:

`request_clarification`

Additional input is then incorporated in the next turn.

This approach surfaces ambiguity explicitly rather than collapsing uncertainty internally.

## 10. Instrumentation

Each turn produces a structured interaction record containing:

- raw observations
- signal values
- state vector
- projection output
- policy version
- selected action
- control state

These records allow complete replay of system behavior.

## 11. Instrumented Deterministic Evolution (IDE)

System behavior evolves through explicit artifact revision.

Artifacts subject to versioning include:

- signal detectors
- projection logic
- policy rules
- control state update logic

Each revision must be:

- versioned
- recorded
- testable through replay

Under this regime system evolution occurs intentionally rather than through implicit parameter drift.

## 12. Architectural Boundaries

The ESM architecture enforces strict separation between interpretation and authority.

Interpretation mechanisms may assist in describing system conditions but cannot directly authorize actions.

This boundary allows systems to incorporate probabilistic or generative models while preserving deterministic governance of consequential decisions.

## 13. Reference Implementation Structure

A minimal ESM implementation contains the following components:

```text
signals/
    primitive detectors
projection/
    state interpretation logic
policy/
    decision rules
control/
    state update logic
instrumentation/
    interaction logging
```

Each component must be independently versioned.

## 14. Domain Adaptation

The ESM architecture is domain-agnostic.

To deploy an ESM system in a new domain, developers must define:

- domain-specific signals
- projection functions
- policy rules
- action sets

The architectural separation between measurement, interpretation, and authority remains invariant.

## 15. Summary

The Emergent State Machine provides a deterministic architecture for systems that must convert observations into decisions while preserving transparency and governance.

By separating measurement, interpretation, and authority, the architecture enables:

- inspectable reasoning
- deterministic decision control
- replayable system behavior
- controlled system evolution

This structure allows automated systems to remain understandable, auditable, and governable even as they grow in complexity.
