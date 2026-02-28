Emergent State Machine (ESM)
Architectural Specification (vCurrent)

1. System Definition

The Emergent State Machine (ESM) is a deterministic control architecture composed of three strictly separated layers:

    1. Projection Operator (R) — State construction

    2. Deterministic Policy (pi) — Action authority

    3. Schema-Constrained Generative Instrument (G) — Optional bounded assistance

Behavioral evolution occurs only through explicit, versioned modification.

The architecture guarantees determinism, replayability, and traceable change.

2. Terminology

Primitive
An explicitly defined, bounded feature representing a domain-relevant signal.

Feature Vector (x_t)
The bounded scalar vector constructed from primitives.

Projection Matrix (R)
A versioned linear transformation mapping feature space to role space.

Role Score (r_t)
Projected state representing interpreted structural conditions.

Policy (pi)
Deterministic mapping from projected state and control state to action.

Control State (m_t)
Bounded internal system state (norm tier, persistence counters, cooldowns, volatility windows, etc.).

Generative Instrument (G)
Optional schema-constrained generation mechanism with no decision authority.

3. Input

At turn t:

I_t = { u_t, h_t, m_t }

Where:

- u_t = current input

- h_t = bounded rolling history

- m_t = control state

History depth is finite and versioned.

4. Primitive Feature Extraction

From input I_t, deterministic detectors compute bounded scalars:

x_t = Features(I_t)

Each feature:

- Is explicitly defined

- Has a bounded numeric range

- Is versioned

- Is independently testable

Examples include:

Role presence signals

- Intra-role coherence

- Inter-role alignment

- Temporal coherence

- Volatility measures

- Persistence counters

No feature may be unbounded.

5. Projection Operator (R)

Projection maps feature space to role space:

r_t = R x_t

Where:

R in R^(k x n)
r_t in R^k

Each row of R corresponds to a role.

Properties:

- Linear transformation

- Deterministic

- Fully versioned

- Replayable

- Projection does not branch

Projection describes structural state.
Projection does not decide action.

6. Deterministic Policy (pi)

Policy selects action:

a_t = pi(r_t, m_t)

Policy may include:

- Threshold logic

- Escalation rules

- Persistence requirements

- Cooldowns

- Norm tier thresholds

- Hard contradiction gating

Properties:

- Deterministic

- Explicit branching

- Fully versioned

- Instrumented

Policy decides action authority.

7. Control State Update

System state updates deterministically:

m\_{t+1} = f(m_t, r_t, a_t)

Examples:

- Increment persistence counters

- Adjust norm tier

- Apply cooldowns

- Update volatility windows

Control state is bounded and versioned.

8. Optional Generative Instrument (G)

Generation is optional and invoked only when policy permits.

g_t = G(I_t, schema)

Constraints:

- Output must conform to schema

- Schema validation is required

- Fail-closed on violation

- No authority to override policy

Generative output may inform feature computation but cannot bypass pi.

9. Execution Flow

At each turn:

1. Receive input I_t

2. Compute features x_t = Features(I_t)

3. Compute projection r_t = R x_t

4. Select action a_t = pi(r_t, m_t)

5. Update control state m\_{t+1} = f(m_t, r_t, a_t)

6. Optionally invoke G under policy constraints

No other execution path exists.

10. Norm Ladder

Norm Ladder is implemented within policy.

Define tier-indexed thresholds:

theta_tier

Advancement requires:

- Role score >= threshold

- Sustained signal strength

- Stable coherence

- Bounded volatility

- Persistence satisfied

Norm tier is part of control state m_t.

Projection remains unchanged across tiers.

11. Coherence Structure

Coherence is decomposed into:

- Intra-role coherence (internal consistency)

- Inter-role alignment (relational coherence)

- Temporal coherence (stability across turns)

Each coherence dimension:

- Is explicitly computed

- Is bounded

- Is versioned

Coherence may influence:

- Projection

- Policy gating

- Temporal escalation

12. Stability Guarantees

Given fixed:

- Feature definitions

- Projection matrix R

- Policy pi

- Control state initialization

The system guarantees:

- Deterministic action selection

- Replayability

- Version-differentiable behavior

- Failure localization

- Drift diagnosability

No implicit learning occurs.

13. Instrumented Deterministic Evolution (IDE)

Behavioral change occurs only through:

- Modification of primitive definitions

- Modification of projection matrix R

- Modification of policy pi

- Modification of tier thresholds

Each modification:

- Is versioned

- Is replay-tested

- Is logged

No implicit adaptation occurs.

14. Portability

To deploy ESM in a new domain:

- Define primitives

- Define bounded feature ranges

- Define projection matrix R

- Define deterministic policy pi

- Define optional generative schema

- Define norm tiers (optional)

Architecture remains invariant.

15. Constraints

ESM does not:

- Perform gradient descent

- Self-update weights

- Modify policy dynamically

- Permit generative override of authority

- Evolve without explicit version change

All adaptation is governed.

16. Formal Summary

At each turn:

x*t = Features(I_t)
r_t = R x_t
a_t = pi(r_t, m_t)
m*{t+1} = f(m_t, r_t, a_t)

Optional:

g_t = G(I_t, schema)

All components are deterministic and versioned.
