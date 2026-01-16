# Technical Notes: Atomium Dynamics (Minimal)

This document provides a minimal, implementation-agnostic sketch
of the system dynamics behind Atomium.

It is not a reference implementation.

---

## State representation

Each cell i maintains a state vector:

h_i(t) ∈ ℝ^n   (or ℂ^n in some prototypes)

The exact dimensionality is intentionally unspecified.

---

## Message passing

Each directed edge (j → i) has a weight w_ji.

At each time step:

m_i(t) = Σ_j w_ji · h_j(t)

---

## State update (conceptual)

State updates follow a damped integration:

h_i(t+1) = (1 − α) · h_i(t) + α · f(m_i(t))

Where:
- α ∈ (0,1) is a damping / leak factor
- f(·) is a bounded activation (e.g. tanh, clipping, normalization)

No loss function.
No backpropagation.
No training loop.

---

## Conflict metric (example)

For a set of relevant cells R:

D(t) = max_{i,j ∈ R} || h_i(t) − h_j(t) ||

Conflict is active if:

D(t) > θ   for all t ∈ [T − W, T]

Where:
- θ is a divergence threshold
- W is a sliding window length

---

## Refusal gating

If conflict is active:
- output = BLOCKED
- no candidate answers are generated

This is a hard gate, not a heuristic.

---

## Structural mediation (sketch)

If conflict persists for N steps:
- introduce mediator cell k
- connect conflicting cells to k with bounded weights
- mediator redistributes signals but does not produce output

Mediator influence is constrained:
- bounded weights
- optional decay / removal after stabilization

---

## Consensus

Consensus is reached if:

|| h_i(t+Δ) − h_i(t) || < ε   for all i ∈ R

for Δ ≥ C steps.

Only then is output unblocked.
