# Choice, Uncertainty, and Entropy

## The Fundamental Question

**Goal:** Define a quantity to measure how much information is "produced" by a discrete information source (Markov process), or at what rate.

**Setup:**
- Set of possible events with probabilities p₁, p₂, ..., pₙ
- Probabilities are known, but not which event will occur
- Need a measure of "choice" or "uncertainty"

---

## Required Properties of H(p₁, p₂, ..., pₙ)

### Property 1: Continuity
H should be continuous in the pᵢ

**What this means:** Small changes in probabilities cause small changes in entropy.

**Example:**
- If p₁ = 0.5, p₂ = 0.5 → H ≈ 1.0 bit
- If p₁ = 0.51, p₂ = 0.49 → H ≈ 0.9997 bits
- If p₁ = 0.6, p₂ = 0.4 → H ≈ 0.971 bits

**Why important:** Entropy shouldn't jump discontinuously when probabilities change slightly.

---

### Property 2: Monotonicity for Equal Probabilities
If all pᵢ = 1/n, then H should be a monotonic increasing function of n.

**Intuition:** More equally likely events → more choice/uncertainty

**Example with equal probabilities:**

**2 outcomes:** p₁ = p₂ = 1/2
- H = log₂(2) = 1 bit

**4 outcomes:** p₁ = p₂ = p₃ = p₄ = 1/4
- H = log₂(4) = 2 bits

**8 outcomes:** All pᵢ = 1/8
- H = log₂(8) = 3 bits

**Pattern:** H increases as n increases (1 < 2 < 3)

**Why intuitive:** Choosing from 8 equally likely options requires more information (3 yes/no questions) than choosing from 2 options (1 yes/no question).

---

### Property 3: Decomposition

If a choice is broken down into successive choices, H should be the weighted sum of individual H values.

**Simple example:**

**Direct choice:** Pick one fruit from {apple, banana, cherry}
- p(apple) = 1/2
- p(banana) = 1/3
- p(cherry) = 1/6

**Two-stage choice:**
1. First: "Is it apple?" → Yes (1/2) or No (1/2)
2. If No: "Which one?" → banana (2/3) or cherry (1/3)

**Verification:**

Direct: H(1/2, 1/3, 1/6)

Two-stage: H(1/2, 1/2) + (1/2)·H(2/3, 1/3)

The (1/2) weight is because stage 2 only happens when "No" is chosen (probability 1/2).

---

**Another example - Choosing a number:**

**Direct:** Pick from {1, 2, 3, 4} with equal probability 1/4 each
- H = log₂(4) = 2 bits

**Two-stage:**
1. "Is it 1 or 2?" → Yes (1/2) or No (1/2)
2. If Yes: "Which?" → 1 (1/2) or 2 (1/2)
3. If No: "Which?" → 3 (1/2) or 4 (1/2)

**Calculation:**
- Stage 1: H(1/2, 1/2) = 1 bit
- Stage 2 (if Yes): H(1/2, 1/2) = 1 bit, happens with prob 1/2
- Stage 2 (if No): H(1/2, 1/2) = 1 bit, happens with prob 1/2

**Total:** 1 + (1/2)·1 + (1/2)·1 = 1 + 0.5 + 0.5 = 2 bits ✓

**Matches direct calculation!**

---

**Example:**

Left side: 3 possibilities with p₁ = 1/2, p₂ = 1/3, p₃ = 1/6

Right side: Two-stage choice
1. First: choose between two options (each prob 1/2)
2. If second option chosen, make another choice (probs 2/3, 1/3)

**Requirement:**
```
H(1/2, 1/3, 1/6) = H(1/2, 1/2) + (1/2)·H(2/3, 1/3)
```

The coefficient 1/2 appears because the second choice only occurs half the time.

---

## Theorem 2: The Entropy Formula

**Result:** The only H satisfying the three properties is:

```
H = -K Σᵢ pᵢ log pᵢ
```

where K is a positive constant.

**Notes:**
- K is just a choice of unit (often K=1 for natural log, or K=1/ln(2) for log₂)
- This theorem provides plausibility for the definition
- Real justification comes from implications and usefulness

---

## Entropy Definition

**Standard form (K=1):**
```
H = -Σᵢ pᵢ log pᵢ
```

**Notation:**
- If x is a random variable, write H(x) for its entropy
- x is a label, not a function argument

**Connection to statistical mechanics:**
- Same form as entropy in statistical mechanics
- pᵢ = probability of system being in cell i of phase space
- Related to Boltzmann's H theorem

---

## Binary Entropy Example

**Two possibilities:** p and q = 1-p

**Formula:**
```
H = -(p log p + q log q)
```

**Graph characteristics:**
- H = 0 when p = 0 or p = 1 (certainty)
- H is maximum at p = 0.5 (maximum uncertainty)
- Symmetric around p = 0.5
- Maximum value = 1 bit (when using log₂)

---

## Properties of Entropy

### Property 1: Zero Only at Certainty

H = 0 if and only if all pᵢ except one are zero (that one = 1)

**Interpretation:** Entropy vanishes only when outcome is certain. Otherwise H > 0.

---

### Property 2: Maximum at Equal Probabilities

For given n, H is maximum when all pᵢ = 1/n

**Maximum value:** H = log n

**Interpretation:** Equal probabilities = most uncertain situation

---

### Property 3: Joint Entropy

**Two events x and y:**
- x has m possibilities, y has n possibilities
- p(i,j) = probability of joint occurrence

