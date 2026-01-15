# atomium-ai 
AI architecture that refuses to guess under uncertainty

# Atomium — AI that refuses to guess

Atomium is a conceptual AI architecture that explores a simple idea:

**An AI system should be allowed to refuse to answer when it detects internal conflict,
instead of producing a best-guess output.**

This repository documents an early prototype and the architectural ideas behind it.
It is not a product and not a replacement for LLMs.

---

## What this is
- A small dynamic, graph-based decision system
- Components (“cells”) exchange signals via weighted connections
- Output is only allowed when internal consensus is reached

## What this is not
- Not a new LLM
- Not an ensemble or voting-over-answers system
- Not policy-based refusal or confidence thresholds
- Not a rule-based chatbot

---

## Core principles

**Conflict detection**  
Sustained divergence between internal components blocks output entirely.

**Refusal by design**  
No fallback answers. No confidence-based guessing.

**Structural mediation**  
If conflict persists, a mediator component is introduced to absorb and redistribute conflicting signals.

**Consensus gating**  
Only bounded convergence over time re-enables output.

Refusal is an *emergent property of system dynamics*, not a trained behavior.

---

## Why explore this?

Most current AI systems are optimized to always respond.
This work explores whether allowing explicit non-answer states
and structural adaptation leads to different failure modes,
stability properties, or interpretability.

---

## Status

Early prototype / exploratory research.
Shared for discussion and critical feedback.

---

## Discussion

This idea has been discussed on Reddit and Tweakers.
If you have relevant references, critiques, or comparable work,
feel free to open an issue.

## Example behavior

![Conflict vs mediator dynamics]
<img width="1495" height="543" alt="Screenshot 2026-01-14 232553" src="https://github.com/user-attachments/assets/38681bc1-6e0a-4233-8e3d-7e483c2d054d" />


## Architecture overview

Atomium is modeled as a dynamic graph of interacting components ("cells").

Each cell:
- maintains a continuous internal state
- exchanges signals with connected cells
- does not represent a neuron or a language token

The system evolves over discrete time steps via damped message passing.

Key properties:
- no backpropagation
- no training loop
- no global loss function

## Conflict detection and refusal

Conflict is defined as sustained divergence between internal cell states
beyond a configurable threshold over time.

When conflict is detected:
- the output gate is hard-blocked
- no candidate answers are generated
- the system enters a non-answering state

Refusal is therefore an emergent system property,
not a policy or confidence-based heuristic.

## Structural mediation

If conflict persists for N steps:
- a mediator cell is introduced
- the mediator does not produce output
- it absorbs, dampens, and redistributes conflicting signals

This changes the system topology instead of retraining parameters.

See [ARCHITECTURE.md](ARCHITECTURE.md) for a system description.


## More details
- [FAQ](FAQ.md)
