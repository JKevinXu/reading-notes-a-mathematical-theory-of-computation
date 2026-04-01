# Ergodic and Mixed Sources

## Ergodic Processes - Basic Concept

**Definition (intuitive):**

An ergodic process is one where every sequence produced has the same statistical properties.

**Key property:**

As sequence length increases, statistical measures (letter frequencies, digram frequencies, etc.) approach definite limits that are:
- Independent of the particular sequence
- The same for (almost) all sequences

**Exception:** Some sequences may not have this property, but the probability of getting such a sequence is zero.

**Simple interpretation:** Ergodic = statistically homogeneous

---

## Graph Conditions for Ergodic Processes

A Markov process is ergodic if its graph satisfies two conditions:

### Condition 1: Strong Connectivity

The graph must NOT consist of two isolated parts A and B where:
- Cannot go from A to B following arrows
- Cannot go from B to A following arrows

**In other words:** Must be able to reach any state from any other state (eventually)

**Example of violation:**
```
Part A: State 1 ⟲ ⟲ State 2
Part B: State 3 ⟲ ⟲ State 4
(No arrows between A and B)
```

---

### Condition 2: Aperiodic (GCD = 1)

**Definitions:**
- **Circuit:** A closed series of lines with all arrows pointing in same direction
- **Length:** Number of lines in the circuit

**Requirement:** The greatest common divisor (GCD) of all circuit lengths must be 1

**Example:** If circuit lengths are 3, 5, 7 → GCD(3,5,7) = 1 ✓

**Simple example - Finding circuits:**

Consider a graph:
```
State A ──→ State B ──→ State C ──→ State A
   ↓                                    ↑
   └────────────────────────────────────┘
```

**Circuits:**
1. A → B → C → A (length 3)
2. A → A (direct loop, length 1)

**GCD(3, 1) = 1** ✓ Ergodic (satisfies Condition 2)

---

**Example violating Condition 2 (GCD = 2):**

```
State A ──→ State B ──→ State A
```

**Circuits:**
- A → B → A (length 2)

**GCD(2) = 2** ✗ Not ergodic (periodic with period 2)

**What happens:** Must alternate between A and B. Can only return to A after even number of steps.

---

**Example with GCD = 3:**

```
State A ──→ State B ──→ State C ──→ State A
```

**Circuits:**
- A → B → C → A (length 3)

**GCD(3) = 3** ✗ Not ergodic (periodic with period 3)

**What happens:** Must cycle A → B → C → A → B → C... Can only return to A after multiples of 3 steps.

---

**Example with GCD = 1 (multiple circuits):**

```
State A ──→ State B ──→ State A
   ↓                       ↑
   └───→ State C ──────────┘
```

**Circuits:**
1. A → B → A (length 2)
2. A → C → A (length 2)
3. A → B → A → C → A (length 4)

**GCD(2, 2, 4) = 2** ✗ Still periodic!

**Better example:**
```
State A ──→ State B ──→ State A
   ↓
   └───→ State C ──→ State D ──→ State A
```

**Circuits:**
1. A → B → A (length 2)
2. A → C → D → A (length 3)

**GCD(2, 3) = 1** ✓ Ergodic!

**Why it works:** With circuits of length 2 and 3, you can return to A after 2, 3, 4 (2+2), 5 (3+2), 6 (3+3 or 2+2+2), etc. Eventually can return after ANY number of steps.

---

## Periodic Case (GCD = d > 1)

**What happens when Condition 2 is violated:**

If GCD of circuit lengths = d > 1, sequences have periodic structure.

**Characteristics:**
- Sequences fall into d different classes
- Classes are statistically the same except for shift of origin
- Any sequence can be made equivalent to any other by shifting 0 to d-1 positions

**Example with d = 2:**

3 letters: a, b, c
- After a: go to b (prob 1/3) or c (prob 2/3)
- After b or c: always go to a

Typical sequence:
```
abacacacabacababacac
```

Pattern: a alternates with b or c (period 2)

**Note:** This periodic case is not important for most communication work.

---

## Mixed Sources

**What happens when Condition 1 is violated:**

The graph separates into multiple subgraphs, each satisfying Condition 1 (and assumed to satisfy Condition 2).

**Definition:**

A mixed source is made up of pure ergodic components:
```
L = p₁L₁ + p₂L₂ + p₃L₃ + ...
```

Where:
- Lᵢ = component source (ergodic)
- pᵢ = probability of component i

---

**Physical interpretation:**

1. There are several different ergodic sources L₁, L₂, L₃, ...
2. We don't know in advance which will be used
3. Once a sequence starts in component Lᵢ, it continues indefinitely in that component
4. Each component has its own homogeneous statistical structure

**Example:**

Take two processes from earlier examples:
```
L = 0.2L₁ + 0.8L₂
```

To generate a sequence:
1. Choose L₁ with probability 0.2, or L₂ with probability 0.8
2. Generate entire sequence from the chosen component

---

## Ergodic Property - Practical Implications

**Assumption:** Unless stated otherwise, we assume sources are ergodic.

**Key benefit:** Can identify averages along a sequence with averages over the ensemble.

**Example:**

The relative frequency of letter A in a particular infinite sequence will equal (with probability 1) its relative frequency in the ensemble of all sequences.

**In practice:**
- Can estimate probabilities from a single long sequence
- Don't need to generate many sequences
- One sequence is statistically representative

---

## Stationary Conditions

**For a stationary process:**

If Pᵢ = probability of being in state i, and pᵢ(j) = transition probability from i to j, then:

```
Pⱼ = Σᵢ Pᵢ·pᵢ(j)
```

**Interpretation:** Equilibrium condition - probability of being in state j equals sum of probabilities of arriving there from all other states.

**Convergence in ergodic case:**

Starting from any initial conditions, the probabilities Pⱼ(N) of being in state j after N symbols approach the equilibrium values as N → ∞.

---

## Key Insights

1. **Ergodic = homogeneous** - All sequences have same statistical properties
2. **Graph structure determines ergodicity** - Check connectivity and aperiodicity
3. **Mixed sources = weighted components** - Separate ergodic parts
4. **Practical advantage** - Single sequence sufficient for statistical analysis
5. **Equilibrium exists** - Probabilities converge to steady state

