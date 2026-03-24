# Emergent State Machine (ESM)

## Architectural Specification (v1.4.0)

> Note: This version refines the architecture to explicitly define coherent state construction, projection semantics, relevance determination as an authorization boundary, and turn outcome behavior, aligning the specification with the formal architectural framing.

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

### 2.1 Deterministic Authority

Authoritative outcomes must be selected by deterministic policy functions. Identical inputs under fixed versions must produce identical results.

### 2.2 Inspectable Reasoning

Each turn must expose a complete reasoning chain from observation to outcome.

### 2.3 Separation of Interpretation and Authority

Interpretation may describe system conditions but cannot authorize outcomes.

### 2.4 Versioned Evolution

System behavior evolves only through explicit revision of versioned artifacts.

### 2.5 Conditional Intervention

The system evaluates continuously but intervenes selectively.

## 3. Core Concepts

### 3.1 Turn

A turn is the fundamental unit of reasoning.

Each turn:

- incorporates new observations
- constructs a coherent state
- determines whether the situation warrants evaluation
- conditionally produces an outcome

A turn is a bounded, replayable decision frame.

#### 3.1.1 Turn Outcome

A turn outcome represents the result of evaluating the current situation.

Possible outcomes include:

- no-op — no action taken
- local_action — bounded action executed
- escalation — authority transferred
- handoff — control transferred
- request_clarification — additional input required

A no-op may arise from:

- relevance determination (no evaluation required), or
- policy evaluation (evaluation occurred, no action authorized)

### 3.2 Observations

Observations are measurable inputs from the environment.

```text
o_t
```

Sources include sensors, users, systems, or records.

### 3.3 Signals

Signals are structured, testable measurements derived from observations.

```text
S_t = { s1, s2, ..., sn }
```

Signals must be:

- explicitly defined
- bounded
- independently testable
- versioned

### 3.4 State Vector (Coherent State)

Signals are organized into a coherent state vector:

```text
x_t = [ s1, s2, ..., sn ]
```

This state represents a fully constructed interpretation of the situation.

Properties:

- internally consistent
- fully resolved for decision purposes
- reproducible from signals
- independent of policy

The state vector contains all semantic content required for reasoning.

## 4. Projection

Projection re-expresses the coherent state in policy-relevant coordinates.

```text
y_t = P(x_t)
```

Where:

- x_t is the coherent state
- P is the projection function
- y_t is the policy-space representation

Critical property:

Projection introduces no new semantic content.  
It re-expresses an already fully interpreted state.

Projection may:

- reorganize dimensions
- scale or normalize features
- align state with decision thresholds

Projection does not:

- infer new meaning
- resolve ambiguity
- authorize action

## 5. Relevance Determination (Gating)

Relevance determination evaluates whether the projected state warrants policy evaluation.

```text
g_t = G(y_t)
```

Where:

- g_t ∈ {0,1}

Behavior:

- g_t = 0 → no policy evaluation
- g_t = 1 → proceed to policy

Relevance determination defines the:

- authorization boundary for decision-making

It distinguishes:

- continuous situational awareness
- from discrete decision engagement

Typical conditions include:

- deviation from desired region
- instability or volatility
- persistence thresholds
- uncertainty conditions

## 6. Policy (Authority)

Policy selects outcomes when relevance conditions are satisfied.

```text
a_t = π(y_t) if g_t = 1
a_t = ∅ if g_t = 0
```

Policy is the exclusive source of authority.

Policy must be:

- deterministic
- explicitly defined
- versioned
- auditable

Policy may produce:

- actions
- escalation
- handoff
- no-op

## 7. Action and Outcome

Actions are externally visible operations.

```text
A = { a1, a2, ..., ak }
```

Outcomes extend beyond actions to include:

- no-op
- escalation
- handoff
- clarification

## 8. Control State

The system maintains internal operational state:

```text
m_t
```

Examples:

- workflow stage
- cooldown timers
- persistence counters
- escalation levels

State evolves deterministically:

```text
m\_{t+1} = f(m_t, y_t, a_t)
```

## 9. Turn Execution Flow

Each turn executes:

- receive observations
- compute signals
- construct coherent state
- project into policy space
- evaluate relevance
- (if relevant) evaluate policy
- determine outcome
- update control state

## 10. Clarification and Partial Observability

If interpretation is insufficient:

- the system may produce request_clarification

Ambiguity is surfaced explicitly rather than hidden.

## 11. Instrumentation

Each turn records:

- observations
- signals
- coherent state (x_t)
- projection (y_t)
- relevance result (g_t)
- policy version
- outcome
- action (if any)
- control state

Optional:

- confidence
- volatility

This enables full replay.

## 12. Temporal Dynamics

The system operates in discrete turns over continuous time.

Temporal logic may include:

- persistence
- aggregation
- decay
- change detection

All temporal features must be explicit and reproducible.

## 13. Layered ESMs

Multiple ESMs may operate hierarchically.

Higher-level systems may initialize downstream state.

After initialization, systems operate independently.

## 14. Instrumented Deterministic Evolution (IDE)

System behavior evolves through versioned artifacts:

- signals
- projection
- relevance logic
- policy
- control updates

All changes must be:

- versioned
- recorded
- replayable

## 15. Architectural Boundaries

Interpretation and authority remain strictly separated.

Probabilistic systems may assist interpretation but cannot authorize outcomes.

All outcomes must be:

- explicitly defined
- deterministically selected
- governed

## 16. Reference Implementation Structure

```text
signals/
projection/
relevance/
policy/
control/
instrumentation/
```

Each component is independently versioned.

## 17. Domain Adaptation

To deploy ESM:

- define signals
- construct coherent state
- define projection
- define relevance logic
- define policy
- define actions

Architecture remains invariant.

## 18. Summary

The Emergent State Machine provides a deterministic architecture for transforming observations into governed outcomes.

By separating:

- measurement
- interpretation
- relevance determination
- authority

the system achieves:

- inspectable reasoning
- deterministic control
- replayable execution
- governed evolution
