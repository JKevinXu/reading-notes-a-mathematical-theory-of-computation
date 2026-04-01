# Graphical Representation of a Markov Process

## Discrete Markov Processes

**Mathematical definition:**

A discrete Markov process consists of:
- Finite number of possible "states": S₁, S₂, ..., Sₙ
- Set of transition probabilities: pᵢ(j) = probability of going from state Sᵢ to state Sⱼ

**Converting to information source:**
- Produce a letter for each state transition
- States represent "residue of influence" from preceding letters

---

## Graph Representation

**Components:**
- **Nodes (junction points)** = states
- **Edges (arrows)** = transitions
- **Edge labels** = probability and letter produced

**Reading the graph:**
- Start at a state
- Follow an edge with its probability
- Produce the letter on that edge
- Arrive at next state

---

## Example B: Independent Letters (Zero-Order)

**From information-sources.md Example B:**
- 5 letters: A, B, C, D, E
- Probabilities: 0.4, 0.1, 0.2, 0.2, 0.1
- Successive choices independent

**Graph structure:**
```
        ┌─────────────────────────────────┐
        │         Single State            │
        │                                 │
        └─────────────────────────────────┘
         ↻ A (0.4)
         ↻ B (0.1)
         ↻ C (0.2)
         ↻ D (0.2)
         ↻ E (0.1)
```

**Characteristics:**
- Only 1 state (no memory of previous letters)
- All transitions loop back to same state
- Each letter has fixed probability regardless of history

---

## Example C: First-Order Markov (Digram Structure)

**From information-sources.md Example C:**
- 3 letters: A, B, C
- Transition probabilities depend on previous letter

**Graph structure:**
```
    State A ──B(0.8)──→ State B
       │                   │
       │                   │
    C(0.2)            A(0.5), B(0.5)
       │                   │
       ↓                   ↓
    State C ──────────────→
         A(0.5)
         B(0.4)
         C(0.1) ↻
```

**Characteristics:**
- 3 states (one for each letter)
- Current state = last letter produced
- Next letter depends on current state
- Example: From State A, 80% chance of B, 20% chance of C

---

## Higher-Order Markov Processes

**Trigram (Second-Order):**
- States represent pairs of previous letters
- Up to n² states for n letters
- Example: States could be AA, AB, AC, BA, BB, BC, CA, CB, CC
- Current state = last 2 letters produced
- Next letter depends on previous 2 letters

**General n-gram:**
- States represent (n-1) previous letters
- Up to n^(n-1) states
- More states = more memory = more complex patterns

---

## Key Insights

**Relationship between states and order:**
- **0-order (independent):** 1 state
- **1st-order (digram):** n states (n = number of letters)
- **2nd-order (trigram):** up to n² states
- **k-th order:** up to n^k states

**States as memory:**
- States encode "what matters from the past"
- More states = more context = richer statistical structure
- Graph makes the dependencies visual and explicit

**Practical use:**
- Graphs help design and analyze information sources
- Easy to compute probabilities by following paths
- Clear visualization of statistical structure

