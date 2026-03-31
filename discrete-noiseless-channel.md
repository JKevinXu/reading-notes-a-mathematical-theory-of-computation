# The Discrete Noiseless Channel

## Definition

A discrete channel transmits sequences of symbols from a finite set S₁, S₂, ..., Sₙ.

**What is a symbol?**
- A symbol is a basic unit of communication - one elementary choice the channel can transmit
- Examples: a letter in teletype, a dot/dash in telegraph, a bit in digital systems
- The smallest discrete unit sent at a time

**Key properties:**
- Each symbol Sᵢ has duration tᵢ seconds (time to transmit)
- Not all sequences may be allowed (constraints exist)
- Measures: how much information can be transmitted

---

## Channel Capacity

**Definition:**
```
C = lim(T→∞) [log N(T)] / T
```

Where N(T) = number of allowed signals of duration T

---

## Example 1: Teletype (Simple Case)

**Setup:**
- 32 symbols (all equal duration)
- Any sequence allowed
- Transmits n symbols/second

**Capacity:**
- Each symbol = 5 bits (since 2⁵ = 32)
- C = 5n bits/second

**Why 5 bits?**
- log₂(32) = 5
- Each symbol choice from 32 options = 5 binary decisions

---

## Example 2: Telegraph with Constraints

**Symbols:**
1. **Dot:** 1 unit closed + 1 unit open (duration = 2)
2. **Dash:** 3 units closed + 1 unit open (duration = 4)
3. **Letter space:** 3 units open (duration = 3)
4. **Word space:** 6 units open (duration = 6)

**Constraint:** No two spaces can follow each other

**Recurrence relation:**
```
N(t) = N(t-2) + N(t-4) + N(t-5) + N(t-7) + N(t-8) + N(t-10)
```

**How to derive this:**

To count sequences of duration t, consider what symbol(s) could end the sequence:

1. **Ends with dot (duration 2):**
   - Before the dot, we need a valid sequence of duration (t-2)
   - Count: N(t-2)

2. **Ends with dash (duration 4):**
   - Before the dash, we need duration (t-4)
   - Count: N(t-4)

3. **Ends with letter space (duration 3):**
   - But space can't follow space (constraint!)
   - So before letter space, must be dot or dash
   - Two cases:
     - dot + letter space = duration 2+3 = 5 → N(t-5)
     - dash + letter space = duration 4+3 = 7 → N(t-7)

4. **Ends with word space (duration 6):**
   - Same logic - can't follow another space
   - Two cases:
     - dot + word space = 2+6 = 8 → N(t-8)
     - dash + word space = 4+6 = 10 → N(t-10)

**Total:** N(t) = N(t-2) + N(t-4) + N(t-5) + N(t-7) + N(t-8) + N(t-10)

---

**Characteristic equation:**
```
1 = X⁻² + X⁻⁴ + X⁻⁵ + X⁻⁷ + X⁻⁸ + X⁻¹⁰
```

**How to get this from the recurrence:**

The recurrence N(t) = N(t-2) + N(t-4) + N(t-5) + N(t-7) + N(t-8) + N(t-10) has an asymptotic solution of the form:

```
N(t) ≈ X₀ᵗ  (for large t)
```

Substituting into the recurrence:
```
X₀ᵗ = X₀ᵗ⁻² + X₀ᵗ⁻⁴ + X₀ᵗ⁻⁵ + X₀ᵗ⁻⁷ + X₀ᵗ⁻⁸ + X₀ᵗ⁻¹⁰
```

Divide both sides by X₀ᵗ:
```
1 = X₀⁻² + X₀⁻⁴ + X₀⁻⁵ + X₀⁻⁷ + X₀⁻⁸ + X₀⁻¹⁰
```

This is the characteristic equation.

---

**Result:** C = log X₀ = 0.539 (where X₀ is the largest positive root)

**Why this works:**