**Joint entropy:**
```
H(x,y) = -Σᵢ,ⱼ p(i,j) log p(i,j)
```

**Individual entropies:**
```
H(x) = -Σᵢ,ⱼ p(i,j) log Σⱼ p(i,j)
H(y) = -Σᵢ,ⱼ p(i,j) log Σᵢ p(i,j)
```

**Inequality:**
```
H(x,y) ≤ H(x) + H(y)
```

Equality only if x and y are independent: p(i,j) = p(i)·p(j)

**Interpretation:** Uncertainty of joint event ≤ sum of individual uncertainties

---

**Simple Example 1: Independent Events**

**Setup:**
- Coin flip: x ∈ {H, T} with p(H) = p(T) = 1/2
- Die roll: y ∈ {1,2,3,4,5,6} with p(i) = 1/6 each
- Independent: p(x,y) = p(x)·p(y)

**Calculations:**
- H(x) = log₂(2) = 1 bit
- H(y) = log₂(6) ≈ 2.58 bits
- H(x,y) = log₂(12) ≈ 3.58 bits

**Check:** H(x,y) = 3.58 = 1 + 2.58 = H(x) + H(y) ✓

**Interpretation:** When independent, joint uncertainty = sum of individual uncertainties

---

**Simple Example 2: Dependent Events**

**Setup:**
- x = weather: {Sunny, Rainy}
- y = umbrella: {Yes, No}
- Dependent: people carry umbrellas when it rains

**Joint probabilities:**
```
           y=Yes   y=No
x=Sunny    0.1     0.4     → p(Sunny) = 0.5
x=Rainy    0.4     0.1     → p(Rainy) = 0.5
           ↓       ↓
        p(Yes)=0.5  p(No)=0.5
```

**Calculations:**

H(x) = -[0.5 log₂(0.5) + 0.5 log₂(0.5)] = 1 bit

H(y) = -[0.5 log₂(0.5) + 0.5 log₂(0.5)] = 1 bit

H(x,y) = -[0.1 log₂(0.1) + 0.4 log₂(0.4) + 0.4 log₂(0.4) + 0.1 log₂(0.1)]
       ≈ 1.72 bits

**Check:** H(x,y) = 1.72 < 2 = H(x) + H(y) ✓

**Interpretation:** Knowing weather tells you about umbrella (and vice versa), so joint uncertainty is less than sum.

---

**Simple Example 3: Perfectly Correlated (Extreme Case)**

**Setup:**
- x = coin flip: {H, T}
- y = same coin flip: {H, T}
- Perfectly correlated: y always equals x

**Joint probabilities:**
```
         y=H    y=T
x=H      0.5    0
x=T      0      0.5
```

**Calculations:**

H(x) = 1 bit

H(y) = 1 bit

H(x,y) = -[0.5 log₂(0.5) + 0.5 log₂(0.5)] = 1 bit

**Check:** H(x,y) = 1 < 2 = H(x) + H(y) ✓

**Interpretation:** Knowing x completely determines y, so joint uncertainty equals H(x) alone. No additional uncertainty from y.

---

### Property 4: Equalization Increases Entropy

Any change toward equalizing probabilities increases H.

**Example:** If p₁ < p₂, and we increase p₁ while decreasing p₂ by the same amount (making them more equal), then H increases.

**General averaging operation:**
```
p'ᵢ = Σⱼ aᵢⱼ pⱼ
```
where Σᵢ aᵢⱼ = Σⱼ aᵢⱼ = 1 and all aᵢⱼ ≥ 0

This increases H (except when it's just a permutation).

---

### Property 5: Conditional Entropy

**Setup:** Two events x and y (not necessarily independent)

**Conditional probability:**
```
pᵢ(j) = p(i,j) / Σⱼ p(i,j)
```

Probability that y = j given x = i

**Conditional entropy Hₓ(y):**

Average entropy of y weighted by probability of each x value:
```
Hₓ(y) = -Σᵢ,ⱼ p(i,j) log pᵢ(j)
```

**Interpretation:** How uncertain we are of y on average when we know x

**Chain rule:**

Substituting pᵢ(j) = p(i,j) / Σⱼ p(i,j):
```
Hₓ(y) = -Σᵢ,ⱼ p(i,j) log p(i,j) + Σᵢ,ⱼ p(i,j) log Σⱼ p(i,j)
      = H(x,y) - H(x)
```

Therefore:
```
H(x,y) = H(x) + Hₓ(y)
```

**Interpretation:** Uncertainty of joint event = uncertainty of x + uncertainty of y when x is known

---

### Property 6: Knowledge Never Increases Uncertainty

From Properties 3 and 5:
```
H(x) + H(y) ≥ H(x,y) = H(x) + Hₓ(y)
```

Therefore:
```
H(y) ≥ Hₓ(y)
```

**Interpretation:**
- Uncertainty of y is never increased by knowledge of x
- It decreases unless x and y are independent
- If independent, knowledge of x doesn't change uncertainty about y

---

## Key Insights

1. **Entropy measures uncertainty** - H quantifies choice/information/uncertainty
2. **Unique formula** - Only H = -Σ pᵢ log pᵢ satisfies natural requirements
3. **Maximum at uniformity** - Equal probabilities give maximum entropy
4. **Subadditivity** - Joint entropy ≤ sum of individual entropies
5. **Chain rule** - H(x,y) = H(x) + Hₓ(y)
6. **Information reduces uncertainty** - Knowing x never increases uncertainty about y
