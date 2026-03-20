# Emergent State Machine (ESM)

## Architectural Specification (v1.2.0)

**Note:** This version refines the core ontology of the Emergent State Machine to make projection, gating, temporal dynamics, and turn outcomes explicit, while preserving the original architectural simplicity.

---

## 1. Overview

The Emergent State Machine (ESM) is a deterministic control architecture for systems that transform observations into actions while preserving transparency, auditability, and governance.

The architecture separates three responsibilities:

- Measurement -- extracting signals from observations
- Interpretation -- constructing a structured representation of system state
- Authority -- selecting actions through explicit deterministic policy

This separation prevents probabilistic interpretation mechanisms from directly authorizing consequential actions. Instead, authoritative decisions remain governed by explicit policy rules.

The architecture operates through a sequence of turns, each representing a bounded reasoning frame in which the system evaluates state, determines relevance, and produces a turn outcome.

---

## 2. Architectural Principles

### 2.1 Deterministic Authority

Authoritative actions must be selected by deterministic policy functions. Identical system state must produce identical decisions under fixed policy versions.

### 2.2 Inspectable Reasoning

Every decision must be traceable through an explicit reasoning chain linking actions to underlying observations.

### 2.3 Separation of Description and Authority

Interpretation mechanisms may describe system conditions but cannot directly authorize actions.

### 2.4 Versioned Evolution

Changes to system behavior must occur through explicit revision of versioned artifacts rather than implicit model drift.

### 2.5 Conditional Intervention

The system continuously evaluates its environment but only intervenes when conditions warrant action.

---

## 3. Core Concepts

### 3.1 Turn

A turn is the fundamental unit of reasoning within an Emergent State Machine.

Each turn processes new observations and produces a **turn outcome**.

A turn contains the following stages:

- observation intake
- signal extraction
- state construction
- projection into policy space
- gating evaluation
- policy evaluation (conditional)
- outcome determination

Turns provide a bounded computational frame that supports replayability and auditability.

---

### 3.1.1 Turn Outcome

A turn outcome represents the result of evaluating the current situation.

Possible outcomes include:

- **no-op** — no action is taken
- **local_action** — a bounded action is executed
- **escalation** — authority is transferred to a higher-level system or human operator
- **handoff** — control is transferred to another system

Not all turns produce actions. Non-action is a valid and expected outcome.

---

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

---

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

---

### 3.4 State Vector

Signals are organized into a structured representation called the state vector.

The state vector describes the system's current situation in a form suitable for interpretation and policy evaluation.

`x_t = [ s1, s2, ..., sn ]`

Each component corresponds to a signal derived during the current turn.

The state vector may include derived features such as temporal summaries or diagnostic indicators, provided they remain interpretable and reproducible.

---

## 4. Projection

The state vector alone does not determine which actions should occur.

The system therefore projects the state vector into policy space, where dimensions correspond to decision-relevant conditions.

Projection is represented as:

`y_t = P(x_t)`

where:

- `x_t` is the state vector
- `P` is the projection function
- `y_t` is the policy-space representation

Projection is a required step that transforms state into policy-relevant coordinates.

Projection may be implemented through deterministic algorithms or statistical models, but the resulting representation must remain structured and reproducible.

Projection does not authorize action.

---

## 5. Gating

Gating determines whether the projected state warrants policy evaluation and potential action.

Gating is represented as:

`g_t = G(y_t)`

where:

- `y_t` is the projected state
- `G` is the gating function
- `g_t ∈ {0, 1}`

Behavior:

- if `g_t = 0` → no-op
- if `g_t = 1` → proceed to policy evaluation

Gating implements conditional intervention by distinguishing between continuous evaluation and discrete action.

Typical gating conditions may include:

- deviation from a desirable region
- high volatility or rapid change
- low confidence in interpretation
- violation of persistence constraints

---

## 6. Policy

Policy governs authoritative action selection.