1. N(t) grows exponentially: N(t) ≈ X₀ᵗ
2. Capacity formula: C = lim(T→∞) [log N(T)] / T
3. Substitute: C = lim(T→∞) [log(X₀ᵀ)] / T = lim(T→∞) [T·log X₀] / T = log X₀
4. Solve characteristic equation numerically to find X₀
5. C = log X₀ ≈ 0.539 bits per unit time

---

## General Case: Different Symbol Durations

**Given:** Symbols S₁, ..., Sₙ with durations t₁, ..., tₙ (all sequences allowed)

**Recurrence:**
```
N(t) = N(t-t₁) + N(t-t₂) + ... + N(t-tₙ)
```

**Asymptotic behavior:**
```
N(t) ~ X₀ᵗ  (for large t)
```

**Characteristic equation:**
```
X⁻ᵗ¹ + X⁻ᵗ² + ... + X⁻ᵗⁿ = 1
```

**Capacity:** C = log X₀ (X₀ = largest real solution)

---

## State-Based Constraints

**General restriction model:**
- System has states: a₁, a₂, ..., aₘ
- Each state allows only certain symbols
- Transmitting a symbol changes the state
- This models complex constraints more elegantly than recurrence relations

**Why use states?**
- Captures "memory" of what was sent previously
- Enforces rules like "no two spaces in a row"
- State = context needed to determine what's allowed next

---

**Telegraph example (2 states):**

The constraint is: **no space can follow another space**

We need to track: "was the last symbol a space?"

**State 1:** Last symbol was NOT a space
- **Allowed symbols:** dot (2), dash (4), letter space (3), word space (6)
- **Transitions:**
  - Send dot → stay in State 1 (last symbol now = dot, not a space)
  - Send dash → stay in State 1 (last symbol now = dash, not a space)
  - Send letter space → go to State 2 (last symbol now = space!)
  - Send word space → go to State 2 (last symbol now = space!)

**State 2:** Last symbol WAS a space
- **Allowed symbols:** dot (2), dash (4) only
- **Why restricted?** Can't send another space (would violate constraint)
- **Transitions:**
  - Send dot → go to State 1 (last symbol now = dot, not a space)
  - Send dash → go to State 1 (last symbol now = dash, not a space)

---

---

**Graph representation:**
```
State 1 ⟲ (dot, dash)
State 1 → State 2 (letter space, word space)
State 2 → State 1 (dot, dash)
```

**Visual diagram:**
```
        dot(2), dash(4)
    ┌─────────────────────┐
    │                     │
    ▼                     │
┌─────────┐               │
│ State 1 │               │
│(non-sp) │───────────────┘
└─────────┘
    │
    │ letter_space(3)
    │ word_space(6)
    │
    ▼
┌─────────┐
│ State 2 │
│(space)  │
└─────────┘
    │
    │ dot(2), dash(4)
    │
    └──────────────────────> back to State 1
```

---

**Example sequence walkthrough:**

Let's trace: **dot → dash → letter_space → dot → word_space → dash**

1. Start in State 1
2. Send **dot** (duration 2) → stay in State 1 (last = non-space)
3. Send **dash** (duration 4) → stay in State 1 (last = non-space)
4. Send **letter_space** (duration 3) → move to State 2 (last = space)
5. Send **dot** (duration 2) → move to State 1 (last = non-space)
6. Send **word_space** (duration 6) → move to State 2 (last = space)
7. Send **dash** (duration 4) → move to State 1 (last = non-space)

Total duration: 2+4+3+2+6+4 = 21 time units

**Invalid sequence:** dot → letter_space → word_space
- After letter_space, we're in State 2
- State 2 doesn't allow word_space (another space)
- Sequence is **forbidden** by the constraint

---

## Theorem 1: State-Based Capacity

