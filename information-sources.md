# Information Sources

## Key Concept

**Channel capacity** grows logarithmically with time, measured in bits per second.

**Information source** must be described mathematically to determine how much information (bits/second) it produces.

**Central question:** How does statistical knowledge about the source reduce the required channel capacity through proper encoding?

---

## Encoding and Statistical Structure

**Telegraphy example:**

Messages are sequences of letters, but NOT completely random - they follow English statistical structure:

- Letter E is more frequent than Q
- Sequence TH is more common than XP
- This structure allows saving in time/capacity

**Encoding strategies:**

1. **Morse code:** Shortest symbol (dot) for most common letter (E); longer sequences for rare letters (Q, X, Z)
2. **Commercial codes:** Common words/phrases → short 4-5 letter codes
3. **Standardized telegrams:** Entire sentences → short number sequences

**Principle:** Exploit statistical patterns to minimize transmission time

---

## Stochastic Processes

**Definition:** A discrete source generates messages symbol by symbol, choosing successive symbols according to probabilities that may depend on:
- Previous choices
- The particular symbols in question

**Mathematical model:** A stochastic process - a system that produces a sequence of symbols governed by a set of probabilities

**Equivalence:**
- Discrete source = stochastic process
- Any stochastic process producing discrete symbols from a finite set = discrete source

**Examples of discrete sources:**
1. Natural written languages (English, German, Chinese)
2. Quantized continuous sources (PCM speech, quantized TV signal)
3. Abstract mathematical stochastic processes

---

## Example A: Equal Probability, Independent Choices

**Setup:**
- 5 letters: A, B, C, D, E
- Each with probability 0.2
- Successive choices independent

**Sample message:**
```
BDCBCECCCADCBDDAAECEEA
ABBDAEECACEEBAEECBCEAD
```

**Characteristics:**
- Completely random
- No structure or patterns
- Each position independent of others

---

## Example B: Unequal Probabilities, Independent Choices

**Setup:**
- 5 letters: A, B, C, D, E
- Probabilities: 0.4, 0.1, 0.2, 0.2, 0.1
- Successive choices independent

**Sample message:**
```
AAACDCBDCEAADADACEDA
EADCABEDADDCECAAAAAD
```

**Characteristics:**
- A appears much more frequently (40%)
- B and E are rare (10% each)
- Still independent - no influence between positions
- Different from Example A due to unequal probabilities

---

## Example C: First-Order Markov Chain (Digram Structure)

**Setup:**
- Probabilities depend on the preceding letter only
- Described by transition probabilities pᵢ(j) = probability that letter i is followed by j

**Key relationships:**

Letter frequencies:
```
p(i) = Σⱼ p(i,j) = Σⱼ p(j,i) = Σⱼ p(j)·pⱼ(i)
```

Digram probabilities:
```
p(i,j) = p(i)·pᵢ(j)
```

Normalization:
```
Σⱼ pᵢ(j) = Σᵢ p(i) = Σᵢ,ⱼ p(i,j) = 1
```

**Understanding these formulas:**

**1. Letter frequency p(i):**

The probability of letter i appearing in the text.

Example: If A appears 30% of the time, then p(A) = 0.3

**2. Transition probability pᵢ(j):**

Given that letter i just occurred, what's the probability that letter j comes next?

Example: pₐ(B) = 0.8 means "after A, there's 80% chance of B"

**3. Digram probability p(i,j):**

The probability of seeing the pair "ij" in the text.

Formula: p(i,j) = p(i)·pᵢ(j)

Example: If p(A) = 0.3 and pₐ(B) = 0.8, then p(A,B) = 0.3 × 0.8 = 0.24
- Meaning: 24% of all letter pairs are "AB"

---

**4. Computing p(i) from digrams:**

Formula: p(i) = Σⱼ p(i,j)

Sum all digrams starting with i.

Example with 3 letters A, B, C:
```
p(A,A) = 0.1
p(A,B) = 0.15
p(A,C) = 0.05
```
Then: p(A) = 0.1 + 0.15 + 0.05 = 0.3

**Why?** Every occurrence of A must be followed by something (A, B, or C), so summing all "A→?" gives total frequency of A.

---

**5. Alternative: p(i) = Σⱼ p(j,i)**

Sum all digrams ending with i.

