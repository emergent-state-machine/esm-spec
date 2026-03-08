# Emergent State Machine (ESM)

## Architectural Specification (v1.0.0)

## 1. System Definition

The **Emergent State Machine (ESM)** is a deterministic, turn-based control architecture for governing state mutation in model-assisted systems.

The architecture is composed of three structurally separated layers:

1. **Signal Layer** — Structured state observation and measurement
2. **Projection Layer** — Interpretable state construction
3. **Authority Layer** — Deterministic, versioned mutation control

All authoritative state mutation occurs exclusively within the **Authority Layer**.

Optional generative mechanisms MAY assist interpretation but SHALL NOT possess decision authority.

Behavioral evolution occurs only through explicit, versioned modification of system components.

The architecture guarantees:

- determinism
- replayability
- traceable change
- inspectable decision boundaries

## 2. Terminology

### Primitive Detector

A **primitive detector** is a deterministic function that extracts a bounded scalar measurement from system input.

Primitive detectors represent domain-relevant measurement instruments defined by system designers or domain experts.

Primitive detectors MUST:

- be explicitly defined
- produce bounded outputs
- be versioned
- be independently testable

### Signal

A **signal** is the bounded scalar value produced by a primitive detector.

Signals represent **measured conditions of the system state**.

Signals are deterministic measurements and do not contain interpretation or decision authority.

### Feature Vector (`x_t`)

The **feature vector** is the ordered collection of signal values produced by primitive detectors during a turn.