**Notation note:**
- W⁻ᵗ means 1/Wᵗ (W to the power of -t)
- Examples: W⁻¹ = 1/W, W⁻² = 1/W², W⁻³ = 1/W³
- Represents "discount factor" for a symbol of duration t
- Longer durations → smaller contribution to the sum

**Given:**
- b(s)ᵢⱼ = duration of sth symbol allowed in state i leading to state j
- δᵢⱼ = 1 if i=j, else 0

**Capacity formula:**
```
C = log W
```

Where W is the largest real root of:
```
|∑ₛ W⁻ᵇ⁽ˢ⁾ⁱʲ - δᵢⱼ| = 0
```

**Telegraph example determinant:**
```
| 1-(W⁻²+W⁻⁴)      -(W⁻³+W⁻⁶)    |
| -(W⁻²+W⁻⁴)    1-(W⁻²+W⁻⁴)      | = 0
```

Expands to the characteristic equation found earlier.

---

### Understanding the Formula with Simple Examples

**Example 1: Single state, two symbols**

Suppose we have:
- 1 state only
- Symbol A: duration 1
- Symbol B: duration 2
- All sequences allowed

**Build the matrix:**
- State 1 to State 1 via A (duration 1): contributes W⁻¹
- State 1 to State 1 via B (duration 2): contributes W⁻²

**Determinant equation:**
```
|W⁻¹ + W⁻² - 1| = 0
```

This simplifies to:
```
W⁻¹ + W⁻² = 1
```

Multiply by W²:
```
W + 1 = W²
W² - W - 1 = 0
```

Solve: W = (1 + √5)/2 ≈ 1.618 (golden ratio!)

**Capacity:** C = log(1.618) ≈ 0.694 bits per time unit

---

**Example 2: Two states with constraints**

Setup:
- State 1: can send symbol A (duration 2) → stay in State 1
- State 1: can send symbol B (duration 3) → go to State 2
- State 2: can send symbol A (duration 2) → go back to State 1

**Build the matrix (2×2):**

Position (1,1): State 1 → State 1
- Symbol A with duration 2: contributes W⁻²
- Entry: W⁻² - 1 (subtract δ₁₁ = 1)

Position (1,2): State 1 → State 2
- Symbol B with duration 3: contributes W⁻³
- Entry: W⁻³ - 0 = W⁻³

Position (2,1): State 2 → State 1
- Symbol A with duration 2: contributes W⁻²
- Entry: W⁻² - 0 = W⁻²

Position (2,2): State 2 → State 2
- No symbols go from State 2 to itself
- Entry: 0 - 1 = -1

**Determinant:**
```
| W⁻²-1    W⁻³  |
| W⁻²      -1   | = 0
```

Expand:
```
(W⁻²-1)(-1) - (W⁻³)(W⁻²) = 0
-W⁻² + 1 - W⁻⁵ = 0
1 = W⁻² + W⁻⁵
```

Multiply by W⁵:
```
W⁵ = W³ + 1
W⁵ - W³ - 1 = 0
```

Solve numerically for W, then C = log W

---

**Step-by-step guide to apply Theorem 1:**

1. **Draw the state diagram**
   - Identify all states
   - Mark allowed symbols and their durations
   - Show state transitions

2. **Create the matrix**
   - Size: m×m (m = number of states)
   - For each position (i,j):
     - Sum W⁻ᵇ for all symbols going from state i to state j
     - If i=j, subtract 1

3. **Set up determinant equation**
   - |Matrix| = 0

4. **Expand and simplify**
   - Get polynomial equation in W

5. **Solve for W**
   - Find largest positive real root

6. **Calculate capacity**
   - C = log W (or log₂ W for bits)

---

## Key Insights

1. **Capacity is logarithmic** - relates to exponential growth of sequences
2. **Constraints reduce capacity** - fewer allowed sequences = lower C
3. **State machines model restrictions** - powerful framework for complex constraints
4. **Asymptotic behavior** - N(t) grows exponentially as X₀ᵗ