Example:
```
p(A,B) = 0.15
p(B,B) = 0.20
p(C,B) = 0.05
```
Then: p(B) = 0.15 + 0.20 + 0.05 = 0.4

**Why?** Every occurrence of B must be preceded by something, so summing all "?→B" gives total frequency of B.

---

**6. Normalization constraints:**

**Σⱼ pᵢ(j) = 1** - After letter i, probabilities of all next letters sum to 1

Example: After A, must go somewhere:
```
pₐ(A) = 0.2
pₐ(B) = 0.5
pₐ(C) = 0.3
Sum = 1.0 ✓
```

**Σᵢ p(i) = 1** - All letter frequencies sum to 1

Example:
```
p(A) = 0.3
p(B) = 0.4
p(C) = 0.3
Sum = 1.0 ✓
```

**Σᵢ,ⱼ p(i,j) = 1** - All digram probabilities sum to 1

Example: All possible pairs AA, AB, AC, BA, BB, BC, CA, CB, CC must sum to 1.0

---

**Specific example with 3 letters (A, B, C):**

**Transition probabilities pᵢ(j):**
```
     j→  A    B    C
i↓
A       0   4/5  1/5
B      1/2  1/2   0
C      1/2  2/5  1/10
```

**Letter frequencies p(i):**
```
p(A) = 9/27
p(B) = 16/27
p(C) = 2/27
```

**Digram probabilities p(i,j):**
```
     j→    A      B      C
i↓
A         0    4/15   1/15
B       8/27   8/27    0
C       1/27  4/135  1/135
```

**Sample message:**
```
ABBABABABABABABBBABBBBBABABABABABBBACACAB
BABBBBBABBABACBBBABA
```

**Characteristics:**
- B is most common (16/27 ≈ 59%)
- After A, usually get B (4/5 probability)
- After B, equal chance of A or B
- Creates patterns like "AB" and "BB" sequences

---

## Higher-Order Processes

**Trigram (2nd-order Markov):**
- Choice depends on preceding 2 letters
- Requires trigram probabilities p(i,j,k) or transition probabilities pᵢⱼ(k)

**n-gram (n-1 order Markov):**
- Choice depends on preceding n-1 letters
- Requires n-gram probabilities p(i₁,i₂,...,iₙ) or pᵢ₁,ᵢ₂,...,ᵢₙ₋₁(iₙ)
- More complex statistical structure

---

## Example D: Word-Based Process

**Setup:**
- 5 letters: A, B, C, D, E
- 16 "words" with probabilities:

```
.10 A          .16 BEBE      .11 CABED     .04 DEB
.04 ADEB       .04 BED       .05 CEED      .15 DEED
.05 ADEE       .02 BEED      .08 DAB       .01 EAB
.01 BADD       .05 CA        .04 DAD       .05 EE
```

- Words chosen independently
- Separated by spaces

**Sample message:**
```
DAB EE A BEBE DEED DEB ADEE ADEE EE DEB BEBE BEBE BEBE
ADEE BED DEED DEED CEED ADEE A DEED DEED BEBE CABED
BEBE BED DAB DEED ADEB
```

**Characteristics:**
- Higher-level structure (words, not just letters)
- DEED and BEBE are most common words
- If all words finite length → equivalent to n-gram process
- Can generalize with transition probabilities between words

---

## Approximating Natural Languages

**Purpose:** Use artificial languages to approximate natural language structure

**Zero-order approximation:**
- All letters chosen with equal probability
- Independent choices
- No structure

**First-order approximation:**
- Letters chosen independently
- Each letter has same probability as in natural language
- Example: E chosen with p=0.12, W with p=0.02
- No influence between adjacent letters
- No preferred digrams (TH, ED, etc.)

**Second-order approximation:**
- Introduces digram structure
- After choosing a letter, next letter chosen based on digram frequencies pᵢ(j)
- Captures which letters tend to follow others

**Third-order approximation:**
- Introduces trigram structure
- Each letter chosen based on preceding 2 letters
- More realistic language patterns

**Progression:** Each higher order captures more of the statistical structure of natural language

---

## Key Insights

1. **Statistical structure enables compression** - Non-random patterns allow shorter encodings
2. **Stochastic processes model sources** - Mathematical framework for information generation
3. **Order matters** - Higher-order dependencies create more realistic language models
4. **Encoding exploits structure** - Proper encoding reduces required channel capacity