Policy is evaluated only when gating conditions are satisfied.

`a_t = π(y_t)  if g_t = 1`  
`a_t = ∅       if g_t = 0`

where:

- `π` is the policy function
- `y_t` is the projected state
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

---

## 7. Action and Outcome

An action represents an authoritative operation executed by the system.

Actions are one type of turn outcome.

Possible outcomes include:

- no-op
- local_action
- escalation
- handoff

The action set is defined as:

`A = { a1, a2, ..., ak }`

Action sets are externally defined and may be constrained to pre-authorized operations depending on deployment context.

---

## 8. Control State

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

---

## 9. Turn Execution Flow

At each turn the system executes the following pipeline:

- receive observations
- compute signals
- construct state vector
- project state into policy space
- evaluate gating
- (if gated) evaluate policy
- determine turn outcome
- update control state

This pipeline ensures that authoritative decisions always pass through explicit policy.

---

## 10. Clarification and Partial Observability

In some situations available signals may not uniquely determine a valid interpretation or action.

When ambiguity is detected, the system may produce:

`request_clarification`

Additional input is then incorporated in the next turn.

This approach surfaces ambiguity explicitly rather than collapsing uncertainty internally.

---

## 11. Instrumentation

Each turn produces a structured interaction record containing:

- raw observations
- signal values
- state vector
- projection output
- gating result
- policy version
- turn outcome
- selected action (if any)
- control state

Optional fields may include:

- confidence measures
- volatility indicators

These records allow complete replay of system behavior.

---

## 12. Temporal Dynamics

The ESM operates over discrete turns while interacting with continuous real-world time.

Time between turns may vary.

Temporal reasoning may include:

- persistence requirements
- temporal aggregation
- stability and change detection
- decay of signal relevance

Signals and derived features may decrease in influence over time as they become less relevant to current interpretation.

Temporal features must remain explicitly defined and reproducible.

---

## 13. Layered ESMs

Multiple ESMs may operate at different levels of abstraction within a system.

Higher-level ESMs may provide initialized state to downstream ESMs through structured state transfer.

After initialization, ESMs operate independently on their own observation streams.

Interaction between ESMs occurs through:

- state transfer
- outcome-triggered coordination

Continuous coupling between ESMs is not required.

---

## 14. Instrumented Deterministic Evolution (IDE)

System behavior evolves through explicit artifact revision.

Artifacts subject to versioning include:

- signal detectors
- projection logic
- gating functions
- policy rules
- control state update logic

Each revision must be:

- versioned
- recorded
- testable through replay

Under this regime system evolution occurs intentionally rather than through implicit parameter drift.

---

## 15. Architectural Boundaries

The ESM architecture enforces strict separation between interpretation and authority.

Interpretation mechanisms may assist in describing system conditions but cannot directly authorize actions.

All actions must be:

- explicitly defined
- externally governed
- deterministically selected

This boundary allows systems to incorporate probabilistic or generative models while preserving deterministic governance of consequential decisions.

---

## 16. Reference Implementation Structure

A minimal ESM implementation contains the following components:

signals/
primitive detectors

projection/
state interpretation logic

gating/
relevance evaluation logic

policy/
decision rules

control/
state update logic

instrumentation/
interaction logging

Each component must be independently versioned.

---

## 17. Domain Adaptation

The ESM architecture is domain-agnostic.

To deploy an ESM system in a new domain, developers must define:

- domain-specific signals
- projection functions
- gating logic
- policy rules
- action sets

The architectural separation between measurement, interpretation, and authority remains invariant.

---

## 18. Summary

The Emergent State Machine provides a deterministic architecture for systems that convert observations into outcomes while preserving transparency and governance.

By separating measurement, interpretation, relevance evaluation, and authority, the architecture enables:

- inspectable reasoning
- deterministic decision control
- replayable system behavior
- controlled system evolution

This structure allows automated systems to remain understandable, auditable, and governable even as they grow in complexity.