```text
x_t = [s₁, s₂, …, sₙ]

Where each sᵢ is a signal.

Projection Matrix / Projection Function (R or P)

A projection maps the feature vector into interpreted structural state.

Projection produces role scores representing interpreted system conditions.

Projection MAY be implemented as:

linear transformation

deterministic function

probabilistic or model-assisted interpretation

Projection outputs MUST remain structured and deterministic with respect to recorded inputs and environment identifiers.

Role Score (r_t)

A role score represents an interpreted structural condition derived from signals.

Role scores describe the degree to which the system state occupies a particular structural role.

Examples include:

stability

alignment

claim strength

defect likelihood

system drift

Role scores are interpreted state, not authoritative decisions.

Policy (π)

A policy is a deterministic mapping from interpreted state and control state to an action.

a_t = π(r_t, m_t)

Policy contains explicit decision rules governing system behavior.

Control State (m_t)

Control state represents the internal operational state of the system.

Examples include:

norm tiers

persistence counters

cooldown timers

volatility windows

active objective

workflow stage

operating mode

Control state evolves deterministically across turns.

Generative Instrument (G)

A generative instrument is an optional schema-constrained generative mechanism.

Generative instruments MAY assist interpretation or structured input generation but SHALL NOT mutate authoritative system state.

Generative outputs MUST:

conform to explicit schema

be versioned

fail closed on validation violation

3. Input

At turn t:

I_t = { u_t, h_t, m_t }

Where:

u_t = current input

h_t = bounded rolling history

m_t = control state

History depth is finite and versioned.

4. Signal Layer

The Signal Layer performs deterministic measurement of observable system conditions.

The Signal Layer consists of two internal stages:

Primitive Detection

Signal Assembly

Primitive detectors operate on system input:

s_i = detector_i(I_t)

Signals are then assembled into the feature vector:

x_t = [s₁, s₂, …, sₙ]

Signals represent policy-relevant measurements required to evaluate system state at the current turn.

Signals MUST:

be bounded

be deterministic

be versioned

represent measurable system properties

The Signal Layer performs measurement only and does not perform interpretation or decision making.

5. Projection Layer

Projection transforms measured signals into interpreted structural state.

r_t = R x_t

or

r_t = P(x_t)

Where:

x_t = feature vector

r_t = role scores

Projection describes structural conditions of the system.

Examples include:

system stability

argument structure

process drift

coordination alignment

Projection does not produce decisions.

Projection Determinism and Allowed Implementations

Projection MAY include:

linear transformation

deterministic algorithms

probabilistic interpretation

constrained generative interpretation

Regardless of implementation, projection MUST satisfy:

Replayability

Projection MUST be reproducible given:

signal_pack_id

projection_version_id

projection_input_ref

projection_env_id

No Authority

Projection MUST NOT mutate authoritative system state.

Structured Output

Projection outputs MUST be structured and suitable for deterministic policy evaluation.

Versioning

Projection logic MUST be explicitly versioned.

6. Authority Layer (Policy)

Policy selects the authoritative system action.

a_t = π(r_t, m_t)

Policy MAY include:

threshold logic

escalation rules

persistence requirements

cooldown constraints

tier thresholds

contradiction gating

Policy properties:

deterministic

explicit

fully versioned

inspectable

Policy is the only component permitted to authorize state mutation.

7. Control State Update

After action selection, system state evolves deterministically:

m_{t+1} = f(m_t, r_t, a_t)

Examples include:

updating persistence counters

adjusting operational tiers

triggering cooldowns

advancing workflow stages

updating objectives

Control state evolution is fully versioned.

8. Optional Generative Assistance

Generative instruments MAY assist interpretation or structured input generation.

However:

generative mechanisms SHALL NOT mutate authoritative state

generative outputs MUST be schema-constrained

generative outputs MUST be traceable to versioned generation logic

All generative outputs must pass validation before entering the decision pipeline.

9. Execution Flow

At each turn:

Receive input I_t

Run primitive detectors

Assemble signals into feature vector x_t

Compute projection r_t

Evaluate policy a_t = π(r_t, m_t)

Update control state m_{t+1}

Optionally invoke generative instruments under policy constraints

No other execution path exists.

10. Norm Ladder

Norm ladders implement staged progression of acceptable system behavior.

Each tier defines threshold requirements for interpreted state.

Advancement requires:

role score ≥ threshold

sustained signal strength

bounded volatility

persistence requirements

Norm tiers are represented within control state.

Norm ladders may represent:

skill progression

operational maturity stages

escalation tiers

safety gates

Projection remains unchanged across tiers.

11. Coherence Structure

Coherence may be decomposed into dimensions such as:

intra-role coherence

inter-role alignment

temporal coherence

Each dimension:

is explicitly computed

is bounded

is versioned

Coherence signals may influence projection or policy gating.

12. Stability Guarantees

Given fixed:

primitive detectors

signal definitions

projection logic

policy logic

control state initialization

The system guarantees:

deterministic action selection

replayable decision history

version-differentiable behavior

failure localization

drift diagnosability

No implicit learning occurs.

13. Instrumented Deterministic Evolution (IDE)

System behavior evolves only through explicit modification of:

primitive detectors

signal definitions

projection logic

policy logic

tier thresholds

Each modification MUST be:

versioned

replay-tested

recorded

No implicit adaptation occurs.

14. Portability

To deploy ESM in a new domain:

define primitive detectors

define signal ranges

define projection logic

define deterministic policy

optionally define generative schema

optionally define norm ladders

The architecture itself remains invariant.

15. Composition of ESMs

Emergent State Machines may be composed hierarchically.

Higher-level ESMs may:

set objectives

define operating modes

update policy context

Lower-level ESMs operate within those conditions while maintaining their own deterministic turn boundaries.

Each ESM remains locally deterministic and fully replayable.

16. Constraints

An ESM does not:

perform gradient descent

modify policy dynamically

self-update weights

allow generative override of authority

evolve without explicit version change

All adaptation is governed.

17. Formal Summary

At each turn:

s_i = detector_i(I_t)
x_t = [s₁ … sₙ]
r_t = P(x_t)
a_t = π(r_t, m_t)
m_{t+1} = f(m_t, r_t, a_t)

Optional:

g_t = G(I_t, schema)

All components are deterministic, versioned, and replayable.
```
