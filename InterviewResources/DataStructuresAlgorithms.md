# Data Structures & Algorithms Interview Handbook

**Target Role:** Software Engineer, Backend Developer, Algorithm Engineer, Competitive Programmer.  
**Focus:** Fundamentals to Advanced DSA Concepts (Fresher to Principal Level). 

---

## Table of Contents

### Part 0 — Foundations
- Mathematical Foundations
- Logarithms & Properties
- Summations & Series
- Recurrence Relations
- Master Theorem
- Proof Techniques
- Algorithm Analysis
- Time Complexity (Big O, Omega, Theta)
- Space Complexity
- Amortized Analysis
- Asymptotic Growth
- Memory & Computation Model
- Stack vs Heap
- Recursion Stack Behavior

### Part I — Core Data Structures
- Arrays (Static, Dynamic, Multidimensional)
- Prefix Sum, Sliding Window, Two Pointer
- Kadane's Algorithm
- Linked Lists (Singly, Doubly, Circular)
- Fast & Slow Pointer, Cycle Detection
- Stack (Array & Linked List Implementation)
- Monotonic Stack, Expression Evaluation
- Queue (Linear, Circular, Deque)
- Monotonic Queue
- Hashing & Hash Tables
- Collision Resolution, Load Factor

### Part II — Trees
- Tree Fundamentals
- Binary Trees & Traversals
- Binary Search Trees (BST)
- Self-Balancing Trees (AVL, Red-Black, Splay)
- B-Trees & B+ Trees
- Heaps (Min Heap, Max Heap)
- Priority Queues
- Advanced Trees (Trie, Segment Tree, Fenwick Tree)

### Part III — Graph Theory
- Graph Fundamentals & Representations
- Graph Traversal (BFS, DFS)
- Shortest Path (Dijkstra, Bellman-Ford, Floyd-Warshall)
- Minimum Spanning Tree (Kruskal, Prim)
- Topological Sorting
- Strongly Connected Components
- Network Flow

### Part IV — Algorithm Paradigms
- Divide and Conquer
- Greedy Algorithms
- Dynamic Programming (Memoization, Tabulation)
- Backtracking
- Recursion

### Part V — Searching & Sorting
- Searching Algorithms
- Sorting Algorithms (Comparison & Non-Comparison)
- Stability & In-Place Sorting

### Part VI — String Algorithms
- Pattern Matching
- KMP, Rabin-Karp, Z-Algorithm
- Suffix Array & Suffix Tree

### Part VII — Mathematical & Special Algorithms
- Number Theory
- Computational Geometry
- Disjoint Set Union (Union-Find)
- Advanced Topics (FFT, Matrix Exponentiation)

### Part VIII — Complexity & Theory
- P, NP, NP-Complete, NP-Hard
- Intractable Problems
- Game Tree Search

### Part IX — Practical Patterns & System-Level DS
- Problem-Solving Patterns
- LRU Cache, LFU Cache
- Consistent Hashing
- Bloom Filters

---

## Part 0 — Foundations

### 0.1 Mathematical Foundations

#### Logarithms

**What is a Logarithm?**

A logarithm answers the fundamental question: *"To what power must we raise a base to get a certain number?"*

**Formal Definition**:

If $b^y = x$, then $\log_b(x) = y$

Where:
- $b$ is the **base** (the number being raised to a power)
- $y$ is the **exponent** (the answer we're looking for)
- $x$ is the **result** (the number we want to express as a power)

**Example**: Since $2^3 = 8$, we can say $\log_2(8) = 3$

---

**Why Logarithms Matter in Computer Science**

Logarithms appear everywhere in algorithm analysis because they represent **exponential inverse growth**:

1. **Binary Search**: $O(\log n)$ - Each comparison halves the search space
2. **Tree Height**: A balanced binary tree with $n$ nodes has height $O(\log n)$
3. **Divide & Conquer**: Algorithms that recursively split problems in half
4. **Bit Representation**: Number of bits needed to represent $n$ is $\lceil \log_2(n+1) \rceil$
5. **Sorting Lower Bound**: Comparison-based sorting requires at least $O(n \log n)$ comparisons

**Key Insight**: Logarithms grow **extremely slowly**. Even for 1 billion elements, $\log_2(10^9) \approx 30$.

---

**Common Logarithm Bases**

| Notation | Base | Primary Use |
|:---------|:-----|:------------|
| $\log_2(x)$ or $\lg(x)$ | 2 | **Computer Science** - Binary operations, tree analysis |
| $\log_{10}(x)$ or $\log(x)$ | 10 | Scientific calculations, orders of magnitude |
| $\ln(x)$ or $\log_e(x)$ | $e \approx 2.718$ | Calculus, continuous growth, natural processes |

**Convention**: In algorithm analysis, $\log n$ typically means $\log_2 n$ (base 2).

---

**Essential Logarithm Properties**

1. **Product Rule**: $\log_b(xy) = \log_b(x) + \log_b(y)$
   - *Multiplying numbers becomes adding logarithms*
   - Example: $\log_2(8 \times 4) = \log_2(8) + \log_2(4) = 3 + 2 = 5$
   - Verification: $2^5 = 32 = 8 \times 4$ ✓

2. **Quotient Rule**: $\log_b\left(\frac{x}{y}\right) = \log_b(x) - \log_b(y)$
   - *Dividing numbers becomes subtracting logarithms*
   - Example: $\log_2\left(\frac{16}{4}\right) = \log_2(16) - \log_2(4) = 4 - 2 = 2$
   - Verification: $2^2 = 4 = \frac{16}{4}$ ✓

3. **Power Rule**: $\log_b(x^n) = n \cdot \log_b(x)$
   - *Exponentiation becomes multiplication*
   - Example: $\log_2(8^3) = 3 \cdot \log_2(8) = 3 \times 3 = 9$
   - Verification: $2^9 = 512 = 8^3$ ✓

4. **Change of Base Formula**: $\log_b(x) = \frac{\log_c(x)}{\log_c(b)}$
   - *Convert between different logarithm bases*
   - Example: $\log_2(8) = \frac{\log_{10}(8)}{\log_{10}(2)} = \frac{0.903}{0.301} \approx 3$

5. **Identity Properties**:
   - $\log_b(b) = 1$ (because $b^1 = b$)
   - $\log_b(1) = 0$ (because $b^0 = 1$)
   - $b^{\log_b(x)} = x$ (logarithm and exponentiation cancel out)

---

**Logarithm Growth Comparison**

Understanding how slowly logarithms grow:

| $n$ | $\log_2(n)$ | $\log_{10}(n)$ | $\ln(n)$ |
|:----|:------------|:---------------|:---------|
| 1 | 0 | 0 | 0 |
| 10 | 3.32 | 1 | 2.30 |
| 100 | 6.64 | 2 | 4.61 |
| 1,000 | 9.97 | 3 | 6.91 |
| 1,000,000 | 19.93 | 6 | 13.82 |
| 1,000,000,000 | 29.90 | 9 | 20.72 |

**Observation**: To go from 1 million to 1 billion (1000× increase), $\log_2$ only increases by ~10!

**Ruby Examples**:
```ruby
# Logarithm calculations in Ruby
require 'bigdecimal/math'

# Binary logarithm (log base 2)
def log2(n)
  Math.log2(n)
end

# Common logarithm (log base 10)
def log10(n)
  Math.log10(n)
end

# Natural logarithm
def ln(n)
  Math.log(n)
end

# Change of base formula: log_b(x) = ln(x) / ln(b)
def log_base(x, base)
  Math.log(x) / Math.log(base)
end

# Examples
puts log2(8)           # => 3.0 (because 2^3 = 8)
puts log2(1024)        # => 10.0 (because 2^10 = 1024)
puts log10(100)        # => 2.0 (because 10^2 = 100)
puts log_base(27, 3)   # => 3.0 (because 3^3 = 27)
```

**Why Logarithms Matter in DSA**:
- **Binary Search**: O(log n) - halves search space each iteration
- **Balanced Trees**: Height is O(log n) for n nodes
- **Merge Sort**: O(n log n) - log n levels, n work per level
- **Heap Operations**: O(log n) - tree height

**Interview Question**: "Why is binary search $O(\log n)$?"

**Answer**: At each step, we eliminate half the remaining elements. If we start with $n$ elements:
- After 1 comparison: $\frac{n}{2}$ elements remain
- After 2 comparisons: $\frac{n}{4}$ elements remain
- After $k$ comparisons: $\frac{n}{2^k}$ elements remain

We stop when $\frac{n}{2^k} = 1$. Solving for $k$:

$$\frac{n}{2^k} = 1$$
$$n = 2^k$$
$$k = \log_2(n)$$

Therefore, binary search requires $O(\log n)$ comparisons.

---

#### Summations & Series

**What are Summations?**

Summations represent the sum of a sequence of terms. They're crucial for analyzing loops and recursive algorithms.

**Notation**: $\sum_{i=1}^{n} f(i)$ means "sum $f(i)$ for $i$ from 1 to $n$"

---

**1. Arithmetic Series**

**Definition**: Sum of consecutive integers

$$\sum_{i=1}^{n} i = 1 + 2 + 3 + \cdots + n = \frac{n(n+1)}{2}$$

**Complexity**: $O(n^2)$ when $n$ is the variable

**Derivation** (Gauss's Method):
```
  S = 1   + 2   + 3   + ... + (n-1) + n
+ S = n   + (n-1) + (n-2) + ... + 2   + 1
────────────────────────────────────────────
 2S = (n+1) + (n+1) + (n+1) + ... + (n+1) + (n+1)
 2S = n(n+1)
  S = n(n+1)/2
```

**Example**: $\sum_{i=1}^{100} i = \frac{100 \times 101}{2} = 5050$

**Use Case**: Analyzing nested loops where inner loop depends on outer loop index

---

**2. Geometric Series**

**Definition**: Each term is a constant multiple of the previous term

$$\sum_{i=0}^{n} ar^i = a + ar + ar^2 + \cdots + ar^n = a \cdot \frac{r^{n+1} - 1}{r - 1}$$

**Special Case** (Powers of 2):

$$\sum_{i=0}^{n} 2^i = 1 + 2 + 4 + 8 + \cdots + 2^n = 2^{n+1} - 1$$

**Complexity**: $O(2^n)$ - exponential growth

**Key Insight**: The last term dominates! $2^n > 1 + 2 + 4 + \cdots + 2^{n-1}$

**Example**: $1 + 2 + 4 + 8 + 16 = 31 = 2^5 - 1$

**Use Case**:
- Binary tree nodes: A complete binary tree of height $h$ has $2^{h+1} - 1$ nodes
- Recursive algorithms that double work at each level

---

**3. Harmonic Series**

**Definition**: Sum of reciprocals

$$H_n = \sum_{i=1}^{n} \frac{1}{i} = 1 + \frac{1}{2} + \frac{1}{3} + \cdots + \frac{1}{n} \approx \ln(n)$$

**Complexity**: $O(\log n)$

**Key Property**: Grows very slowly, approximately equal to natural logarithm

**Example**:
- $H_{10} = 1 + 0.5 + 0.333... + ... + 0.1 \approx 2.93$
- $\ln(10) \approx 2.30$

**Use Case**:
- QuickSort average case analysis
- Hash table collision analysis
- Coupon collector problem

**Ruby Implementation**:
```ruby
# Arithmetic series: 1 + 2 + 3 + ... + n
def arithmetic_sum(n)
  n * (n + 1) / 2
end

# Geometric series: 1 + 2 + 4 + ... + 2^n
def geometric_sum_powers_of_2(n)
  (2 ** (n + 1)) - 1
end

# General geometric series: a + ar + ar² + ... + ar^(n-1)
def geometric_sum(a, r, n)
  return a * n if r == 1
  a * ((r ** n) - 1) / (r - 1)
end

# Harmonic series (approximate)
def harmonic_sum(n)
  (1..n).sum { |i| 1.0 / i }
end

# Examples
puts arithmetic_sum(100)           # => 5050
puts geometric_sum_powers_of_2(10) # => 2047
puts harmonic_sum(10).round(4)     # => 2.9290
```

**Common Loop Analysis Using Summations**:

**Example 1**: Nested loops with constant bounds
```ruby
# O(n²) - Both loops run n times
def example1(n)
  sum = 0
  (1..n).each do |i|
    (1..n).each do |j|
      sum += i * j  # Constant work
    end
  end
  sum
end
```
**Analysis**: $\sum_{i=1}^{n} \sum_{j=1}^{n} 1 = \sum_{i=1}^{n} n = n \cdot n = n^2$

---

**Example 2**: Triangular pattern (dependent loops)
```ruby
# O(n²) - Inner loop depends on outer loop
def example2(n)
  sum = 0
  (1..n).each do |i|
    (1..i).each do |j|  # Inner loop runs i times
      sum += j
    end
  end
  sum
end
```
**Analysis**:
$$\sum_{i=1}^{n} \sum_{j=1}^{i} 1 = \sum_{i=1}^{n} i = \frac{n(n+1)}{2} = O(n^2)$$

Total iterations: $1 + 2 + 3 + \cdots + n = \frac{n(n+1)}{2}$ (arithmetic series)

---

**Example 3**: Logarithmic inner loop
```ruby
# O(n log n) - Outer linear, inner logarithmic
def example3(n)
  sum = 0
  (1..n).each do |i|
    j = n
    while j > 0
      sum += j
      j /= 2  # Halving each iteration
    end
  end
  sum
end
```
**Analysis**:
- Outer loop: $n$ iterations
- Inner loop: $\log_2(n)$ iterations (halving from $n$ to 1)
- Total: $n \times \log_2(n) = O(n \log n)$

---

#### Recurrence Relations

**What is a Recurrence Relation?**

A recurrence relation defines a sequence where each term is expressed as a function of previous terms. In algorithm analysis, they describe the running time of recursive algorithms.

**General Form**: $T(n) = \text{(work to split)} + \text{(recursive calls)} + \text{(work to combine)}$

---

**Common Recurrence Patterns**

| Recurrence | Solution | Intuition | Example Algorithm |
|:-----------|:---------|:----------|:------------------|
| $T(n) = T(n-1) + O(1)$ | $O(n)$ | Decrease by 1, constant work | Linear search, factorial |
| $T(n) = T(n-1) + O(n)$ | $O(n^2)$ | Decrease by 1, linear work | Selection sort, insertion sort |
| $T(n) = 2T(n/2) + O(1)$ | $O(n)$ | Split in 2, constant combine | Binary tree traversal |
| $T(n) = 2T(n/2) + O(n)$ | $O(n \log n)$ | Split in 2, linear combine | Merge sort, quick sort (avg) |
| $T(n) = T(n/2) + O(1)$ | $O(\log n)$ | Halve problem, constant work | Binary search |
| $T(n) = T(n/2) + O(n)$ | $O(n)$ | Halve problem, linear work | Binary search tree operations |
| $T(n) = 2T(n-1) + O(1)$ | $O(2^n)$ | Two calls, decrease by 1 | Fibonacci (naive), Tower of Hanoi |
| $T(n) = T(n-1) + T(n-2) + O(1)$ | $O(2^n)$ | Fibonacci pattern | Naive Fibonacci |

---

**Understanding Through Examples**

**Pattern 1**: $T(n) = T(n-1) + c$ where $c$ is constant

**Expansion**:
$$T(n) = T(n-1) + c$$
$$= [T(n-2) + c] + c = T(n-2) + 2c$$
$$= [T(n-3) + c] + 2c = T(n-3) + 3c$$
$$= T(n-k) + kc$$

When $k = n-1$: $T(n) = T(1) + (n-1)c = O(n)$

**Pattern 2**: $T(n) = 2T(n/2) + cn$ (Merge Sort)

**Recursion Tree**:
```
Level 0:              cn                    (1 node,  work = cn)
                     /  \
Level 1:          cn/2  cn/2                (2 nodes, work = cn)
                  / \    / \
Level 2:       cn/4 cn/4 cn/4 cn/4          (4 nodes, work = cn)
                ...
Level log n:   c c c c ... c c c            (n nodes, work = cn)
```

Total work: $cn \times (\log n + 1) = O(n \log n)$

**Ruby Examples**:
```ruby
# T(n) = T(n-1) + O(1) => O(n)
def factorial(n)
  return 1 if n <= 1
  n * factorial(n - 1)
end

# T(n) = 2T(n-1) + O(1) => O(2^n)
def fibonacci_naive(n)
  return n if n <= 1
  fibonacci_naive(n - 1) + fibonacci_naive(n - 2)
end

# T(n) = T(n/2) + O(1) => O(log n)
def binary_search(arr, target, left = 0, right = arr.length - 1)
  return -1 if left > right

  mid = (left + right) / 2
  return mid if arr[mid] == target

  if arr[mid] > target
    binary_search(arr, target, left, mid - 1)
  else
    binary_search(arr, target, mid + 1, right)
  end
end

# T(n) = 2T(n/2) + O(n) => O(n log n)
def merge_sort(arr)
  return arr if arr.length <= 1

  mid = arr.length / 2
  left = merge_sort(arr[0...mid])
  right = merge_sort(arr[mid..-1])

  merge(left, right)  # O(n) merge operation
end

def merge(left, right)
  result = []
  i = j = 0

  while i < left.length && j < right.length
    if left[i] <= right[j]
      result << left[i]
      i += 1
    else
      result << right[j]
      j += 1
    end
  end

  result + left[i..-1] + right[j..-1]
end
```

---

#### Master Theorem

**What is the Master Theorem?**

The Master Theorem provides a "cookbook" method for solving recurrence relations of divide-and-conquer algorithms. It gives us the time complexity without manually expanding the recurrence.

**Applies to Recurrences of the Form**:

$$T(n) = aT\left(\frac{n}{b}\right) + f(n)$$

Where:
- $a \geq 1$ = **number of subproblems** (how many recursive calls)
- $b > 1$ = **factor by which problem size is reduced** (division factor)
- $f(n)$ = **cost of work done outside recursive calls** (split + combine cost)
- $T(n)$ = total time complexity

---

**The Three Cases**

Let $c = \log_b(a)$ (the "critical exponent")

**Case 1**: Recursion dominates (many subproblems)

If $f(n) = O(n^d)$ where $d < c$, then:
$$T(n) = \Theta(n^c) = \Theta(n^{\log_b a})$$

**Intuition**: The recursive calls do most of the work. The tree is "leaf-heavy."

---

**Case 2**: Recursion and work are balanced

If $f(n) = \Theta(n^c \log^k n)$ where $k \geq 0$, then:
$$T(n) = \Theta(n^c \log^{k+1} n)$$

**Special case** (most common): If $f(n) = \Theta(n^c)$, then:
$$T(n) = \Theta(n^c \log n)$$

**Intuition**: Work is evenly distributed across all levels of the recursion tree.

---

**Case 3**: Non-recursive work dominates

If $f(n) = \Omega(n^d)$ where $d > c$, **AND** the regularity condition holds:
$$a \cdot f\left(\frac{n}{b}\right) \leq k \cdot f(n) \text{ for some } k < 1$$

Then:
$$T(n) = \Theta(f(n))$$

**Intuition**: The root does most of the work. The tree is "root-heavy."

---

**Master Theorem Examples**

| Recurrence | $a$ | $b$ | $f(n)$ | $c=\log_b a$ | Comparison | Case | Solution |
|:-----------|:----|:----|:-------|:-------------|:-----------|:-----|:---------|
| $T(n) = 2T(n/2) + O(1)$ | 2 | 2 | $1$ | $1$ | $1 < n^1$ | 1 | $\Theta(n)$ |
| $T(n) = 2T(n/2) + O(n)$ | 2 | 2 | $n$ | $1$ | $n = n^1$ | 2 | $\Theta(n \log n)$ |
| $T(n) = 4T(n/2) + O(n)$ | 4 | 2 | $n$ | $2$ | $n < n^2$ | 1 | $\Theta(n^2)$ |
| $T(n) = T(n/2) + O(1)$ | 1 | 2 | $1$ | $0$ | $1 = n^0$ | 2 | $\Theta(\log n)$ |
| $T(n) = 2T(n/2) + O(n^2)$ | 2 | 2 | $n^2$ | $1$ | $n^2 > n^1$ | 3 | $\Theta(n^2)$ |
| $T(n) = 3T(n/4) + O(n)$ | 3 | 4 | $n$ | $\log_4 3 \approx 0.79$ | $n > n^{0.79}$ | 3 | $\Theta(n)$ |
| $T(n) = 9T(n/3) + O(n)$ | 9 | 3 | $n$ | $2$ | $n < n^2$ | 1 | $\Theta(n^2)$ |

---

**Step-by-Step Application**

**Example**: Merge Sort has $T(n) = 2T(n/2) + O(n)$

**Step 1**: Identify parameters
- $a = 2$ (two recursive calls)
- $b = 2$ (problem size halved)
- $f(n) = n$ (merging takes linear time)

**Step 2**: Calculate critical exponent
$$c = \log_b a = \log_2 2 = 1$$

**Step 3**: Compare $f(n)$ with $n^c$
- $f(n) = n$
- $n^c = n^1 = n$
- They're equal! $f(n) = \Theta(n^c)$

**Step 4**: Apply Case 2
$$T(n) = \Theta(n^c \log n) = \Theta(n \log n)$$

**Conclusion**: Merge Sort is $\Theta(n \log n)$ ✓

**Ruby Visualization**:
```ruby
# Example: Merge Sort - T(n) = 2T(n/2) + O(n)
# a=2, b=2, f(n)=n, c=log₂(2)=1
# f(n)=n = Θ(n^1) => Case 2 => T(n) = Θ(n log n)

def merge_sort_with_count(arr, depth = 0)
  puts "#{'  ' * depth}Sorting array of size #{arr.length}"
  return arr if arr.length <= 1

  mid = arr.length / 2
  left = merge_sort_with_count(arr[0...mid], depth + 1)
  right = merge_sort_with_count(arr[mid..-1], depth + 1)

  puts "#{'  ' * depth}Merging #{left.inspect} and #{right.inspect}"
  merge(left, right)
end

# Test
arr = [38, 27, 43, 3, 9, 82, 10]
sorted = merge_sort_with_count(arr)
# Output shows log n levels, each doing O(n) work
```

---

#### Proof Techniques

**1. Mathematical Induction**

**Structure**:
1. **Base Case**: Prove P(1) or P(0) is true
2. **Inductive Hypothesis**: Assume P(k) is true for some k
3. **Inductive Step**: Prove P(k+1) is true using P(k)

**Example**: Prove that 1 + 2 + 3 + ... + n = n(n+1)/2

```ruby
# Proof by induction (verification in Ruby)
def verify_arithmetic_sum(n)
  # Direct calculation
  direct = (1..n).sum

  # Formula
  formula = n * (n + 1) / 2

  puts "n=#{n}: Direct sum=#{direct}, Formula=#{formula}, Match: #{direct == formula}"
end

# Verify for multiple values
(1..10).each { |n| verify_arithmetic_sum(n) }

# Mathematical proof:
# Base case: n=1 => 1 = 1(1+1)/2 = 1 ✓
# Assume true for k: 1+2+...+k = k(k+1)/2
# Prove for k+1:
#   1+2+...+k+(k+1) = k(k+1)/2 + (k+1)
#                    = (k+1)(k/2 + 1)
#                    = (k+1)(k+2)/2 ✓
```

**2. Proof by Contradiction**

**Structure**:
1. Assume the opposite of what you want to prove
2. Show this leads to a logical contradiction
3. Conclude the original statement must be true

**Example**: Prove √2 is irrational

```
Assume √2 is rational => √2 = p/q (in lowest terms, gcd(p,q)=1)
=> 2 = p²/q²
=> 2q² = p²
=> p² is even => p is even => p = 2k
=> 2q² = (2k)² = 4k²
=> q² = 2k²
=> q² is even => q is even
=> Both p and q are even => gcd(p,q) ≥ 2
=> Contradiction! (we said gcd(p,q)=1)
=> √2 must be irrational
```

**3. Proof by Counterexample**

To disprove a statement, find one counterexample.

```ruby
# Claim: "All prime numbers are odd"
# Counterexample:
puts "2 is prime and even" # Disproves the claim

# Claim: "n² + n + 41 is always prime"
def is_prime?(n)
  return false if n < 2
  (2..Math.sqrt(n)).none? { |i| n % i == 0 }
end

(0..50).each do |n|
  result = n**2 + n + 41
  unless is_prime?(result)
    puts "Counterexample: n=#{n}, n²+n+41=#{result} is NOT prime"
    break
  end
end
# Output: n=40, 40²+40+41=1681=41² is NOT prime
```

---

### 0.2 Algorithm Analysis

#### Time Complexity

**What is Time Complexity?**

Time complexity measures how the **runtime** of an algorithm grows as the **input size** increases. It's not about exact seconds, but about the **rate of growth**.

**Why Not Measure in Seconds?**
- Different machines have different speeds
- Same code runs differently on different hardware
- We want a **machine-independent** measure

**Solution**: Count **fundamental operations** (comparisons, assignments, arithmetic) as a function of input size $n$.

---

#### Big O Notation (O) - Upper Bound

**Formal Definition**:

$f(n) = O(g(n))$ if there exist constants $c > 0$ and $n_0 > 0$ such that:
$$f(n) \leq c \cdot g(n) \text{ for all } n \geq n_0$$

**Intuitive Meaning**:
- $O(g(n))$ is an **upper bound** on growth rate
- "The algorithm takes **at most** $g(n)$ time"
- Describes **worst-case** scenario
- We can say "$f(n)$ grows no faster than $g(n)$"

**Example**: If an algorithm takes $3n^2 + 5n + 2$ operations:
- We say it's $O(n^2)$ because $3n^2 + 5n + 2 \leq 4n^2$ for $n \geq 6$
- We drop constants and lower-order terms

**Visual Representation**:
```
Runtime
  |
  |     f(n) = actual runtime
  |    /
  |   /  c·g(n) = upper bound
  |  / /
  | / /
  |/ /
  |/___________ n₀
  |________________ Input size (n)

After n₀, f(n) stays below c·g(n)
```

---

#### Big Omega (Ω) - Lower Bound

**Formal Definition**:

$f(n) = \Omega(g(n))$ if there exist constants $c > 0$ and $n_0 > 0$ such that:
$$f(n) \geq c \cdot g(n) \text{ for all } n \geq n_0$$

**Intuitive Meaning**:
- $\Omega(g(n))$ is a **lower bound** on growth rate
- "The algorithm takes **at least** $g(n)$ time"
- Describes **best-case** scenario
- We can say "$f(n)$ grows at least as fast as $g(n)$"

**Example**: Binary search is $\Omega(1)$ because in the best case, we find the element immediately.

---

#### Big Theta (Θ) - Tight Bound

**Formal Definition**:

$f(n) = \Theta(g(n))$ if there exist constants $c_1, c_2 > 0$ and $n_0 > 0$ such that:
$$c_1 \cdot g(n) \leq f(n) \leq c_2 \cdot g(n) \text{ for all } n \geq n_0$$

**Intuitive Meaning**:
- $\Theta(g(n))$ is a **tight bound** - both upper AND lower bound
- "The algorithm takes **exactly** $g(n)$ time (asymptotically)"
- $f(n) = \Theta(g(n))$ means $f(n) = O(g(n))$ **AND** $f(n) = \Omega(g(n))$
- Most precise notation

**Example**: Merge sort is $\Theta(n \log n)$ in all cases (best, average, worst).

---

**Relationship Between O, Ω, and Θ**:

```
Runtime
  |
  |   c₂·g(n) ← Upper bound (Big O)
  |    /
  |   /  f(n) ← Actual runtime
  |  / /
  | / /  c₁·g(n) ← Lower bound (Big Ω)
  |/ /
  |/___________ n₀
  |________________ Input size (n)

If f(n) is sandwiched between c₁·g(n) and c₂·g(n),
then f(n) = Θ(g(n))
```

**Summary**:
- **Big O (O)**: Upper bound - "at most"
- **Big Omega (Ω)**: Lower bound - "at least"
- **Big Theta (Θ)**: Tight bound - "exactly"

---

**Common Time Complexities** (from best to worst):

| Notation | Name | Example Algorithms | $n=10$ | $n=100$ | $n=1000$ |
|:---------|:-----|:-------------------|:-------|:--------|:---------|
| $O(1)$ | Constant | Array access, hash lookup | 1 | 1 | 1 |
| $O(\log n)$ | Logarithmic | Binary search, balanced tree ops | 3 | 7 | 10 |
| $O(\sqrt{n})$ | Square root | Prime checking | 3 | 10 | 32 |
| $O(n)$ | Linear | Linear search, array traversal | 10 | 100 | 1,000 |
| $O(n \log n)$ | Linearithmic | Merge sort, heap sort, quick sort (avg) | 30 | 664 | 9,966 |
| $O(n^2)$ | Quadratic | Bubble sort, selection sort, nested loops | 100 | 10,000 | 1,000,000 |
| $O(n^3)$ | Cubic | Matrix multiplication (naive), triple nested loops | 1,000 | 1,000,000 | 1,000,000,000 |
| $O(2^n)$ | Exponential | Fibonacci (naive), power set, subsets | 1,024 | $10^{30}$ | $10^{301}$ |
| $O(n!)$ | Factorial | Permutations, TSP brute force | 3,628,800 | $10^{157}$ | $10^{2567}$ |

**Growth Comparison**:
```
For n = 20:
O(1)       = 1
O(log n)   = 4
O(n)       = 20
O(n log n) = 86
O(n²)      = 400
O(2^n)     = 1,048,576
O(n!)      = 2,432,902,008,176,640,000
```

**Key Insight**: Exponential and factorial complexities become **intractable** very quickly!

**Ruby Examples**:
```ruby
# O(1) - Constant time
def get_first_element(arr)
  arr[0]  # Always 1 operation
end

# O(log n) - Logarithmic
def binary_search_iterative(arr, target)
  left, right = 0, arr.length - 1

  while left <= right
    mid = (left + right) / 2
    return mid if arr[mid] == target

    if arr[mid] < target
      left = mid + 1
    else
      right = mid - 1
    end
  end

  -1
end

# O(n) - Linear
def linear_search(arr, target)
  arr.each_with_index do |val, idx|
    return idx if val == target
  end
  -1
end

# O(n log n) - Linearithmic
# (merge_sort from earlier)

# O(n²) - Quadratic
def bubble_sort(arr)
  n = arr.length
  (0...n).each do |i|
    (0...n-i-1).each do |j|
      if arr[j] > arr[j+1]
        arr[j], arr[j+1] = arr[j+1], arr[j]
      end
    end
  end
  arr
end

# O(2^n) - Exponential
def fibonacci_recursive(n)
  return n if n <= 1
  fibonacci_recursive(n-1) + fibonacci_recursive(n-2)
end

# O(n!) - Factorial
def permutations(arr)
  return [arr] if arr.length <= 1

  result = []
  arr.each_with_index do |elem, i|
    rest = arr[0...i] + arr[i+1..-1]
    permutations(rest).each do |perm|
      result << [elem] + perm
    end
  end
  result
end

# Benchmark comparison
require 'benchmark'

sizes = [10, 100, 1000]
sizes.each do |n|
  arr = (1..n).to_a.shuffle

  puts "\n--- Array size: #{n} ---"
  Benchmark.bm(20) do |x|
    x.report("O(1) - access:") { arr[0] }
    x.report("O(log n) - binary:") { binary_search_iterative(arr.sort, arr[n/2]) }
    x.report("O(n) - linear:") { linear_search(arr, arr[n/2]) }
    x.report("O(n log n) - merge:") { merge_sort(arr.dup) }
    x.report("O(n²) - bubble:") { bubble_sort(arr.dup) } if n <= 100
  end
end
```

#### Space Complexity

**What is Space Complexity?**

Space complexity measures the **total amount of memory** an algorithm uses as a function of input size $n$. Just like time complexity, we express it using Big O notation.

**Why Space Complexity Matters:**
- Memory is a limited resource
- Some algorithms trade time for space (or vice versa)
- Critical for embedded systems, mobile apps, large-scale systems
- Can be the bottleneck even if time complexity is good

---

**Components of Space Complexity**

**Total Space** = **Input Space** + **Auxiliary Space**

1. **Input Space**: Memory to store the input data
   - Usually $O(n)$ for an array of size $n$
   - Often excluded when analyzing space complexity

2. **Auxiliary Space**: Extra memory used by the algorithm
   - Variables, temporary arrays, call stack
   - **This is what we typically mean by "space complexity"**

**Example**:
```ruby
def sum_array(arr)  # Input: O(n)
  sum = 0           # Auxiliary: O(1) - just one variable
  arr.each { |x| sum += x }
  sum
end
```
- Input space: $O(n)$ (the array)
- Auxiliary space: $O(1)$ (just the `sum` variable)
- We say this algorithm has $O(1)$ space complexity

---

**Common Space Complexities**

| Complexity | Description | Example Algorithms |
|:-----------|:------------|:-------------------|
| $O(1)$ | Constant space | Iterative algorithms with fixed variables |
| $O(\log n)$ | Logarithmic space | Recursive binary search (call stack depth) |
| $O(n)$ | Linear space | Recursive algorithms, hash tables, extra arrays |
| $O(n \log n)$ | Linearithmic space | Merge sort (with recursion stack) |
| $O(n^2)$ | Quadratic space | 2D matrices, dynamic programming tables |

---

**Space-Time Tradeoffs**

Often we can trade space for time or vice versa:

| Problem | Time-Optimized | Space-Optimized |
|:--------|:---------------|:----------------|
| Fibonacci | $O(n)$ time, $O(n)$ space (memoization) | $O(n)$ time, $O(1)$ space (iterative) |
| Sorting | $O(n \log n)$ time, $O(n)$ space (merge sort) | $O(n^2)$ time, $O(1)$ space (bubble sort) |
| String reversal | $O(n)$ time, $O(n)$ space (new array) | $O(n)$ time, $O(1)$ space (in-place swap) |

**Ruby Examples**:
```ruby
# O(1) space - constant auxiliary space
def sum_array(arr)
  sum = 0  # Only one variable
  arr.each { |num| sum += num }
  sum
end

# O(n) space - linear auxiliary space
def reverse_array(arr)
  result = []  # New array of size n
  arr.reverse_each { |elem| result << elem }
  result
end

# O(log n) space - recursive call stack
def binary_search_recursive(arr, target, left = 0, right = arr.length - 1)
  return -1 if left > right

  mid = (left + right) / 2
  return mid if arr[mid] == target

  if arr[mid] > target
    binary_search_recursive(arr, target, left, mid - 1)  # Stack depth: log n
  else
    binary_search_recursive(arr, target, mid + 1, right)
  end
end

# O(n) space - merge sort auxiliary space
def merge_sort_space(arr)
  return arr if arr.length <= 1

  mid = arr.length / 2
  left = merge_sort_space(arr[0...mid])   # O(n/2) space
  right = merge_sort_space(arr[mid..-1])  # O(n/2) space

  merge(left, right)  # O(n) space for result array
  # Total: O(n) space + O(log n) call stack
end

# O(1) space - in-place bubble sort
def bubble_sort_inplace(arr)
  n = arr.length
  (0...n).each do |i|
    (0...n-i-1).each do |j|
      if arr[j] > arr[j+1]
        arr[j], arr[j+1] = arr[j+1], arr[j]  # Swap in place
      end
    end
  end
  arr  # No extra array created
end
```

**Time vs Space Tradeoff**:
```ruby
# Fibonacci: Time-optimized (O(n) time, O(n) space)
def fib_memoized(n, memo = {})
  return n if n <= 1
  return memo[n] if memo[n]

  memo[n] = fib_memoized(n-1, memo) + fib_memoized(n-2, memo)
end

# Fibonacci: Space-optimized (O(n) time, O(1) space)
def fib_iterative(n)
  return n if n <= 1

  prev, curr = 0, 1
  (2..n).each do
    prev, curr = curr, prev + curr
  end
  curr
end

# Comparison
require 'benchmark'
n = 35

Benchmark.bm(20) do |x|
  x.report("Memoized (O(n) space):") { fib_memoized(n) }
  x.report("Iterative (O(1) space):") { fib_iterative(n) }
end
```

---

#### Amortized Analysis

**What is Amortized Analysis?**

Amortized analysis calculates the **average cost per operation** over a sequence of operations, even when individual operations might be expensive. It's different from average-case analysis:

- **Average-case**: Average over all possible inputs
- **Amortized**: Average over a sequence of operations on the **same** data structure

**Why Amortized Analysis?**

Some operations are occasionally expensive but rare. Amortized analysis shows that the **average** cost is still low.

**Real-World Analogy**:
- You pay $1/month for a service, but every 12 months you pay $100 for renewal
- Amortized cost: $(11 \times 1 + 1 \times 100) / 12 = \$9.25$ per month
- Not $1, not $100, but the average over time

---

**Classic Example: Dynamic Array Resizing**

When a dynamic array (like Ruby's `Array`) runs out of capacity:
1. Allocate new array with **double** the capacity
2. Copy all elements to new array
3. Continue insertions

**Analysis**:
- Most insertions: $O(1)$ - just add to end
- Occasional resize: $O(n)$ - copy all elements
- **Amortized cost**: $O(1)$ per insertion!

**Why $O(1)$ amortized?**

Starting with capacity 1, after $n$ insertions:
- Resizes happen at sizes: 1, 2, 4, 8, 16, ..., $n$
- Total copy cost: $1 + 2 + 4 + 8 + \cdots + n = 2n - 1$ (geometric series)
- Total insertions: $n$
- Amortized cost: $\frac{2n - 1}{n} \approx 2 = O(1)$

**Proof**:
$$\text{Total cost} = \sum_{i=0}^{\log_2 n} 2^i = 2^{\log_2 n + 1} - 1 = 2n - 1$$
$$\text{Amortized cost} = \frac{2n - 1}{n} = 2 - \frac{1}{n} = O(1)$$

When a Ruby array grows beyond capacity:
1. Allocate new array (2x size)
2. Copy all elements
3. Add new element

```ruby
class DynamicArray
  attr_reader :size, :capacity

  def initialize
    @capacity = 1
    @size = 0
    @arr = Array.new(@capacity)
  end

  def push(value)
    resize if @size == @capacity
    @arr[@size] = value
    @size += 1
  end

  def get(index)
    raise IndexError if index >= @size
    @arr[index]
  end

  private

  def resize
    @capacity *= 2
    new_arr = Array.new(@capacity)
    @size.times { |i| new_arr[i] = @arr[i] }
    @arr = new_arr
    puts "Resized to capacity #{@capacity}"
  end
end

# Test
arr = DynamicArray.new
(1..10).each { |i| arr.push(i) }
# Output shows resizing at powers of 2: 1→2, 2→4, 4→8, 8→16
```

---

**Three Methods of Amortized Analysis**

**1. Aggregate Method**

Calculate total cost of $n$ operations, divide by $n$.

**Example**: Dynamic array with $n$ insertions
- Insertions at indices: $1, 2, 3, \ldots, n$
- Resizes at: $1, 2, 4, 8, 16, \ldots, 2^k$ where $2^k \leq n$
- Copy costs: $1 + 2 + 4 + 8 + \cdots + 2^k = 2^{k+1} - 1 < 2n$
- Total cost: $n$ (insertions) $+ 2n$ (copies) $= 3n$
- Amortized: $\frac{3n}{n} = 3 = O(1)$

```ruby
# Demonstrate aggregate method
def analyze_dynamic_array(n)
  arr = DynamicArray.new
  total_cost = 0

  (1..n).each do |i|
    cost = 1  # Cost of adding element

    # If resize happens (at powers of 2), add copy cost
    if (i & (i - 1)) == 0  # Power of 2 check
      cost += i  # Copy i elements
      puts "Operation #{i}: Resize! Cost = #{cost}"
    end

    total_cost += cost
    arr.push(i)
  end

  puts "\nTotal cost for #{n} operations: #{total_cost}"
  puts "Amortized cost per operation: #{total_cost.to_f / n}"
  puts "Expected: ~3 operations per insertion"
end

analyze_dynamic_array(16)
# Output shows amortized O(1) despite occasional O(n) resizes
```

---

**2. Accounting Method**

Assign different charges to operations. Some operations "save" credits for future expensive operations.

**Example**: Dynamic array
- Charge **3 credits** per insertion
  - 1 credit: Insert the element
  - 1 credit: Pay for copying this element in next resize
  - 1 credit: Pay for copying an old element in next resize
- When resize happens, we've already "saved" enough credits!

**Invariant**: Credits never go negative (we always have enough saved)

```ruby
# Accounting method visualization
def accounting_method_demo(n)
  credits = 0

  (1..n).each do |i|
    # Charge 3 credits per operation
    credits += 3

    # Spend 1 credit for insertion
    credits -= 1

    # If resize happens
    if (i & (i - 1)) == 0
      copy_cost = i
      puts "Resize at #{i}: Need #{copy_cost} credits, Have #{credits}"
      credits -= copy_cost
      puts "After resize: #{credits} credits remaining"
    end
  end

  puts "\nFinal credits: #{credits} (always non-negative!)"
end

accounting_method_demo(16)
```

---

**3. Potential Method**

Define a potential function $\Phi$ that represents "stored energy" in the data structure.

**Amortized cost** = **Actual cost** + **Change in potential**

$$\hat{c_i} = c_i + \Phi(D_i) - \Phi(D_{i-1})$$

Where:
- $\hat{c_i}$ = amortized cost of operation $i$
- $c_i$ = actual cost of operation $i$
- $\Phi(D_i)$ = potential after operation $i$

**Example**: Dynamic array
- Potential: $\Phi(D) = 2 \times \text{size} - \text{capacity}$
- After insertion without resize: $\Phi$ increases by 2
- After resize: $\Phi$ drops significantly
- Amortized cost works out to $O(1)$

---

**Comparison of Methods**

| Method | Approach | Best For |
|:-------|:---------|:---------|
| **Aggregate** | Total cost ÷ operations | Simple, straightforward analysis |
| **Accounting** | Assign credits to operations | Intuitive, easy to explain |
| **Potential** | Mathematical function | Complex data structures, formal proofs |
---

**Interview Question**: "Why is dynamic array push $O(1)$ amortized when resize is $O(n)$?"

**Answer**:
1. Resizes are **rare** - only at powers of 2
2. Between resizes, we do many $O(1)$ operations
3. Total cost over $n$ operations: $n + (1 + 2 + 4 + \cdots + n) = n + (2n - 1) = 3n$
4. Average per operation: $\frac{3n}{n} = 3 = O(1)$

The expensive operations are "paid for" by the many cheap operations!

---

#### Asymptotic Growth Comparison

**What is Asymptotic Growth?**

Asymptotic growth describes how a function behaves as $n \to \infty$. We care about the **dominant term** - the one that grows fastest.

**Example**: $f(n) = 3n^2 + 5n + 100$
- For small $n$: constant 100 might matter
- For large $n$: $3n^2$ dominates everything
- Asymptotically: $f(n) = O(n^2)$

---

**Growth Rate Hierarchy** (slowest to fastest):

$$1 < \log \log n < \log n < \sqrt{n} < n < n \log n < n^2 < n^3 < 2^n < n! < n^n$$

**Intuition**:
- **Constant** $O(1)$: Doesn't grow at all
- **Logarithmic** $O(\log n)$: Grows very slowly (doubling $n$ adds constant)
- **Linear** $O(n)$: Grows proportionally
- **Linearithmic** $O(n \log n)$: Slightly worse than linear
- **Polynomial** $O(n^k)$: Grows as power of $n$
- **Exponential** $O(2^n)$: Doubles with each increment of $n$
- **Factorial** $O(n!)$: Explodes extremely fast

---

**Concrete Comparison**

| $n$ | $\log_2 n$ | $n$ | $n \log n$ | $n^2$ | $2^n$ | $n!$ |
|:----|:-----------|:----|:-----------|:------|:------|:-----|
| 1 | 0 | 1 | 0 | 1 | 2 | 1 |
| 10 | 3 | 10 | 33 | 100 | 1,024 | 3,628,800 |
| 20 | 4 | 20 | 86 | 400 | 1,048,576 | $2.4 \times 10^{18}$ |
| 100 | 7 | 100 | 664 | 10,000 | $1.3 \times 10^{30}$ | $9.3 \times 10^{157}$ |
| 1000 | 10 | 1000 | 9,966 | 1,000,000 | $1.1 \times 10^{301}$ | $4.0 \times 10^{2567}$ |

**Key Insight**: Exponential and factorial become **intractable** very quickly!

**Ruby Comparison**:
```ruby
def compare_growth(n)
  results = {
    "O(1)" => 1,
    "O(log log n)" => Math.log2(Math.log2(n)),
    "O(log n)" => Math.log2(n),
    "O(√n)" => Math.sqrt(n),
    "O(n)" => n,
    "O(n log n)" => n * Math.log2(n),
    "O(n²)" => n ** 2,
    "O(n³)" => n ** 3,
    "O(2^n)" => 2 ** [n, 20].min,  # Cap to avoid overflow
    "O(n!)" => (1..[n, 10].min).reduce(1, :*)  # Cap factorial
  }

  puts "Growth comparison for n = #{n}:"
  results.sort_by { |_, v| v }.each do |name, value|
    puts "#{name.ljust(15)} = #{value.to_i}"
  end
end

compare_growth(10)
compare_growth(100)
```

---

**Polynomial vs Exponential Growth**

**Polynomial**: $O(n^k)$ for constant $k$

$$f(n) = n^k \text{ where } k \text{ is a constant}$$

Examples: $O(n)$, $O(n^2)$, $O(n^3)$, even $O(n^{100})$

**Characteristics**:
- **Tractable**: Can solve for reasonable $n$ (thousands, millions)
- Doubling $n$ multiplies runtime by $2^k$
- Example: $n = 1000 \to n = 2000$ for $O(n^2)$: $4 \times$ slower

---

**Exponential**: $O(k^n)$ for constant $k > 1$

$$f(n) = k^n \text{ where } k \text{ is a constant}$$

Examples: $O(2^n)$, $O(3^n)$, $O(10^n)$

**Characteristics**:
- **Intractable**: Only solvable for small $n$ (< 30 typically)
- Incrementing $n$ by 1 multiplies runtime by $k$
- Example: $n = 20 \to n = 21$ for $O(2^n)$: $2 \times$ slower

---

**Critical Difference**

| $n$ | $n^{10}$ (polynomial) | $2^n$ (exponential) |
|:----|:----------------------|:--------------------|
| 10 | $10^{10}$ | 1,024 |
| 20 | $1.0 \times 10^{13}$ | 1,048,576 |
| 30 | $5.9 \times 10^{14}$ | $1.1 \times 10^9$ |
| 40 | $1.0 \times 10^{16}$ | $1.1 \times 10^{12}$ |
| 50 | $9.8 \times 10^{16}$ | $1.1 \times 10^{15}$ |

**Crossover point**: Around $n = 60$, $2^n$ overtakes $n^{10}$ and never looks back!

**Practical Impact**:
- $O(n^{10})$: Slow but can handle $n = 1000$ (takes time but finishes)
- $O(2^n)$: Can't handle $n = 100$ (would take longer than age of universe)

**Example**:
```ruby
# Polynomial: O(n³) - still manageable
def polynomial_example(n)
  count = 0
  (1..n).each do |i|
    (1..n).each do |j|
      (1..n).each do |k|
        count += 1
      end
    end
  end
  count
end

# Exponential: O(2^n) - quickly becomes impossible
def exponential_example(n)
  return 1 if n == 0
  2 * exponential_example(n - 1)
end

# Comparison
require 'benchmark'

puts "Polynomial O(n³):"
[10, 50, 100].each do |n|
  time = Benchmark.realtime { polynomial_example(n) }
  puts "n=#{n}: #{time.round(4)}s"
end

puts "\nExponential O(2^n):"
[10, 20, 25].each do |n|
  time = Benchmark.realtime { exponential_example(n) }
  puts "n=#{n}: #{time.round(4)}s"
end
# Notice: n=100 is fine for O(n³), but n=30 is impossible for O(2^n)
```

---

### 0.3 Memory & Computation Model

#### Stack vs Heap Memory

**What is Memory Organization?**

Programs use two main memory regions: **Stack** and **Heap**. Understanding the difference is crucial for:
- Analyzing space complexity
- Understanding recursion limits
- Avoiding memory leaks
- Optimizing performance

---

**Stack Memory**

**Characteristics**:
- **Structure**: LIFO (Last In, First Out) - like a stack of plates
- **Stores**: Local variables, function parameters, return addresses
- **Allocation**: **Automatic** - happens when function is called
- **Deallocation**: **Automatic** - happens when function returns
- **Speed**: **Very fast** - just move stack pointer
- **Size**: **Limited** (typically 1-8 MB, OS-dependent)
- **Memory**: **Contiguous** - sequential addresses

**When to Use**:
- Small, fixed-size data
- Short-lived variables
- Function call management

**Limitations**:
- Stack overflow if too many recursive calls
- Can't return references to local variables (they're destroyed)

---

**Heap Memory**

**Characteristics**:
- **Structure**: Unordered pool of memory
- **Stores**: Objects, arrays, dynamically allocated data
- **Allocation**: **Manual** request (Ruby's GC handles this)
- **Deallocation**: **Manual** or Garbage Collection
- **Speed**: **Slower** - need to find free block
- **Size**: **Large** (limited by available RAM)
- **Memory**: **Fragmented** - scattered addresses

**When to Use**:
- Large data structures
- Data that outlives function scope
- Size unknown at compile time
- Shared data between functions

**Limitations**:
- Slower allocation/deallocation
- Memory fragmentation
- Potential memory leaks (if not freed)

---

**Stack vs Heap Comparison**

| Aspect | Stack | Heap |
|:-------|:------|:-----|
| **Allocation** | Automatic (function call) | Manual (new/malloc) or GC |
| **Deallocation** | Automatic (function return) | Manual (free) or GC |
| **Speed** | Very fast (pointer bump) | Slower (find free block) |
| **Size** | Small (1-8 MB) | Large (GB of RAM) |
| **Structure** | LIFO, contiguous | Unordered, fragmented |
| **Access** | Local scope only | Global (via pointers/references) |
| **Lifetime** | Function duration | Until explicitly freed or GC |
| **Errors** | Stack overflow | Memory leaks, fragmentation |

---

**Memory Layout in a Process**

```
High Address (0xFFFFFFFF)
┌─────────────────────────┐
│   Command Line Args     │
│   & Environment Vars    │
├─────────────────────────┤
│                         │
│        Stack            │  ← Grows DOWNWARD (↓)
│          ↓              │    - Function calls
│                         │    - Local variables
│                         │    - Return addresses
│                         │
│    (Free Space)         │
│                         │
│          ↑              │
│        Heap             │  ← Grows UPWARD (↑)
│                         │    - Dynamic allocations
│                         │    - Objects, arrays
├─────────────────────────┤
│   Uninitialized Data    │  ← BSS segment
│   (Global/Static vars)  │    (initialized to 0)
├─────────────────────────┤
│   Initialized Data      │  ← Data segment
│   (Global/Static vars)  │    (with initial values)
├─────────────────────────┤
│   Code (Text Segment)   │  ← Program instructions
│   (Read-only)           │    (machine code)
└─────────────────────────┘
Low Address (0x00000000)
```

**Key Points**:
- Stack and Heap grow **toward each other**
- If they meet: **out of memory**
- Stack overflow: too many function calls
- Heap exhaustion: too many allocations

**Ruby Example** (conceptual - Ruby abstracts this):
```ruby
# Stack allocation (local variables)
def stack_example
  x = 10        # Stored on stack
  y = 20        # Stored on stack
  z = x + y     # Stored on stack
  z
end  # x, y, z automatically deallocated

# Heap allocation (objects, arrays)
def heap_example
  arr = [1, 2, 3, 4, 5]  # Array object on heap
  hash = { a: 1, b: 2 }  # Hash object on heap

  # arr and hash references on stack
  # Actual data on heap
  # GC will clean up when no references remain
end

# Stack overflow example
def recursive_overflow(n)
  puts n
  recursive_overflow(n + 1)  # Each call adds stack frame
end

# This will eventually cause SystemStackError
# recursive_overflow(1)
```

**Stack Frame**:
```
Each function call creates a stack frame containing:
- Return address
- Parameters
- Local variables
- Saved registers

┌──────────────────┐ ← Stack Pointer (SP)
│  Local vars (z)  │
├──────────────────┤
│  Parameters      │
├──────────────────┤
│  Return address  │
├──────────────────┤
│  Previous frame  │
└──────────────────┘
```

---

#### Static vs Dynamic Memory Allocation

**What's the Difference?**

The key difference is **when** the size is determined:

---

**Static Memory Allocation**

**Definition**: Memory size is **known at compile time** and fixed throughout program execution.

**Characteristics**:
- Size **determined before** program runs
- Allocated at **program start**
- Deallocated at **program end**
- **Fast access** - direct addressing
- **No runtime overhead** for allocation
- **Memory efficient** - no fragmentation

**Examples**:
- Fixed-size arrays: `int arr[100]`
- Global variables
- Static variables
- Constants

**Advantages**:
- ✅ Fast - no allocation overhead
- ✅ Predictable memory usage
- ✅ No fragmentation

**Disadvantages**:
- ❌ Inflexible - can't change size
- ❌ May waste memory if overallocated
- ❌ May run out if underallocated

---

**Dynamic Memory Allocation**

**Definition**: Memory size is **determined at runtime** and can change during execution.

**Characteristics**:
- Size **determined during** program execution
- Allocated/deallocated **as needed**
- **Flexible** - can grow/shrink
- **Slower** - allocation overhead
- **Fragmentation** possible
- Requires **garbage collection** or manual management

**Examples**:
- Dynamic arrays (Ruby's `Array`)
- Linked lists
- Trees, graphs
- Objects created at runtime

**Advantages**:
- ✅ Flexible - size adapts to needs
- ✅ Efficient memory use - allocate only what's needed
- ✅ Can handle unknown sizes

**Disadvantages**:
- ❌ Slower - allocation/deallocation overhead
- ❌ Fragmentation
- ❌ Potential memory leaks (not in GC languages)

**Ruby Examples**:
```ruby
# Static-like (fixed size)
class StaticArray
  def initialize
    @arr = Array.new(10, 0)  # Fixed size 10
  end

  def set(index, value)
    raise IndexError if index >= 10
    @arr[index] = value
  end

  def get(index)
    @arr[index]
  end
end

# Dynamic (grows as needed)
class DynamicList
  def initialize
    @list = []
  end

  def add(value)
    @list << value  # Grows automatically
  end

  def get(index)
    @list[index]
  end
end

# Comparison
static = StaticArray.new
# static.set(15, 100)  # Error: IndexError

dynamic = DynamicList.new
(1..100).each { |i| dynamic.add(i) }  # No problem
```

---

#### Recursion Stack Behavior

**What Happens During Recursion?**

Recursion is when a function calls itself. Each call creates a new **stack frame** containing:
- Function parameters
- Local variables
- Return address (where to resume after return)

---

**The Recursion Process**

**Phase 1: Building the Stack** (Going Down)
1. Function calls itself with smaller input
2. New stack frame created and pushed
3. Previous frame paused, waiting
4. Repeat until base case reached

**Phase 2: Unwinding the Stack** (Coming Back Up)
5. Base case returns a value
6. Previous frame resumes with that value
7. Computes its result and returns
8. Repeat until original call completes

---

**Visualization: factorial(4)**

**Recursion Tree** (Logical view):
```
factorial(4)
│
├─ 4 * factorial(3)
│      │
│      ├─ 3 * factorial(2)
│      │      │
│      │      ├─ 2 * factorial(1)
│      │      │      │
│      │      │      └─ 1 * factorial(0)
│      │      │             │
│      │      │             └─ return 1
│      │      │      return 1
│      │      return 2
│      return 6
return 24
```

**Ruby Implementation with Stack Trace**:
```ruby
def factorial_traced(n, depth = 0)
  indent = "  " * depth
  puts "#{indent}→ factorial(#{n}) called"

  if n <= 1
    puts "#{indent}← factorial(#{n}) returns 1 (base case)"
    return 1
  end

  result = n * factorial_traced(n - 1, depth + 1)
  puts "#{indent}← factorial(#{n}) returns #{result}"
  result
end

factorial_traced(5)
```

**Stack Depth**:
```ruby
# Check maximum recursion depth
def max_recursion_depth(n = 0)
  max_recursion_depth(n + 1)
rescue SystemStackError
  puts "Maximum recursion depth: ~#{n}"
end

# max_recursion_depth
# Typically 10,000 - 15,000 in Ruby
```

**Tail Recursion** (Ruby doesn't optimize by default):
```ruby
# Non-tail recursive (not optimized)
def factorial_non_tail(n)
  return 1 if n <= 1
  n * factorial_non_tail(n - 1)  # Multiplication after recursive call
end

# Tail recursive (can be optimized)
def factorial_tail(n, acc = 1)
  return acc if n <= 1
  factorial_tail(n - 1, n * acc)  # Recursive call is last operation
end

# Enable tail call optimization (experimental)
RubyVM::InstructionSequence.compile_option = {
  tailcall_optimization: true,
  trace_instruction: false
}

# Now tail recursive functions won't grow stack
```

---

**Recursion vs Iteration: When to Use Each?**

| Aspect | Recursion | Iteration |
|:-------|:----------|:----------|
| **Readability** | Often clearer for tree/graph problems | Can be verbose for complex logic |
| **Memory** | $O(\text{depth})$ stack space | $O(1)$ typically |
| **Performance** | Function call overhead (~10-100 ns/call) | Faster - no call overhead |
| **Stack Overflow** | Risk for deep recursion (>10K calls) | No risk |
| **Natural Fit** | Trees, graphs, divide & conquer | Arrays, simple loops |
| **Code Length** | Usually shorter | Can be longer |

**When to Use Recursion**:
- ✅ Tree/graph traversal
- ✅ Divide and conquer algorithms
- ✅ Backtracking problems
- ✅ When problem naturally recursive

**When to Use Iteration**:
- ✅ Simple loops over arrays
- ✅ Deep recursion (>1000 levels)
- ✅ Performance-critical code
- ✅ Limited stack space

```ruby
# Recursive approach
def sum_recursive(arr, index = 0)
  return 0 if index >= arr.length
  arr[index] + sum_recursive(arr, index + 1)
end

# Iterative approach
def sum_iterative(arr)
  sum = 0
  arr.each { |num| sum += num }
  sum
end

# Benchmark
require 'benchmark'
arr = (1..10000).to_a

Benchmark.bm(15) do |x|
  x.report("Recursive:") { sum_recursive(arr) }
  x.report("Iterative:") { sum_iterative(arr) }
end
# Iterative is faster and uses less memory
```

---

#### Cache Locality

**What is Cache Locality?**

Modern CPUs have a **memory hierarchy**:
1. **Registers** (fastest, smallest) - ~1 cycle
2. **L1 Cache** - ~4 cycles, ~32 KB
3. **L2 Cache** - ~12 cycles, ~256 KB
4. **L3 Cache** - ~40 cycles, ~8 MB
5. **RAM** (slowest, largest) - ~200 cycles, GB

**Cache Locality Principle**: Accessing memory locations **close together** is much faster than random access because:
- Data is loaded in **cache lines** (typically 64 bytes)
- Nearby data comes "for free" when you access one location
- CPU prefetcher predicts and loads next cache lines

---

**Two Types of Locality**

**1. Temporal Locality** (Time-based)

**Definition**: If you access a memory location, you're likely to access it again **soon**.

**Example**: Loop counter variable
```ruby
sum = 0
(1..1000).each do |i|  # 'i' accessed repeatedly
  sum += i              # 'sum' accessed repeatedly
end
```

**2. Spatial Locality** (Space-based)

**Definition**: If you access a memory location, you're likely to access **nearby** locations soon.

**Example**: Array traversal
```ruby
arr = [1, 2, 3, 4, 5]
arr.each { |x| puts x }  # Access arr[0], arr[1], arr[2]... sequentially
```

---

**Why This Matters for Performance**

**Cache Hit**: Data found in cache - **fast** (~4-40 cycles)
**Cache Miss**: Data not in cache, fetch from RAM - **slow** (~200 cycles)

**Performance Impact**: Cache miss can be **50-100× slower** than cache hit!

**Example**: Accessing 1 million integers
- All cache hits: ~4 million cycles = ~1 ms
- All cache misses: ~200 million cycles = ~50 ms
- **50× difference!**

**Types**:
1. **Temporal Locality**: Recently accessed data likely to be accessed again
2. **Spatial Locality**: Data near recently accessed data likely to be accessed

**Impact on Performance**:
```ruby
# Good cache locality (row-major order)
def sum_matrix_row_major(matrix)
  sum = 0
  matrix.each do |row|
    row.each do |val|
      sum += val
    end
  end
  sum
end

# Poor cache locality (column-major order)
def sum_matrix_column_major(matrix)
  sum = 0
  return 0 if matrix.empty?

  (0...matrix[0].length).each do |col|
    (0...matrix.length).each do |row|
      sum += matrix[row][col]
    end
  end
  sum
end

# Benchmark
require 'benchmark'

size = 1000
matrix = Array.new(size) { Array.new(size) { rand(100) } }

Benchmark.bm(20) do |x|
  x.report("Row-major (good):") { sum_matrix_row_major(matrix) }
  x.report("Column-major (poor):") { sum_matrix_column_major(matrix) }
end
# Row-major is faster due to better cache locality
```

**Array vs Linked List Cache Performance**:
```
Array: [1][2][3][4][5]  ← Contiguous, good cache locality
       ↑  ↑  ↑  ↑  ↑
       All in same cache line

Linked List: [1]→[2]→[3]→[4]→[5]  ← Scattered, poor cache locality
             ↑   ↑   ↑   ↑   ↑
             Different memory locations
```

---

## Part I — Core Data Structures

### 1. Arrays

**What is an Array?**

An array is a **contiguous block of memory** that stores elements of the same type, accessible by **index** in constant time.

**Key Properties**:
- **Contiguous memory**: Elements stored sequentially in memory
- **Random access**: Access any element in $O(1)$ time using index
- **Fixed element size**: All elements same size (or references)
- **Index-based**: Elements accessed via integer index (0-based)

**Memory Layout**:
```
Array: [10, 20, 30, 40, 50]

Memory:
┌────┬────┬────┬────┬────┐
│ 10 │ 20 │ 30 │ 40 │ 50 │
└────┴────┴────┴────┴────┘
  ↑
Base address (e.g., 0x1000)

Address of arr[i] = base_address + (i × element_size)
Example: arr[3] = 0x1000 + (3 × 4) = 0x100C
```

---

#### Static vs Dynamic Arrays

**Static Array**

**Definition**: Array with **fixed size** determined at creation time.

**Characteristics**:
- Size **cannot change** after creation
- Memory allocated **once** at creation
- **No reallocation** overhead
- **Predictable** memory usage
- Common in C, C++, Java

**Time Complexity**:
- Access: $O(1)$
- Search: $O(n)$
- Insert/Delete: Not supported (size fixed)

**Space**: $O(n)$ where $n$ is the fixed size

---

**Dynamic Array**

**Definition**: Array that **automatically resizes** when capacity is exceeded (Ruby's default `Array`).

**How It Works**:
1. Start with initial capacity (e.g., 4)
2. When full, allocate **new array** with **2× capacity**
3. **Copy** all elements to new array
4. Continue insertions

**Characteristics**:
- Size **grows automatically**
- **Amortized** $O(1)$ append (occasional $O(n)$ resize)
- More **flexible** than static arrays
- Slight **memory overhead** (unused capacity)

**Time Complexity**:
- Access: $O(1)$
- Search: $O(n)$
- Append: $O(1)$ amortized, $O(n)$ worst case
- Insert at index $i$: $O(n - i)$ (shift elements)
- Delete at index $i$: $O(n - i)$ (shift elements)

**Space**: $O(n)$ where $n$ is current size (capacity may be larger)

**Ruby Implementation**:
```ruby
# Static array (simulated)
class StaticArray
  def initialize(size)
    @size = size
    @arr = Array.new(size)
  end

  def get(index)
    raise IndexError, "Index out of bounds" if index < 0 || index >= @size
    @arr[index]
  end

  def set(index, value)
    raise IndexError, "Index out of bounds" if index < 0 || index >= @size
    @arr[index] = value
  end

  def size
    @size
  end
end

# Dynamic array (Ruby's built-in)
arr = []
arr << 1  # O(1) amortized
arr << 2
arr << 3
puts arr.inspect  # [1, 2, 3]
```

**Time Complexity Comparison**:

| Operation | Static Array | Dynamic Array |
|:----------|:-------------|:--------------|
| Access | O(1) | O(1) |
| Search | O(n) | O(n) |
| Insert at end | N/A | O(1) amortized |
| Insert at beginning | O(n) | O(n) |
| Insert at middle | O(n) | O(n) |
| Delete at end | N/A | O(1) |
| Delete at beginning | O(n) | O(n) |
| Delete at middle | O(n) | O(n) |

---

#### Multidimensional Arrays

**2D Array (Matrix)**:
```ruby
# Create 2D array
rows, cols = 3, 4
matrix = Array.new(rows) { Array.new(cols, 0) }

# Initialize with values
matrix = [
  [1, 2, 3, 4],
  [5, 6, 7, 8],
  [9, 10, 11, 12]
]

# Access element
puts matrix[1][2]  # => 7 (row 1, col 2)

# Traverse row-major
matrix.each do |row|
  row.each do |val|
    print "#{val} "
  end
  puts
end

# Traverse column-major
(0...matrix[0].length).each do |col|
  (0...matrix.length).each do |row|
    print "#{matrix[row][col]} "
  end
  puts
end
```

**Common Matrix Operations**:
```ruby
# Transpose matrix
def transpose(matrix)
  rows = matrix.length
  cols = matrix[0].length
  result = Array.new(cols) { Array.new(rows) }

  (0...rows).each do |i|
    (0...cols).each do |j|
      result[j][i] = matrix[i][j]
    end
  end
  result
end

# Rotate matrix 90° clockwise
def rotate_90_clockwise(matrix)
  n = matrix.length
  # Transpose then reverse each row
  transposed = transpose(matrix)
  transposed.map(&:reverse)
end

# Spiral traversal
def spiral_order(matrix)
  return [] if matrix.empty?

  result = []
  top, bottom = 0, matrix.length - 1
  left, right = 0, matrix[0].length - 1

  while top <= bottom && left <= right
    # Traverse right
    (left..right).each { |col| result << matrix[top][col] }
    top += 1

    # Traverse down
    (top..bottom).each { |row| result << matrix[row][right] }
    right -= 1

    # Traverse left
    if top <= bottom
      (left..right).reverse_each { |col| result << matrix[bottom][col] }
      bottom -= 1
    end

    # Traverse up
    if left <= right
      (top..bottom).reverse_each { |row| result << matrix[row][left] }
      left += 1
    end
  end

  result
end

# Test
matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
]

puts "Original:"
matrix.each { |row| puts row.inspect }

puts "\nTransposed:"
transpose(matrix).each { |row| puts row.inspect }

puts "\nRotated 90°:"
rotate_90_clockwise(matrix).each { |row| puts row.inspect }

puts "\nSpiral order:"
puts spiral_order(matrix).inspect
```

---

#### Prefix Sum (Cumulative Sum)

**What is Prefix Sum?**

Prefix sum is a **preprocessing technique** that allows us to answer **range sum queries** in $O(1)$ time after $O(n)$ preprocessing.

**Problem**: Given array `arr`, answer multiple queries: "What is the sum of elements from index $i$ to $j$?"

**Naive Approach**: For each query, loop from $i$ to $j$ → $O(n)$ per query
**Prefix Sum Approach**: Precompute cumulative sums → $O(1)$ per query

---

**The Idea**

Build an array `prefix` where:

$$\text{prefix}[i] = \sum_{k=0}^{i} \text{arr}[k] = \text{arr}[0] + \text{arr}[1] + \cdots + \text{arr}[i]$$

Then, sum from index $i$ to $j$ is:

$$\text{sum}(i, j) = \text{prefix}[j] - \text{prefix}[i-1]$$

**Why this works?**

$$\text{prefix}[j] = \text{arr}[0] + \cdots + \text{arr}[i-1] + \text{arr}[i] + \cdots + \text{arr}[j]$$
$$\text{prefix}[i-1] = \text{arr}[0] + \cdots + \text{arr}[i-1]$$
$$\text{prefix}[j] - \text{prefix}[i-1] = \text{arr}[i] + \cdots + \text{arr}[j]$$

---

**Visual Example**

```
Array:    [3,  1,  4,  1,  5]
Index:     0   1   2   3   4

Prefix:   [0,  3,  4,  8,  9, 14]
Index:     0   1   2   3   4   5

Query: sum(1, 3) = arr[1] + arr[2] + arr[3] = 1 + 4 + 1 = 6
Using prefix: prefix[4] - prefix[1] = 9 - 3 = 6 ✓
```

**Note**: We add `prefix[0] = 0` to handle edge cases (sum from index 0)

**Ruby Implementation**:
```ruby
class PrefixSum
  def initialize(arr)
    @arr = arr
    @prefix = build_prefix(arr)
  end

  def build_prefix(arr)
    prefix = [0]  # prefix[0] = 0 for easier calculation
    arr.each { |num| prefix << prefix.last + num }
    prefix
  end

  # Get sum of elements from index i to j (inclusive)
  def range_sum(i, j)
    @prefix[j + 1] - @prefix[i]
  end

  # Update element at index (requires rebuilding prefix)
  def update(index, value)
    @arr[index] = value
    @prefix = build_prefix(@arr)
  end
end

# Example
arr = [1, 2, 3, 4, 5]
ps = PrefixSum.new(arr)

puts ps.range_sum(1, 3)  # => 9 (2+3+4)
puts ps.range_sum(0, 4)  # => 15 (1+2+3+4+5)
puts ps.range_sum(2, 2)  # => 3 (just element at index 2)
```

---

**Time Complexity Analysis**

| Operation | Time | Space |
|:----------|:-----|:------|
| Build prefix array | $O(n)$ | $O(n)$ |
| Range sum query | $O(1)$ | - |
| Update element | $O(n)$ | - |

**Trade-off**: Fast queries, slow updates (need to rebuild prefix array)

---

**2D Prefix Sum (Matrix)**

**Extension to 2D**: Answer "sum of submatrix" queries in $O(1)$.

**Formula**:

$$\text{prefix}[i][j] = \sum_{r=0}^{i} \sum_{c=0}^{j} \text{matrix}[r][c]$$

**Recurrence** (Inclusion-Exclusion Principle):

$$\text{prefix}[i][j] = \text{matrix}[i][j] + \text{prefix}[i-1][j] + \text{prefix}[i][j-1] - \text{prefix}[i-1][j-1]$$

**Why subtract** $\text{prefix}[i-1][j-1]$? Because it's counted twice (once in $\text{prefix}[i-1][j]$ and once in $\text{prefix}[i][j-1]$).

**Range Sum** from $(r_1, c_1)$ to $(r_2, c_2)$:

$$\text{sum} = \text{prefix}[r_2][c_2] - \text{prefix}[r_1-1][c_2] - \text{prefix}[r_2][c_1-1] + \text{prefix}[r_1-1][c_1-1]$$

**Visual**:
```
Submatrix sum = Total - Top - Left + TopLeft (added back)

    c1      c2
r1  ┌───────┐
    │ Want  │
r2  └───────┘
```

```ruby
class PrefixSum2D
  def initialize(matrix)
    @matrix = matrix
    @prefix = build_prefix_2d(matrix)
  end

  def build_prefix_2d(matrix)
    return [[0]] if matrix.empty?

    rows = matrix.length
    cols = matrix[0].length
    # Add padding row/col of zeros for easier calculation
    prefix = Array.new(rows + 1) { Array.new(cols + 1, 0) }

    (1..rows).each do |i|
      (1..cols).each do |j|
        # Inclusion-Exclusion Principle
        prefix[i][j] = matrix[i-1][j-1] +      # Current cell
                       prefix[i-1][j] +         # Sum above
                       prefix[i][j-1] -         # Sum to left
                       prefix[i-1][j-1]         # Subtract overlap
      end
    end

    prefix
  end

  # Sum of submatrix from (r1,c1) to (r2,c2) inclusive
  def range_sum(r1, c1, r2, c2)
    # Inclusion-Exclusion for query
    @prefix[r2+1][c2+1] -      # Total up to bottom-right
    @prefix[r1][c2+1] -        # Subtract top part
    @prefix[r2+1][c1] +        # Subtract left part
    @prefix[r1][c1]            # Add back top-left (subtracted twice)
  end
end

# Example
matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
]

ps2d = PrefixSum2D.new(matrix)
puts ps2d.range_sum(0, 0, 1, 1)  # => 12 (1+2+4+5)
puts ps2d.range_sum(1, 1, 2, 2)  # => 28 (5+6+8+9)
```

---

**Applications of Prefix Sum**

1. **Range Sum Queries**: Answer multiple sum queries efficiently
2. **Subarray Sum Problems**: Find subarrays with specific sum properties
3. **Image Processing**: Integral images for fast region sum computation
4. **Equilibrium Index**: Find index where left sum = right sum
5. **Count Subarrays**: Count subarrays with sum divisible by $k$

**Interview Question**: "Given array, find number of subarrays with sum = $k$"

**Answer**: Use prefix sum + hash map
- For each prefix sum $s$, check if $s - k$ exists in hash map
- If yes, those positions form valid subarrays
- Time: $O(n)$, Space: $O(n)$

---

#### Sliding Window Technique

**What is Sliding Window?**

Sliding window is an **optimization technique** for problems involving **contiguous subarrays/substrings**. Instead of recalculating from scratch for each position, we **maintain a window** and **slide** it efficiently.

**Key Idea**:
- Expand window by adding new element on right
- Shrink window by removing element on left
- Avoid redundant recalculation

**When to Use**:
- Problems involving **contiguous** elements
- Finding **maximum/minimum** in subarrays
- **Substring** problems
- Keywords: "consecutive", "contiguous", "subarray"

---

**Two Types of Sliding Window**

**1. Fixed-Size Window**

Window size $k$ is **constant**. Slide by removing leftmost and adding rightmost.

**Time Complexity**: $O(n)$ - each element added/removed once

**Template**:
```
1. Calculate sum/property of first k elements
2. For each new position:
   - Remove arr[i-k] (left element leaving window)
   - Add arr[i] (right element entering window)
   - Update result
```

**2. Variable-Size Window**

Window size **changes dynamically** based on condition.

**Time Complexity**: $O(n)$ - each element added/removed at most once

**Template**:
```
1. Expand window (move right pointer)
2. While condition violated:
   - Shrink window (move left pointer)
3. Update result
```

**Fixed-Size Window**:
```ruby
# Maximum sum of k consecutive elements
def max_sum_subarray(arr, k)
  return nil if arr.length < k

  # Calculate sum of first window
  window_sum = arr[0...k].sum
  max_sum = window_sum

  # Slide window
  (k...arr.length).each do |i|
    window_sum = window_sum - arr[i - k] + arr[i]
    max_sum = [max_sum, window_sum].max
  end

  max_sum
end

# Example
arr = [1, 4, 2, 10, 23, 3, 1, 0, 20]
k = 4
puts max_sum_subarray(arr, k)  # => 39 (10+23+3+1)
```

**Variable-Size Window**:
```ruby
# Smallest subarray with sum >= target
def min_subarray_len(arr, target)
  left = 0
  current_sum = 0
  min_len = Float::INFINITY

  arr.each_with_index do |num, right|
    current_sum += num

    # Shrink window while sum >= target
    while current_sum >= target
      min_len = [min_len, right - left + 1].min
      current_sum -= arr[left]
      left += 1
    end
  end

  min_len == Float::INFINITY ? 0 : min_len
end

# Example
arr = [2, 3, 1, 2, 4, 3]
target = 7
puts min_subarray_len(arr, target)  # => 2 (4+3)
```

**Longest Substring Without Repeating Characters**:
```ruby
def length_of_longest_substring(s)
  char_index = {}
  left = 0
  max_len = 0

  s.each_char.with_index do |char, right|
    # If char seen and in current window, move left
    if char_index[char] && char_index[char] >= left
      left = char_index[char] + 1
    end

    char_index[char] = right
    max_len = [max_len, right - left + 1].max
  end

  max_len
end

# Example
puts length_of_longest_substring("abcabcbb")  # => 3 ("abc")
puts length_of_longest_substring("bbbbb")     # => 1 ("b")
puts length_of_longest_substring("pwwkew")    # => 3 ("wke")
```

---

#### Two Pointer Technique

**What is Two Pointer?**

Two pointer is a technique where we use **two indices** to traverse an array, often to find pairs or partitions that satisfy certain conditions.

**Key Advantage**: Reduces time complexity from $O(n^2)$ (nested loops) to $O(n)$ (single pass).

---

**Three Patterns of Two Pointers**

**1. Opposite Direction** (Converging)
- Start: `left = 0`, `right = n-1`
- Move: Pointers move **toward each other**
- Use: Sorted arrays, palindrome checking, two sum

**2. Same Direction** (Fast & Slow)
- Start: Both at beginning
- Move: One pointer moves faster than the other
- Use: Remove duplicates, partition, cycle detection

**3. Sliding Window** (Expanding/Shrinking)
- Start: Both at beginning
- Move: Expand right, shrink left based on condition
- Use: Substring problems, subarray sums

---

**Pattern 1: Opposite Direction**

**Problem**: Find two numbers in **sorted array** that sum to target.

**Why Two Pointers Work Here?**
- If `arr[left] + arr[right] < target`: Need larger sum → move `left++`
- If `arr[left] + arr[right] > target`: Need smaller sum → move `right--`
- If equal: Found!

**Time**: $O(n)$, **Space**: $O(1)$

**Visual**:
```
arr = [1, 2, 3, 4, 6], target = 6

Step 1: left=0, right=4 → 1+6=7 > 6 → right--
Step 2: left=0, right=3 → 1+4=5 < 6 → left++
Step 3: left=1, right=3 → 2+4=6 ✓ Found!
```

**Opposite Direction (Two Sum in Sorted Array)**:
```ruby
def two_sum_sorted(arr, target)
  left, right = 0, arr.length - 1

  while left < right
    sum = arr[left] + arr[right]

    if sum == target
      return [left, right]
    elsif sum < target
      left += 1
    else
      right -= 1
    end
  end

  nil
end

# Example
arr = [1, 2, 3, 4, 6]
target = 6
puts two_sum_sorted(arr, target).inspect  # => [1, 3] (2+4=6)
```

---

**Pattern 2: Same Direction (Fast & Slow)**

**Problem**: Remove duplicates from **sorted array** in-place.

**Why Two Pointers Work Here?**
- **Slow pointer** (`write`): Position to write next unique element
- **Fast pointer** (`read`): Scans through array
- When `arr[read] != arr[read-1]`: Found new unique → write it

**Time**: $O(n)$, **Space**: $O(1)$

**Visual**:
```
arr = [1, 1, 2, 2, 3]

Initial:  [1, 1, 2, 2, 3]
           w  r

Step 1: arr[r]=1, duplicate → r++
        [1, 1, 2, 2, 3]
           w     r

Step 2: arr[r]=2, unique → arr[w]=2, w++, r++
        [1, 2, 2, 2, 3]
              w     r

Step 3: arr[r]=2, duplicate → r++
        [1, 2, 2, 2, 3]
              w        r

Step 4: arr[r]=3, unique → arr[w]=3, w++
        [1, 2, 3, 2, 3]
                 w

Result: [1, 2, 3] (first w elements)
```

```ruby
def remove_duplicates(arr)
  return 0 if arr.empty?

  write_index = 1  # Slow pointer

  (1...arr.length).each do |read_index|  # Fast pointer
    if arr[read_index] != arr[read_index - 1]
      arr[write_index] = arr[read_index]
      write_index += 1
    end
  end

  write_index  # New length
end

# Example
arr = [1, 1, 2, 2, 2, 3, 4, 4, 5]
new_len = remove_duplicates(arr)
puts arr[0...new_len].inspect  # => [1, 2, 3, 4, 5]
```

---

**Pattern 3: Three Pointers (Dutch National Flag)**

**Problem**: Sort array containing only 0s, 1s, and 2s in **one pass**.

**Algorithm**: Partition array into three regions:
- `[0...low)`: All 0s
- `[low...mid)`: All 1s
- `[mid...high]`: Unknown (being processed)
- `(high...n)`: All 2s

**Invariants**:
- Everything before `low` is 0
- Everything between `low` and `mid` is 1
- Everything after `high` is 2

**Time**: $O(n)$, **Space**: $O(1)$

**Visual**:
```
Initial: [2, 0, 2, 1, 1, 0]
         l,m           h

Step 1: arr[m]=2 → swap(m,h), h--
        [0, 0, 2, 1, 1, 2]
         l,m        h

Step 2: arr[m]=0 → swap(l,m), l++, m++
        [0, 0, 2, 1, 1, 2]
            l  m     h

Step 3: arr[m]=2 → swap(m,h), h--
        [0, 0, 1, 1, 2, 2]
            l  m  h

Step 4: arr[m]=1 → m++
        [0, 0, 1, 1, 2, 2]
            l     m,h

Done! [0, 0, 1, 1, 2, 2]
```

```ruby
# Sort array of 0s, 1s, and 2s (Dutch National Flag)
def sort_colors(arr)
  low, mid, high = 0, 0, arr.length - 1

  while mid <= high
    case arr[mid]
    when 0  # Move 0 to left region
      arr[low], arr[mid] = arr[mid], arr[low]
      low += 1
      mid += 1
    when 1  # 1 is in correct region, just move mid
      mid += 1
    when 2  # Move 2 to right region
      arr[mid], arr[high] = arr[high], arr[mid]
      high -= 1  # Don't increment mid (need to check swapped element)
    end
  end

  arr
end

# Example
arr = [2, 0, 2, 1, 1, 0]
puts sort_colors(arr).inspect  # => [0, 0, 1, 1, 2, 2]
```

**Container With Most Water**:
```ruby
def max_area(heights)
  left, right = 0, heights.length - 1
  max_water = 0

  while left < right
    width = right - left
    height = [heights[left], heights[right]].min
    area = width * height
    max_water = [max_water, area].max

    # Move pointer with smaller height
    if heights[left] < heights[right]
      left += 1
    else
      right -= 1
    end
  end

  max_water
end

# Example
heights = [1, 8, 6, 2, 5, 4, 8, 3, 7]
puts max_area(heights)  # => 49 (7 * 7)
```

---

#### Kadane's Algorithm (Maximum Subarray Sum)

**What is Kadane's Algorithm?**

Kadane's algorithm finds the **maximum sum of any contiguous subarray** in $O(n)$ time using **dynamic programming**.

**Problem**: Given array `arr`, find the contiguous subarray with the largest sum.

**Example**: `arr = [-2, 1, -3, 4, -1, 2, 1, -5, 4]`
- Maximum subarray: `[4, -1, 2, 1]` with sum = 6

---

**The Key Insight**

At each position $i$, we have two choices:
1. **Extend** the previous subarray: `max_ending_here + arr[i]`
2. **Start new** subarray from current element: `arr[i]`

We choose whichever is **larger**!

**Recurrence**:

$$\text{max\_ending\_here}[i] = \max(\text{arr}[i], \text{max\_ending\_here}[i-1] + \text{arr}[i])$$

$$\text{max\_so\_far} = \max(\text{max\_so\_far}, \text{max\_ending\_here}[i])$$

---

**Why This Works?**

**Intuition**: If adding current element to previous sum makes it **negative**, it's better to **start fresh** from current element.

**Example Walkthrough**:
```
arr = [-2, 1, -3, 4, -1, 2, 1, -5, 4]

i=0: max_ending_here = -2, max_so_far = -2
i=1: max_ending_here = max(1, -2+1) = 1, max_so_far = 1
i=2: max_ending_here = max(-3, 1-3) = -2, max_so_far = 1
i=3: max_ending_here = max(4, -2+4) = 4, max_so_far = 4
i=4: max_ending_here = max(-1, 4-1) = 3, max_so_far = 4
i=5: max_ending_here = max(2, 3+2) = 5, max_so_far = 5
i=6: max_ending_here = max(1, 5+1) = 6, max_so_far = 6
i=7: max_ending_here = max(-5, 6-5) = 1, max_so_far = 6
i=8: max_ending_here = max(4, 1+4) = 5, max_so_far = 6

Result: 6
```

---

**Time Complexity**: $O(n)$ - single pass
**Space Complexity**: $O(1)$ - only two variables

```ruby
def max_subarray_sum(arr)
  return nil if arr.empty?

  max_ending_here = arr[0]  # Max sum ending at current position
  max_so_far = arr[0]        # Global maximum

  (1...arr.length).each do |i|
    # Either extend existing subarray or start new one
    max_ending_here = [arr[i], max_ending_here + arr[i]].max
    max_so_far = [max_so_far, max_ending_here].max
  end

  max_so_far
end

# Example
arr = [-2, 1, -3, 4, -1, 2, 1, -5, 4]
puts max_subarray_sum(arr)  # => 6 ([4, -1, 2, 1])
```

**With Indices**:
```ruby
def max_subarray_with_indices(arr)
  return [nil, -1, -1] if arr.empty?

  max_ending_here = arr[0]
  max_so_far = arr[0]
  start = 0
  end_idx = 0
  temp_start = 0

  (1...arr.length).each do |i|
    if arr[i] > max_ending_here + arr[i]
      max_ending_here = arr[i]
      temp_start = i
    else
      max_ending_here += arr[i]
    end

    if max_ending_here > max_so_far
      max_so_far = max_ending_here
      start = temp_start
      end_idx = i
    end
  end

  [max_so_far, start, end_idx]
end

# Example
arr = [-2, 1, -3, 4, -1, 2, 1, -5, 4]
sum, start, end_idx = max_subarray_with_indices(arr)
puts "Max sum: #{sum}"
puts "Subarray: #{arr[start..end_idx].inspect}"
```

**Circular Array Variant**:
```ruby
def max_circular_subarray_sum(arr)
  # Case 1: Maximum subarray is not circular (use Kadane's)
  max_kadane = max_subarray_sum(arr)

  # Case 2: Maximum subarray is circular
  # = Total sum - Minimum subarray sum
  total_sum = arr.sum

  # Find minimum subarray sum (invert signs and use Kadane's)
  inverted = arr.map { |x| -x }
  max_inverted = max_subarray_sum(inverted)
  min_subarray = -max_inverted

  max_circular = total_sum - min_subarray

  # Handle all negative case
  return max_kadane if max_circular == 0

  [max_kadane, max_circular].max
end

# Example
arr = [8, -1, 3, 4]
puts max_circular_subarray_sum(arr)  # => 15 (8 + (-1) + 3 + 4 + circular)
```

**2D Kadane's (Maximum Sum Rectangle)**:
```ruby
def max_sum_rectangle(matrix)
  return 0 if matrix.empty?

  rows = matrix.length
  cols = matrix[0].length
  max_sum = -Float::INFINITY

  # Try all column combinations
  (0...cols).each do |left|
    temp = Array.new(rows, 0)

    (left...cols).each do |right|
      # Add current column to temp
      (0...rows).each do |i|
        temp[i] += matrix[i][right]
      end

      # Apply Kadane's on temp
      current_max = max_subarray_sum(temp)
      max_sum = [max_sum, current_max].max
    end
  end

  max_sum
end

# Example
matrix = [
  [1, 2, -1, -4, -20],
  [-8, -3, 4, 2, 1],
  [3, 8, 10, 1, 3],
  [-4, -1, 1, 7, -6]
]

puts max_sum_rectangle(matrix)  # => 29
```

---

#### Matrix Problems

**Search in Sorted Matrix**:
```ruby
# Matrix sorted row-wise and column-wise
def search_matrix(matrix, target)
  return false if matrix.empty?

  row = 0
  col = matrix[0].length - 1

  # Start from top-right corner
  while row < matrix.length && col >= 0
    if matrix[row][col] == target
      return true
    elsif matrix[row][col] > target
      col -= 1  # Move left
    else
      row += 1  # Move down
    end
  end

  false
end

# Example
matrix = [
  [1, 4, 7, 11],
  [2, 5, 8, 12],
  [3, 6, 9, 16],
  [10, 13, 14, 17]
]

puts search_matrix(matrix, 5)   # => true
puts search_matrix(matrix, 20)  # => false
```

**Set Matrix Zeroes**:
```ruby
def set_zeroes(matrix)
  rows = matrix.length
  cols = matrix[0].length
  first_row_zero = false
  first_col_zero = false

  # Check if first row/col should be zero
  first_row_zero = matrix[0].any?(&:zero?)
  first_col_zero = matrix.any? { |row| row[0].zero? }

  # Use first row/col as markers
  (1...rows).each do |i|
    (1...cols).each do |j|
      if matrix[i][j].zero?
        matrix[i][0] = 0
        matrix[0][j] = 0
      end
    end
  end

  # Set zeros based on markers
  (1...rows).each do |i|
    (1...cols).each do |j|
      if matrix[i][0].zero? || matrix[0][j].zero?
        matrix[i][j] = 0
      end
    end
  end

  # Handle first row/col
  matrix[0].map! { 0 } if first_row_zero
  matrix.each { |row| row[0] = 0 } if first_col_zero

  matrix
end

# Example
matrix = [
  [1, 1, 1],
  [1, 0, 1],
  [1, 1, 1]
]

set_zeroes(matrix).each { |row| puts row.inspect }
# Output:
# [1, 0, 1]
# [0, 0, 0]
# [1, 0, 1]
```

---

### 2. Linked Lists

**What is a Linked List?**

A linked list is a **linear data structure** where elements (nodes) are **not stored contiguously** in memory. Each node contains:
1. **Data**: The value stored
2. **Pointer(s)**: Reference to next (and/or previous) node

**Key Difference from Arrays**:
- **Arrays**: Contiguous memory, $O(1)$ access, $O(n)$ insertion/deletion
- **Linked Lists**: Scattered memory, $O(n)$ access, $O(1)$ insertion/deletion (if position known)

---

**Why Use Linked Lists?**

**Advantages**:
- ✅ **Dynamic size**: Grows/shrinks easily
- ✅ **Efficient insertion/deletion**: $O(1)$ if position known
- ✅ **No wasted space**: Allocate exactly what's needed
- ✅ **Easy to implement** stacks, queues, graphs

**Disadvantages**:
- ❌ **No random access**: Must traverse from head ($O(n)$)
- ❌ **Extra memory**: Pointers take space
- ❌ **Poor cache locality**: Nodes scattered in memory
- ❌ **No binary search**: Can't jump to middle

---

#### Singly Linked List

**Definition**: Each node has **one pointer** to the **next** node.

**Structure**:
```
Head
  ↓
┌────┬────┐    ┌────┬────┐    ┌────┬────┐
│ 10 │  ●─┼───→│ 20 │  ●─┼───→│ 30 │ nil│
└────┴────┘    └────┴────┘    └────┴────┘
 Data Next      Data Next      Data Next
                                  ↑
                                 Tail
```

**Time Complexity**:

| Operation | Time | Explanation |
|:----------|:-----|:------------|
| Access by index | $O(n)$ | Must traverse from head |
| Search | $O(n)$ | Must check each node |
| Insert at head | $O(1)$ | Just update head pointer |
| Insert at tail | $O(n)$ | Must traverse to end (or $O(1)$ with tail pointer) |
| Insert at position | $O(n)$ | Must traverse to position |
| Delete at head | $O(1)$ | Just update head pointer |
| Delete at tail | $O(n)$ | Must traverse to second-last node |
| Delete at position | $O(n)$ | Must traverse to position |

**Space**: $O(n)$ for $n$ nodes (plus pointer overhead)

**Ruby Implementation**:
```ruby
class Node
  attr_accessor :data, :next

  def initialize(data)
    @data = data
    @next = nil
  end
end

class SinglyLinkedList
  attr_accessor :head

  def initialize
    @head = nil
  end

  # Insert at beginning - O(1)
  def prepend(data)
    new_node = Node.new(data)
    new_node.next = @head
    @head = new_node
  end

  # Insert at end - O(n)
  def append(data)
    new_node = Node.new(data)

    if @head.nil?
      @head = new_node
      return
    end

    current = @head
    current = current.next while current.next
    current.next = new_node
  end

  # Insert after specific node - O(1) if node given
  def insert_after(node, data)
    return if node.nil?

    new_node = Node.new(data)
    new_node.next = node.next
    node.next = new_node
  end

  # Delete node with specific value - O(n)
  def delete(data)
    return if @head.nil?

    # If head needs to be deleted
    if @head.data == data
      @head = @head.next
      return
    end

    current = @head
    while current.next
      if current.next.data == data
        current.next = current.next.next
        return
      end
      current = current.next
    end
  end

  # Search - O(n)
  def search(data)
    current = @head
    while current
      return current if current.data == data
      current = current.next
    end
    nil
  end

  # Display list
  def display
    current = @head
    result = []
    while current
      result << current.data
      current = current.next
    end
    puts result.join(" → ")
  end

  # Get length - O(n)
  def length
    count = 0
    current = @head
    while current
      count += 1
      current = current.next
    end
    count
  end

  # Reverse list - O(n)
  def reverse!
    prev = nil
    current = @head

    while current
      next_node = current.next
      current.next = prev
      prev = current
      current = next_node
    end

    @head = prev
  end
end

# Example usage
list = SinglyLinkedList.new
list.append(1)
list.append(2)
list.append(3)
list.prepend(0)
list.display  # => 0 → 1 → 2 → 3

list.delete(2)
list.display  # => 0 → 1 → 3

list.reverse!
list.display  # => 3 → 1 → 0
```

---

#### Doubly Linked List

**Definition**: Each node has **two pointers**: one to the **next** node and one to the **previous** node.

**Structure**:
```
       Head                                           Tail
         ↓                                             ↓
nil ←┌────┬────┬────┐  ┌────┬────┬────┐  ┌────┬────┬────┐→ nil
     │prev│ 10 │next│⇄│prev│ 20 │next│⇄│prev│ 30 │next│
     └────┴────┴────┘  └────┴────┴────┘  └────┴────┴────┘
```

**Advantages over Singly Linked List**:
- ✅ **Bidirectional traversal**: Can move forward and backward
- ✅ **Easier deletion**: Can delete node in $O(1)$ if node reference given (no need to find previous)
- ✅ **Easier insertion**: Can insert before a node easily

**Disadvantages**:
- ❌ **More memory**: Two pointers per node instead of one
- ❌ **More complex**: More pointers to maintain

---

**Time Complexity Comparison**

| Operation | Singly Linked List | Doubly Linked List |
|:----------|:-------------------|:-------------------|
| Insert at head | $O(1)$ | $O(1)$ |
| Insert at tail | $O(n)$ or $O(1)$ with tail pointer | $O(1)$ with tail pointer |
| Delete at head | $O(1)$ | $O(1)$ |
| Delete at tail | $O(n)$ | $O(1)$ with tail pointer |
| Delete given node | $O(n)$ (need to find previous) | $O(1)$ (have previous pointer) |
| Traverse forward | $O(n)$ | $O(n)$ |
| Traverse backward | Not possible | $O(n)$ |

**Space**: $O(n)$ but **2× pointer overhead** compared to singly linked list

**Ruby Implementation**:
```ruby
class DNode
  attr_accessor :data, :prev, :next

  def initialize(data)
    @data = data
    @prev = nil
    @next = nil
  end
end

class DoublyLinkedList
  attr_accessor :head, :tail

  def initialize
    @head = nil
    @tail = nil
  end

  # Insert at beginning - O(1)
  def prepend(data)
    new_node = DNode.new(data)

    if @head.nil?
      @head = @tail = new_node
    else
      new_node.next = @head
      @head.prev = new_node
      @head = new_node
    end
  end

  # Insert at end - O(1)
  def append(data)
    new_node = DNode.new(data)

    if @tail.nil?
      @head = @tail = new_node
    else
      new_node.prev = @tail
      @tail.next = new_node
      @tail = new_node
    end
  end

  # Delete node - O(1) if node reference given
  def delete_node(node)
    return if node.nil?

    if node.prev
      node.prev.next = node.next
    else
      @head = node.next
    end

    if node.next
      node.next.prev = node.prev
    else
      @tail = node.prev
    end
  end

  # Display forward
  def display_forward
    current = @head
    result = []
    while current
      result << current.data
      current = current.next
    end
    puts result.join(" ⇄ ")
  end

  # Display backward
  def display_backward
    current = @tail
    result = []
    while current
      result << current.data
      current = current.prev
    end
    puts result.join(" ⇄ ")
  end
end

# Example
dll = DoublyLinkedList.new
dll.append(1)
dll.append(2)
dll.append(3)
dll.prepend(0)

dll.display_forward   # => 0 ⇄ 1 ⇄ 2 ⇄ 3
dll.display_backward  # => 3 ⇄ 2 ⇄ 1 ⇄ 0
```

---

#### Circular Linked List

**Definition**: Last node points **back to the first node** instead of `nil`, forming a **circle**.

**Structure**:
```
       Head
         ↓
      ┌────┬────┐    ┌────┬────┐    ┌────┬────┐
   ┌─→│ 10 │  ●─┼───→│ 20 │  ●─┼───→│ 30 │  ●─┼─┐
   │  └────┴────┘    └────┴────┘    └────┴────┘ │
   │                                             │
   └─────────────────────────────────────────────┘
```

**Key Characteristics**:
- **No `nil` pointers**: Last node points to head
- **Infinite traversal**: Can keep going in circle
- **No natural end**: Need to track when we've completed one loop

**Advantages**:
- ✅ **Circular traversal**: Useful for round-robin scheduling
- ✅ **No null checks**: Every node has a next
- ✅ **Efficient for circular buffers**: Audio/video streaming

**Disadvantages**:
- ❌ **Infinite loop risk**: Must be careful in traversal
- ❌ **More complex**: Need special handling for insertion/deletion

**Use Cases**:
- Round-robin scheduling (CPU scheduling)
- Circular buffers
- Multiplayer games (turn-based)
- Music playlists (repeat mode)

**Ruby Implementation**:
```ruby
class CircularLinkedList
  attr_accessor :head

  def initialize
    @head = nil
  end

  def append(data)
    new_node = Node.new(data)

    if @head.nil?
      @head = new_node
      new_node.next = @head  # Point to itself
    else
      current = @head
      current = current.next while current.next != @head
      current.next = new_node
      new_node.next = @head
    end
  end

  def display
    return if @head.nil?

    current = @head
    result = []
    loop do
      result << current.data
      current = current.next
      break if current == @head
    end
    puts result.join(" → ") + " → (back to #{@head.data})"
  end
end

# Example
cll = CircularLinkedList.new
cll.append(1)
cll.append(2)
cll.append(3)
cll.display  # => 1 → 2 → 3 → (back to 1)
```

---

#### Fast & Slow Pointer (Floyd's Tortoise and Hare)

**What is Fast & Slow Pointer?**

A technique using **two pointers** that move at **different speeds** through a linked list:
- **Slow pointer**: Moves **1 step** at a time
- **Fast pointer**: Moves **2 steps** at a time

**Why This Works?**

If there's a **cycle**, the fast pointer will eventually "lap" the slow pointer (like runners on a circular track). If there's **no cycle**, the fast pointer reaches the end.

---

**Mathematical Proof of Cycle Detection**

**Claim**: If there's a cycle, fast and slow pointers **must meet**.

**Proof**:
- Let slow pointer be at position $s$ when it enters the cycle
- Let fast pointer be at position $f$ in the cycle
- Distance between them: $d = f - s$
- Each iteration: distance decreases by 1 (fast gains 2, slow gains 1)
- After $d$ iterations: distance = 0 → **they meet!**

**Time**: $O(n)$ where $n$ is number of nodes
**Space**: $O(1)$ - only two pointers

---

**Four Classic Applications**

**1. Detect Cycle**
- If fast meets slow → cycle exists
- If fast reaches `nil` → no cycle

**2. Find Middle of List**
- When fast reaches end, slow is at middle
- Works because fast moves 2× speed

**3. Find Cycle Start**
- After detecting cycle, reset one pointer to head
- Move both at same speed → they meet at cycle start

**4. Check Palindrome**
- Find middle using fast/slow
- Reverse second half
- Compare first and second halves

**Cycle Detection**:
```ruby
def has_cycle?(head)
  return false if head.nil?

  slow = fast = head

  while fast && fast.next
    slow = slow.next
    fast = fast.next.next

    return true if slow == fast
  end

  false
end

# Find cycle start
def detect_cycle_start(head)
  return nil if head.nil?

  slow = fast = head

  # Detect cycle
  while fast && fast.next
    slow = slow.next
    fast = fast.next.next

    if slow == fast
      # Found cycle, now find start
      slow = head
      while slow != fast
        slow = slow.next
        fast = fast.next
      end
      return slow
    end
  end

  nil
end
```

**Find Middle**:
```ruby
def find_middle(head)
  return nil if head.nil?

  slow = fast = head

  while fast && fast.next
    slow = slow.next
    fast = fast.next.next
  end

  slow  # Middle node
end
```

**Palindrome Check**:
```ruby
def is_palindrome?(head)
  return true if head.nil? || head.next.nil?

  # Find middle
  slow = fast = head
  while fast && fast.next
    slow = slow.next
    fast = fast.next.next
  end

  # Reverse second half
  second_half = reverse_list(slow)

  # Compare
  first = head
  second = second_half

  while second
    return false if first.data != second.data
    first = first.next
    second = second.next
  end

  true
end

def reverse_list(head)
  prev = nil
  current = head

  while current
    next_node = current.next
    current.next = prev
    prev = current
    current = next_node
  end

  prev
end
```

---

#### Linked List Reversal Techniques

**Iterative Reversal**:
```ruby
def reverse_iterative(head)
  prev = nil
  current = head

  while current
    next_node = current.next
    current.next = prev
    prev = current
    current = next_node
  end

  prev  # New head
end
```

**Recursive Reversal**:
```ruby
def reverse_recursive(head)
  return head if head.nil? || head.next.nil?

  new_head = reverse_recursive(head.next)
  head.next.next = head
  head.next = nil

  new_head
end
```

**Reverse in Groups of K**:
```ruby
def reverse_k_group(head, k)
  return head if head.nil? || k == 1

  # Check if we have k nodes
  current = head
  count = 0
  while current && count < k
    current = current.next
    count += 1
  end

  return head if count < k

  # Reverse first k nodes
  prev = nil
  current = head
  count = 0

  while current && count < k
    next_node = current.next
    current.next = prev
    prev = current
    current = next_node
    count += 1
  end

  # Recursively reverse remaining
  if current
    head.next = reverse_k_group(current, k)
  end

  prev  # New head of this group
end
```

**Reverse Between Positions**:
```ruby
def reverse_between(head, left, right)
  return head if left == right

  dummy = Node.new(0)
  dummy.next = head
  prev = dummy

  # Move to position left-1
  (1...left).each { prev = prev.next }

  # Reverse from left to right
  current = prev.next
  (left...right).each do
    next_node = current.next
    current.next = next_node.next
    next_node.next = prev.next
    prev.next = next_node
  end

  dummy.next
end
```

---

#### Common Linked List Problems

**Merge Two Sorted Lists**:
```ruby
def merge_two_lists(l1, l2)
  dummy = Node.new(0)
  current = dummy

  while l1 && l2
    if l1.data <= l2.data
      current.next = l1
      l1 = l1.next
    else
      current.next = l2
      l2 = l2.next
    end
    current = current.next
  end

  current.next = l1 || l2
  dummy.next
end
```

**Remove Nth Node From End**:
```ruby
def remove_nth_from_end(head, n)
  dummy = Node.new(0)
  dummy.next = head

  fast = slow = dummy

  # Move fast n+1 steps ahead
  (n + 1).times { fast = fast.next }

  # Move both until fast reaches end
  while fast
    fast = fast.next
    slow = slow.next
  end

  # Remove nth node
  slow.next = slow.next.next

  dummy.next
end
```

**Intersection of Two Lists**:
```ruby
def get_intersection_node(headA, headB)
  return nil if headA.nil? || headB.nil?

  a, b = headA, headB

  # Traverse both lists
  # When one reaches end, switch to other list's head
  # They will meet at intersection or both become nil
  while a != b
    a = a.nil? ? headB : a.next
    b = b.nil? ? headA : b.next
  end

  a  # Intersection node or nil
end
```

**Add Two Numbers (Linked Lists)**:
```ruby
# Numbers stored in reverse order: 342 = 2→4→3
def add_two_numbers(l1, l2)
  dummy = Node.new(0)
  current = dummy
  carry = 0

  while l1 || l2 || carry > 0
    sum = carry
    sum += l1.data if l1
    sum += l2.data if l2

    carry = sum / 10
    current.next = Node.new(sum % 10)
    current = current.next

    l1 = l1.next if l1
    l2 = l2.next if l2
  end

  dummy.next
end
```

---

#### Array vs Linked List Comparison

| Operation | Array | Linked List |
|:----------|:------|:------------|
| **Access by index** | O(1) | O(n) |
| **Search** | O(n) | O(n) |
| **Insert at beginning** | O(n) | O(1) |
| **Insert at end** | O(1) amortized | O(n) or O(1) with tail |
| **Insert at middle** | O(n) | O(1) if node given |
| **Delete at beginning** | O(n) | O(1) |
| **Delete at end** | O(1) | O(n) or O(1) with tail |
| **Delete at middle** | O(n) | O(1) if node given |
| **Memory** | Contiguous | Scattered |
| **Cache locality** | Good | Poor |
| **Memory overhead** | None | Extra for pointers |

**When to Use**:
- **Array**: Random access, cache-friendly, known size
- **Linked List**: Frequent insertions/deletions, unknown size, no random access needed

---

### 3. Stack

**What is a Stack?**

A stack is a **linear data structure** that follows the **LIFO** (Last In, First Out) principle:
- The **last** element added is the **first** one removed
- Like a stack of plates: you can only add/remove from the top

**Real-World Analogies**:
- Stack of plates
- Browser back button (navigation history)
- Undo/Redo in text editors
- Function call stack in programming

---

#### Stack Fundamentals

**Core Operations**:

| Operation | Description | Time | Space |
|:----------|:------------|:-----|:------|
| `push(x)` | Add element to top | $O(1)$ | - |
| `pop()` | Remove and return top element | $O(1)$ | - |
| `peek()` / `top()` | Return top without removing | $O(1)$ | - |
| `is_empty()` | Check if stack is empty | $O(1)$ | - |
| `size()` | Return number of elements | $O(1)$ | - |

**Space Complexity**: $O(n)$ for $n$ elements

---

**Visual Representation**:

```
Initial Stack       push(3)           push(5)           pop()
─────────────       ───────           ───────           ─────
                                      ┌─────┐
                                      │  5  │ ← top
                    ┌─────┐           ├─────┤           ┌─────┐
                    │  3  │ ← top     │  3  │           │  3  │ ← top
┌─────┐             ├─────┤           ├─────┤           ├─────┤
│  1  │ ← top       │  1  │           │  1  │           │  1  │
└─────┘             └─────┘           └─────┘           └─────┘

LIFO: Last In (5), First Out (5)
```

---

**When to Use a Stack?**

**Use Cases**:
- ✅ **Reversing**: Reverse a string, array
- ✅ **Backtracking**: DFS, maze solving, undo operations
- ✅ **Expression evaluation**: Infix to postfix, calculator
- ✅ **Parentheses matching**: Check balanced brackets
- ✅ **Function calls**: Call stack in recursion
- ✅ **Browser history**: Back/forward navigation

**Key Insight**: If you need to process items in **reverse order** of arrival, use a stack!

---

#### Array Implementation

```ruby
class StackArray
  def initialize
    @stack = []
  end

  def push(value)
    @stack << value
  end

  def pop
    raise "Stack underflow" if empty?
    @stack.pop
  end

  def peek
    raise "Stack is empty" if empty?
    @stack.last
  end

  def empty?
    @stack.empty?
  end

  def size
    @stack.length
  end

  def display
    puts @stack.reverse.inspect
  end
end

# Example
stack = StackArray.new
stack.push(1)
stack.push(2)
stack.push(3)
stack.display  # => [3, 2, 1]
puts stack.pop  # => 3
puts stack.peek  # => 2
```

---

#### Linked List Implementation

```ruby
class StackNode
  attr_accessor :data, :next

  def initialize(data)
    @data = data
    @next = nil
  end
end

class StackLinkedList
  def initialize
    @top = nil
    @size = 0
  end

  def push(value)
    new_node = StackNode.new(value)
    new_node.next = @top
    @top = new_node
    @size += 1
  end

  def pop
    raise "Stack underflow" if empty?

    value = @top.data
    @top = @top.next
    @size -= 1
    value
  end

  def peek
    raise "Stack is empty" if empty?
    @top.data
  end

  def empty?
    @top.nil?
  end

  def size
    @size
  end

  def display
    current = @top
    result = []
    while current
      result << current.data
      current = current.next
    end
    puts result.inspect
  end
end
```

---

#### Balanced Parentheses

```ruby
def is_balanced?(s)
  stack = []
  pairs = { '(' => ')', '[' => ']', '{' => '}' }

  s.each_char do |char|
    if pairs.key?(char)
      stack.push(char)
    elsif pairs.value?(char)
      return false if stack.empty?
      return false if pairs[stack.pop] != char
    end
  end

  stack.empty?
end

# Examples
puts is_balanced?("()")           # => true
puts is_balanced?("()[]{}")       # => true
puts is_balanced?("(]")           # => false
puts is_balanced?("([)]")         # => false
puts is_balanced?("{[]}")         # => true
```

---

#### Expression Evaluation

**Infix to Postfix Conversion**:
```ruby
def infix_to_postfix(expression)
  precedence = { '+' => 1, '-' => 1, '*' => 2, '/' => 2, '^' => 3 }
  stack = []
  output = []

  expression.each_char do |char|
    if char =~ /[a-zA-Z0-9]/
      output << char
    elsif char == '('
      stack.push(char)
    elsif char == ')'
      while !stack.empty? && stack.last != '('
        output << stack.pop
      end
      stack.pop  # Remove '('
    elsif precedence.key?(char)
      while !stack.empty? && stack.last != '(' &&
            precedence[stack.last] >= precedence[char]
        output << stack.pop
      end
      stack.push(char)
    end
  end

  output.concat(stack.reverse)
  output.join
end

# Examples
puts infix_to_postfix("a+b*c")      # => abc*+
puts infix_to_postfix("(a+b)*c")    # => ab+c*
puts infix_to_postfix("a+b*c-d")    # => abc*+d-
```

**Evaluate Postfix Expression**:
```ruby
def evaluate_postfix(expression)
  stack = []

  expression.split.each do |token|
    if token =~ /^\d+$/
      stack.push(token.to_i)
    else
      b = stack.pop
      a = stack.pop

      result = case token
               when '+' then a + b
               when '-' then a - b
               when '*' then a * b
               when '/' then a / b
               end

      stack.push(result)
    end
  end

  stack.pop
end

# Example
puts evaluate_postfix("2 3 1 * + 9 -")  # => -4
# Explanation: 2 + (3 * 1) - 9 = -4
```

**Evaluate Infix Expression**:
```ruby
def evaluate_infix(expression)
  values = []
  operators = []
  precedence = { '+' => 1, '-' => 1, '*' => 2, '/' => 2 }

  i = 0
  while i < expression.length
    char = expression[i]

    if char == ' '
      i += 1
      next
    end

    if char =~ /\d/
      num = 0
      while i < expression.length && expression[i] =~ /\d/
        num = num * 10 + expression[i].to_i
        i += 1
      end
      values.push(num)
      next
    end

    if char == '('
      operators.push(char)
    elsif char == ')'
      while operators.last != '('
        values.push(apply_op(operators.pop, values.pop, values.pop))
      end
      operators.pop
    elsif precedence.key?(char)
      while !operators.empty? && precedence[operators.last] &&
            precedence[operators.last] >= precedence[char]
        values.push(apply_op(operators.pop, values.pop, values.pop))
      end
      operators.push(char)
    end

    i += 1
  end

  while !operators.empty?
    values.push(apply_op(operators.pop, values.pop, values.pop))
  end

  values.pop
end

def apply_op(op, b, a)
  case op
  when '+' then a + b
  when '-' then a - b
  when '*' then a * b
  when '/' then a / b
  end
end

# Example
puts evaluate_infix("10 + 2 * 6")     # => 22
puts evaluate_infix("100 * 2 + 12")   # => 212
puts evaluate_infix("(10 + 2) * 6")   # => 72
```

---

#### Monotonic Stack

**Concept**: Stack where elements are always in increasing or decreasing order.

**Next Greater Element**:
```ruby
def next_greater_element(arr)
  result = Array.new(arr.length, -1)
  stack = []  # Stores indices

  arr.each_with_index do |num, i|
    while !stack.empty? && arr[stack.last] < num
      idx = stack.pop
      result[idx] = num
    end
    stack.push(i)
  end

  result
end

# Example
arr = [4, 5, 2, 10, 8]
puts next_greater_element(arr).inspect
# => [5, 10, 10, -1, -1]
```

**Next Smaller Element**:
```ruby
def next_smaller_element(arr)
  result = Array.new(arr.length, -1)
  stack = []

  arr.each_with_index do |num, i|
    while !stack.empty? && arr[stack.last] > num
      idx = stack.pop
      result[idx] = num
    end
    stack.push(i)
  end

  result
end

# Example
arr = [4, 5, 2, 10, 8]
puts next_smaller_element(arr).inspect
# => [2, 2, -1, 8, -1]
```

**Largest Rectangle in Histogram**:
```ruby
def largest_rectangle_area(heights)
  stack = []
  max_area = 0
  index = 0

  while index < heights.length
    if stack.empty? || heights[index] >= heights[stack.last]
      stack.push(index)
      index += 1
    else
      top = stack.pop
      width = stack.empty? ? index : index - stack.last - 1
      area = heights[top] * width
      max_area = [max_area, area].max
    end
  end

  while !stack.empty?
    top = stack.pop
    width = stack.empty? ? index : index - stack.last - 1
    area = heights[top] * width
    max_area = [max_area, area].max
  end

  max_area
end

# Example
heights = [2, 1, 5, 6, 2, 3]
puts largest_rectangle_area(heights)  # => 10
```

**Stock Span Problem**:
```ruby
def calculate_span(prices)
  span = Array.new(prices.length)
  stack = []

  prices.each_with_index do |price, i|
    while !stack.empty? && prices[stack.last] <= price
      stack.pop
    end

    span[i] = stack.empty? ? (i + 1) : (i - stack.last)
    stack.push(i)
  end

  span
end

# Example
prices = [100, 80, 60, 70, 60, 75, 85]
puts calculate_span(prices).inspect
# => [1, 1, 1, 2, 1, 4, 6]
```

---

#### Stack Applications

**Min Stack** (Get minimum in O(1)):
```ruby
class MinStack
  def initialize
    @stack = []
    @min_stack = []
  end

  def push(value)
    @stack.push(value)

    if @min_stack.empty? || value <= @min_stack.last
      @min_stack.push(value)
    end
  end

  def pop
    value = @stack.pop
    @min_stack.pop if value == @min_stack.last
    value
  end

  def top
    @stack.last
  end

  def get_min
    @min_stack.last
  end
end

# Example
min_stack = MinStack.new
min_stack.push(5)
min_stack.push(2)
min_stack.push(3)
min_stack.push(1)
puts min_stack.get_min  # => 1
min_stack.pop
puts min_stack.get_min  # => 2
```

**Valid Parentheses with Star**:
```ruby
def check_valid_string(s)
  low = high = 0

  s.each_char do |char|
    if char == '('
      low += 1
      high += 1
    elsif char == ')'
      low = [low - 1, 0].max
      high -= 1
    else  # '*'
      low = [low - 1, 0].max
      high += 1
    end

    return false if high < 0
  end

  low == 0
end

# Examples
puts check_valid_string("()")      # => true
puts check_valid_string("(*)")     # => true
puts check_valid_string("(*))")    # => true
```

**Decode String**:
```ruby
def decode_string(s)
  stack = []
  current_num = 0
  current_str = ""

  s.each_char do |char|
    if char =~ /\d/
      current_num = current_num * 10 + char.to_i
    elsif char == '['
      stack.push([current_str, current_num])
      current_str = ""
      current_num = 0
    elsif char == ']'
      prev_str, num = stack.pop
      current_str = prev_str + current_str * num
    else
      current_str += char
    end
  end

  current_str
end

# Examples
puts decode_string("3[a]2[bc]")      # => "aaabcbc"
puts decode_string("3[a2[c]]")       # => "accaccacc"
puts decode_string("2[abc]3[cd]ef")  # => "abcabccdcdcdef"
```

---

### 4. Queue

**What is a Queue?**

A queue is a **linear data structure** that follows the **FIFO** (First In, First Out) principle:
- The **first** element added is the **first** one removed
- Like a line of people: first person in line is served first

**Real-World Analogies**:
- Line at a ticket counter
- Print queue
- Task scheduling in OS
- Breadth-First Search (BFS)
- Message queues in distributed systems

---

#### Queue Fundamentals

**Core Operations**:

| Operation | Description | Time | Space |
|:----------|:------------|:-----|:------|
| `enqueue(x)` | Add element to rear (back) | $O(1)$ | - |
| `dequeue()` | Remove and return front element | $O(1)$ | - |
| `front()` / `peek()` | Return front without removing | $O(1)$ | - |
| `is_empty()` | Check if queue is empty | $O(1)$ | - |
| `size()` | Return number of elements | $O(1)$ | - |

**Space Complexity**: $O(n)$ for $n$ elements

---

**Visual Representation**:

```
Initial Queue       enqueue(3)         enqueue(5)         dequeue()
─────────────       ──────────         ──────────         ─────────

Front → [1][2] ← Rear   Front → [1][2][3] ← Rear   Front → [1][2][3][5] ← Rear   Front → [2][3][5] ← Rear
                                                                                    (1 removed)

FIFO: First In (1), First Out (1)
```

---

**Stack vs Queue Comparison**

| Aspect | Stack (LIFO) | Queue (FIFO) |
|:-------|:-------------|:-------------|
| **Principle** | Last In, First Out | First In, First Out |
| **Insertion** | Top (push) | Rear (enqueue) |
| **Deletion** | Top (pop) | Front (dequeue) |
| **Access** | Top only | Front only |
| **Use Cases** | Undo, DFS, recursion | BFS, scheduling, buffering |
| **Analogy** | Stack of plates | Line of people |

---

**When to Use a Queue?**

**Use Cases**:
- ✅ **Order processing**: First-come, first-served
- ✅ **BFS traversal**: Level-order tree/graph traversal
- ✅ **Task scheduling**: CPU scheduling, print spooler
- ✅ **Buffering**: IO buffers, streaming data
- ✅ **Asynchronous processing**: Message queues (RabbitMQ, Kafka)

**Key Insight**: If you need to process items in **same order** as arrival, use a queue!

---

#### Linear Queue (Array Implementation)

```ruby
class QueueArray
  def initialize(capacity = 10)
    @queue = Array.new(capacity)
    @front = 0
    @rear = -1
    @size = 0
    @capacity = capacity
  end

  def enqueue(value)
    raise "Queue overflow" if full?

    @rear = (@rear + 1) % @capacity
    @queue[@rear] = value
    @size += 1
  end

  def dequeue
    raise "Queue underflow" if empty?

    value = @queue[@front]
    @front = (@front + 1) % @capacity
    @size -= 1
    value
  end

  def front
    raise "Queue is empty" if empty?
    @queue[@front]
  end

  def empty?
    @size == 0
  end

  def full?
    @size == @capacity
  end

  def size
    @size
  end
end
```

---

#### Circular Queue

```ruby
class CircularQueue
  def initialize(k)
    @queue = Array.new(k)
    @head = -1
    @tail = -1
    @size = k
  end

  def enqueue(value)
    return false if is_full?

    if is_empty?
      @head = 0
    end

    @tail = (@tail + 1) % @size
    @queue[@tail] = value
    true
  end

  def dequeue
    return false if is_empty?

    if @head == @tail
      @head = -1
      @tail = -1
      return true
    end

    @head = (@head + 1) % @size
    true
  end

  def front
    return -1 if is_empty?
    @queue[@head]
  end

  def rear
    return -1 if is_empty?
    @queue[@tail]
  end

  def is_empty?
    @head == -1
  end

  def is_full?
    (@tail + 1) % @size == @head
  end
end
```

---

#### Deque (Double-Ended Queue)

```ruby
class Deque
  def initialize
    @deque = []
  end

  def add_front(value)
    @deque.unshift(value)
  end

  def add_rear(value)
    @deque.push(value)
  end

  def remove_front
    raise "Deque is empty" if empty?
    @deque.shift
  end

  def remove_rear
    raise "Deque is empty" if empty?
    @deque.pop
  end

  def front
    raise "Deque is empty" if empty?
    @deque.first
  end

  def rear
    raise "Deque is empty" if empty?
    @deque.last
  end

  def empty?
    @deque.empty?
  end

  def size
    @deque.length
  end
end
```

---

#### Monotonic Queue

**Sliding Window Maximum**:
```ruby
def max_sliding_window(nums, k)
  return [] if nums.empty?

  result = []
  deque = []  # Stores indices

  nums.each_with_index do |num, i|
    # Remove elements outside window
    deque.shift if !deque.empty? && deque.first < i - k + 1

    # Remove smaller elements from rear
    while !deque.empty? && nums[deque.last] < num
      deque.pop
    end

    deque.push(i)

    # Add to result if window is complete
    result << nums[deque.first] if i >= k - 1
  end

  result
end

# Example
nums = [1, 3, -1, -3, 5, 3, 6, 7]
k = 3
puts max_sliding_window(nums, k).inspect
# => [3, 3, 5, 5, 6, 7]
```

**Sliding Window Minimum**:
```ruby
def min_sliding_window(nums, k)
  return [] if nums.empty?

  result = []
  deque = []

  nums.each_with_index do |num, i|
    deque.shift if !deque.empty? && deque.first < i - k + 1

    while !deque.empty? && nums[deque.last] > num
      deque.pop
    end

    deque.push(i)
    result << nums[deque.first] if i >= k - 1
  end

  result
end
```

---

#### Queue using Stacks

```ruby
class QueueUsingStacks
  def initialize
    @stack1 = []  # For enqueue
    @stack2 = []  # For dequeue
  end

  def enqueue(value)
    @stack1.push(value)
  end

  def dequeue
    if @stack2.empty?
      while !@stack1.empty?
        @stack2.push(@stack1.pop)
      end
    end

    raise "Queue is empty" if @stack2.empty?
    @stack2.pop
  end

  def front
    if @stack2.empty?
      while !@stack1.empty?
        @stack2.push(@stack1.pop)
      end
    end

    raise "Queue is empty" if @stack2.empty?
    @stack2.last
  end

  def empty?
    @stack1.empty? && @stack2.empty?
  end
end
```

---

#### Stack using Queues

```ruby
class StackUsingQueues
  def initialize
    @queue = []
  end

  def push(value)
    @queue.push(value)

    # Rotate queue to make new element front
    (@queue.length - 1).times do
      @queue.push(@queue.shift)
    end
  end

  def pop
    raise "Stack is empty" if empty?
    @queue.shift
  end

  def top
    raise "Stack is empty" if empty?
    @queue.first
  end

  def empty?
    @queue.empty?
  end
end
```

---

### 5. Hashing & Hash Tables

#### Hash Function Fundamentals

**Definition**: Function that maps data of arbitrary size to fixed-size values.

**Properties of Good Hash Function**:
1. **Deterministic**: Same input → same output
2. **Uniform Distribution**: Minimizes collisions
3. **Fast Computation**: O(1) time
4. **Avalanche Effect**: Small input change → large output change

**Common Hash Functions**:
```ruby
# Division method
def hash_division(key, table_size)
  key.hash % table_size
end

# Multiplication method
def hash_multiplication(key, table_size)
  a = 0.6180339887  # (√5 - 1) / 2
  ((key * a) % 1 * table_size).floor
end

# String hashing (polynomial rolling hash)
def hash_string(s, table_size)
  hash = 0
  prime = 31

  s.each_char do |char|
    hash = (hash * prime + char.ord) % table_size
  end

  hash
end

# Examples
puts hash_division(12345, 100)           # => 45
puts hash_multiplication(12345, 100)     # => 32
puts hash_string("hello", 100)           # => 99
```

---

#### Collision Resolution

**1. Chaining (Separate Chaining)**:
```ruby
class HashTableChaining
  def initialize(size = 10)
    @size = size
    @table = Array.new(size) { [] }
    @count = 0
  end

  def hash(key)
    key.hash % @size
  end

  def put(key, value)
    index = hash(key)
    bucket = @table[index]

    # Update if key exists
    bucket.each do |pair|
      if pair[0] == key
        pair[1] = value
        return
      end
    end

    # Add new key-value pair
    bucket << [key, value]
    @count += 1

    # Resize if load factor > 0.75
    resize if load_factor > 0.75
  end

  def get(key)
    index = hash(key)
    bucket = @table[index]

    bucket.each do |pair|
      return pair[1] if pair[0] == key
    end

    nil
  end

  def delete(key)
    index = hash(key)
    bucket = @table[index]

    bucket.each_with_index do |pair, i|
      if pair[0] == key
        bucket.delete_at(i)
        @count -= 1
        return pair[1]
      end
    end

    nil
  end

  def contains?(key)
    !get(key).nil?
  end

  def load_factor
    @count.to_f / @size
  end

  def resize
    old_table = @table
    @size *= 2
    @table = Array.new(@size) { [] }
    @count = 0

    old_table.each do |bucket|
      bucket.each do |key, value|
        put(key, value)
      end
    end
  end

  def display
    @table.each_with_index do |bucket, i|
      next if bucket.empty?
      puts "#{i}: #{bucket.inspect}"
    end
  end
end

# Example
ht = HashTableChaining.new(5)
ht.put("apple", 1)
ht.put("banana", 2)
ht.put("cherry", 3)
ht.put("date", 4)
ht.display
puts ht.get("banana")  # => 2
ht.delete("banana")
puts ht.get("banana")  # => nil
```

**2. Open Addressing**:

**Linear Probing**:
```ruby
class HashTableLinearProbing
  def initialize(size = 10)
    @size = size
    @keys = Array.new(size)
    @values = Array.new(size)
    @count = 0
  end

  def hash(key)
    key.hash % @size
  end

  def put(key, value)
    resize if @count >= @size / 2

    index = hash(key)

    # Linear probing
    while @keys[index]
      if @keys[index] == key
        @values[index] = value
        return
      end
      index = (index + 1) % @size
    end

    @keys[index] = key
    @values[index] = value
    @count += 1
  end

  def get(key)
    index = hash(key)

    while @keys[index]
      return @values[index] if @keys[index] == key
      index = (index + 1) % @size
    end

    nil
  end

  def delete(key)
    index = hash(key)

    while @keys[index]
      if @keys[index] == key
        @keys[index] = nil
        @values[index] = nil
        @count -= 1

        # Rehash subsequent entries
        rehash_from(index)
        return
      end
      index = (index + 1) % @size
    end
  end

  def rehash_from(start)
    index = (start + 1) % @size

    while @keys[index]
      key = @keys[index]
      value = @values[index]
      @keys[index] = nil
      @values[index] = nil
      @count -= 1

      put(key, value)
      index = (index + 1) % @size
    end
  end

  def resize
    old_keys = @keys
    old_values = @values

    @size *= 2
    @keys = Array.new(@size)
    @values = Array.new(@size)
    @count = 0

    old_keys.each_with_index do |key, i|
      put(key, old_values[i]) if key
    end
  end
end
```

**Quadratic Probing**:
```ruby
class HashTableQuadraticProbing
  def initialize(size = 10)
    @size = size
    @keys = Array.new(size)
    @values = Array.new(size)
    @count = 0
  end

  def hash(key)
    key.hash % @size
  end

  def put(key, value)
    index = hash(key)
    i = 0

    loop do
      probe_index = (index + i * i) % @size

      if @keys[probe_index].nil? || @keys[probe_index] == key
        @keys[probe_index] = key
        @values[probe_index] = value
        @count += 1 if @keys[probe_index] != key
        return
      end

      i += 1
      raise "Hash table full" if i >= @size
    end
  end

  def get(key)
    index = hash(key)
    i = 0

    loop do
      probe_index = (index + i * i) % @size

      return nil if @keys[probe_index].nil?
      return @values[probe_index] if @keys[probe_index] == key

      i += 1
      return nil if i >= @size
    end
  end
end
```

**Double Hashing**:
```ruby
class HashTableDoubleHashing
  def initialize(size = 10)
    @size = size
    @keys = Array.new(size)
    @values = Array.new(size)
    @count = 0
  end

  def hash1(key)
    key.hash % @size
  end

  def hash2(key)
    prime = 7
    prime - (key.hash % prime)
  end

  def put(key, value)
    index = hash1(key)
    step = hash2(key)
    i = 0

    loop do
      probe_index = (index + i * step) % @size

      if @keys[probe_index].nil? || @keys[probe_index] == key
        @keys[probe_index] = key
        @values[probe_index] = value
        @count += 1 if @keys[probe_index] != key
        return
      end

      i += 1
      raise "Hash table full" if i >= @size
    end
  end

  def get(key)
    index = hash1(key)
    step = hash2(key)
    i = 0

    loop do
      probe_index = (index + i * step) % @size

      return nil if @keys[probe_index].nil?
      return @values[probe_index] if @keys[probe_index] == key

      i += 1
      return nil if i >= @size
    end
  end
end
```

---

#### Load Factor & Rehashing

**Load Factor**: α = n / m (n = elements, m = table size)

**Guidelines**:
- **Chaining**: α can be > 1, but performance degrades
- **Open Addressing**: α should be < 0.7 for good performance

**Rehashing Strategy**:
```ruby
class HashTableWithRehashing
  def initialize(size = 10)
    @size = size
    @table = Array.new(size) { [] }
    @count = 0
    @max_load_factor = 0.75
  end

  def put(key, value)
    rehash if load_factor > @max_load_factor

    index = hash(key)
    bucket = @table[index]

    bucket.each do |pair|
      if pair[0] == key
        pair[1] = value
        return
      end
    end

    bucket << [key, value]
    @count += 1
  end

  def load_factor
    @count.to_f / @size
  end

  def rehash
    puts "Rehashing: #{@size} → #{@size * 2}"
    old_table = @table
    @size *= 2
    @table = Array.new(@size) { [] }
    @count = 0

    old_table.each do |bucket|
      bucket.each do |key, value|
        put(key, value)
      end
    end
  end

  def hash(key)
    key.hash % @size
  end
end
```

---

#### Hash Table Applications

**Two Sum Problem**:
```ruby
def two_sum(nums, target)
  hash = {}

  nums.each_with_index do |num, i|
    complement = target - num
    return [hash[complement], i] if hash.key?(complement)
    hash[num] = i
  end

  nil
end

# Example
nums = [2, 7, 11, 15]
target = 9
puts two_sum(nums, target).inspect  # => [0, 1]
```

**Group Anagrams**:
```ruby
def group_anagrams(strs)
  hash = Hash.new { |h, k| h[k] = [] }

  strs.each do |str|
    key = str.chars.sort.join
    hash[key] << str
  end

  hash.values
end

# Example
strs = ["eat", "tea", "tan", "ate", "nat", "bat"]
puts group_anagrams(strs).inspect
# => [["eat", "tea", "ate"], ["tan", "nat"], ["bat"]]
```

**Longest Consecutive Sequence**:
```ruby
def longest_consecutive(nums)
  return 0 if nums.empty?

  num_set = nums.to_set
  max_length = 0

  nums.each do |num|
    # Only start counting if it's the beginning of a sequence
    next if num_set.include?(num - 1)

    current_num = num
    current_length = 1

    while num_set.include?(current_num + 1)
      current_num += 1
      current_length += 1
    end

    max_length = [max_length, current_length].max
  end

  max_length
end

# Example
nums = [100, 4, 200, 1, 3, 2]
puts longest_consecutive(nums)  # => 4 ([1, 2, 3, 4])
```

**Subarray Sum Equals K**:
```ruby
def subarray_sum(nums, k)
  count = 0
  sum = 0
  hash = { 0 => 1 }  # sum => frequency

  nums.each do |num|
    sum += num
    count += hash[sum - k] if hash[sum - k]
    hash[sum] = (hash[sum] || 0) + 1
  end

  count
end

# Example
nums = [1, 1, 1]
k = 2
puts subarray_sum(nums, k)  # => 2
```

**LRU Cache**:
```ruby
class LRUCache
  def initialize(capacity)
    @capacity = capacity
    @cache = {}
    @order = []
  end

  def get(key)
    return -1 unless @cache.key?(key)

    # Move to end (most recently used)
    @order.delete(key)
    @order.push(key)

    @cache[key]
  end

  def put(key, value)
    if @cache.key?(key)
      @order.delete(key)
    elsif @cache.size >= @capacity
      # Remove least recently used
      lru_key = @order.shift
      @cache.delete(lru_key)
    end

    @cache[key] = value
    @order.push(key)
  end
end

# Example
cache = LRUCache.new(2)
cache.put(1, 1)
cache.put(2, 2)
puts cache.get(1)     # => 1
cache.put(3, 3)       # Evicts key 2
puts cache.get(2)     # => -1 (not found)
cache.put(4, 4)       # Evicts key 1
puts cache.get(1)     # => -1 (not found)
puts cache.get(3)     # => 3
puts cache.get(4)     # => 4
```

**First Non-Repeating Character**:
```ruby
def first_uniq_char(s)
  freq = Hash.new(0)

  s.each_char { |char| freq[char] += 1 }

  s.each_char.with_index do |char, i|
    return i if freq[char] == 1
  end

  -1
end

# Example
puts first_uniq_char("leetcode")     # => 0 ('l')
puts first_uniq_char("loveleetcode") # => 2 ('v')
puts first_uniq_char("aabb")         # => -1
```

**Isomorphic Strings**:
```ruby
def is_isomorphic?(s, t)
  return false if s.length != t.length

  s_to_t = {}
  t_to_s = {}

  s.each_char.with_index do |char, i|
    t_char = t[i]

    if s_to_t[char]
      return false if s_to_t[char] != t_char
    else
      s_to_t[char] = t_char
    end

    if t_to_s[t_char]
      return false if t_to_s[t_char] != char
    else
      t_to_s[t_char] = char
    end
  end

  true
end

# Examples
puts is_isomorphic?("egg", "add")    # => true
puts is_isomorphic?("foo", "bar")    # => false
puts is_isomorphic?("paper", "title") # => true
```

---

#### Collision Resolution Comparison

| Method | Pros | Cons | Best For |
|:-------|:-----|:-----|:---------|
| **Chaining** | Simple, handles high load factors | Extra memory for pointers | General purpose |
| **Linear Probing** | Cache-friendly, simple | Primary clustering | Small load factors |
| **Quadratic Probing** | Reduces clustering | Secondary clustering | Medium load factors |
| **Double Hashing** | Minimal clustering | More complex | High performance needs |

**Clustering Visualization**:
```
Linear Probing (Primary Clustering):
[X][X][X][X][ ][ ][ ]  ← Long cluster

Quadratic Probing (Secondary Clustering):
[X][ ][X][ ][X][ ][X]  ← Better distribution

Double Hashing (Minimal Clustering):
[X][ ][ ][X][ ][X][ ]  ← Best distribution
```

---

#### Hash Table vs Other Data Structures

| Operation | Hash Table | Array | BST |
|:----------|:-----------|:------|:----|
| **Search** | O(1) avg, O(n) worst | O(n) | O(log n) avg |
| **Insert** | O(1) avg, O(n) worst | O(1) end, O(n) middle | O(log n) avg |
| **Delete** | O(1) avg, O(n) worst | O(1) end, O(n) middle | O(log n) avg |
| **Ordered Traversal** | No | No | Yes |
| **Min/Max** | O(n) | O(n) or O(1) if sorted | O(log n) |
| **Space** | O(n) | O(n) | O(n) |

**When to Use Hash Table**:
- ✅ Fast lookups needed
- ✅ Key-value associations
- ✅ Checking existence
- ✅ Counting frequencies
- ❌ Need ordered data
- ❌ Need range queries
- ❌ Memory constrained

---

## Part II — Trees

**What is a Tree?**

A tree is a **hierarchical data structure** consisting of nodes connected by edges, with:
- **One root** node at the top
- **No cycles** (acyclic graph)
- **Unique path** between any two nodes

**Why Trees?**

Trees are fundamental for:
- ✅ **Hierarchical data**: File systems, organization charts, DOM
- ✅ **Fast search**: Binary Search Trees ($O(\log n)$)
- ✅ **Sorted data**: In-order traversal gives sorted sequence
- ✅ **Efficient operations**: Insert, delete, search in $O(\log n)$

---

### 6. Tree Fundamentals

#### Tree Terminology

**Basic Structure**:
```
                 A              ← Root (no parent)
               /   \
              B     C           ← Internal nodes (have children)
             / \     \
            D   E     F         ← Leaf nodes (no children)

Level 0:     A
Level 1:     B, C
Level 2:     D, E, F
```

---

**Essential Definitions**:

| Term | Definition | Example (from tree above) |
|:-----|:-----------|:--------------------------|
| **Root** | Top node with no parent | A |
| **Parent** | Node with children | A is parent of B, C |
| **Child** | Node descended from another | B, C are children of A |
| **Leaf** | Node with **no children** | D, E, F |
| **Internal Node** | Node with **at least one child** | A, B, C |
| **Sibling** | Nodes with **same parent** | B and C are siblings |
| **Ancestor** | Nodes on path from **root to node** | A, B are ancestors of D |
| **Descendant** | Nodes on path from **node to leaves** | D, E are descendants of B |
| **Subtree** | Tree formed by node and descendants | Subtree rooted at B: {B, D, E} |
| **Edge** | Connection between two nodes | (A,B), (A,C), (B,D), etc. |

---

**Height & Depth** (Critical Concepts!)

**Depth of a node**: Number of edges from **root to that node**

$$\text{depth}(\text{node}) = \text{number of edges from root to node}$$

**Height of a node**: Number of edges on **longest path from node to a leaf**

$$\text{height}(\text{node}) = \max(\text{edges from node to any leaf})$$

**Height of tree**: Height of the **root node**

$$\text{height}(\text{tree}) = \text{height}(\text{root})$$

**Visual Example**:
```
                 A              depth=0, height=2
               /   \
              B     C           depth=1, height=1 (B), height=1 (C)
             / \     \
            D   E     F         depth=2, height=0 (all leaves)
```

**Key Relationships**:
- Leaf nodes: height = 0
- Root node: depth = 0
- For any node: $\text{depth} + \text{height} \leq \text{height of tree}$

---

**Degree**

**Degree of a node**: Number of **children** it has

$$\text{degree}(\text{node}) = \text{number of children}$$

**Degree of a tree**: **Maximum degree** among all nodes

$$\text{degree}(\text{tree}) = \max(\text{degree of all nodes})$$

**Example**:
- degree(A) = 2 (children: B, C)
- degree(B) = 2 (children: D, E)
- degree(C) = 1 (child: F)
- degree(D) = degree(E) = degree(F) = 0 (leaves)
- degree(tree) = 2

---

#### Tree Properties (Mathematical Formulas)

**Universal Tree Properties** (for any tree with $n$ nodes):

1. **Number of edges**:
   $$\text{edges} = n - 1$$

   **Why?** Each node except root has exactly one incoming edge.

2. **Minimum height** (balanced/complete tree):
   $$h_{\min} = \lceil \log_2(n+1) \rceil - 1$$

   **Why?** Complete binary tree is most compact.

3. **Maximum height** (skewed/degenerate tree):
   $$h_{\max} = n - 1$$

   **Why?** All nodes in a single chain (like a linked list).

---

**Binary Tree Specific Properties**:

1. **Maximum nodes at level** $i$:
   $$\text{nodes at level } i = 2^i$$

   **Example**: Level 0: $2^0=1$, Level 1: $2^1=2$, Level 2: $2^2=4$

2. **Maximum nodes in tree of height** $h$:
   $$\text{max nodes} = 2^{h+1} - 1$$

   **Derivation**: $1 + 2 + 4 + \cdots + 2^h = 2^{h+1} - 1$ (geometric series)

3. **Minimum height for** $n$ **nodes**:
   $$h_{\min} = \lceil \log_2(n+1) \rceil - 1$$

4. **Relationship between leaves** ($L$) **and internal nodes** ($I$) **with degree 2**:
   $$L = I + 1$$

   **Why?** In a binary tree, each internal node with 2 children adds one more leaf than itself.

---

**Complete vs Full vs Perfect Binary Trees**

| Property | Full Binary Tree | Complete Binary Tree | Perfect Binary Tree |
|:---------|:-----------------|:---------------------|:--------------------|
| **Definition** | Every node has 0 or 2 children | All levels filled except possibly last, filled left-to-right | All levels completely filled |
| **Nodes** | $n = 2k + 1$ (odd) | $2^h \leq n \leq 2^{h+1} - 1$ | $n = 2^{h+1} - 1$ |
| **Height** | $h = \lfloor \log_2 n \rfloor$ | $h = \lfloor \log_2 n \rfloor$ | $h = \log_2(n+1) - 1$ |
| **Example** | All internal nodes have 2 kids | Heap structure | All leaves at same level |

**Ruby Calculation**:
```ruby
def tree_properties(n)
  min_height = Math.log2(n + 1).ceil - 1
  max_height = n - 1
  edges = n - 1

  puts "Nodes: #{n}"
  puts "Edges: #{edges}"
  puts "Min height: #{min_height} (complete tree)"
  puts "Max height: #{max_height} (skewed tree)"
end

tree_properties(7)
# Nodes: 7
# Edges: 6
# Min height: 2 (complete tree)
# Max height: 6 (skewed tree)
```

---

#### Tree Representations

**1. Array Representation** (for complete binary trees):
```
Index:  0   1   2   3   4   5   6
Array: [A] [B] [C] [D] [E] [F] [G]

         A (0)
       /       \
     B (1)     C (2)
    /   \     /   \
  D(3) E(4) F(5) G(6)

For node at index i:
- Left child: 2i + 1
- Right child: 2i + 2
- Parent: (i - 1) / 2
```

```ruby
class BinaryTreeArray
  def initialize(size)
    @tree = Array.new(size)
  end

  def set_root(value)
    @tree[0] = value
  end

  def set_left(parent_index, value)
    left_index = 2 * parent_index + 1
    @tree[left_index] = value if left_index < @tree.length
  end

  def set_right(parent_index, value)
    right_index = 2 * parent_index + 2
    @tree[right_index] = value if right_index < @tree.length
  end

  def get_left(parent_index)
    left_index = 2 * parent_index + 1
    left_index < @tree.length ? @tree[left_index] : nil
  end

  def get_right(parent_index)
    right_index = 2 * parent_index + 2
    right_index < @tree.length ? @tree[right_index] : nil
  end

  def get_parent(child_index)
    return nil if child_index == 0
    parent_index = (child_index - 1) / 2
    @tree[parent_index]
  end
end
```

**2. Linked Representation**:
```ruby
class TreeNode
  attr_accessor :data, :left, :right

  def initialize(data)
    @data = data
    @left = nil
    @right = nil
  end
end

# Create tree
root = TreeNode.new('A')
root.left = TreeNode.new('B')
root.right = TreeNode.new('C')
root.left.left = TreeNode.new('D')
root.left.right = TreeNode.new('E')
```

---

### 7. Binary Trees

#### Types of Binary Trees

**1. Full Binary Tree**: Every node has 0 or 2 children
```
       A
     /   \
    B     C
   / \
  D   E
```

**2. Complete Binary Tree**: All levels filled except possibly last, filled left to right
```
       A
     /   \
    B     C
   / \   /
  D   E F
```

**3. Perfect Binary Tree**: All internal nodes have 2 children, all leaves at same level
```
       A
     /   \
    B     C
   / \   / \
  D   E F   G
```

**4. Balanced Binary Tree**: Height difference between left and right subtrees ≤ 1
```
       A
     /   \
    B     C
   /
  D
```

**5. Degenerate/Skewed Tree**: Each node has only one child
```
  A
   \
    B
     \
      C
       \
        D
```

**Ruby Implementation to Check Types**:
```ruby
class TreeNode
  attr_accessor :data, :left, :right

  def initialize(data)
    @data = data
    @left = nil
    @right = nil
  end
end

# Check if full binary tree
def is_full?(root)
  return true if root.nil?
  return true if root.left.nil? && root.right.nil?
  return false if root.left.nil? || root.right.nil?

  is_full?(root.left) && is_full?(root.right)
end

# Check if complete binary tree
def is_complete?(root)
  return true if root.nil?

  queue = [root]
  flag = false  # Flag when we see a node with missing child

  while !queue.empty?
    node = queue.shift

    if node.left
      return false if flag
      queue.push(node.left)
    else
      flag = true
    end

    if node.right
      return false if flag
      queue.push(node.right)
    else
      flag = true
    end
  end

  true
end

# Check if perfect binary tree
def is_perfect?(root)
  depth = tree_depth(root)
  is_perfect_helper(root, depth, 0)
end

def is_perfect_helper(root, depth, level)
  return true if root.nil?

  # Leaf node
  if root.left.nil? && root.right.nil?
    return depth == level
  end

  # Internal node must have both children
  return false if root.left.nil? || root.right.nil?

  is_perfect_helper(root.left, depth, level + 1) &&
  is_perfect_helper(root.right, depth, level + 1)
end

def tree_depth(root)
  return -1 if root.nil?
  1 + tree_depth(root.left)
end

# Check if balanced
def is_balanced?(root)
  check_balance(root) != -1
end

def check_balance(root)
  return 0 if root.nil?

  left_height = check_balance(root.left)
  return -1 if left_height == -1

  right_height = check_balance(root.right)
  return -1 if right_height == -1

  return -1 if (left_height - right_height).abs > 1

  [left_height, right_height].max + 1
end
```

---

#### Tree Traversals

**What is Tree Traversal?**

Tree traversal is the process of **visiting each node** in a tree exactly once in a specific order. Unlike linear data structures (arrays, linked lists), trees can be traversed in multiple ways.

**Two Main Categories**:
1. **Depth-First Search (DFS)**: Go deep before going wide
2. **Breadth-First Search (BFS)**: Go wide before going deep

---

**Depth-First Traversals (DFS)**

Three types based on when we **visit the root**:

| Traversal | Order | Use Case |
|:----------|:------|:---------|
| **Preorder** | Root → Left → Right | Copy tree, prefix expression |
| **Inorder** | Left → Root → Right | Get sorted sequence (BST) |
| **Postorder** | Left → Right → Root | Delete tree, postfix expression |

**Visual Example**:
```
         1
       /   \
      2     3
     / \
    4   5

Preorder:   1, 2, 4, 5, 3  (Root first)
Inorder:    4, 2, 5, 1, 3  (Root middle)
Postorder:  4, 5, 2, 3, 1  (Root last)
```

---

**1. Preorder Traversal** (Root → Left → Right)

**Process**:
1. Visit **root**
2. Traverse **left** subtree
3. Traverse **right** subtree

**Use Cases**:
- Create a copy of the tree
- Get prefix expression of expression tree
- Serialize a tree

**Time**: $O(n)$, **Space**: $O(h)$ where $h$ is height (recursion stack)
```ruby
def preorder(root, result = [])
  return result if root.nil?

  result << root.data
  preorder(root.left, result)
  preorder(root.right, result)
  result
end

# Iterative
def preorder_iterative(root)
  return [] if root.nil?

  result = []
  stack = [root]

  while !stack.empty?
    node = stack.pop
    result << node.data

    stack.push(node.right) if node.right
    stack.push(node.left) if node.left
  end

  result
end
```

---

**2. Inorder Traversal** (Left → Root → Right)

**Process**:
1. Traverse **left** subtree
2. Visit **root**
3. Traverse **right** subtree

**Use Cases**:
- Get **sorted sequence** from Binary Search Tree (BST)
- Get infix expression from expression tree
- Validate BST property

**Key Property**: For BST, inorder traversal gives **sorted order**!

**Time**: $O(n)$, **Space**: $O(h)$

```ruby
def inorder(root, result = [])
  return result if root.nil?

  inorder(root.left, result)   # Left
  result << root.data           # Root
  inorder(root.right, result)   # Right
  result
end

# Iterative (using stack)
def inorder_iterative(root)
  return [] if root.nil?

  result = []
  stack = []
  current = root

  while current || !stack.empty?
    # Go to leftmost node
    while current
      stack.push(current)
      current = current.left
    end

    # Process node
    current = stack.pop
    result << current.data

    # Move to right subtree
    current = current.right
  end

  result
end
```

---

**3. Postorder Traversal** (Left → Right → Root)

**Process**:
1. Traverse **left** subtree
2. Traverse **right** subtree
3. Visit **root**

**Use Cases**:
- **Delete tree** (delete children before parent)
- Get **postfix expression** from expression tree
- Calculate **directory size** (process subdirectories first)

**Key Property**: Root is processed **last** - useful for cleanup operations!

**Time**: $O(n)$, **Space**: $O(h)$

```ruby
def postorder(root, result = [])
  return result if root.nil?

  postorder(root.left, result)
  postorder(root.right, result)
  result << root.data
  result
end

# Iterative (using two stacks)
def postorder_iterative(root)
  return [] if root.nil?

  stack1 = [root]
  stack2 = []

  while !stack1.empty?
    node = stack1.pop
    stack2.push(node)

    stack1.push(node.left) if node.left
    stack1.push(node.right) if node.right
  end

  stack2.reverse.map(&:data)
end
```

---

**Breadth-First Traversal (Level Order / BFS)**

**What is Level Order Traversal?**

Visit nodes **level by level**, from left to right at each level. Uses a **queue** (FIFO).

**Process**:
1. Start with root in queue
2. While queue not empty:
   - Dequeue node
   - Visit node
   - Enqueue left child (if exists)
   - Enqueue right child (if exists)

**Visual**:
```
         1              Level 0: [1]
       /   \            Level 1: [2, 3]
      2     3           Level 2: [4, 5]
     / \
    4   5

Level Order: 1, 2, 3, 4, 5
```

**Use Cases**:
- Find **shortest path** in unweighted tree
- **Level-wise processing** (print tree level by level)
- Find **nodes at distance k** from root

**Time**: $O(n)$, **Space**: $O(w)$ where $w$ is maximum width of tree

```ruby
def level_order(root)
  return [] if root.nil?

  result = []
  queue = [root]

  while !queue.empty?
    node = queue.shift
    result << node.data

    queue.push(node.left) if node.left
    queue.push(node.right) if node.right
  end

  result
end

# Level order with levels separated (useful for many problems!)
def level_order_levels(root)
  return [] if root.nil?

  result = []
  queue = [root]

  while !queue.empty?
    level_size = queue.length
    level = []

    level_size.times do
      node = queue.shift
      level << node.data

      queue.push(node.left) if node.left
      queue.push(node.right) if node.right
    end

    result << level
  end

  result
end
```

**Traversal Example**:
```ruby
# Build tree:
#       1
#      / \
#     2   3
#    / \
#   4   5

root = TreeNode.new(1)
root.left = TreeNode.new(2)
root.right = TreeNode.new(3)
root.left.left = TreeNode.new(4)
root.left.right = TreeNode.new(5)

puts "Preorder:  #{preorder(root).inspect}"      # => [1, 2, 4, 5, 3]
puts "Inorder:   #{inorder(root).inspect}"       # => [4, 2, 5, 1, 3]
puts "Postorder: #{postorder(root).inspect}"     # => [4, 5, 2, 3, 1]
puts "Level:     #{level_order(root).inspect}"   # => [1, 2, 3, 4, 5]
```

---

#### Binary Tree Problems

**Maximum Depth**:
```ruby
def max_depth(root)
  return 0 if root.nil?
  1 + [max_depth(root.left), max_depth(root.right)].max
end
```

**Minimum Depth**:
```ruby
def min_depth(root)
  return 0 if root.nil?
  return 1 if root.left.nil? && root.right.nil?

  left = root.left ? min_depth(root.left) : Float::INFINITY
  right = root.right ? min_depth(root.right) : Float::INFINITY

  1 + [left, right].min
end
```

**Diameter of Tree**:
```ruby
def diameter_of_tree(root)
  @diameter = 0
  height(root)
  @diameter
end

def height(root)
  return 0 if root.nil?

  left = height(root.left)
  right = height(root.right)

  @diameter = [@diameter, left + right].max

  1 + [left, right].max
end
```

**Invert Binary Tree**:
```ruby
def invert_tree(root)
  return nil if root.nil?

  root.left, root.right = root.right, root.left
  invert_tree(root.left)
  invert_tree(root.right)

  root
end
```

**Symmetric Tree**:
```ruby
def is_symmetric?(root)
  return true if root.nil?
  is_mirror?(root.left, root.right)
end

def is_mirror?(left, right)
  return true if left.nil? && right.nil?
  return false if left.nil? || right.nil?

  left.data == right.data &&
  is_mirror?(left.left, right.right) &&
  is_mirror?(left.right, right.left)
end
```

**Path Sum**:
```ruby
def has_path_sum?(root, target_sum)
  return false if root.nil?
  return root.data == target_sum if root.left.nil? && root.right.nil?

  has_path_sum?(root.left, target_sum - root.data) ||
  has_path_sum?(root.right, target_sum - root.data)
end

# All paths with sum
def path_sum(root, target_sum)
  result = []
  find_paths(root, target_sum, [], result)
  result
end

def find_paths(root, target_sum, path, result)
  return if root.nil?

  path << root.data

  if root.left.nil? && root.right.nil? && path.sum == target_sum
    result << path.dup
  end

  find_paths(root.left, target_sum, path, result)
  find_paths(root.right, target_sum, path, result)

  path.pop
end
```

**Lowest Common Ancestor**:
```ruby
def lowest_common_ancestor(root, p, q)
  return nil if root.nil?
  return root if root == p || root == q

  left = lowest_common_ancestor(root.left, p, q)
  right = lowest_common_ancestor(root.right, p, q)

  return root if left && right
  left || right
end
```

**Serialize and Deserialize**:
```ruby
def serialize(root)
  return "null" if root.nil?

  result = []
  queue = [root]

  while !queue.empty?
    node = queue.shift

    if node
      result << node.data.to_s
      queue.push(node.left)
      queue.push(node.right)
    else
      result << "null"
    end
  end

  result.join(",")
end

def deserialize(data)
  return nil if data == "null"

  values = data.split(",")
  root = TreeNode.new(values[0].to_i)
  queue = [root]
  i = 1

  while !queue.empty? && i < values.length
    node = queue.shift

    if values[i] != "null"
      node.left = TreeNode.new(values[i].to_i)
      queue.push(node.left)
    end
    i += 1

    if i < values.length && values[i] != "null"
      node.right = TreeNode.new(values[i].to_i)
      queue.push(node.right)
    end
    i += 1
  end

  root
end
```

**Vertical Order Traversal**:
```ruby
def vertical_order(root)
  return [] if root.nil?

  column_table = Hash.new { |h, k| h[k] = [] }
  queue = [[root, 0]]  # [node, column]

  while !queue.empty?
    node, column = queue.shift
    column_table[column] << node.data

    queue.push([node.left, column - 1]) if node.left
    queue.push([node.right, column + 1]) if node.right
  end

  column_table.keys.sort.map { |col| column_table[col] }
end
```

**Zigzag Level Order**:
```ruby
def zigzag_level_order(root)
  return [] if root.nil?

  result = []
  queue = [root]
  left_to_right = true

  while !queue.empty?
    level_size = queue.length
    level = []

    level_size.times do
      node = queue.shift
      level << node.data

      queue.push(node.left) if node.left
      queue.push(node.right) if node.right
    end

    level.reverse! unless left_to_right
    result << level
    left_to_right = !left_to_right
  end

  result
end
```

**Right Side View**:
```ruby
def right_side_view(root)
  return [] if root.nil?

  result = []
  queue = [root]

  while !queue.empty?
    level_size = queue.length

    level_size.times do |i|
      node = queue.shift
      result << node.data if i == level_size - 1  # Last node in level

      queue.push(node.left) if node.left
      queue.push(node.right) if node.right
    end
  end

  result
end
```

**Count Complete Tree Nodes**:
```ruby
def count_nodes(root)
  return 0 if root.nil?

  left_height = get_height(root, :left)
  right_height = get_height(root, :right)

  if left_height == right_height
    # Perfect binary tree
    (2 ** left_height) - 1
  else
    1 + count_nodes(root.left) + count_nodes(root.right)
  end
end

def get_height(root, direction)
  height = 0
  node = root

  while node
    height += 1
    node = direction == :left ? node.left : node.right
  end

  height
end
```

---

### 8. Binary Search Trees (BST)

**What is a Binary Search Tree?**

A Binary Search Tree (BST) is a **binary tree** with a special **ordering property** that enables **fast search**, similar to binary search on arrays.

**BST Property** (for every node):

$$\text{All left descendants} < \text{node} < \text{All right descendants}$$

**Formal Definition**: For every node $N$:
- All values in **left subtree** of $N$ are **less than** $N$'s value
- All values in **right subtree** of $N$ are **greater than** $N$'s value
- Both left and right subtrees are also BSTs (recursive property)

---

**Visual Example**:
```
           8                Valid BST
         /   \
        3     10            Left of 8: {3,1,6,4,7} all < 8
       / \      \           Right of 8: {10,14,13} all > 8
      1   6      14
         / \    /
        4   7  13

Inorder: 1, 3, 4, 6, 7, 8, 10, 13, 14  (SORTED!)
```

**Key Insight**: **Inorder traversal** of BST gives **sorted sequence**!

---

**Why Use BST?**

**Advantages**:
- ✅ **Fast search**: $O(\log n)$ average (like binary search)
- ✅ **Dynamic**: Can insert/delete (unlike sorted array)
- ✅ **Sorted traversal**: Inorder gives sorted sequence
- ✅ **Range queries**: Find all elements in range $[a, b]$

**Disadvantages**:
- ❌ **Can degenerate**: Worst case $O(n)$ if unbalanced
- ❌ **No random access**: Must traverse from root
- ❌ **Extra space**: Pointers overhead

---

**Time Complexity** (Average vs Worst Case)

| Operation | Average (Balanced) | Worst (Skewed) |
|:----------|:-------------------|:---------------|
| **Search** | $O(\log n)$ | $O(n)$ |
| **Insert** | $O(\log n)$ | $O(n)$ |
| **Delete** | $O(\log n)$ | $O(n)$ |
| **Min/Max** | $O(\log n)$ | $O(n)$ |
| **Inorder** | $O(n)$ | $O(n)$ |

**Space**: $O(n)$ for $n$ nodes

**Worst case** happens when tree becomes **skewed** (like a linked list):
```
1          Skewed BST (worst case)
 \         All operations: O(n)
  2
   \
    3
     \
      4
```

**Ruby Implementation**:
```ruby
class BSTNode
  attr_accessor :data, :left, :right

  def initialize(data)
    @data = data
    @left = nil
    @right = nil
  end
end

class BST
  attr_accessor :root

  def initialize
    @root = nil
  end

  # Insert - O(log n) average, O(n) worst
  def insert(value)
    @root = insert_helper(@root, value)
  end

  def insert_helper(node, value)
    return BSTNode.new(value) if node.nil?

    if value < node.data
      node.left = insert_helper(node.left, value)
    elsif value > node.data
      node.right = insert_helper(node.right, value)
    end

    node
  end

  # Search - O(log n) average, O(n) worst
  def search(value)
    search_helper(@root, value)
  end

  def search_helper(node, value)
    return nil if node.nil?
    return node if node.data == value

    if value < node.data
      search_helper(node.left, value)
    else
      search_helper(node.right, value)
    end
  end

  # Delete - O(log n) average, O(n) worst
  def delete(value)
    @root = delete_helper(@root, value)
  end

  def delete_helper(node, value)
    return nil if node.nil?

    if value < node.data
      node.left = delete_helper(node.left, value)
    elsif value > node.data
      node.right = delete_helper(node.right, value)
    else
      # Node to delete found

      # Case 1: No children
      return nil if node.left.nil? && node.right.nil?

      # Case 2: One child
      return node.right if node.left.nil?
      return node.left if node.right.nil?

      # Case 3: Two children
      # Find inorder successor (smallest in right subtree)
      successor = find_min(node.right)
      node.data = successor.data
      node.right = delete_helper(node.right, successor.data)
    end

    node
  end

  def find_min(node)
    node = node.left while node.left
    node
  end

  def find_max(node)
    node = node.right while node.right
    node
  end

  # Inorder traversal (gives sorted order)
  def inorder
    result = []
    inorder_helper(@root, result)
    result
  end

  def inorder_helper(node, result)
    return if node.nil?

    inorder_helper(node.left, result)
    result << node.data
    inorder_helper(node.right, result)
  end
end

# Example
bst = BST.new
[8, 3, 10, 1, 6, 14, 4, 7, 13].each { |val| bst.insert(val) }
puts bst.inorder.inspect  # => [1, 3, 4, 6, 7, 8, 10, 13, 14]
puts bst.search(6).data   # => 6
bst.delete(3)
puts bst.inorder.inspect  # => [1, 4, 6, 7, 8, 10, 13, 14]
```

---

#### BST Operations

**Find Successor**:
```ruby
def inorder_successor(root, node)
  # Case 1: Node has right subtree
  if node.right
    return find_min(node.right)
  end

  # Case 2: No right subtree, find ancestor
  successor = nil
  current = root

  while current
    if node.data < current.data
      successor = current
      current = current.left
    elsif node.data > current.data
      current = current.right
    else
      break
    end
  end

  successor
end
```

**Find Predecessor**:
```ruby
def inorder_predecessor(root, node)
  # Case 1: Node has left subtree
  if node.left
    return find_max(node.left)
  end

  # Case 2: No left subtree
  predecessor = nil
  current = root

  while current
    if node.data > current.data
      predecessor = current
      current = current.right
    elsif node.data < current.data
      current = current.left
    else
      break
    end
  end

  predecessor
end
```

**Validate BST**:
```ruby
def is_valid_bst?(root)
  validate(root, -Float::INFINITY, Float::INFINITY)
end

def validate(node, min, max)
  return true if node.nil?
  return false if node.data <= min || node.data >= max

  validate(node.left, min, node.data) &&
  validate(node.right, node.data, max)
end
```

**Kth Smallest Element**:
```ruby
def kth_smallest(root, k)
  @count = 0
  @result = nil
  inorder_kth(root, k)
  @result
end

def inorder_kth(node, k)
  return if node.nil? || @result

  inorder_kth(node.left, k)

  @count += 1
  if @count == k
    @result = node.data
    return
  end

  inorder_kth(node.right, k)
end
```

**BST from Preorder**:
```ruby
def bst_from_preorder(preorder)
  return nil if preorder.empty?

  root = BSTNode.new(preorder[0])
  stack = [root]

  (1...preorder.length).each do |i|
    node = BSTNode.new(preorder[i])

    if preorder[i] < stack.last.data
      stack.last.left = node
    else
      parent = nil
      while !stack.empty? && preorder[i] > stack.last.data
        parent = stack.pop
      end
      parent.right = node
    end

    stack.push(node)
  end

  root
end
```

---

### 9. Self-Balancing Trees

#### AVL Trees

**Definition**: Self-balancing BST where height difference between left and right subtrees ≤ 1 for all nodes.

**Balance Factor**: BF = height(left) - height(right)
- Valid BF ∈ {-1, 0, 1}
- BF > 1: Left-heavy
- BF < -1: Right-heavy

**Rotations**:

**1. Left Rotation (LL)**:
```
    y                x
   / \              / \
  x   C    =>      A   y
 / \                  / \
A   B                B   C
```

**2. Right Rotation (RR)**:
```
  x                  y
 / \                / \
A   y      =>      x   C
   / \            / \
  B   C          A   B
```

**3. Left-Right Rotation (LR)**:
```
    z              z              y
   / \            / \            / \
  x   D   =>     y   D   =>     x   z
 / \            / \            / \ / \
A   y          x   C          A  B C  D
   / \        / \
  B   C      A   B
```

**4. Right-Left Rotation (RL)**:
```
  x              x              y
 / \            / \            / \
A   z   =>     A   y   =>     x   z
   / \            / \        / \ / \
  y   D          B   z      A  B C  D
 / \                / \
B   C              C   D
```

**Ruby Implementation**:
```ruby
class AVLNode
  attr_accessor :data, :left, :right, :height

  def initialize(data)
    @data = data
    @left = nil
    @right = nil
    @height = 1
  end
end

class AVLTree
  attr_accessor :root

  def initialize
    @root = nil
  end

  def height(node)
    node ? node.height : 0
  end

  def balance_factor(node)
    return 0 if node.nil?
    height(node.left) - height(node.right)
  end

  def update_height(node)
    node.height = 1 + [height(node.left), height(node.right)].max
  end

  # Right rotation
  def rotate_right(y)
    x = y.left
    t2 = x.right

    x.right = y
    y.left = t2

    update_height(y)
    update_height(x)

    x
  end

  # Left rotation
  def rotate_left(x)
    y = x.right
    t2 = y.left

    y.left = x
    x.right = t2

    update_height(x)
    update_height(y)

    y
  end

  # Insert
  def insert(value)
    @root = insert_helper(@root, value)
  end

  def insert_helper(node, value)
    # Standard BST insertion
    return AVLNode.new(value) if node.nil?

    if value < node.data
      node.left = insert_helper(node.left, value)
    elsif value > node.data
      node.right = insert_helper(node.right, value)
    else
      return node  # Duplicate values not allowed
    end

    # Update height
    update_height(node)

    # Get balance factor
    balance = balance_factor(node)

    # Left-Left Case
    if balance > 1 && value < node.left.data
      return rotate_right(node)
    end

    # Right-Right Case
    if balance < -1 && value > node.right.data
      return rotate_left(node)
    end

    # Left-Right Case
    if balance > 1 && value > node.left.data
      node.left = rotate_left(node.left)
      return rotate_right(node)
    end

    # Right-Left Case
    if balance < -1 && value < node.right.data
      node.right = rotate_right(node.right)
      return rotate_left(node)
    end

    node
  end

  # Delete
  def delete(value)
    @root = delete_helper(@root, value)
  end

  def delete_helper(node, value)
    return nil if node.nil?

    # Standard BST deletion
    if value < node.data
      node.left = delete_helper(node.left, value)
    elsif value > node.data
      node.right = delete_helper(node.right, value)
    else
      # Node to delete found
      if node.left.nil? || node.right.nil?
        temp = node.left || node.right
        return temp
      end

      # Two children: get inorder successor
      temp = find_min(node.right)
      node.data = temp.data
      node.right = delete_helper(node.right, temp.data)
    end

    return nil if node.nil?

    # Update height
    update_height(node)

    # Get balance factor
    balance = balance_factor(node)

    # Left-Left Case
    if balance > 1 && balance_factor(node.left) >= 0
      return rotate_right(node)
    end

    # Left-Right Case
    if balance > 1 && balance_factor(node.left) < 0
      node.left = rotate_left(node.left)
      return rotate_right(node)
    end

    # Right-Right Case
    if balance < -1 && balance_factor(node.right) <= 0
      return rotate_left(node)
    end

    # Right-Left Case
    if balance < -1 && balance_factor(node.right) > 0
      node.right = rotate_right(node.right)
      return rotate_left(node)
    end

    node
  end

  def find_min(node)
    node = node.left while node.left
    node
  end

  # Inorder traversal
  def inorder(node = @root, result = [])
    return result if node.nil?

    inorder(node.left, result)
    result << node.data
    inorder(node.right, result)
    result
  end

  # Check if balanced
  def is_balanced?(node = @root)
    return true if node.nil?

    balance = balance_factor(node)
    return false if balance.abs > 1

    is_balanced?(node.left) && is_balanced?(node.right)
  end
end

# Example
avl = AVLTree.new
[10, 20, 30, 40, 50, 25].each { |val| avl.insert(val) }
puts avl.inorder.inspect  # => [10, 20, 25, 30, 40, 50]
puts "Balanced: #{avl.is_balanced?}"  # => true

avl.delete(40)
puts avl.inorder.inspect  # => [10, 20, 25, 30, 50]
puts "Balanced: #{avl.is_balanced?}"  # => true
```

**Time Complexity**:
- Insert: O(log n)
- Delete: O(log n)
- Search: O(log n)
- Space: O(n)

**AVL vs BST Comparison**:

| Operation | BST (Avg) | BST (Worst) | AVL |
|:----------|:----------|:------------|:----|
| Insert | O(log n) | O(n) | O(log n) |
| Delete | O(log n) | O(n) | O(log n) |
| Search | O(log n) | O(n) | O(log n) |
| Height | O(log n) | O(n) | O(log n) |

---

#### Red-Black Trees

**What is a Red-Black Tree?**

A Red-Black Tree is a **self-balancing BST** where each node has a **color** (red or black) and follows specific rules to maintain **approximate balance**.

**Why Red-Black Trees?**

Red-Black Trees provide **guaranteed** $O(\log n)$ operations while requiring **fewer rotations** than AVL trees during insertions/deletions.

---

**Red-Black Tree Properties** (5 Rules)

1. **Color Property**: Every node is either **RED** or **BLACK**

2. **Root Property**: The **root** is always **BLACK**

3. **Leaf Property**: All **leaves** (NIL/null nodes) are **BLACK**

4. **Red Property**: A **RED** node cannot have **RED** children
   $$\text{If node is RED} \implies \text{both children must be BLACK}$$

   **No two consecutive red nodes on any path!**

5. **Black Height Property**: All paths from a node to descendant leaves contain the **same number of BLACK nodes**
   $$\text{black-height}(\text{node}) = \text{same for all paths to leaves}$$

---

**Visual Example**:
```
           10(B)              B = Black, R = Red
          /     \
        5(R)    15(B)         Valid Red-Black Tree
       /   \    /    \
     3(B) 7(B) 12(R) 20(R)   - Root is black ✓
                             - No red-red parent-child ✓
                             - All paths have 2 black nodes ✓
```

---

**Height Guarantee**

For a Red-Black Tree with $n$ nodes:

$$h \leq 2 \log_2(n + 1)$$

**Why?** The black-height property ensures the tree cannot be too unbalanced.

**Comparison**: AVL trees are **more strictly balanced** ($h \leq 1.44 \log_2 n$), but Red-Black trees require **fewer rotations**.

---

**Red-Black vs AVL Trees**

| Aspect | Red-Black Tree | AVL Tree |\n|:-------|:---------------|:---------|\n| **Balance** | Approximately balanced | Strictly balanced |\n| **Height** | $h \leq 2 \log_2(n+1)$ | $h \leq 1.44 \log_2 n$ |\n| **Search** | $O(\log n)$ (slightly slower) | $O(\log n)$ (faster) |\n| **Insert** | $O(\log n)$ (fewer rotations) | $O(\log n)$ (more rotations) |\n| **Delete** | $O(\log n)$ (fewer rotations) | $O(\log n)$ (more rotations) |\n| **Rotations** | Max 2 for insert, 3 for delete | Can be $O(\log n)$ |\n| **Use Case** | Frequent insertions/deletions | Frequent searches |\n| **Examples** | Java TreeMap, C++ std::map | Databases, in-memory indexes |

**When to Use**:
- ✅ **Red-Black**: Frequent insertions/deletions (e.g., language libraries)
- ✅ **AVL**: Frequent searches, read-heavy workloads

**Ruby Implementation** (Simplified):
```ruby
class RBNode
  attr_accessor :data, :color, :left, :right, :parent

  RED = :red
  BLACK = :black

  def initialize(data, color = RED)
    @data = data
    @color = color
    @left = nil
    @right = nil
    @parent = nil
  end

  def red?
    @color == RED
  end

  def black?
    @color == BLACK
  end
end

class RedBlackTree
  attr_accessor :root

  def initialize
    @root = nil
  end

  def insert(value)
    new_node = RBNode.new(value)

    if @root.nil?
      @root = new_node
      @root.color = RBNode::BLACK
      return
    end

    # Standard BST insertion
    parent = nil
    current = @root

    while current
      parent = current
      if value < current.data
        current = current.left
      elsif value > current.data
        current = current.right
      else
        return  # Duplicate
      end
    end

    new_node.parent = parent
    if value < parent.data
      parent.left = new_node
    else
      parent.right = new_node
    end

    # Fix Red-Black properties
    fix_insert(new_node)
  end

  def fix_insert(node)
    while node != @root && node.parent.red?
      if node.parent == node.parent.parent.left
        uncle = node.parent.parent.right

        if uncle && uncle.red?
          # Case 1: Uncle is red
          node.parent.color = RBNode::BLACK
          uncle.color = RBNode::BLACK
          node.parent.parent.color = RBNode::RED
          node = node.parent.parent
        else
          if node == node.parent.right
            # Case 2: Node is right child
            node = node.parent
            rotate_left(node)
          end

          # Case 3: Node is left child
          node.parent.color = RBNode::BLACK
          node.parent.parent.color = RBNode::RED
          rotate_right(node.parent.parent)
        end
      else
        # Mirror cases
        uncle = node.parent.parent.left

        if uncle && uncle.red?
          node.parent.color = RBNode::BLACK
          uncle.color = RBNode::BLACK
          node.parent.parent.color = RBNode::RED
          node = node.parent.parent
        else
          if node == node.parent.left
            node = node.parent
            rotate_right(node)
          end

          node.parent.color = RBNode::BLACK
          node.parent.parent.color = RBNode::RED
          rotate_left(node.parent.parent)
        end
      end
    end

    @root.color = RBNode::BLACK
  end

  def rotate_left(node)
    right_child = node.right
    node.right = right_child.left

    right_child.left.parent = node if right_child.left
    right_child.parent = node.parent

    if node.parent.nil?
      @root = right_child
    elsif node == node.parent.left
      node.parent.left = right_child
    else
      node.parent.right = right_child
    end

    right_child.left = node
    node.parent = right_child
  end

  def rotate_right(node)
    left_child = node.left
    node.left = left_child.right

    left_child.right.parent = node if left_child.right
    left_child.parent = node.parent

    if node.parent.nil?
      @root = left_child
    elsif node == node.parent.right
      node.parent.right = left_child
    else
      node.parent.left = left_child
    end

    left_child.right = node
    node.parent = left_child
  end

  def inorder(node = @root, result = [])
    return result if node.nil?

    inorder(node.left, result)
    result << "#{node.data}(#{node.color})"
    inorder(node.right, result)
    result
  end
end

# Example
rbt = RedBlackTree.new
[7, 3, 18, 10, 22, 8, 11, 26].each { |val| rbt.insert(val) }
puts rbt.inorder.inspect
```

---

### 10. B-Trees & m-way Trees

#### B-Tree Fundamentals

**Definition**: Self-balancing search tree optimized for disk-based storage.

**Properties** (B-Tree of order m):
1. Every node has at most m children
2. Every non-leaf node (except root) has at least ⌈m/2⌉ children
3. Root has at least 2 children (if not leaf)
4. All leaves are at same level
5. Non-leaf node with k children has k-1 keys

**Example B-Tree (order 3)**:
```
         [10, 20]
        /    |    \
    [5]   [15]   [25, 30]
```

**Time Complexity**:
- Search: O(log n)
- Insert: O(log n)
- Delete: O(log n)
- Height: O(log_m n)

**Use Cases**:
- Database indexing
- File systems
- Large datasets on disk

**B+ Tree**:
- All data in leaf nodes
- Internal nodes only store keys
- Leaf nodes linked (range queries)
- Better for sequential access

**Comparison**:

| Feature | B-Tree | B+ Tree |
|:--------|:-------|:--------|
| Data location | All nodes | Leaf nodes only |
| Leaf linking | No | Yes |
| Range queries | Slower | Faster |
| Space | Less | More |
| Use case | General | Databases |

---

### 11. Heaps

**What is a Heap?**

A heap is a **complete binary tree** that satisfies the **heap property**, enabling **efficient priority queue** operations.

**Why Heaps?**

Heaps provide:
- ✅ **Fast access to min/max**: $O(1)$
- ✅ **Efficient insert/delete**: $O(\log n)$
- ✅ **Space efficient**: Array representation (no pointers!)
- ✅ **In-place sorting**: Heap sort

---

#### Binary Heap Fundamentals

**Heap Property** (two types):

1. **Max Heap Property**: For every node $i$:
   $$\text{value}(i) \geq \text{value}(\text{children of } i)$$

   **Parent is always ≥ children**

2. **Min Heap Property**: For every node $i$:
   $$\text{value}(i) \leq \text{value}(\text{children of } i)$$

   **Parent is always ≤ children**

**Complete Binary Tree**: All levels filled except possibly last, filled left-to-right.

---

**Visual Examples**:

**Max Heap**:
```
           100                Parent ≥ Children
          /   \
        19     36             100 ≥ 19, 100 ≥ 36
       /  \   /  \            19 ≥ 17, 19 ≥ 3
      17   3 25   1           36 ≥ 25, 36 ≥ 1

Array: [100, 19, 36, 17, 3, 25, 1]
Index:   0   1   2   3  4   5  6
```

**Min Heap**:
```
            1                 Parent ≤ Children
          /   \
         3     25             1 ≤ 3, 1 ≤ 25
       /  \   /  \            3 ≤ 17, 3 ≤ 19
      17  19 36  100          25 ≤ 36, 25 ≤ 100

Array: [1, 3, 25, 17, 19, 36, 100]
```

---

**Array Representation** (Key Insight!)

For node at index $i$ (0-indexed):
- **Left child**: $2i + 1$
- **Right child**: $2i + 2$
- **Parent**: $\lfloor (i-1)/2 \rfloor$

**Example**:
```
Index:  0   1   2   3   4   5   6
Array: [100, 19, 36, 17, 3, 25, 1]

Node at index 1 (value 19):
- Left child: 2(1)+1 = 3 → value 17
- Right child: 2(1)+2 = 4 → value 3
- Parent: (1-1)/2 = 0 → value 100
```

**Why Array?**
- ✅ No pointer overhead
- ✅ Cache-friendly (contiguous memory)
- ✅ Easy parent/child navigation

**Array Representation**:
```
Index:  0   1   2   3   4   5   6
Array: [100, 19, 36, 17, 3, 25, 1]

For index i:
- Parent: (i - 1) / 2
- Left child: 2i + 1
- Right child: 2i + 2
```

**Ruby Implementation - Min Heap**:
```ruby
class MinHeap
  def initialize
    @heap = []
  end

  def parent(i)
    (i - 1) / 2
  end

  def left_child(i)
    2 * i + 1
  end

  def right_child(i)
    2 * i + 2
  end

  def swap(i, j)
    @heap[i], @heap[j] = @heap[j], @heap[i]
  end

  # Insert - O(log n)
  def insert(value)
    @heap << value
    heapify_up(@heap.length - 1)
  end

  def heapify_up(i)
    while i > 0 && @heap[parent(i)] > @heap[i]
      swap(i, parent(i))
      i = parent(i)
    end
  end

  # Extract min - O(log n)
  def extract_min
    return nil if @heap.empty?

    min = @heap[0]
    @heap[0] = @heap.pop
    heapify_down(0) unless @heap.empty?

    min
  end

  def heapify_down(i)
    loop do
      smallest = i
      left = left_child(i)
      right = right_child(i)

      smallest = left if left < @heap.length && @heap[left] < @heap[smallest]
      smallest = right if right < @heap.length && @heap[right] < @heap[smallest]

      break if smallest == i

      swap(i, smallest)
      i = smallest
    end
  end

  # Peek - O(1)
  def peek
    @heap[0]
  end

  def size
    @heap.length
  end

  def empty?
    @heap.empty?
  end

  def to_a
    @heap.dup
  end
end

# Example
heap = MinHeap.new
[5, 3, 7, 1, 9, 2].each { |val| heap.insert(val) }
puts heap.to_a.inspect  # => [1, 3, 2, 5, 9, 7]
puts heap.extract_min   # => 1
puts heap.peek          # => 2
```

**Max Heap Implementation**:
```ruby
class MaxHeap
  def initialize
    @heap = []
  end

  def parent(i)
    (i - 1) / 2
  end

  def left_child(i)
    2 * i + 1
  end

  def right_child(i)
    2 * i + 2
  end

  def swap(i, j)
    @heap[i], @heap[j] = @heap[j], @heap[i]
  end

  def insert(value)
    @heap << value
    heapify_up(@heap.length - 1)
  end

  def heapify_up(i)
    while i > 0 && @heap[parent(i)] < @heap[i]
      swap(i, parent(i))
      i = parent(i)
    end
  end

  def extract_max
    return nil if @heap.empty?

    max = @heap[0]
    @heap[0] = @heap.pop
    heapify_down(0) unless @heap.empty?

    max
  end

  def heapify_down(i)
    loop do
      largest = i
      left = left_child(i)
      right = right_child(i)

      largest = left if left < @heap.length && @heap[left] > @heap[largest]
      largest = right if right < @heap.length && @heap[right] > @heap[largest]

      break if largest == i

      swap(i, largest)
      i = largest
    end
  end

  def peek
    @heap[0]
  end

  def size
    @heap.length
  end
end
```

---

#### Heapify Algorithm

**Build Heap from Array** - O(n):
```ruby
def build_min_heap(arr)
  heap = arr.dup
  n = heap.length

  # Start from last non-leaf node
  ((n / 2) - 1).downto(0) do |i|
    heapify_down_array(heap, n, i)
  end

  heap
end

def heapify_down_array(heap, n, i)
  loop do
    smallest = i
    left = 2 * i + 1
    right = 2 * i + 2

    smallest = left if left < n && heap[left] < heap[smallest]
    smallest = right if right < n && heap[right] < heap[smallest]

    break if smallest == i

    heap[i], heap[smallest] = heap[smallest], heap[i]
    i = smallest
  end
end

# Example
arr = [4, 10, 3, 5, 1]
heap = build_min_heap(arr)
puts heap.inspect  # => [1, 4, 3, 5, 10]
```

**Max Heapify**:
```ruby
def build_max_heap(arr)
  heap = arr.dup
  n = heap.length

  ((n / 2) - 1).downto(0) do |i|
    heapify_down_max(heap, n, i)
  end

  heap
end

def heapify_down_max(heap, n, i)
  loop do
    largest = i
    left = 2 * i + 1
    right = 2 * i + 2

    largest = left if left < n && heap[left] > heap[largest]
    largest = right if right < n && heap[right] > heap[largest]

    break if largest == i

    heap[i], heap[largest] = heap[largest], heap[i]
    i = largest
  end
end
```

---

#### Heap Sort

**What is Heap Sort?**

Heap Sort is a **comparison-based sorting algorithm** that uses a **binary heap** data structure. It provides **guaranteed** $O(n \log n)$ time complexity with $O(1)$ space.

**Algorithm** (Two Phases):

1. **Build Max Heap**: Convert array into max heap - $O(n)$
2. **Extract Max Repeatedly**: Swap root with last element, reduce heap size, heapify - $O(n \log n)$

**Visual Process**:
```
Initial: [12, 11, 13, 5, 6, 7]

Step 1: Build Max Heap
         13
        /  \
      12    7
     / \   /
    5  6  11

Array: [13, 12, 7, 5, 6, 11]

Step 2: Extract Max (swap 13 with last, heapify)
         12
        /  \
      11    7
     / \
    5  6  [13]

Step 3: Continue...
Final: [5, 6, 7, 11, 12, 13]
```

---

**Ruby Implementation**:

```ruby
def heap_sort(arr)
  n = arr.length

  # Phase 1: Build max heap - O(n)
  ((n / 2) - 1).downto(0) do |i|
    heapify_down_max(arr, n, i)
  end

  # Phase 2: Extract elements one by one - O(n log n)
  (n - 1).downto(1) do |i|
    # Move current root (max) to end
    arr[0], arr[i] = arr[i], arr[0]

    # Heapify reduced heap
    heapify_down_max(arr, i, 0)
  end

  arr
end

# Example
arr = [12, 11, 13, 5, 6, 7]
puts heap_sort(arr).inspect  # => [5, 6, 7, 11, 12, 13]
```

---

**Time & Space Complexity**:

| Case | Time | Explanation |
|:-----|:-----|:------------|
| **Best** | $O(n \log n)$ | Even if sorted, must heapify |
| **Average** | $O(n \log n)$ | Build heap + extract all |
| **Worst** | $O(n \log n)$ | **Guaranteed!** No worst case like Quick Sort |
| **Space** | $O(1)$ | **In-place** sorting |

**Breakdown**:
- Build heap: $O(n)$ (not $O(n \log n)$!)
- Extract max $n$ times: $n \times O(\log n) = O(n \log n)$
- **Total**: $O(n) + O(n \log n) = O(n \log n)$

---

**Heap Sort vs Other Sorting Algorithms**:

| Algorithm | Best | Average | Worst | Space | Stable | In-Place |
|:----------|:-----|:--------|:------|:------|:-------|:---------|
| **Heap Sort** | $O(n \log n)$ | $O(n \log n)$ | $O(n \log n)$ | $O(1)$ | ❌ No | ✅ Yes |
| **Quick Sort** | $O(n \log n)$ | $O(n \log n)$ | $O(n^2)$ | $O(\log n)$ | ❌ No | ✅ Yes |
| **Merge Sort** | $O(n \log n)$ | $O(n \log n)$ | $O(n \log n)$ | $O(n)$ | ✅ Yes | ❌ No |
| **Insertion Sort** | $O(n)$ | $O(n^2)$ | $O(n^2)$ | $O(1)$ | ✅ Yes | ✅ Yes |

**When to Use Heap Sort**:
- ✅ **Guaranteed** $O(n \log n)$ performance (no worst case like Quick Sort)
- ✅ **Memory constrained** (in-place, $O(1)$ space)
- ✅ **Embedded systems** (predictable performance)
- ❌ **Not stable** (doesn't preserve relative order of equal elements)
- ❌ **Cache unfriendly** (random memory access pattern)

---

#### Heap Applications

**K Largest Elements**:
```ruby
def k_largest(arr, k)
  min_heap = MinHeap.new

  arr.each do |num|
    min_heap.insert(num)
    min_heap.extract_min if min_heap.size > k
  end

  min_heap.to_a
end

# Example
arr = [3, 2, 1, 5, 6, 4]
k = 2
puts k_largest(arr, k).inspect  # => [5, 6]
```

**K Smallest Elements**:
```ruby
def k_smallest(arr, k)
  max_heap = MaxHeap.new

  arr.each do |num|
    max_heap.insert(num)
    max_heap.extract_max if max_heap.size > k
  end

  max_heap.to_a
end

# Example
arr = [7, 10, 4, 3, 20, 15]
k = 3
puts k_smallest(arr, k).inspect  # => [3, 4, 7]
```

**Kth Largest Element**:
```ruby
def find_kth_largest(nums, k)
  min_heap = MinHeap.new

  nums.each do |num|
    min_heap.insert(num)
    min_heap.extract_min if min_heap.size > k
  end

  min_heap.peek
end

# Example
nums = [3, 2, 1, 5, 6, 4]
k = 2
puts find_kth_largest(nums, k)  # => 5
```

**Merge K Sorted Arrays**:
```ruby
def merge_k_sorted(arrays)
  min_heap = MinHeap.new
  result = []

  # Insert first element from each array
  arrays.each_with_index do |arr, i|
    min_heap.insert([arr[0], i, 0]) unless arr.empty?
  end

  while !min_heap.empty?
    value, array_idx, elem_idx = min_heap.extract_min
    result << value

    # Insert next element from same array
    if elem_idx + 1 < arrays[array_idx].length
      next_val = arrays[array_idx][elem_idx + 1]
      min_heap.insert([next_val, array_idx, elem_idx + 1])
    end
  end

  result
end

# Example
arrays = [[1, 4, 7], [2, 5, 8], [3, 6, 9]]
puts merge_k_sorted(arrays).inspect  # => [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

**Running Median**:
```ruby
class MedianFinder
  def initialize
    @max_heap = MaxHeap.new  # Lower half
    @min_heap = MinHeap.new  # Upper half
  end

  def add_num(num)
    if @max_heap.empty? || num <= @max_heap.peek
      @max_heap.insert(num)
    else
      @min_heap.insert(num)
    end

    # Balance heaps
    if @max_heap.size > @min_heap.size + 1
      @min_heap.insert(@max_heap.extract_max)
    elsif @min_heap.size > @max_heap.size
      @max_heap.insert(@min_heap.extract_min)
    end
  end

  def find_median
    if @max_heap.size > @min_heap.size
      @max_heap.peek.to_f
    else
      (@max_heap.peek + @min_heap.peek) / 2.0
    end
  end
end

# Example
mf = MedianFinder.new
mf.add_num(1)
mf.add_num(2)
puts mf.find_median  # => 1.5
mf.add_num(3)
puts mf.find_median  # => 2.0
```

---

### 12. Priority Queues

#### Priority Queue Fundamentals

**Definition**: Abstract data type where each element has a priority.

**Operations**:
- `insert(element, priority)` - O(log n)
- `extract_max/min()` - O(log n)
- `peek()` - O(1)
- `change_priority()` - O(log n)

**Implementation using Heap**:
```ruby
class PriorityQueue
  def initialize(type = :max)
    @heap = []
    @type = type
  end

  def insert(value, priority = value)
    @heap << [priority, value]
    heapify_up(@heap.length - 1)
  end

  def extract
    return nil if @heap.empty?

    top = @heap[0]
    @heap[0] = @heap.pop
    heapify_down(0) unless @heap.empty?

    top[1]  # Return value, not priority
  end

  def peek
    @heap[0] ? @heap[0][1] : nil
  end

  def empty?
    @heap.empty?
  end

  def size
    @heap.length
  end

  private

  def parent(i)
    (i - 1) / 2
  end

  def left_child(i)
    2 * i + 1
  end

  def right_child(i)
    2 * i + 2
  end

  def compare(i, j)
    if @type == :max
      @heap[i][0] > @heap[j][0]
    else
      @heap[i][0] < @heap[j][0]
    end
  end

  def heapify_up(i)
    while i > 0 && compare(i, parent(i))
      @heap[i], @heap[parent(i)] = @heap[parent(i)], @heap[i]
      i = parent(i)
    end
  end

  def heapify_down(i)
    loop do
      target = i
      left = left_child(i)
      right = right_child(i)

      target = left if left < @heap.length && compare(left, target)
      target = right if right < @heap.length && compare(right, target)

      break if target == i

      @heap[i], @heap[target] = @heap[target], @heap[i]
      i = target
    end
  end
end

# Example - Max Priority Queue
pq = PriorityQueue.new(:max)
pq.insert("Task A", 3)
pq.insert("Task B", 1)
pq.insert("Task C", 5)
pq.insert("Task D", 2)

puts pq.extract  # => "Task C" (priority 5)
puts pq.extract  # => "Task A" (priority 3)
puts pq.peek     # => "Task D" (priority 2)
```

**Applications**:

**1. Task Scheduling**:
```ruby
class TaskScheduler
  def initialize
    @pq = PriorityQueue.new(:max)
  end

  def add_task(name, priority)
    @pq.insert(name, priority)
  end

  def execute_next
    task = @pq.extract
    puts "Executing: #{task}" if task
    task
  end

  def pending_tasks
    @pq.size
  end
end

# Example
scheduler = TaskScheduler.new
scheduler.add_task("Critical Bug Fix", 10)
scheduler.add_task("Code Review", 5)
scheduler.add_task("Documentation", 2)
scheduler.execute_next  # => "Critical Bug Fix"
```

**2. Dijkstra's Algorithm** (Shortest Path):
```ruby
def dijkstra(graph, start)
  distances = Hash.new(Float::INFINITY)
  distances[start] = 0

  pq = PriorityQueue.new(:min)
  pq.insert(start, 0)

  while !pq.empty?
    current = pq.extract

    graph[current].each do |neighbor, weight|
      distance = distances[current] + weight

      if distance < distances[neighbor]
        distances[neighbor] = distance
        pq.insert(neighbor, distance)
      end
    end
  end

  distances
end

# Example
graph = {
  'A' => [['B', 4], ['C', 2]],
  'B' => [['D', 3]],
  'C' => [['B', 1], ['D', 5]],
  'D' => []
}

puts dijkstra(graph, 'A').inspect
# => {"A"=>0, "C"=>2, "B"=>3, "D"=>6}
```

**3. Huffman Encoding**:
```ruby
class HuffmanNode
  attr_accessor :char, :freq, :left, :right

  def initialize(char, freq)
    @char = char
    @freq = freq
    @left = nil
    @right = nil
  end
end

def huffman_encoding(text)
  # Calculate frequencies
  freq = Hash.new(0)
  text.each_char { |char| freq[char] += 1 }

  # Build priority queue
  pq = PriorityQueue.new(:min)
  freq.each { |char, f| pq.insert(HuffmanNode.new(char, f), f) }

  # Build Huffman tree
  while pq.size > 1
    left = pq.extract
    right = pq.extract

    merged = HuffmanNode.new(nil, left.freq + right.freq)
    merged.left = left
    merged.right = right

    pq.insert(merged, merged.freq)
  end

  root = pq.extract

  # Generate codes
  codes = {}
  generate_codes(root, "", codes)
  codes
end

def generate_codes(node, code, codes)
  return if node.nil?

  if node.char
    codes[node.char] = code
    return
  end

  generate_codes(node.left, code + "0", codes)
  generate_codes(node.right, code + "1", codes)
end

# Example
text = "hello world"
codes = huffman_encoding(text)
puts codes.inspect
```

---

### 13. Advanced Trees

#### Trie (Prefix Tree)

**What is a Trie?**

A Trie (pronounced "try") is a **tree-based data structure** for storing strings where:
- Each **path from root to node** represents a **prefix**
- Each **path to a terminal node** represents a **complete word**

**Why Trie?**

Tries excel at:
- ✅ **Prefix matching**: Find all words with prefix "pre" in $O(m)$ where $m$ = prefix length
- ✅ **Autocomplete**: Fast word suggestions
- ✅ **Spell checking**: Dictionary lookups
- ✅ **IP routing**: Longest prefix matching

---

**Structure & Properties**:

**Visual Example** (words: "cat", "dog", "top"):
```
                root
               / | \
              c  d  t
             /   |   \
            a    o    o
           /     |     \
         [t]   [g]    [p]    [ ] = end of word marker

Words stored: "cat", "dog", "top"
```

**Key Properties**:
- **Root**: Empty, represents empty string
- **Edges**: Labeled with characters
- **Nodes**: May mark end of word
- **Path**: Sequence of edges forms a string

**Time Complexity**:

| Operation | Time | Explanation |
|:----------|:-----|:------------|
| **Insert** | $O(m)$ | $m$ = length of word |
| **Search** | $O(m)$ | $m$ = length of word |
| **Delete** | $O(m)$ | $m$ = length of word |
| **Prefix Search** | $O(m + k)$ | $m$ = prefix length, $k$ = results |

**Space**: $O(N \times M)$ where $N$ = number of words, $M$ = average word length

**Comparison with Hash Table**:

| Aspect | Trie | Hash Table |
|:-------|:-----|:-----------|
| **Search** | $O(m)$ | $O(1)$ average |
| **Prefix Search** | $O(m)$ | $O(N)$ (scan all) |
| **Space** | Higher (pointers) | Lower |
| **Collisions** | No | Yes |
| **Sorted Order** | Yes (DFS) | No |

**Ruby Implementation**:
```ruby
class TrieNode
  attr_accessor :children, :is_end_of_word

  def initialize
    @children = {}
    @is_end_of_word = false
  end
end

class Trie
  def initialize
    @root = TrieNode.new
  end

  # Insert - O(m) where m = word length
  def insert(word)
    node = @root

    word.each_char do |char|
      node.children[char] ||= TrieNode.new
      node = node.children[char]
    end

    node.is_end_of_word = true
  end

  # Search - O(m)
  def search(word)
    node = find_node(word)
    node && node.is_end_of_word
  end

  # Starts with - O(m)
  def starts_with?(prefix)
    !find_node(prefix).nil?
  end

  def find_node(word)
    node = @root

    word.each_char do |char|
      return nil unless node.children[char]
      node = node.children[char]
    end

    node
  end

  # Delete word
  def delete(word)
    delete_helper(@root, word, 0)
  end

  def delete_helper(node, word, index)
    return false if node.nil?

    if index == word.length
      return false unless node.is_end_of_word

      node.is_end_of_word = false
      return node.children.empty?
    end

    char = word[index]
    child = node.children[char]

    should_delete = delete_helper(child, word, index + 1)

    if should_delete
      node.children.delete(char)
      return node.children.empty? && !node.is_end_of_word
    end

    false
  end

  # Get all words with prefix
  def words_with_prefix(prefix)
    node = find_node(prefix)
    return [] if node.nil?

    words = []
    collect_words(node, prefix, words)
    words
  end

  def collect_words(node, prefix, words)
    words << prefix if node.is_end_of_word

    node.children.each do |char, child|
      collect_words(child, prefix + char, words)
    end
  end

  # Autocomplete
  def autocomplete(prefix)
    words_with_prefix(prefix)
  end
end

# Example
trie = Trie.new
["cat", "car", "card", "care", "dog", "dodge"].each { |word| trie.insert(word) }

puts trie.search("car")           # => true
puts trie.search("can")           # => false
puts trie.starts_with?("ca")      # => true
puts trie.autocomplete("car").inspect  # => ["car", "card", "care"]

trie.delete("car")
puts trie.search("car")           # => false
puts trie.search("card")          # => true
```

**Trie Applications**:
- Autocomplete
- Spell checker
- IP routing (longest prefix matching)
- Dictionary implementation

---

#### Segment Tree

**Definition**: Tree for range queries and updates.

**Use Cases**:
- Range sum queries
- Range minimum/maximum queries
- Range updates

**Structure for array [1, 3, 5, 7, 9, 11]**:
```
              36 (sum of all)
            /    \
          9        27
        /  \      /  \
       4    5   16    11
      / \       / \
     1   3     7   9
```

**Ruby Implementation**:
```ruby
class SegmentTree
  def initialize(arr)
    @n = arr.length
    @tree = Array.new(4 * @n, 0)
    build(arr, 0, 0, @n - 1)
  end

  def build(arr, node, start, finish)
    if start == finish
      @tree[node] = arr[start]
      return
    end

    mid = (start + finish) / 2
    left_child = 2 * node + 1
    right_child = 2 * node + 2

    build(arr, left_child, start, mid)
    build(arr, right_child, mid + 1, finish)

    @tree[node] = @tree[left_child] + @tree[right_child]
  end

  # Range sum query - O(log n)
  def query(left, right)
    query_helper(0, 0, @n - 1, left, right)
  end

  def query_helper(node, start, finish, left, right)
    # No overlap
    return 0 if right < start || left > finish

    # Complete overlap
    return @tree[node] if left <= start && right >= finish

    # Partial overlap
    mid = (start + finish) / 2
    left_sum = query_helper(2 * node + 1, start, mid, left, right)
    right_sum = query_helper(2 * node + 2, mid + 1, finish, left, right)

    left_sum + right_sum
  end

  # Update value - O(log n)
  def update(index, value)
    update_helper(0, 0, @n - 1, index, value)
  end

  def update_helper(node, start, finish, index, value)
    if start == finish
      @tree[node] = value
      return
    end

    mid = (start + finish) / 2

    if index <= mid
      update_helper(2 * node + 1, start, mid, index, value)
    else
      update_helper(2 * node + 2, mid + 1, finish, index, value)
    end

    @tree[node] = @tree[2 * node + 1] + @tree[2 * node + 2]
  end
end

# Example
arr = [1, 3, 5, 7, 9, 11]
seg_tree = SegmentTree.new(arr)

puts seg_tree.query(1, 3)  # => 15 (3 + 5 + 7)
seg_tree.update(1, 10)
puts seg_tree.query(1, 3)  # => 22 (10 + 5 + 7)
```

---

#### Fenwick Tree (Binary Indexed Tree)

**Definition**: Tree for efficient prefix sum queries and updates.

**Advantages over Segment Tree**:
- Less memory (n vs 4n)
- Simpler implementation
- Faster in practice

**Ruby Implementation**:
```ruby
class FenwickTree
  def initialize(n)
    @n = n
    @tree = Array.new(n + 1, 0)
  end

  # Update - O(log n)
  def update(index, delta)
    index += 1  # 1-indexed

    while index <= @n
      @tree[index] += delta
      index += index & -index  # Add last set bit
    end
  end

  # Prefix sum [0, index] - O(log n)
  def prefix_sum(index)
    index += 1  # 1-indexed
    sum = 0

    while index > 0
      sum += @tree[index]
      index -= index & -index  # Remove last set bit
    end

    sum
  end

  # Range sum [left, right] - O(log n)
  def range_sum(left, right)
    prefix_sum(right) - (left > 0 ? prefix_sum(left - 1) : 0)
  end
end

# Example
ft = FenwickTree.new(6)
[1, 3, 5, 7, 9, 11].each_with_index { |val, i| ft.update(i, val) }

puts ft.prefix_sum(2)      # => 9 (1 + 3 + 5)
puts ft.range_sum(1, 3)    # => 15 (3 + 5 + 7)

ft.update(1, 7)  # Change 3 to 10 (delta = 7)
puts ft.range_sum(1, 3)    # => 22 (10 + 5 + 7)
```

**Comparison**:

| Feature | Segment Tree | Fenwick Tree |
|:--------|:-------------|:-------------|
| Space | O(4n) | O(n) |
| Build | O(n) | O(n log n) |
| Query | O(log n) | O(log n) |
| Update | O(log n) | O(log n) |
| Range update | Yes | Complex |
| Implementation | Complex | Simple |

---

## Part III — Graph Theory

**What is a Graph?**

A graph is a **non-linear data structure** consisting of **vertices** (nodes) connected by **edges**. Graphs model relationships and networks.

**Why Graphs?**

Graphs are essential for:
- ✅ **Social networks**: Friends, followers, connections
- ✅ **Maps & Navigation**: Cities, roads, shortest paths
- ✅ **Web**: Pages, links, PageRank
- ✅ **Dependencies**: Tasks, prerequisites, build systems
- ✅ **Networks**: Computers, routers, communication

---

### 14. Graph Fundamentals

#### Graph Terminology

**Formal Definition**:

A graph $G$ is defined as:

$$G = (V, E)$$

where:
- $V$ = set of **vertices** (nodes)
- $E$ = set of **edges** (connections between vertices)

**Example**: $V = \{A, B, C, D\}$, $E = \{(A,B), (B,C), (C,D), (D,A)\}$

---

**Graph Types**:

**1. Directed vs Undirected**:

| Type | Definition | Edge Representation | Example |
|:-----|:-----------|:-------------------|:--------|
| **Undirected** | Edges have no direction | $(u, v) = (v, u)$ | Facebook friends |
| **Directed** | Edges have direction | $(u, v) \neq (v, u)$ | Twitter followers |

```
Undirected:        Directed (Digraph):
  A --- B            A --> B
  |     |            |     ^
  C --- D            v     |
                     C --> D
```

**2. Weighted vs Unweighted**:

| Type | Definition | Use Case |
|:-----|:-----------|:---------|
| **Unweighted** | All edges equal weight (1) | Social connections |
| **Weighted** | Edges have weights/costs | Road distances, costs |

```
Unweighted:        Weighted:
  A --- B            A -5- B
  |     |            |     |
  C --- D            3     2
                     |     |
                     C -4- D
```

**3. Cyclic vs Acyclic**:

| Type | Definition | Example |
|:-----|:-----------|:--------|
| **Cyclic** | Contains at least one cycle | Road networks |
| **Acyclic** | No cycles | DAG (Directed Acyclic Graph) - task dependencies |

```
Cyclic:            Acyclic (DAG):
  A --> B            A --> B
  ^     |                  |
  |     v                  v
  D <-- C            C --> D
```

---

**Graph Properties & Terminology**:

**Degree**:
- **Undirected graph**: $\text{degree}(v)$ = number of edges connected to $v$
- **Directed graph**:
  - $\text{in-degree}(v)$ = number of incoming edges
  - $\text{out-degree}(v)$ = number of outgoing edges

**Path**: Sequence of vertices $v_1, v_2, \ldots, v_k$ where $(v_i, v_{i+1}) \in E$

**Cycle**: Path where $v_1 = v_k$ (starts and ends at same vertex)

**Connected** (undirected): Path exists between **any two vertices**

**Strongly Connected** (directed): Path exists between any two vertices **in both directions**

**Complete Graph**: Edge between **every pair** of vertices
- For $n$ vertices: $|E| = \frac{n(n-1)}{2}$ (undirected), $|E| = n(n-1)$ (directed)

**Sparse vs Dense**:
- **Sparse**: $|E| \approx |V|$ (few edges)
- **Dense**: $|E| \approx |V|^2$ (many edges)

---

#### Graph Representations

**How to Store a Graph?**

Two main approaches:
1. **Adjacency Matrix**: 2D array
2. **Adjacency List**: Array of lists

---

**1. Adjacency Matrix**

**What is it?**

A **2D array** of size $|V| \times |V|$ where:

$$\text{matrix}[i][j] = \begin{cases}
1 & \text{if edge } (i, j) \text{ exists} \\
0 & \text{otherwise}
\end{cases}$$

For weighted graphs: $\text{matrix}[i][j] = \text{weight of edge } (i, j)$

**Visual Example**:
```
Graph:          Adjacency Matrix:
  0 --- 1           0  1  2  3
  |     |       0 [ 0  1  1  0 ]
  2 --- 3       1 [ 1  0  1  0 ]
                2 [ 1  1  0  1 ]
                3 [ 0  0  1  0 ]
```

**Time Complexity**:

| Operation | Time |
|:----------|:-----|
| Add edge | $O(1)$ |
| Remove edge | $O(1)$ |
| Check if edge exists | $O(1)$ |
| Get all neighbors | $O(V)$ |
| Space | $O(V^2)$ |

**Pros & Cons**:
- ✅ **Fast edge lookup**: $O(1)$
- ✅ **Simple implementation**
- ❌ **Space inefficient**: $O(V^2)$ even for sparse graphs
- ❌ **Slow neighbor iteration**: $O(V)$
```ruby
class GraphMatrix
  def initialize(vertices)
    @v = vertices
    @matrix = Array.new(vertices) { Array.new(vertices, 0) }
  end

  def add_edge(u, v, weight = 1)
    @matrix[u][v] = weight
  end

  def add_undirected_edge(u, v, weight = 1)
    @matrix[u][v] = weight
    @matrix[v][u] = weight
  end

  def has_edge?(u, v)
    @matrix[u][v] != 0
  end

  def get_weight(u, v)
    @matrix[u][v]
  end

  def neighbors(u)
    neighbors = []
    @v.times do |v|
      neighbors << v if @matrix[u][v] != 0
    end
    neighbors
  end

  def display
    @matrix.each { |row| puts row.inspect }
  end
end

# Example
g = GraphMatrix.new(4)
g.add_undirected_edge(0, 1)
g.add_undirected_edge(0, 2)
g.add_undirected_edge(1, 2)
g.add_undirected_edge(2, 3)
g.display
# [0, 1, 1, 0]
# [1, 0, 1, 0]
# [1, 1, 0, 1]
# [0, 0, 1, 0]
```

---

**2. Adjacency List**

**What is it?**

An **array of lists** where:
- Index $i$ stores a list of all vertices adjacent to vertex $i$
- For weighted graphs: store $(neighbor, weight)$ pairs

**Visual Example**:
```
Graph:          Adjacency List:
  0 --- 1       0: [1, 2]
  |     |       1: [0, 2]
  2 --- 3       2: [0, 1, 3]
                3: [2]
```

**Time Complexity**:

| Operation | Time |
|:----------|:-----|
| Add edge | $O(1)$ |
| Remove edge | $O(V)$ (must search list) |
| Check if edge exists | $O(V)$ (worst case) |
| Get all neighbors | $O(\text{degree}(v))$ |
| Space | $O(V + E)$ |

**Pros & Cons**:
- ✅ **Space efficient**: $O(V + E)$ - great for sparse graphs
- ✅ **Fast neighbor iteration**: $O(\text{degree})$
- ❌ **Slower edge lookup**: $O(V)$ worst case
- ✅ **Most commonly used** in practice!

```ruby
class GraphList
  def initialize(vertices)
    @v = vertices
    @adj = Array.new(vertices) { [] }
  end

  def add_edge(u, v, weight = 1)
    @adj[u] << [v, weight]
  end

  def add_undirected_edge(u, v, weight = 1)
    @adj[u] << [v, weight]
    @adj[v] << [u, weight]
  end

  def neighbors(u)
    @adj[u]
  end

  def display
    @v.times do |i|
      print "#{i}: "
      @adj[i].each { |v, w| print "(#{v}, #{w}) " }
      puts
    end
  end
end

# Example
g = GraphList.new(4)
g.add_undirected_edge(0, 1, 5)
g.add_undirected_edge(0, 2, 3)
g.add_undirected_edge(1, 2, 2)
g.add_undirected_edge(2, 3, 4)
g.display
# 0: (1, 5) (2, 3)
# 1: (0, 5) (2, 2)
# 2: (0, 3) (1, 2) (3, 4)
# 3: (2, 4)
```

**3. Edge List**:
```ruby
class GraphEdgeList
  def initialize
    @edges = []
  end

  def add_edge(u, v, weight = 1)
    @edges << [u, v, weight]
  end

  def edges
    @edges
  end

  def display
    @edges.each { |u, v, w| puts "#{u} -> #{v} (#{w})" }
  end
end
```

---

**Representation Comparison**:

| Aspect | Adjacency Matrix | Adjacency List | Edge List |
|:-------|:-----------------|:---------------|:----------|
| **Space** | $O(V^2)$ | $O(V + E)$ | $O(E)$ |
| **Add edge** | $O(1)$ | $O(1)$ | $O(1)$ |
| **Remove edge** | $O(1)$ | $O(V)$ | $O(E)$ |
| **Check edge** | $O(1)$ | $O(V)$ | $O(E)$ |
| **Get neighbors** | $O(V)$ | $O(\text{degree})$ | $O(E)$ |
| **Iterate all edges** | $O(V^2)$ | $O(V + E)$ | $O(E)$ |

**When to Use Each**:

| Representation | Best For | Example Use Case |
|:---------------|:---------|:-----------------|
| **Adjacency Matrix** | Dense graphs ($E \approx V^2$), Fast edge lookup | Complete graphs, small graphs |
| **Adjacency List** | Sparse graphs ($E \ll V^2$), Neighbor iteration | Social networks, web graphs, **most common!** |
| **Edge List** | Simple edge iteration, Sorting edges | Kruskal's MST, edge-centric algorithms |

**Key Decision**:
- If $E \approx V^2$ (dense): Use **Matrix**
- If $E \ll V^2$ (sparse): Use **List** ✅ (most real-world graphs)

---

### 15. Graph Traversal

#### Breadth-First Search (BFS)

**What is BFS?**

BFS is a **graph traversal algorithm** that explores vertices **level by level**, visiting all neighbors before moving to the next level.

**Key Characteristics**:
- Uses a **Queue** (FIFO)
- Explores **nearest vertices first**
- Finds **shortest path** in unweighted graphs

**Algorithm**:
1. Start at source vertex, mark as visited
2. Add to queue
3. While queue not empty:
   - Dequeue vertex
   - Visit all unvisited neighbors
   - Mark neighbors as visited, enqueue them

---

**Visualization**:
```
         0              Level 0: [0]
       / | \            Level 1: [1, 2, 3]
      1  2  3           Level 2: [4, 5, 6]
     /      / \
    4      5   6

BFS order: 0, 1, 2, 3, 4, 5, 6
```

**Time Complexity**: $O(V + E)$ where $V$ = vertices, $E$ = edges
**Space Complexity**: $O(V)$ for queue and visited set

**Why $O(V + E)$?**
- Visit each vertex once: $O(V)$
- Explore each edge once: $O(E)$
- **Total**: $O(V + E)$

**Ruby Implementation**:
```ruby
def bfs(graph, start)
  visited = Set.new
  queue = [start]
  visited.add(start)
  result = []

  while !queue.empty?
    vertex = queue.shift
    result << vertex

    graph.neighbors(vertex).each do |neighbor, _|
      unless visited.include?(neighbor)
        visited.add(neighbor)
        queue.push(neighbor)
      end
    end
  end

  result
end

# Example
g = GraphList.new(7)
g.add_undirected_edge(0, 1)
g.add_undirected_edge(0, 2)
g.add_undirected_edge(0, 3)
g.add_undirected_edge(1, 4)
g.add_undirected_edge(3, 5)
g.add_undirected_edge(3, 6)

puts bfs(g, 0).inspect  # => [0, 1, 2, 3, 4, 5, 6]
```

**BFS with Levels**:
```ruby
def bfs_levels(graph, start)
  visited = Set.new([start])
  queue = [[start, 0]]  # [vertex, level]
  levels = Hash.new { |h, k| h[k] = [] }

  while !queue.empty?
    vertex, level = queue.shift
    levels[level] << vertex

    graph.neighbors(vertex).each do |neighbor, _|
      unless visited.include?(neighbor)
        visited.add(neighbor)
        queue.push([neighbor, level + 1])
      end
    end
  end

  levels
end

# Example
puts bfs_levels(g, 0).inspect
# => {0=>[0], 1=>[1, 2, 3], 2=>[4, 5, 6]}
```

**Shortest Path (Unweighted)**:
```ruby
def shortest_path_bfs(graph, start, target)
  visited = Set.new([start])
  queue = [[start, [start]]]  # [vertex, path]

  while !queue.empty?
    vertex, path = queue.shift

    return path if vertex == target

    graph.neighbors(vertex).each do |neighbor, _|
      unless visited.include?(neighbor)
        visited.add(neighbor)
        queue.push([neighbor, path + [neighbor]])
      end
    end
  end

  nil
end

# Example
path = shortest_path_bfs(g, 0, 6)
puts path.inspect  # => [0, 3, 6]
```

**Time Complexity**: O(V + E)
**Space Complexity**: O(V)

---

#### Depth-First Search (DFS)

**What is DFS?**

DFS is a **graph traversal algorithm** that explores as **deep as possible** along each branch before backtracking.

**Key Characteristics**:
- Uses a **Stack** (LIFO) or **Recursion**
- Explores **one path completely** before trying others
- Good for **detecting cycles**, **topological sort**, **pathfinding**

**Algorithm**:
1. Start at source vertex, mark as visited
2. For each unvisited neighbor:
   - Recursively visit that neighbor (go deep!)
3. Backtrack when no unvisited neighbors

---

**Visualization**:
```
         0              Visit order: 0 → 1 → 4 (backtrack)
       / | \                         → 2 (backtrack)
      1  2  3                        → 3 → 5 → 6
     /      / \
    4      5   6

DFS order: 0, 1, 4, 2, 3, 5, 6
```

**Time Complexity**: $O(V + E)$
**Space Complexity**: $O(V)$ for recursion stack/visited set

**DFS vs BFS**:

| Aspect | DFS | BFS |
|:-------|:----|:----|
| **Data Structure** | Stack (recursion) | Queue |
| **Exploration** | Deep first | Level by level |
| **Shortest Path** | ❌ No | ✅ Yes (unweighted) |
| **Space** | $O(h)$ height | $O(w)$ width |
| **Use Cases** | Cycle detection, topological sort | Shortest path, level-order |

**Recursive Implementation**:
```ruby
def dfs_recursive(graph, start, visited = Set.new, result = [])
  visited.add(start)
  result << start

  graph.neighbors(start).each do |neighbor, _|
    dfs_recursive(graph, neighbor, visited, result) unless visited.include?(neighbor)
  end

  result
end

# Example
puts dfs_recursive(g, 0).inspect  # => [0, 1, 4, 2, 3, 5, 6]
```

**Iterative Implementation**:
```ruby
def dfs_iterative(graph, start)
  visited = Set.new
  stack = [start]
  result = []

  while !stack.empty?
    vertex = stack.pop

    unless visited.include?(vertex)
      visited.add(vertex)
      result << vertex

      graph.neighbors(vertex).reverse_each do |neighbor, _|
        stack.push(neighbor) unless visited.include?(neighbor)
      end
    end
  end

  result
end

# Example
puts dfs_iterative(g, 0).inspect  # => [0, 1, 4, 2, 3, 5, 6]
```

**DFS with Path**:
```ruby
def dfs_all_paths(graph, start, target, path = [], all_paths = [])
  path = path + [start]

  if start == target
    all_paths << path
    return all_paths
  end

  graph.neighbors(start).each do |neighbor, _|
    unless path.include?(neighbor)
      dfs_all_paths(graph, neighbor, target, path, all_paths)
    end
  end

  all_paths
end

# Example
paths = dfs_all_paths(g, 0, 6)
puts paths.inspect  # => [[0, 3, 6]]
```

**Time Complexity**: O(V + E)
**Space Complexity**: O(V)

---

#### Connected Components

**For Undirected Graph**:
```ruby
def count_connected_components(graph, vertices)
  visited = Set.new
  count = 0

  vertices.times do |v|
    unless visited.include?(v)
      dfs_component(graph, v, visited)
      count += 1
    end
  end

  count
end

def dfs_component(graph, vertex, visited)
  visited.add(vertex)

  graph.neighbors(vertex).each do |neighbor, _|
    dfs_component(graph, neighbor, visited) unless visited.include?(neighbor)
  end
end

# Example
g = GraphList.new(5)
g.add_undirected_edge(0, 1)
g.add_undirected_edge(1, 2)
g.add_undirected_edge(3, 4)

puts count_connected_components(g, 5)  # => 2
```

**Get All Components**:
```ruby
def get_connected_components(graph, vertices)
  visited = Set.new
  components = []

  vertices.times do |v|
    unless visited.include?(v)
      component = []
      dfs_collect(graph, v, visited, component)
      components << component
    end
  end

  components
end

def dfs_collect(graph, vertex, visited, component)
  visited.add(vertex)
  component << vertex

  graph.neighbors(vertex).each do |neighbor, _|
    dfs_collect(graph, neighbor, visited, component) unless visited.include?(neighbor)
  end
end

# Example
components = get_connected_components(g, 5)
puts components.inspect  # => [[0, 1, 2], [3, 4]]
```

---

#### Cycle Detection

**Undirected Graph**:
```ruby
def has_cycle_undirected?(graph, vertices)
  visited = Set.new

  vertices.times do |v|
    unless visited.include?(v)
      return true if dfs_cycle_undirected(graph, v, visited, -1)
    end
  end

  false
end

def dfs_cycle_undirected(graph, vertex, visited, parent)
  visited.add(vertex)

  graph.neighbors(vertex).each do |neighbor, _|
    if !visited.include?(neighbor)
      return true if dfs_cycle_undirected(graph, neighbor, visited, vertex)
    elsif neighbor != parent
      return true
    end
  end

  false
end

# Example - Graph with cycle
g = GraphList.new(4)
g.add_undirected_edge(0, 1)
g.add_undirected_edge(1, 2)
g.add_undirected_edge(2, 0)
g.add_undirected_edge(2, 3)

puts has_cycle_undirected?(g, 4)  # => true
```

**Directed Graph** (using DFS):
```ruby
def has_cycle_directed?(graph, vertices)
  visited = Set.new
  rec_stack = Set.new

  vertices.times do |v|
    unless visited.include?(v)
      return true if dfs_cycle_directed(graph, v, visited, rec_stack)
    end
  end

  false
end

def dfs_cycle_directed(graph, vertex, visited, rec_stack)
  visited.add(vertex)
  rec_stack.add(vertex)

  graph.neighbors(vertex).each do |neighbor, _|
    if !visited.include?(neighbor)
      return true if dfs_cycle_directed(graph, neighbor, visited, rec_stack)
    elsif rec_stack.include?(neighbor)
      return true
    end
  end

  rec_stack.delete(vertex)
  false
end

# Example - Directed graph with cycle
g = GraphList.new(4)
g.add_edge(0, 1)
g.add_edge(1, 2)
g.add_edge(2, 0)
g.add_edge(2, 3)

puts has_cycle_directed?(g, 4)  # => true
```

---

#### Bipartite Graph

**Definition**: Graph whose vertices can be divided into two disjoint sets such that no two vertices within same set are adjacent.

**Check using BFS**:
```ruby
def is_bipartite?(graph, vertices)
  color = Array.new(vertices, -1)

  vertices.times do |v|
    if color[v] == -1
      return false unless bfs_bipartite(graph, v, color)
    end
  end

  true
end

def bfs_bipartite(graph, start, color)
  queue = [start]
  color[start] = 0

  while !queue.empty?
    vertex = queue.shift

    graph.neighbors(vertex).each do |neighbor, _|
      if color[neighbor] == -1
        color[neighbor] = 1 - color[vertex]
        queue.push(neighbor)
      elsif color[neighbor] == color[vertex]
        return false
      end
    end
  end

  true
end

# Example - Bipartite graph
g = GraphList.new(4)
g.add_undirected_edge(0, 1)
g.add_undirected_edge(1, 2)
g.add_undirected_edge(2, 3)

puts is_bipartite?(g, 4)  # => true

# Non-bipartite (triangle)
g2 = GraphList.new(3)
g2.add_undirected_edge(0, 1)
g2.add_undirected_edge(1, 2)
g2.add_undirected_edge(2, 0)

puts is_bipartite?(g2, 3)  # => false
```

---

### 16. Shortest Path Algorithms

**What is Shortest Path?**

Finding the **minimum cost path** between two vertices in a weighted graph.

**Types of Problems**:
1. **Single-Source**: Shortest paths from one vertex to all others (Dijkstra, Bellman-Ford)
2. **All-Pairs**: Shortest paths between all pairs of vertices (Floyd-Warshall)
3. **Single-Pair**: Shortest path between two specific vertices (A*)

---

#### Dijkstra's Algorithm

**What is Dijkstra's Algorithm?**

Dijkstra's algorithm finds the **shortest path from a source vertex to all other vertices** in a graph with **non-negative edge weights**.

**Key Idea**: **Greedy approach** - always expand the closest unvisited vertex.

**Requirements**:
- ✅ Works with **non-negative weights** only
- ❌ Fails with **negative weights**

**Algorithm Steps**:
1. Initialize all distances to $\infty$, source to $0$
2. Use **min-heap** (priority queue) to track vertices by distance
3. Extract vertex $u$ with minimum distance
4. **Relax** all neighbors of $u$:
   $$\text{if } dist[u] + weight(u, v) < dist[v] \text{ then } dist[v] = dist[u] + weight(u, v)$$
5. Repeat until all vertices processed

**Time Complexity**:
- With binary heap: $O((V + E) \log V)$
- With Fibonacci heap: $O(E + V \log V)$

**Space**: $O(V)$

**Ruby Implementation**:
```ruby
def dijkstra(graph, vertices, start)
  distances = Array.new(vertices, Float::INFINITY)
  distances[start] = 0

  visited = Set.new
  pq = [[0, start]]  # [distance, vertex]

  while !pq.empty?
    dist, u = pq.min_by { |d, v| d }
    pq.delete([dist, u])

    next if visited.include?(u)
    visited.add(u)

    graph.neighbors(u).each do |v, weight|
      new_dist = distances[u] + weight

      if new_dist < distances[v]
        distances[v] = new_dist
        pq << [new_dist, v]
      end
    end
  end

  distances
end

# Example
g = GraphList.new(5)
g.add_edge(0, 1, 4)
g.add_edge(0, 2, 1)
g.add_edge(2, 1, 2)
g.add_edge(1, 3, 1)
g.add_edge(2, 3, 5)
g.add_edge(3, 4, 3)

distances = dijkstra(g, 5, 0)
puts distances.inspect  # => [0, 3, 1, 4, 7]
```

**With Path Reconstruction**:
```ruby
def dijkstra_with_path(graph, vertices, start, target)
  distances = Array.new(vertices, Float::INFINITY)
  distances[start] = 0
  parent = Array.new(vertices, -1)

  visited = Set.new
  pq = [[0, start]]

  while !pq.empty?
    dist, u = pq.min_by { |d, v| d }
    pq.delete([dist, u])

    next if visited.include?(u)
    visited.add(u)

    break if u == target

    graph.neighbors(u).each do |v, weight|
      new_dist = distances[u] + weight

      if new_dist < distances[v]
        distances[v] = new_dist
        parent[v] = u
        pq << [new_dist, v]
      end
    end
  end

  # Reconstruct path
  path = []
  current = target

  while current != -1
    path.unshift(current)
    current = parent[current]
  end

  { distance: distances[target], path: path }
end

# Example
result = dijkstra_with_path(g, 5, 0, 4)
puts "Distance: #{result[:distance]}"  # => 7
puts "Path: #{result[:path].inspect}"  # => [0, 2, 1, 3, 4]
```

---

#### Bellman-Ford Algorithm

**What is Bellman-Ford?**

Bellman-Ford finds **shortest paths from a source** and can handle **negative edge weights**. It also **detects negative cycles**.

**Key Differences from Dijkstra**:
- ✅ Handles **negative weights**
- ✅ Detects **negative cycles**
- ❌ Slower: $O(VE)$ vs Dijkstra's $O((V+E) \log V)$

**Algorithm Steps**:
1. Initialize all distances to $\infty$, source to $0$
2. **Relax all edges** $V-1$ times:
   $$\text{for each edge } (u, v): \text{ if } dist[u] + weight(u,v) < dist[v] \text{ then } dist[v] = dist[u] + weight(u,v)$$
3. **Check for negative cycles**: If any edge can still be relaxed, negative cycle exists

**Why $V-1$ iterations?**

In a graph with $V$ vertices, the longest simple path has at most $V-1$ edges. After $V-1$ iterations, all shortest paths are found.

**Time Complexity**: $O(VE)$
**Space Complexity**: $O(V)$

**When to Use**:
- ✅ Graph has **negative weights**
- ✅ Need to **detect negative cycles**
- ❌ Use Dijkstra if all weights are non-negative (faster)

**Ruby Implementation**:
```ruby
def bellman_ford(edges, vertices, start)
  distances = Array.new(vertices, Float::INFINITY)
  distances[start] = 0

  # Relax edges V-1 times
  (vertices - 1).times do
    edges.each do |u, v, weight|
      if distances[u] != Float::INFINITY && distances[u] + weight < distances[v]
        distances[v] = distances[u] + weight
      end
    end
  end

  # Check for negative cycles
  edges.each do |u, v, weight|
    if distances[u] != Float::INFINITY && distances[u] + weight < distances[v]
      return { has_negative_cycle: true, distances: nil }
    end
  end

  { has_negative_cycle: false, distances: distances }
end

# Example
edges = [
  [0, 1, 4],
  [0, 2, 1],
  [2, 1, 2],
  [1, 3, 1],
  [2, 3, 5],
  [3, 4, 3]
]

result = bellman_ford(edges, 5, 0)
puts "Has negative cycle: #{result[:has_negative_cycle]}"  # => false
puts "Distances: #{result[:distances].inspect}"  # => [0, 3, 1, 4, 7]

# Example with negative cycle
edges_neg = [
  [0, 1, 1],
  [1, 2, -3],
  [2, 0, 1]
]

result_neg = bellman_ford(edges_neg, 3, 0)
puts "Has negative cycle: #{result_neg[:has_negative_cycle]}"  # => true
```

**Time Complexity**: O(VE)
**Space Complexity**: O(V)

---

#### Floyd-Warshall Algorithm

**Use Case**: All-pairs shortest paths

**Algorithm**: Dynamic programming approach

**Ruby Implementation**:
```ruby
def floyd_warshall(graph, vertices)
  # Initialize distance matrix
  dist = Array.new(vertices) { Array.new(vertices, Float::INFINITY) }

  # Distance from vertex to itself is 0
  vertices.times { |i| dist[i][i] = 0 }

  # Fill initial distances from graph
  vertices.times do |u|
    graph.neighbors(u).each do |v, weight|
      dist[u][v] = weight
    end
  end

  # Floyd-Warshall algorithm
  vertices.times do |k|
    vertices.times do |i|
      vertices.times do |j|
        if dist[i][k] + dist[k][j] < dist[i][j]
          dist[i][j] = dist[i][k] + dist[k][j]
        end
      end
    end
  end

  dist
end

# Example
g = GraphList.new(4)
g.add_edge(0, 1, 3)
g.add_edge(0, 3, 7)
g.add_edge(1, 0, 8)
g.add_edge(1, 2, 2)
g.add_edge(2, 0, 5)
g.add_edge(2, 3, 1)
g.add_edge(3, 0, 2)

dist = floyd_warshall(g, 4)
dist.each { |row| puts row.inspect }
# [0, 3, 5, 6]
# [5, 0, 2, 3]
# [3, 6, 0, 1]
# [2, 5, 7, 0]
```

**With Path Reconstruction**:
```ruby
def floyd_warshall_with_path(graph, vertices)
  dist = Array.new(vertices) { Array.new(vertices, Float::INFINITY) }
  next_vertex = Array.new(vertices) { Array.new(vertices, -1) }

  vertices.times { |i| dist[i][i] = 0 }

  vertices.times do |u|
    graph.neighbors(u).each do |v, weight|
      dist[u][v] = weight
      next_vertex[u][v] = v
    end
  end

  vertices.times do |k|
    vertices.times do |i|
      vertices.times do |j|
        if dist[i][k] + dist[k][j] < dist[i][j]
          dist[i][j] = dist[i][k] + dist[k][j]
          next_vertex[i][j] = next_vertex[i][k]
        end
      end
    end
  end

  { distances: dist, next_vertex: next_vertex }
end

def reconstruct_path(next_vertex, u, v)
  return [] if next_vertex[u][v] == -1

  path = [u]
  while u != v
    u = next_vertex[u][v]
    path << u
  end
  path
end

# Example
result = floyd_warshall_with_path(g, 4)
path = reconstruct_path(result[:next_vertex], 0, 3)
puts "Path from 0 to 3: #{path.inspect}"  # => [0, 1, 2, 3]
```

**Time Complexity**: O(V³)
**Space Complexity**: O(V²)

---

#### Shortest Path Algorithms Comparison

| Algorithm | Use Case | Time | Space | Negative Weights | All Pairs |
|:----------|:---------|:-----|:------|:-----------------|:----------|
| **Dijkstra** | Single-source, non-negative | O(E log V) | O(V) | No | No |
| **Bellman-Ford** | Single-source, negative weights | O(VE) | O(V) | Yes | No |
| **Floyd-Warshall** | All-pairs | O(V³) | O(V²) | Yes | Yes |
| **BFS** | Unweighted | O(V + E) | O(V) | N/A | No |

**When to Use**:
- **Dijkstra**: Fast, non-negative weights, single source
- **Bellman-Ford**: Negative weights, detect negative cycles
- **Floyd-Warshall**: All-pairs, small graphs (V ≤ 400)
- **BFS**: Unweighted graphs

---

### 17. Minimum Spanning Tree

#### Kruskal's Algorithm

**Use Case**: Find MST using edge-based approach

**Algorithm**:
1. Sort edges by weight
2. Use Union-Find to detect cycles
3. Add edge if doesn't create cycle

**Disjoint Set Union (DSU)**:
```ruby
class DSU
  def initialize(n)
    @parent = (0...n).to_a
    @rank = Array.new(n, 0)
  end

  def find(x)
    if @parent[x] != x
      @parent[x] = find(@parent[x])  # Path compression
    end
    @parent[x]
  end

  def union(x, y)
    root_x = find(x)
    root_y = find(y)

    return false if root_x == root_y

    # Union by rank
    if @rank[root_x] < @rank[root_y]
      @parent[root_x] = root_y
    elsif @rank[root_x] > @rank[root_y]
      @parent[root_y] = root_x
    else
      @parent[root_y] = root_x
      @rank[root_x] += 1
    end

    true
  end
end
```

**Kruskal's Implementation**:
```ruby
def kruskal(edges, vertices)
  # Sort edges by weight
  edges.sort_by! { |u, v, w| w }

  dsu = DSU.new(vertices)
  mst = []
  total_weight = 0

  edges.each do |u, v, weight|
    if dsu.union(u, v)
      mst << [u, v, weight]
      total_weight += weight
    end
  end

  { mst: mst, total_weight: total_weight }
end

# Example
edges = [
  [0, 1, 4],
  [0, 2, 1],
  [1, 2, 2],
  [1, 3, 5],
  [2, 3, 8],
  [2, 4, 10],
  [3, 4, 2]
]

result = kruskal(edges, 5)
puts "MST edges:"
result[:mst].each { |u, v, w| puts "#{u} - #{v}: #{w}" }
puts "Total weight: #{result[:total_weight]}"
# MST edges:
# 0 - 2: 1
# 1 - 2: 2
# 3 - 4: 2
# 0 - 1: 4
# Total weight: 9
```

**Time Complexity**: O(E log E) or O(E log V)
**Space Complexity**: O(V)

---

#### Prim's Algorithm

**Use Case**: Find MST using vertex-based approach

**Algorithm**:
1. Start from arbitrary vertex
2. Use priority queue for minimum edge
3. Add minimum edge connecting tree to non-tree vertex

**Ruby Implementation**:
```ruby
def prim(graph, vertices, start = 0)
  visited = Set.new
  mst = []
  total_weight = 0

  # Priority queue: [weight, from, to]
  pq = []

  # Add all edges from start vertex
  visited.add(start)
  graph.neighbors(start).each do |v, weight|
    pq << [weight, start, v]
  end

  while !pq.empty? && visited.size < vertices
    weight, u, v = pq.min_by { |w, _, _| w }
    pq.delete([weight, u, v])

    next if visited.include?(v)

    visited.add(v)
    mst << [u, v, weight]
    total_weight += weight

    # Add edges from newly added vertex
    graph.neighbors(v).each do |neighbor, w|
      unless visited.include?(neighbor)
        pq << [w, v, neighbor]
      end
    end
  end

  { mst: mst, total_weight: total_weight }
end

# Example
g = GraphList.new(5)
g.add_undirected_edge(0, 1, 4)
g.add_undirected_edge(0, 2, 1)
g.add_undirected_edge(1, 2, 2)
g.add_undirected_edge(1, 3, 5)
g.add_undirected_edge(2, 3, 8)
g.add_undirected_edge(2, 4, 10)
g.add_undirected_edge(3, 4, 2)

result = prim(g, 5)
puts "MST edges:"
result[:mst].each { |u, v, w| puts "#{u} - #{v}: #{w}" }
puts "Total weight: #{result[:total_weight]}"
# Total weight: 9
```

**Time Complexity**: O(E log V) with binary heap
**Space Complexity**: O(V)

---

#### MST Algorithms Comparison

| Feature | Kruskal | Prim |
|:--------|:--------|:-----|
| Approach | Edge-based | Vertex-based |
| Data Structure | DSU | Priority Queue |
| Time | O(E log E) | O(E log V) |
| Best for | Sparse graphs | Dense graphs |
| Implementation | Simpler | More complex |

---

### 18. Advanced Graph Topics

#### Topological Sorting

**Definition**: Linear ordering of vertices in DAG such that for every edge (u, v), u comes before v.

**Use Cases**:
- Task scheduling
- Build systems
- Course prerequisites

**DFS-based Implementation**:
```ruby
def topological_sort_dfs(graph, vertices)
  visited = Set.new
  stack = []

  vertices.times do |v|
    dfs_topo(graph, v, visited, stack) unless visited.include?(v)
  end

  stack.reverse
end

def dfs_topo(graph, vertex, visited, stack)
  visited.add(vertex)

  graph.neighbors(vertex).each do |neighbor, _|
    dfs_topo(graph, neighbor, visited, stack) unless visited.include?(neighbor)
  end

  stack.push(vertex)
end

# Example - Course prerequisites
g = GraphList.new(6)
g.add_edge(5, 2)  # Course 5 before 2
g.add_edge(5, 0)
g.add_edge(4, 0)
g.add_edge(4, 1)
g.add_edge(2, 3)
g.add_edge(3, 1)

order = topological_sort_dfs(g, 6)
puts order.inspect  # => [5, 4, 2, 3, 1, 0]
```

**Kahn's Algorithm** (BFS-based):
```ruby
def topological_sort_kahn(graph, vertices)
  in_degree = Array.new(vertices, 0)

  # Calculate in-degrees
  vertices.times do |u|
    graph.neighbors(u).each do |v, _|
      in_degree[v] += 1
    end
  end

  # Queue with vertices having in-degree 0
  queue = []
  vertices.times do |v|
    queue.push(v) if in_degree[v] == 0
  end

  result = []

  while !queue.empty?
    u = queue.shift
    result << u

    graph.neighbors(u).each do |v, _|
      in_degree[v] -= 1
      queue.push(v) if in_degree[v] == 0
    end
  end

  # Check if graph has cycle
  result.length == vertices ? result : nil
end

# Example
order = topological_sort_kahn(g, 6)
puts order.inspect  # => [4, 5, 0, 2, 3, 1]
```

**Course Schedule Problem**:
```ruby
def can_finish(num_courses, prerequisites)
  graph = Array.new(num_courses) { [] }
  in_degree = Array.new(num_courses, 0)

  prerequisites.each do |course, prereq|
    graph[prereq] << course
    in_degree[course] += 1
  end

  queue = []
  num_courses.times do |i|
    queue.push(i) if in_degree[i] == 0
  end

  count = 0

  while !queue.empty?
    course = queue.shift
    count += 1

    graph[course].each do |next_course|
      in_degree[next_course] -= 1
      queue.push(next_course) if in_degree[next_course] == 0
    end
  end

  count == num_courses
end

# Example
prerequisites = [[1, 0], [2, 0], [3, 1], [3, 2]]
puts can_finish(4, prerequisites)  # => true

# With cycle
prerequisites_cycle = [[1, 0], [0, 1]]
puts can_finish(2, prerequisites_cycle)  # => false
```

---

#### Strongly Connected Components (SCC)

**Definition**: Maximal set of vertices where every vertex is reachable from every other vertex.

**Kosaraju's Algorithm**:
```ruby
def kosaraju_scc(graph, vertices)
  # Step 1: Fill order of vertices by finish time
  visited = Set.new
  stack = []

  vertices.times do |v|
    dfs_fill_order(graph, v, visited, stack) unless visited.include?(v)
  end

  # Step 2: Create transpose graph
  transpose = Array.new(vertices) { [] }
  vertices.times do |u|
    graph.neighbors(u).each do |v, _|
      transpose[v] << [u, 1]
    end
  end

  # Step 3: DFS on transpose in order of stack
  visited.clear
  sccs = []

  while !stack.empty?
    v = stack.pop
    unless visited.include?(v)
      scc = []
      dfs_collect_scc(transpose, v, visited, scc)
      sccs << scc
    end
  end

  sccs
end

def dfs_fill_order(graph, vertex, visited, stack)
  visited.add(vertex)

  graph.neighbors(vertex).each do |neighbor, _|
    dfs_fill_order(graph, neighbor, visited, stack) unless visited.include?(neighbor)
  end

  stack.push(vertex)
end

def dfs_collect_scc(graph, vertex, visited, scc)
  visited.add(vertex)
  scc << vertex

  graph.each do |neighbor, _|
    dfs_collect_scc(graph, neighbor, visited, scc) unless visited.include?(neighbor)
  end
end

# Example
g = GraphList.new(5)
g.add_edge(0, 1)
g.add_edge(1, 2)
g.add_edge(2, 0)
g.add_edge(1, 3)
g.add_edge(3, 4)

sccs = kosaraju_scc(g, 5)
puts "Strongly Connected Components:"
sccs.each { |scc| puts scc.inspect }
# [0, 2, 1]
# [3]
# [4]
```

**Tarjan's Algorithm** (Single DFS):
```ruby
def tarjan_scc(graph, vertices)
  @index = 0
  @stack = []
  @on_stack = Set.new
  @indices = Array.new(vertices, -1)
  @low_link = Array.new(vertices, -1)
  @sccs = []

  vertices.times do |v|
    tarjan_dfs(graph, v) if @indices[v] == -1
  end

  @sccs
end

def tarjan_dfs(graph, v)
  @indices[v] = @index
  @low_link[v] = @index
  @index += 1
  @stack.push(v)
  @on_stack.add(v)

  graph.neighbors(v).each do |w, _|
    if @indices[w] == -1
      tarjan_dfs(graph, w)
      @low_link[v] = [@low_link[v], @low_link[w]].min
    elsif @on_stack.include?(w)
      @low_link[v] = [@low_link[v], @indices[w]].min
    end
  end

  if @low_link[v] == @indices[v]
    scc = []
    loop do
      w = @stack.pop
      @on_stack.delete(w)
      scc << w
      break if w == v
    end
    @sccs << scc
  end
end
```

---

#### Bridges and Articulation Points

**Bridge**: Edge whose removal increases number of connected components.

**Articulation Point**: Vertex whose removal increases number of connected components.

**Find Bridges**:
```ruby
def find_bridges(graph, vertices)
  @time = 0
  @visited = Set.new
  @disc = Array.new(vertices, -1)
  @low = Array.new(vertices, -1)
  @bridges = []

  vertices.times do |v|
    dfs_bridge(graph, v, -1) unless @visited.include?(v)
  end

  @bridges
end

def dfs_bridge(graph, u, parent)
  @visited.add(u)
  @disc[u] = @low[u] = @time
  @time += 1

  graph.neighbors(u).each do |v, _|
    if !@visited.include?(v)
      dfs_bridge(graph, v, u)
      @low[u] = [@low[u], @low[v]].min

      # Bridge condition
      @bridges << [u, v] if @low[v] > @disc[u]
    elsif v != parent
      @low[u] = [@low[u], @disc[v]].min
    end
  end
end

# Example
g = GraphList.new(5)
g.add_undirected_edge(0, 1)
g.add_undirected_edge(1, 2)
g.add_undirected_edge(2, 0)
g.add_undirected_edge(1, 3)
g.add_undirected_edge(3, 4)

bridges = find_bridges(g, 5)
puts "Bridges:"
bridges.each { |u, v| puts "#{u} - #{v}" }
# 1 - 3
# 3 - 4
```

**Find Articulation Points**:
```ruby
def find_articulation_points(graph, vertices)
  @time = 0
  @visited = Set.new
  @disc = Array.new(vertices, -1)
  @low = Array.new(vertices, -1)
  @parent = Array.new(vertices, -1)
  @ap = Set.new

  vertices.times do |v|
    dfs_ap(graph, v) unless @visited.include?(v)
  end

  @ap.to_a
end

def dfs_ap(graph, u)
  children = 0
  @visited.add(u)
  @disc[u] = @low[u] = @time
  @time += 1

  graph.neighbors(u).each do |v, _|
    if !@visited.include?(v)
      children += 1
      @parent[v] = u
      dfs_ap(graph, v)

      @low[u] = [@low[u], @low[v]].min

      # Articulation point conditions
      if @parent[u] == -1 && children > 1
        @ap.add(u)
      end

      if @parent[u] != -1 && @low[v] >= @disc[u]
        @ap.add(u)
      end
    elsif v != @parent[u]
      @low[u] = [@low[u], @disc[v]].min
    end
  end
end

# Example
aps = find_articulation_points(g, 5)
puts "Articulation Points: #{aps.inspect}"
# [1, 3]
```

---

#### Network Flow (Ford-Fulkerson)

**Use Case**: Maximum flow in flow network

**Algorithm**:
1. Find augmenting path using BFS/DFS
2. Update residual graph
3. Repeat until no augmenting path

**Ruby Implementation** (Edmonds-Karp - BFS variant):
```ruby
def max_flow(graph, vertices, source, sink)
  # Create residual graph
  residual = Array.new(vertices) { Array.new(vertices, 0) }

  vertices.times do |u|
    graph.neighbors(u).each do |v, capacity|
      residual[u][v] = capacity
    end
  end

  max_flow = 0

  # Find augmenting paths using BFS
  while true
    parent = bfs_flow(residual, vertices, source, sink)
    break if parent.nil?

    # Find minimum capacity along path
    path_flow = Float::INFINITY
    v = sink

    while v != source
      u = parent[v]
      path_flow = [path_flow, residual[u][v]].min
      v = u
    end

    # Update residual graph
    v = sink
    while v != source
      u = parent[v]
      residual[u][v] -= path_flow
      residual[v][u] += path_flow
      v = u
    end

    max_flow += path_flow
  end

  max_flow
end

def bfs_flow(residual, vertices, source, sink)
  visited = Set.new([source])
  queue = [source]
  parent = Array.new(vertices, -1)

  while !queue.empty?
    u = queue.shift

    vertices.times do |v|
      if !visited.include?(v) && residual[u][v] > 0
        visited.add(v)
        queue.push(v)
        parent[v] = u
        return parent if v == sink
      end
    end
  end

  nil
end

# Example
g = GraphList.new(6)
g.add_edge(0, 1, 16)
g.add_edge(0, 2, 13)
g.add_edge(1, 2, 10)
g.add_edge(1, 3, 12)
g.add_edge(2, 1, 4)
g.add_edge(2, 4, 14)
g.add_edge(3, 2, 9)
g.add_edge(3, 5, 20)
g.add_edge(4, 3, 7)
g.add_edge(4, 5, 4)

flow = max_flow(g, 6, 0, 5)
puts "Maximum flow: #{flow}"  # => 23
```

---

## Part IV — Algorithm Paradigms

**What are Algorithm Paradigms?**

Algorithm paradigms are **general approaches** or **strategies** for solving computational problems. They provide a framework for designing efficient algorithms.

**Major Paradigms**:
1. **Divide and Conquer**: Break into subproblems, solve, combine
2. **Dynamic Programming**: Solve overlapping subproblems once, reuse
3. **Greedy**: Make locally optimal choices
4. **Backtracking**: Try all possibilities, backtrack on failure

---

### 19. Divide and Conquer

**What is Divide and Conquer?**

A paradigm that **breaks a problem into smaller subproblems**, solves them **recursively**, and **combines** the solutions.

**Three Steps**:

1. **Divide**: Break problem into smaller subproblems of the same type
2. **Conquer**: Solve subproblems recursively (base case: solve directly)
3. **Combine**: Merge subproblem solutions into final solution

**General Recurrence**:

$$T(n) = aT\left(\frac{n}{b}\right) + f(n)$$

where:
- $a$ = number of subproblems
- $b$ = factor by which problem size is reduced
- $f(n)$ = cost of divide and combine steps

**Examples**:
- Binary Search: $T(n) = T(n/2) + O(1)$ → $O(\log n)$
- Merge Sort: $T(n) = 2T(n/2) + O(n)$ → $O(n \log n)$
- Quick Sort: $T(n) = 2T(n/2) + O(n)$ → $O(n \log n)$ average

---

#### Binary Search

**What is Binary Search?**

Binary Search is a **divide and conquer** algorithm that finds an element in a **sorted array** by repeatedly dividing the search interval in half.

**Key Requirement**: Array must be **sorted**!

**Algorithm**:
1. Compare target with middle element
2. If equal: found!
3. If target < middle: search left half
4. If target > middle: search right half
5. Repeat until found or interval empty

**Recurrence**: $T(n) = T(n/2) + O(1)$ → $O(\log n)$

**Why $O(\log n)$?**

Each step reduces problem size by half:
$$n \to \frac{n}{2} \to \frac{n}{4} \to \cdots \to 1$$

Number of steps: $\log_2 n$

**Time**: $O(\log n)$, **Space**: $O(1)$ iterative, $O(\log n)$ recursive (call stack)

```ruby
def binary_search(arr, target)
  left = 0
  right = arr.length - 1

  while left <= right
    mid = left + (right - left) / 2  # Avoid overflow

    return mid if arr[mid] == target

    if arr[mid] < target
      left = mid + 1
    else
      right = mid - 1
    end
  end

  -1  # Not found
end

# Recursive version
def binary_search_recursive(arr, target, left = 0, right = arr.length - 1)
  return -1 if left > right

  mid = left + (right - left) / 2

  return mid if arr[mid] == target

  if arr[mid] < target
    binary_search_recursive(arr, target, mid + 1, right)
  else
    binary_search_recursive(arr, target, left, mid - 1)
  end
end

# Example
arr = [1, 3, 5, 7, 9, 11, 13, 15]
puts binary_search(arr, 7)  # => 3
puts binary_search(arr, 6)  # => -1
```

---

#### Merge Sort

**What is Merge Sort?**

Merge Sort is a **divide and conquer** sorting algorithm that divides the array into halves, sorts them recursively, and merges the sorted halves.

**Algorithm Steps**:
1. **Divide**: Split array into two halves
2. **Conquer**: Recursively sort both halves
3. **Combine**: Merge two sorted halves into one sorted array

**Recurrence**: $T(n) = 2T(n/2) + O(n)$ → $O(n \log n)$

**Why $O(n \log n)$?**

- **Levels**: $\log_2 n$ (each level divides by 2)
- **Work per level**: $O(n)$ (merging all elements)
- **Total**: $O(n) \times O(\log n) = O(n \log n)$

**Visual**:
```
[38, 27, 43, 3]
    /        \
[38, 27]   [43, 3]     Divide
  /  \       /  \
[38] [27] [43] [3]     Base case
  \  /       \  /
[27, 38]   [3, 43]     Merge
    \        /
[3, 27, 38, 43]        Final merge
```

**Time Complexity**:
- **Best**: $O(n \log n)$
- **Average**: $O(n \log n)$
- **Worst**: $O(n \log n)$ ✅ **Guaranteed!**

**Space**: $O(n)$ (temporary arrays for merging)

**Pros & Cons**:
- ✅ **Stable**: Preserves relative order of equal elements
- ✅ **Predictable**: Always $O(n \log n)$
- ❌ **Space**: Requires $O(n)$ extra space
- ✅ **Good for linked lists**: No random access needed

```ruby
def merge_sort(arr)
  return arr if arr.length <= 1

  mid = arr.length / 2
  left = merge_sort(arr[0...mid])
  right = merge_sort(arr[mid..-1])

  merge(left, right)
end

def merge(left, right)
  result = []
  i = j = 0

  while i < left.length && j < right.length
    if left[i] <= right[j]
      result << left[i]
      i += 1
    else
      result << right[j]
      j += 1
    end
  end

  result.concat(left[i..-1]) if i < left.length
  result.concat(right[j..-1]) if j < right.length

  result
end

# Example
arr = [38, 27, 43, 3, 9, 82, 10]
puts merge_sort(arr).inspect  # => [3, 9, 10, 27, 38, 43, 82]
```

---

#### Quick Sort

**What is Quick Sort?**

Quick Sort is a **divide and conquer** sorting algorithm that selects a **pivot** element and partitions the array around it.

**Algorithm Steps**:
1. **Choose pivot**: Select an element (last, first, random, or median)
2. **Partition**: Rearrange so elements < pivot are left, elements > pivot are right
3. **Recursively sort**: Apply quick sort to left and right partitions

**Recurrence**: $T(n) = 2T(n/2) + O(n)$ → $O(n \log n)$ average

**Visual**:
```
[10, 7, 8, 9, 1, 5]  pivot=5
     ↓
[1] 5 [10, 7, 8, 9]  Partition
     ↓
[1] 5 [7, 8, 9, 10]  Recursively sort
     ↓
[1, 5, 7, 8, 9, 10]  Final
```

**Time Complexity**:
- **Best**: $O(n \log n)$ (balanced partitions)
- **Average**: $O(n \log n)$
- **Worst**: $O(n^2)$ (already sorted, poor pivot choice)

**Space**: $O(\log n)$ (recursion stack)

**Pros & Cons**:
- ✅ **In-place**: $O(\log n)$ space (better than Merge Sort)
- ✅ **Fast in practice**: Good cache locality
- ✅ **Average case**: $O(n \log n)$
- ❌ **Unstable**: Doesn't preserve relative order
- ❌ **Worst case**: $O(n^2)$ (can be avoided with random pivot)

**Optimization**: Use **randomized pivot** or **median-of-three** to avoid worst case.

```ruby
def quick_sort(arr, low = 0, high = arr.length - 1)
  if low < high
    pi = partition(arr, low, high)
    quick_sort(arr, low, pi - 1)
    quick_sort(arr, pi + 1, high)
  end
  arr
end

def partition(arr, low, high)
  pivot = arr[high]
  i = low - 1

  (low...high).each do |j|
    if arr[j] <= pivot
      i += 1
      arr[i], arr[j] = arr[j], arr[i]
    end
  end

  arr[i + 1], arr[high] = arr[high], arr[i + 1]
  i + 1
end

# Example
arr = [10, 7, 8, 9, 1, 5]
puts quick_sort(arr).inspect  # => [1, 5, 7, 8, 9, 10]
```

---

#### Maximum Subarray (Divide & Conquer)

**What is Maximum Subarray?**

Find the **contiguous subarray** with the **largest sum**.

**Example**:
- `arr = [-2, 1, -3, 4, -1, 2, 1, -5, 4]`
- Maximum subarray: `[4, -1, 2, 1]` with sum = `6`

**Divide & Conquer Approach**:

The maximum subarray can be in:
1. **Left half** only
2. **Right half** only
3. **Crossing the middle** (part in left, part in right)

**Visual Example**:
```
Array: [-2, 1, -3, 4, -1, 2, 1, -5, 4]
                    ↓ mid
       [-2, 1, -3, 4] | [-1, 2, 1, -5, 4]
        Left Half     |    Right Half

Left max:  4
Right max: 2
Cross max: 6  (4, -1, 2, 1 crosses middle)
           ↑
        Answer!
```

**Recurrence**: $T(n) = 2T(n/2) + O(n)$ → $O(n \log n)$

**Note**: Kadane's algorithm is faster at $O(n)$, but this demonstrates divide & conquer!

**Time**: $O(n \log n)$, **Space**: $O(\log n)$ (recursion stack)

```ruby
def max_subarray_dc(arr, low = 0, high = arr.length - 1)
  return arr[low] if low == high

  mid = (low + high) / 2

  left_sum = max_subarray_dc(arr, low, mid)
  right_sum = max_subarray_dc(arr, mid + 1, high)
  cross_sum = max_crossing_sum(arr, low, mid, high)

  [left_sum, right_sum, cross_sum].max
end

def max_crossing_sum(arr, low, mid, high)
  left_sum = -Float::INFINITY
  sum = 0

  mid.downto(low) do |i|
    sum += arr[i]
    left_sum = sum if sum > left_sum
  end

  right_sum = -Float::INFINITY
  sum = 0

  (mid + 1).upto(high) do |i|
    sum += arr[i]
    right_sum = sum if sum > right_sum
  end

  left_sum + right_sum
end

# Example
arr = [-2, 1, -3, 4, -1, 2, 1, -5, 4]
puts max_subarray_dc(arr)  # => 6 ([4, -1, 2, 1])
```

---

#### Closest Pair of Points

**What is Closest Pair of Points?**

Given $n$ points in 2D plane, find the **two points with minimum distance**.

**Naive Approach**: Check all pairs → $O(n^2)$

**Divide & Conquer Approach**: $O(n \log n)$

**Algorithm**:
1. **Divide**: Split points by vertical line into left and right halves
2. **Conquer**: Recursively find closest pair in each half
3. **Combine**: Check if closest pair crosses the dividing line

**Key Insight**: Only need to check points within distance $d$ from dividing line, where $d$ = min(left_min, right_min).

**Recurrence**: $T(n) = 2T(n/2) + O(n)$ → $O(n \log n)$

**Time**: $O(n \log n)$, **Space**: $O(n)$

```ruby
def closest_pair(points)
  points_x = points.sort_by { |p| p[0] }
  points_y = points.sort_by { |p| p[1] }

  closest_pair_recursive(points_x, points_y)
end

def closest_pair_recursive(px, py)
  n = px.length

  # Base case: brute force for small n
  return brute_force_closest(px) if n <= 3

  mid = n / 2
  midpoint = px[mid]

  pyl = py.select { |p| p[0] <= midpoint[0] }
  pyr = py.select { |p| p[0] > midpoint[0] }

  dl = closest_pair_recursive(px[0...mid], pyl)
  dr = closest_pair_recursive(px[mid..-1], pyr)

  d = [dl, dr].min

  # Check points in strip
  strip = py.select { |p| (p[0] - midpoint[0]).abs < d }

  strip_closest = closest_in_strip(strip, d)

  [d, strip_closest].min
end

def brute_force_closest(points)
  min_dist = Float::INFINITY

  points.each_with_index do |p1, i|
    points.each_with_index do |p2, j|
      next if i >= j
      dist = distance(p1, p2)
      min_dist = dist if dist < min_dist
    end
  end

  min_dist
end

def closest_in_strip(strip, d)
  min_dist = d

  strip.each_with_index do |p1, i|
    strip.each_with_index do |p2, j|
      next if j <= i
      break if (p2[1] - p1[1]) >= min_dist

      dist = distance(p1, p2)
      min_dist = dist if dist < min_dist
    end
  end

  min_dist
end

def distance(p1, p2)
  Math.sqrt((p1[0] - p2[0])**2 + (p1[1] - p2[1])**2)
end

# Example
points = [[2, 3], [12, 30], [40, 50], [5, 1], [12, 10], [3, 4]]
puts closest_pair(points)
```

---

### 20. Greedy Algorithms

**What is a Greedy Algorithm?**

A greedy algorithm makes the **locally optimal choice** at each step, hoping to find a **global optimum**.

**Key Idea**: "Take what looks best right now!"

**When Does Greedy Work?**

Greedy algorithms work when the problem has two properties:

1. **Greedy Choice Property**: A **local optimum** leads to a **global optimum**
   - Making the best choice at each step gives the best overall solution

2. **Optimal Substructure**: Optimal solution contains **optimal solutions to subproblems**
   - Similar to DP, but no overlapping subproblems

**Greedy vs Dynamic Programming**:

| Aspect | Greedy | Dynamic Programming |
|:-------|:-------|:-------------------|
| **Approach** | Make best choice now | Consider all choices |
| **Subproblems** | No overlap | Overlapping |
| **Optimality** | Not always optimal | Always optimal (if correct) |
| **Speed** | Faster ($O(n \log n)$ typical) | Slower ($O(n^2)$ typical) |
| **Examples** | Activity selection, Huffman | Knapsack, LCS |

**Common Greedy Patterns**:
- Sort first, then make greedy choices
- Use priority queue for best choice
- Process in specific order (earliest deadline, shortest job, etc.)

**Warning**: Greedy doesn't always work! Must prove greedy choice property.

---

#### Activity Selection

**What is Activity Selection?**

Given $n$ activities with start and finish times, select the **maximum number of non-overlapping activities**.

**Example**:
```
Activities: [(1,4), (3,5), (0,6), (5,7), (8,11)]
Selected:   [(1,4), (5,7), (8,11)] = 3 activities
```

**Greedy Strategy**: Always pick the activity that **finishes earliest**!

**Why does this work?**
- Finishing early leaves more room for future activities
- This is the **greedy choice property**

**Algorithm**:
1. Sort activities by finish time
2. Select first activity
3. For each remaining activity:
   - If it starts after last selected activity finishes, select it

**Time**: $O(n \log n)$ (sorting), **Space**: $O(1)$

```ruby
def activity_selection(activities)
  # Sort by finish time
  activities.sort_by! { |start, finish| finish }

  selected = [activities[0]]
  last_finish = activities[0][1]

  activities.each do |start, finish|
    if start >= last_finish
      selected << [start, finish]
      last_finish = finish
    end
  end

  selected
end

# Example
activities = [[1, 4], [3, 5], [0, 6], [5, 7], [3, 9], [5, 9], [6, 10], [8, 11], [8, 12], [2, 14], [12, 16]]
result = activity_selection(activities)
puts "Selected activities: #{result.inspect}"
puts "Count: #{result.length}"
```

---

#### Fractional Knapsack

**What is Fractional Knapsack?**

Given items with weights and values, and a knapsack with capacity $W$, maximize total value. **Can take fractions** of items.

**Difference from 0/1 Knapsack**:
- **0/1 Knapsack**: Take whole item or nothing → **DP** required
- **Fractional Knapsack**: Can take fractions → **Greedy** works!

**Greedy Strategy**: Take items with **highest value-to-weight ratio** first!

**Algorithm**:
1. Calculate value/weight ratio for each item
2. Sort by ratio (descending)
3. Take items greedily until capacity full

**Time**: $O(n \log n)$ (sorting), **Space**: $O(1)$

```ruby
def fractional_knapsack(items, capacity)
  # Sort by value/weight ratio
  items.sort_by! { |value, weight| -value.to_f / weight }

  total_value = 0.0
  remaining = capacity

  items.each do |value, weight|
    if weight <= remaining
      total_value += value
      remaining -= weight
    else
      total_value += value * (remaining.to_f / weight)
      break
    end
  end

  total_value
end

# Example
items = [[60, 10], [100, 20], [120, 30]]  # [value, weight]
capacity = 50
puts fractional_knapsack(items, capacity)  # => 240.0
```

**Time**: O(n log n), **Space**: O(1)

---

#### Huffman Encoding

**What is Huffman Encoding?**

A **greedy algorithm** for **lossless data compression** that assigns **variable-length codes** to characters based on their frequency.

**Key Idea**: Frequent characters get **shorter codes**, rare characters get **longer codes**.

**Example**:
```
Text: "aaaaabbbcc"
Frequencies: a=5, b=3, c=2

Fixed-length: 2 bits/char → 10 chars × 2 = 20 bits
Huffman:      a=0, b=10, c=11 → 5×1 + 3×2 + 2×2 = 15 bits
```

**Greedy Strategy**: Build tree by repeatedly merging two **least frequent** nodes.

**Algorithm**:
1. Calculate character frequencies
2. Create leaf node for each character
3. Build min-heap (priority queue)
4. While heap has > 1 node:
   - Extract two minimum frequency nodes
   - Create internal node with frequency = sum
   - Insert back into heap
5. Generate codes by traversing tree (left=0, right=1)

**Huffman Tree Building (Example: "aaaaabbbcc")**:
```
Step 1: Initial nodes
  [a:5]  [b:3]  [c:2]

Step 2: Merge c(2) + b(3) = 5
  [a:5]  [5]
         / \
       [b:3][c:2]

Step 3: Merge a(5) + merged(5) = 10
      [10]
      /  \
   [a:5] [5]
         / \
       [b:3][c:2]

Final Codes (left=0, right=1):
  a = 0
  b = 10
  c = 11
```

**Time**: $O(n \log n)$, **Space**: $O(n)$

**Properties**:
- **Prefix-free**: No code is prefix of another
- **Optimal**: Minimum average code length

```ruby
class HuffmanNode
  attr_accessor :char, :freq, :left, :right

  def initialize(char, freq)
    @char = char
    @freq = freq
    @left = nil
    @right = nil
  end

  def <=>(other)
    @freq <=> other.freq
  end
end

def huffman_codes(text)
  # Calculate frequencies
  freq = Hash.new(0)
  text.each_char { |c| freq[c] += 1 }

  # Build priority queue
  pq = freq.map { |char, f| HuffmanNode.new(char, f) }.sort

  # Build Huffman tree
  while pq.length > 1
    left = pq.shift
    right = pq.shift

    merged = HuffmanNode.new(nil, left.freq + right.freq)
    merged.left = left
    merged.right = right

    pq.push(merged)
    pq.sort!
  end

  root = pq.first
  codes = {}
  generate_codes(root, "", codes)
  codes
end

def generate_codes(node, code, codes)
  return if node.nil?

  if node.char
    codes[node.char] = code
    return
  end

  generate_codes(node.left, code + "0", codes)
  generate_codes(node.right, code + "1", codes)
end

# Example
text = "huffman encoding example"
codes = huffman_codes(text)
puts "Huffman Codes:"
codes.each { |char, code| puts "#{char}: #{code}" }

# Encode
encoded = text.chars.map { |c| codes[c] }.join
puts "\nOriginal: #{text.length * 8} bits"
puts "Encoded: #{encoded.length} bits"
puts "Compression: #{((1 - encoded.length.to_f / (text.length * 8)) * 100).round(2)}%"
```

---

#### Interval Scheduling

**What is Minimum Platforms Problem?**

Given arrival and departure times of trains, find the **minimum number of platforms** required so that no train waits.

**Example**:
```
Arrivals:   [9:00, 9:40, 9:50, 11:00, 15:00, 18:00]
Departures: [9:10, 12:00, 11:20, 11:30, 19:00, 20:00]

Answer: 3 platforms (at 11:00, three trains present)
```

**Greedy Strategy**: Track **overlapping intervals** at any time.

**Algorithm**:
1. Sort arrivals and departures separately
2. Use two pointers
3. If arrival < departure: train arrives, need platform
4. If departure ≤ arrival: train departs, free platform
5. Track maximum platforms needed

**Time**: $O(n \log n)$ (sorting), **Space**: $O(1)$

**Minimum Platforms**:
```ruby
def min_platforms(arrivals, departures)
  arrivals.sort!
  departures.sort!

  platforms = 1
  max_platforms = 1
  i = 1
  j = 0

  while i < arrivals.length && j < departures.length
    if arrivals[i] <= departures[j]
      platforms += 1
      i += 1
      max_platforms = [max_platforms, platforms].max
    else
      platforms -= 1
      j += 1
    end
  end

  max_platforms
end

# Example
arrivals = [900, 940, 950, 1100, 1500, 1800]
departures = [910, 1200, 1120, 1130, 1900, 2000]
puts min_platforms(arrivals, departures)  # => 3
```

---

### 21. Dynamic Programming

**What is Dynamic Programming?**

Dynamic Programming (DP) is an optimization technique that solves complex problems by breaking them into **overlapping subproblems** and **storing results** to avoid redundant computation.

**Key Idea**: "Remember what you've already computed!"

**DP = Recursion + Memoization**

---

**When to Use Dynamic Programming?**

DP works when the problem has two properties:

1. **Optimal Substructure**: Optimal solution can be constructed from optimal solutions of subproblems
   $$\text{Optimal}(n) = f(\text{Optimal}(n-1), \text{Optimal}(n-2), \ldots)$$

2. **Overlapping Subproblems**: Same subproblems are solved multiple times
   - Without DP: Exponential time (recalculating same values)
   - With DP: Polynomial time (calculate once, reuse)

**Example - Fibonacci**:
```
fib(5) calls fib(4) and fib(3)
fib(4) calls fib(3) and fib(2)
fib(3) is computed TWICE! ← Overlapping subproblem
```

---

**Two Approaches**:

| Approach | Method | Direction | When to Use |
|:---------|:-------|:----------|:------------|
| **Memoization** | Recursion + Cache | Top-Down | Natural recursion, not all subproblems needed |
| **Tabulation** | Iteration + Table | Bottom-Up | All subproblems needed, avoid recursion overhead |

**Memoization (Top-Down)**:
- Start with original problem
- Recursively break down
- Cache results in hash/array
- **Space**: $O(n)$ cache + $O(n)$ recursion stack

**Tabulation (Bottom-Up)**:
- Start with base cases
- Build up to final solution
- Fill table iteratively
- **Space**: $O(n)$ table only (no recursion)

**Comparison**:

| Aspect | Memoization | Tabulation |
|:-------|:------------|:-----------|
| **Code** | More intuitive (recursive) | Less intuitive (iterative) |
| **Space** | Cache + stack | Table only |
| **Speed** | Slower (function calls) | Faster (no recursion) |
| **Subproblems** | Only needed ones | All subproblems |

---

#### Fibonacci (Classic DP Example)

**Problem**: Compute $n$-th Fibonacci number

**Recurrence**: $F(n) = F(n-1) + F(n-2)$, $F(0) = 0$, $F(1) = 1$

---

**Approach 1: Naive Recursion** (Exponential - DON'T USE!)

**Time**: $O(2^n)$ - **Exponential!**

```ruby
def fib_recursive(n)
  return n if n <= 1
  fib_recursive(n - 1) + fib_recursive(n - 2)
end
```

**Why so slow?** Recalculates same values many times:
```
fib(5)
├── fib(4)
│   ├── fib(3)
│   │   ├── fib(2)  ← Computed
│   │   └── fib(1)
│   └── fib(2)      ← Recomputed!
└── fib(3)          ← Recomputed!
    ├── fib(2)      ← Recomputed!
    └── fib(1)
```

---

**Approach 2: Memoization** (Top-Down DP)

**Time**: $O(n)$, **Space**: $O(n)$ cache + $O(n)$ stack

```ruby
def fib_memo(n, memo = {})
  return n if n <= 1
  return memo[n] if memo[n]  # Return cached result

  memo[n] = fib_memo(n - 1, memo) + fib_memo(n - 2, memo)
end
```

**Key**: Cache results in hash, compute each subproblem **once**!

---

**Approach 3: Tabulation** (Bottom-Up DP)

**Time**: $O(n)$, **Space**: $O(n)$

```ruby
def fib_tab(n)
  return n if n <= 1

  dp = Array.new(n + 1)
  dp[0] = 0
  dp[1] = 1

  (2..n).each do |i|
    dp[i] = dp[i - 1] + dp[i - 2]
  end

  dp[n]
end
```

**Key**: Build table from bottom up, no recursion!

---

**Approach 4: Space Optimized**

**Time**: $O(n)$, **Space**: $O(1)$ ✅

```ruby
def fib_optimized(n)
  return n if n <= 1

  prev2 = 0
  prev1 = 1

  (2..n).each do
    current = prev1 + prev2
    prev2 = prev1
    prev1 = current
  end

  prev1
end
```

**Key**: Only need last 2 values, not entire array!

---

**Complexity Comparison**:

| Approach | Time | Space | Notes |
|:---------|:-----|:------|:------|
| Naive Recursion | $O(2^n)$ | $O(n)$ | ❌ Too slow! |
| Memoization | $O(n)$ | $O(n)$ | ✅ Good |
| Tabulation | $O(n)$ | $O(n)$ | ✅ Good |
| Space Optimized | $O(n)$ | $O(1)$ | ✅ Best! |

# Comparison
require 'benchmark'

n = 35
Benchmark.bm do |x|
  x.report("Memoization:") { fib_memo(n) }
  x.report("Tabulation:") { fib_tab(n) }
  x.report("Optimized:") { fib_optimized(n) }
end
```

---

#### 0/1 Knapsack

**What is 0/1 Knapsack?**

Given $n$ items with weights $w_i$ and values $v_i$, and a knapsack with capacity $W$, find the **maximum value** you can carry without exceeding capacity.

**Constraint**: Each item can be taken **0 or 1 times** (can't be divided).

**Recurrence Relation**:

$$
dp[i][w] = \begin{cases}
0 & \text{if } i = 0 \text{ or } w = 0 \\
dp[i-1][w] & \text{if } w_i > w \text{ (can't include)} \\
\max(dp[i-1][w], v_i + dp[i-1][w - w_i]) & \text{otherwise}
\end{cases}
$$

where:
- $dp[i][w]$ = max value using first $i$ items with capacity $w$
- $dp[i-1][w]$ = exclude item $i$
- $v_i + dp[i-1][w - w_i]$ = include item $i$

**Visual Example**:

Items: `[(w=2, v=3), (w=3, v=4), (w=4, v=5)]`, Capacity: `5`

```
DP Table:
     w=0  w=1  w=2  w=3  w=4  w=5
i=0   0    0    0    0    0    0
i=1   0    0    3    3    3    3   (item 1: w=2, v=3)
i=2   0    0    3    4    4    7   (item 2: w=3, v=4)
i=3   0    0    3    4    5    7   (item 3: w=4, v=5)

Answer: dp[3][5] = 7 (items 1 and 2)
```

---

**Approach 1: Naive Recursion**

**Time**: $O(2^n)$ - **Exponential!**

```ruby
def knapsack_recursive(weights, values, capacity, n = weights.length)
  return 0 if n == 0 || capacity == 0

  if weights[n - 1] > capacity
    knapsack_recursive(weights, values, capacity, n - 1)
  else
    include_item = values[n - 1] + knapsack_recursive(weights, values, capacity - weights[n - 1], n - 1)
    exclude_item = knapsack_recursive(weights, values, capacity, n - 1)
    [include_item, exclude_item].max
  end
end
```

---

**Approach 2: Memoization** (Top-Down DP)

**Time**: $O(n \times W)$, **Space**: $O(n \times W)$
```ruby
def knapsack_memo(weights, values, capacity, n = weights.length, memo = {})
  return 0 if n == 0 || capacity == 0

  key = [n, capacity]
  return memo[key] if memo[key]

  if weights[n - 1] > capacity
    memo[key] = knapsack_memo(weights, values, capacity, n - 1, memo)
  else
    include_item = values[n - 1] + knapsack_memo(weights, values, capacity - weights[n - 1], n - 1, memo)
    exclude_item = knapsack_memo(weights, values, capacity, n - 1, memo)
    memo[key] = [include_item, exclude_item].max
  end

  memo[key]
end
```

---

**Approach 3: Tabulation** (Bottom-Up DP)

**Time**: $O(n \times W)$, **Space**: $O(n \times W)$

```ruby
def knapsack_tab(weights, values, capacity)
  n = weights.length
  dp = Array.new(n + 1) { Array.new(capacity + 1, 0) }

  (1..n).each do |i|
    (1..capacity).each do |w|
      if weights[i - 1] <= w
        include_item = values[i - 1] + dp[i - 1][w - weights[i - 1]]
        exclude_item = dp[i - 1][w]
        dp[i][w] = [include_item, exclude_item].max
      else
        dp[i][w] = dp[i - 1][w]
      end
    end
  end

  dp[n][capacity]
end
```

**Key**: Build table from base cases up!

# With item tracking
def knapsack_with_items(weights, values, capacity)
  n = weights.length
  dp = Array.new(n + 1) { Array.new(capacity + 1, 0) }

  (1..n).each do |i|
    (1..capacity).each do |w|
      if weights[i - 1] <= w
        include_item = values[i - 1] + dp[i - 1][w - weights[i - 1]]
        exclude_item = dp[i - 1][w]
        dp[i][w] = [include_item, exclude_item].max
      else
        dp[i][w] = dp[i - 1][w]
      end
    end
  end

  # Backtrack to find items
  items = []
  w = capacity

  n.downto(1) do |i|
    if dp[i][w] != dp[i - 1][w]
      items << i - 1
      w -= weights[i - 1]
    end
  end

  { max_value: dp[n][capacity], items: items.reverse }
end

# Example
weights = [10, 20, 30]
values = [60, 100, 120]
capacity = 50

result = knapsack_with_items(weights, values, capacity)
puts "Max value: #{result[:max_value]}"  # => 220
puts "Items: #{result[:items].inspect}"  # => [1, 2]
```

---

#### Longest Common Subsequence (LCS)

**What is LCS?**

Find the **longest subsequence** that appears in **both** strings in the **same order** (but not necessarily consecutive).

**Example**:
- `s1 = "ABCDGH"`, `s2 = "AEDFHR"`
- LCS = `"ADH"` (length 3)

**Subsequence vs Substring**:
- **Subsequence**: Characters in order, but **not necessarily consecutive** (e.g., "ACE" from "ABCDE")
- **Substring**: Characters **must be consecutive** (e.g., "BCD" from "ABCDE")

**Recurrence Relation**:

$$
dp[i][j] = \begin{cases}
0 & \text{if } i = 0 \text{ or } j = 0 \\
dp[i-1][j-1] + 1 & \text{if } s1[i-1] = s2[j-1] \\
\max(dp[i-1][j], dp[i][j-1]) & \text{otherwise}
\end{cases}
$$

where $dp[i][j]$ = length of LCS of $s1[0..i-1]$ and $s2[0..j-1]$

**Visual Example**:

```
s1 = "ABCD", s2 = "ACBD"

DP Table:
      ""  A  C  B  D
  ""   0  0  0  0  0
  A    0  1  1  1  1
  B    0  1  1  2  2
  C    0  1  2  2  2
  D    0  1  2  2  3

LCS = "ACD" (length 3)
```

**Time**: $O(m \times n)$, **Space**: $O(m \times n)$

```ruby
def lcs(s1, s2)
  m = s1.length
  n = s2.length
  dp = Array.new(m + 1) { Array.new(n + 1, 0) }

  (1..m).each do |i|
    (1..n).each do |j|
      if s1[i - 1] == s2[j - 1]
        dp[i][j] = dp[i - 1][j - 1] + 1
      else
        dp[i][j] = [dp[i - 1][j], dp[i][j - 1]].max
      end
    end
  end

  dp[m][n]
end
```

# With sequence reconstruction
def lcs_with_sequence(s1, s2)
  m = s1.length
  n = s2.length
  dp = Array.new(m + 1) { Array.new(n + 1, 0) }

  (1..m).each do |i|
    (1..n).each do |j|
      if s1[i - 1] == s2[j - 1]
        dp[i][j] = dp[i - 1][j - 1] + 1
      else
        dp[i][j] = [dp[i - 1][j], dp[i][j - 1]].max
      end
    end
  end

  # Backtrack to find LCS
  lcs_str = ""
  i = m
  j = n

  while i > 0 && j > 0
    if s1[i - 1] == s2[j - 1]
      lcs_str = s1[i - 1] + lcs_str
      i -= 1
      j -= 1
    elsif dp[i - 1][j] > dp[i][j - 1]
      i -= 1
    else
      j -= 1
    end
  end

  { length: dp[m][n], sequence: lcs_str }
end

# Example
s1 = "AGGTAB"
s2 = "GXTXAYB"
result = lcs_with_sequence(s1, s2)
puts "LCS length: #{result[:length]}"      # => 4
puts "LCS sequence: #{result[:sequence]}"  # => "GTAB"
```

---

#### Longest Increasing Subsequence (LIS)

**What is LIS?**

Find the **longest subsequence** where elements are in **strictly increasing order**.

**Example**:
- `arr = [10, 9, 2, 5, 3, 7, 101, 18]`
- LIS = `[2, 3, 7, 18]` or `[2, 3, 7, 101]` (length 4)

**Recurrence Relation**:

$$dp[i] = \max_{j < i, arr[j] < arr[i]} (dp[j] + 1)$$

where $dp[i]$ = length of LIS ending at index $i$

**Visual Example**:

```
arr = [10, 9, 2, 5, 3, 7, 101, 18]
dp  = [ 1, 1, 1, 2, 2, 3,   4,  4]

For i=5 (arr[5]=7):
  Check j=0..4:
    arr[2]=2 < 7: dp[5] = max(dp[5], dp[2]+1) = max(1, 2) = 2
    arr[3]=5 < 7: dp[5] = max(dp[5], dp[3]+1) = max(2, 3) = 3
    arr[4]=3 < 7: dp[5] = max(dp[5], dp[4]+1) = max(3, 3) = 3
  Final: dp[5] = 3
```

---

**Approach 1: Dynamic Programming** - $O(n^2)$

**Time**: $O(n^2)$, **Space**: $O(n)$

```ruby
def lis(arr)
  n = arr.length
  dp = Array.new(n, 1)

  (1...n).each do |i|
    (0...i).each do |j|
      if arr[j] < arr[i]
        dp[i] = [dp[i], dp[j] + 1].max
      end
    end
  end

  dp.max
end
```

# With sequence
def lis_with_sequence(arr)
  n = arr.length
  dp = Array.new(n, 1)
  parent = Array.new(n, -1)

  (1...n).each do |i|
    (0...i).each do |j|
      if arr[j] < arr[i] && dp[j] + 1 > dp[i]
        dp[i] = dp[j] + 1
        parent[i] = j
      end
    end
  end

  # Find max length and its index
  max_length = dp.max
  max_index = dp.index(max_length)

  # Reconstruct sequence
  sequence = []
  idx = max_index

  while idx != -1
    sequence.unshift(arr[idx])
    idx = parent[idx]
  end

  { length: max_length, sequence: sequence }
end

# Example
arr = [10, 9, 2, 5, 3, 7, 101, 18]
result = lis_with_sequence(arr)
puts "LIS length: #{result[:length]}"      # => 4
puts "LIS sequence: #{result[:sequence].inspect}"  # => [2, 3, 7, 18]
```

---

**Approach 2: Binary Search** - $O(n \log n)$ ✅ **Optimal!**

**Key Idea**: Maintain array `tails` where `tails[i]` = smallest tail element of all increasing subsequences of length `i+1`.

**Time**: $O(n \log n)$, **Space**: $O(n)$

```ruby
def lis_binary_search(arr)
  tails = []

  arr.each do |num|
    left = 0
    right = tails.length

    while left < right
      mid = (left + right) / 2
      if tails[mid] < num
        left = mid + 1
      else
        right = mid
      end
    end

    if left == tails.length
      tails << num
    else
      tails[left] = num
    end
  end

  tails.length
end
```

---

#### Edit Distance (Levenshtein Distance)

**What is Edit Distance?**

The **minimum number of operations** needed to convert string `s1` to string `s2`.

**Allowed Operations**:
1. **Insert** a character
2. **Delete** a character
3. **Replace** a character

**Example**:
- `s1 = "sunday"`, `s2 = "saturday"`
- Operations: Insert 'a', Insert 't', Replace 'n' with 'r' = **3 operations**

**Recurrence Relation**:

$$
dp[i][j] = \begin{cases}
i & \text{if } j = 0 \text{ (delete all)} \\
j & \text{if } i = 0 \text{ (insert all)} \\
dp[i-1][j-1] & \text{if } s1[i-1] = s2[j-1] \\
1 + \min \begin{cases}
dp[i-1][j] & \text{(delete)} \\
dp[i][j-1] & \text{(insert)} \\
dp[i-1][j-1] & \text{(replace)}
\end{cases} & \text{otherwise}
\end{cases}
$$

**Visual Example**:

```
s1 = "horse", s2 = "ros"

DP Table:
      ""  r  o  s
  ""   0  1  2  3
  h    1  1  2  3
  o    2  2  1  2
  r    3  2  2  2
  s    4  3  3  2
  e    5  4  4  3

Answer: dp[5][3] = 3
```

**Time**: $O(m \times n)$, **Space**: $O(m \times n)$

```ruby
def edit_distance(s1, s2)
  m = s1.length
  n = s2.length
  dp = Array.new(m + 1) { Array.new(n + 1, 0) }

  # Base cases
  (0..m).each { |i| dp[i][0] = i }
  (0..n).each { |j| dp[0][j] = j }

  (1..m).each do |i|
    (1..n).each do |j|
      if s1[i - 1] == s2[j - 1]
        dp[i][j] = dp[i - 1][j - 1]
      else
        dp[i][j] = 1 + [
          dp[i - 1][j],      # Delete
          dp[i][j - 1],      # Insert
          dp[i - 1][j - 1]   # Replace
        ].min
      end
    end
  end

  dp[m][n]
end

# Example
s1 = "sunday"
s2 = "saturday"
puts edit_distance(s1, s2)  # => 3
```

---

#### Coin Change

**What is Coin Change?**

Given coins of different denominations and a total amount, solve:
1. **Minimum coins** needed to make the amount
2. **Number of ways** to make the amount

---

**Problem 1: Minimum Coins**

Find the **fewest number of coins** needed to make the amount.

**Recurrence**:

$$dp[i] = \min_{coin \leq i} (dp[i - coin] + 1)$$

where $dp[i]$ = minimum coins needed for amount $i$

**Example**:
- `coins = [1, 2, 5]`, `amount = 11`
- Answer: `3` coins (5 + 5 + 1)

**Time**: $O(amount \times n)$, **Space**: $O(amount)$

```ruby
def coin_change_min(coins, amount)
  dp = Array.new(amount + 1, Float::INFINITY)
  dp[0] = 0

  (1..amount).each do |i|
    coins.each do |coin|
      if coin <= i
        dp[i] = [dp[i], dp[i - coin] + 1].min
      end
    end
  end

  dp[amount] == Float::INFINITY ? -1 : dp[amount]
end

# Example
coins = [1, 2, 5]
amount = 11
puts coin_change_min(coins, amount)  # => 3 (5 + 5 + 1)
```

---

**Problem 2: Number of Ways**

Find the **total number of combinations** to make the amount.

**Recurrence**:

$$dp[i] = \sum_{coin \leq i} dp[i - coin]$$

where $dp[i]$ = number of ways to make amount $i$

**Example**:
- `coins = [1, 2, 5]`, `amount = 5`
- Ways: `[5], [2,2,1], [2,1,1,1], [1,1,1,1,1]` = **4 ways**

**Time**: $O(amount \times n)$, **Space**: $O(amount)$

```ruby
def coin_change_ways(coins, amount)
  dp = Array.new(amount + 1, 0)
  dp[0] = 1

  coins.each do |coin|
    (coin..amount).each do |i|
      dp[i] += dp[i - coin]
    end
  end

  dp[amount]
end

# Example
coins = [1, 2, 5]
amount = 5
puts coin_change_ways(coins, amount)  # => 4
# Ways: [1,1,1,1,1], [1,1,1,2], [1,2,2], [5]
```

---

#### Matrix Chain Multiplication

**What is Matrix Chain Multiplication?**

Given a chain of matrices, find the **optimal order** to multiply them to **minimize scalar multiplications**.

**Key Insight**: Matrix multiplication is **associative** but **not commutative**:
- $(A \times B) \times C = A \times (B \times C)$ ✅ (same result)
- But **different costs**!

**Example**:
```
Matrices: A₁(10×20), A₂(20×30), A₃(30×40)

Option 1: (A₁ × A₂) × A₃
  A₁ × A₂: 10×20×30 = 6,000 ops → Result: 10×30
  Result × A₃: 10×30×40 = 12,000 ops
  Total: 18,000 ops

Option 2: A₁ × (A₂ × A₃)
  A₂ × A₃: 20×30×40 = 24,000 ops → Result: 20×40
  A₁ × Result: 10×20×40 = 8,000 ops
  Total: 32,000 ops

Best: Option 1 (18,000 ops)
```

**Recurrence**:

$$dp[i][j] = \min_{i \leq k < j} (dp[i][k] + dp[k+1][j] + p_i \times p_{k+1} \times p_{j+1})$$

where $dp[i][j]$ = minimum cost to multiply matrices $i$ to $j$

**Time**: $O(n^3)$, **Space**: $O(n^2)$

```ruby
def matrix_chain_order(dimensions)
  n = dimensions.length - 1
  dp = Array.new(n) { Array.new(n, 0) }

  # l is chain length
  (2..n).each do |l|
    (0...(n - l + 1)).each do |i|
      j = i + l - 1
      dp[i][j] = Float::INFINITY

      (i...j).each do |k|
        cost = dp[i][k] + dp[k + 1][j] + dimensions[i] * dimensions[k + 1] * dimensions[j + 1]
        dp[i][j] = cost if cost < dp[i][j]
      end
    end
  end

  dp[0][n - 1]
end

# Example
# Matrices: A1(10x20), A2(20x30), A3(30x40), A4(40x30)
dimensions = [10, 20, 30, 40, 30]
puts matrix_chain_order(dimensions)  # => 30000
```

---

#### Partition Equal Subset Sum

**What is Partition Equal Subset Sum?**

Can an array be partitioned into **two subsets** with **equal sum**?

**Example**:
- `nums = [1, 5, 11, 5]`
- Partition: `[1, 5, 5]` and `[11]` → Both sum to 11 ✅

**Key Insight**: This is a **subset sum** problem!
- Total sum must be **even** (otherwise impossible)
- Find if subset with sum = `total/2` exists

**Recurrence**:

$$dp[i] = dp[i] \text{ OR } dp[i - num]$$

where $dp[i]$ = can we make sum $i$?

**Time**: $O(n \times sum)$, **Space**: $O(sum)$

```ruby
def can_partition(nums)
  total = nums.sum
  return false if total.odd?

  target = total / 2
  dp = Array.new(target + 1, false)
  dp[0] = true

  nums.each do |num|
    target.downto(num) do |i|
      dp[i] = dp[i] || dp[i - num]
    end
  end

  dp[target]
end

# Example
nums = [1, 5, 11, 5]
puts can_partition(nums)  # => true ([1, 5, 5] and [11])
```

---

#### Palindrome Partitioning

**What is Palindrome Partitioning?**

Given a string, partition it into **minimum number of substrings** such that each substring is a **palindrome**.

**Example**:
- `s = "aab"`
- Partitions: `["aa", "b"]` → 1 cut
- Other option: `["a", "a", "b"]` → 2 cuts
- Minimum: **1 cut**

**Key Insight**: Use **DP** to find minimum cuts!

**Recurrence**:

$$dp[i] = \min_{0 \leq j < i} (dp[j] + 1)$$

where substring $s[j+1...i]$ is a palindrome

**Algorithm**:
1. Build palindrome table: `is_palindrome[i][j]` = is substring `s[i...j]` a palindrome?
2. For each position, find minimum cuts needed

**Time**: $O(n^2)$, **Space**: $O(n^2)$

**Minimum cuts for palindrome partitioning**:
```ruby
def min_cut(s)
  n = s.length
  dp = Array.new(n, 0)
  is_palindrome = Array.new(n) { Array.new(n, false) }

  # Build palindrome table
  (0...n).each do |i|
    (0..i).each do |j|
      if s[i] == s[j] && (i - j <= 2 || is_palindrome[j + 1][i - 1])
        is_palindrome[j][i] = true
      end
    end
  end

  # Calculate minimum cuts
  (0...n).each do |i|
    if is_palindrome[0][i]
      dp[i] = 0
    else
      dp[i] = i
      (0...i).each do |j|
        if is_palindrome[j + 1][i]
          dp[i] = [dp[i], dp[j] + 1].min
        end
      end
    end
  end

  dp[n - 1]
end

# Example
s = "aab"
puts min_cut(s)  # => 1 (aa | b)
```

---

#### Word Break

**What is Word Break?**

Can a string be segmented into **dictionary words**?

**Example**:
- `s = "leetcode"`, `dict = ["leet", "code"]`
- Segmentation: `"leet" + "code"` ✅
- Answer: **true**

**Example 2**:
- `s = "applepenapple"`, `dict = ["apple", "pen"]`
- Segmentation: `"apple" + "pen" + "apple"` ✅
- Answer: **true**

**Key Insight**: Use **DP** to check if prefix can be segmented!

**Recurrence**:

$$dp[i] = \bigvee_{0 \leq j < i} (dp[j] \land s[j...i] \in dict)$$

where $dp[i]$ = can substring $s[0...i]$ be segmented?

**Time**: $O(n^2 \times m)$ where $m$ = average word length, **Space**: $O(n)$

```ruby
def word_break(s, word_dict)
  n = s.length
  dp = Array.new(n + 1, false)
  dp[0] = true

  (1..n).each do |i|
    (0...i).each do |j|
      if dp[j] && word_dict.include?(s[j...i])
        dp[i] = true
        break
      end
    end
  end

  dp[n]
end

# Example
s = "leetcode"
word_dict = ["leet", "code"]
puts word_break(s, word_dict)  # => true
```

---

#### House Robber

**What is House Robber?**

You're a robber planning to rob houses along a street. Each house has money. **Cannot rob adjacent houses** (alarm will trigger). Maximize money robbed!

**Example**:
- `nums = [2, 7, 9, 3, 1]`
- Rob houses: `2 + 9 + 1 = 12` ✅
- Cannot rob: `7 + 9` (adjacent) ❌

**Key Insight**: At each house, choose to **rob** or **skip**!

**Recurrence**:

$$dp[i] = \max(dp[i-1], dp[i-2] + nums[i])$$

where:
- $dp[i-1]$ = skip current house (take previous max)
- $dp[i-2] + nums[i]$ = rob current house (add to max from 2 houses back)

**Time**: $O(n)$, **Space**: $O(1)$ (optimized)

```ruby
def rob(nums)
  return 0 if nums.empty?
  return nums[0] if nums.length == 1

  prev2 = 0
  prev1 = nums[0]

  (1...nums.length).each do |i|
    current = [prev1, prev2 + nums[i]].max
    prev2 = prev1
    prev1 = current
  end

  prev1
end

# Example
nums = [2, 7, 9, 3, 1]
puts rob(nums)  # => 12 (2 + 9 + 1)
```

**House Robber II** (Circular):
```ruby
def rob_circular(nums)
  return nums[0] if nums.length == 1

  # Case 1: Rob houses 0 to n-2
  # Case 2: Rob houses 1 to n-1
  [rob_helper(nums[0...-1]), rob_helper(nums[1..-1])].max
end

def rob_helper(nums)
  return 0 if nums.empty?
  return nums[0] if nums.length == 1

  prev2 = 0
  prev1 = nums[0]

  (1...nums.length).each do |i|
    current = [prev1, prev2 + nums[i]].max
    prev2 = prev1
    prev1 = current
  end

  prev1
end
```

---

#### Unique Paths

**What is Unique Paths?**

In an $m \times n$ grid, count the number of **unique paths** from **top-left** to **bottom-right**. Can only move **right** or **down**.

**Example**:
```
3×3 grid:
S . .
. . .
. . E

Paths: 6 unique paths
```

**Key Insight**: To reach cell $(i, j)$, must come from $(i-1, j)$ or $(i, j-1)$!

**Recurrence**:

$$dp[i][j] = dp[i-1][j] + dp[i][j-1]$$

where $dp[i][j]$ = number of paths to reach cell $(i, j)$

**Base Case**: $dp[0][j] = 1$ (only one way to reach first row), $dp[i][0] = 1$ (only one way to reach first column)

**Time**: $O(m \times n)$, **Space**: $O(n)$ (optimized)

```ruby
def unique_paths(m, n)
  dp = Array.new(m) { Array.new(n, 1) }

  (1...m).each do |i|
    (1...n).each do |j|
      dp[i][j] = dp[i - 1][j] + dp[i][j - 1]
    end
  end

  dp[m - 1][n - 1]
end

# Space optimized
def unique_paths_optimized(m, n)
  dp = Array.new(n, 1)

  (1...m).each do |i|
    (1...n).each do |j|
      dp[j] += dp[j - 1]
    end
  end

  dp[n - 1]
end

# Example
puts unique_paths(3, 7)  # => 28
```

**With Obstacles**:
```ruby
def unique_paths_with_obstacles(grid)
  m = grid.length
  n = grid[0].length

  return 0 if grid[0][0] == 1 || grid[m - 1][n - 1] == 1

  dp = Array.new(m) { Array.new(n, 0) }
  dp[0][0] = 1

  (0...m).each do |i|
    (0...n).each do |j|
      next if grid[i][j] == 1

      if i > 0
        dp[i][j] += dp[i - 1][j]
      end

      if j > 0
        dp[i][j] += dp[i][j - 1]
      end
    end
  end

  dp[m - 1][n - 1]
end
```

---

### 22. Backtracking

**What is Backtracking?**

Backtracking is an algorithmic technique that **builds solutions incrementally** and **abandons** (backtracks) when a partial solution cannot lead to a valid complete solution.

**Key Idea**: "Try all possibilities, but abandon early when you know it won't work!"

**When to Use Backtracking**:
- Finding **all solutions** (not just one)
- **Constraint satisfaction** problems
- **Combinatorial** problems (permutations, combinations, subsets)
- **Puzzle solving** (Sudoku, N-Queens, Maze)

**Backtracking vs Brute Force**:
- **Brute Force**: Try **all** possibilities (even invalid ones)
- **Backtracking**: **Prune** invalid branches early (faster!)

**Backtracking vs Dynamic Programming**:
- **DP**: Overlapping subproblems, optimal substructure
- **Backtracking**: No overlapping subproblems, find all solutions

---

**General Template**:

```ruby
def backtrack(state, choices)
  # Base case: found a solution
  if is_solution?(state)
    process_solution(state)
    return
  end

  # Try each choice
  choices.each do |choice|
    # Prune: skip invalid choices
    if is_valid?(state, choice)
      make_choice(state, choice)        # Choose
      backtrack(state, new_choices)     # Explore
      undo_choice(state, choice)        # Unchoose (backtrack)
    end
  end
end
```

**Three Steps**:
1. **Choose**: Make a choice and add to current state
2. **Explore**: Recursively explore with new state
3. **Unchoose**: Remove choice and backtrack

**Time Complexity**: Usually **exponential** $O(b^d)$ where:
- $b$ = branching factor (choices per step)
- $d$ = depth (solution length)

---

#### N-Queens

**What is N-Queens?**

Place $N$ queens on an $N \times N$ chessboard so that **no two queens attack each other**.

**Constraints**:
- No two queens in same **row**
- No two queens in same **column**
- No two queens in same **diagonal**

**Example (4-Queens)**:
```
Solution 1:      Solution 2:
. Q . .          . . Q .
. . . Q          Q . . .
Q . . .          . . . Q
. . Q .          . Q . .
```

**Backtracking Approach**:
1. Place queen in row 0, try each column
2. For each valid placement, recursively solve for row 1
3. If placement leads to no solution, **backtrack** and try next column
4. Continue until all rows filled

**Backtracking Tree (4-Queens, partial)**:
```
                    Row 0
        Q... | .Q.. | ..Q. | ...Q
         ↓      ↓      ↓      ↓
       Row 1  Row 1  Row 1  Row 1
       ...Q   Q...   Q...   .Q..
         ↓      ✗      ✗      ↓
       Row 2         (conflict) Row 2
       .Q..                   ...Q
         ↓                      ↓
       Row 3                  Row 3
       ..Q.                   .Q..
         ✓                      ✓
     Solution!              Solution!
```

**Time**: $O(N!)$ (worst case), **Space**: $O(N^2)$

```ruby
def solve_n_queens(n)
  solutions = []
  board = Array.new(n) { Array.new(n, '.') }
  backtrack_queens(board, 0, solutions)
  solutions
end

def backtrack_queens(board, row, solutions)
  if row == board.length
    solutions << board.map { |r| r.join }
    return
  end

  board[0].length.times do |col|
    if is_safe_queen?(board, row, col)
      board[row][col] = 'Q'
      backtrack_queens(board, row + 1, solutions)
      board[row][col] = '.'
    end
  end
end

def is_safe_queen?(board, row, col)
  # Check column
  (0...row).each do |i|
    return false if board[i][col] == 'Q'
  end

  # Check diagonal (top-left)
  i = row - 1
  j = col - 1
  while i >= 0 && j >= 0
    return false if board[i][j] == 'Q'
    i -= 1
    j -= 1
  end

  # Check diagonal (top-right)
  i = row - 1
  j = col + 1
  while i >= 0 && j < board[0].length
    return false if board[i][j] == 'Q'
    i -= 1
    j += 1
  end

  true
end

# Example
solutions = solve_n_queens(4)
puts "Number of solutions: #{solutions.length}"
solutions.each_with_index do |solution, i|
  puts "\nSolution #{i + 1}:"
  solution.each { |row| puts row }
end
```

---

#### Sudoku Solver

**What is Sudoku Solver?**

Fill a $9 \times 9$ Sudoku board following the rules:
1. Each **row** contains digits 1-9 (no repeats)
2. Each **column** contains digits 1-9 (no repeats)
3. Each **3×3 box** contains digits 1-9 (no repeats)

**Backtracking Approach**:
1. Find empty cell (marked with '.')
2. Try digits 1-9
3. For each valid digit:
   - Place digit
   - Recursively solve rest of board
   - If solution found, done!
   - If no solution, **backtrack** (remove digit and try next)
4. If no digit works, backtrack to previous cell

**Time**: $O(9^{empty\_cells})$ (worst case), **Space**: $O(1)$ (in-place)

```ruby
def solve_sudoku(board)
  backtrack_sudoku(board)
  board
end

def backtrack_sudoku(board)
  (0...9).each do |row|
    (0...9).each do |col|
      if board[row][col] == '.'
        ('1'..'9').each do |num|
          if is_valid_sudoku?(board, row, col, num)
            board[row][col] = num
            return true if backtrack_sudoku(board)
            board[row][col] = '.'
          end
        end
        return false
      end
    end
  end
  true
end

def is_valid_sudoku?(board, row, col, num)
  # Check row
  (0...9).each do |j|
    return false if board[row][j] == num
  end

  # Check column
  (0...9).each do |i|
    return false if board[i][col] == num
  end

  # Check 3x3 box
  box_row = (row / 3) * 3
  box_col = (col / 3) * 3

  (0...3).each do |i|
    (0...3).each do |j|
      return false if board[box_row + i][box_col + j] == num
    end
  end

  true
end
```

---

#### Subsets

**What is Subsets Problem?**

Generate **all possible subsets** (the power set) of a given set.

**Example**:
- `nums = [1, 2, 3]`
- Subsets: `[], [1], [2], [3], [1,2], [1,3], [2,3], [1,2,3]`
- Total: $2^3 = 8$ subsets

**Key Insight**: For each element, we have **2 choices**: include it or exclude it!

**Backtracking Approach**:
1. Start with empty subset
2. For each element, try adding it to current subset
3. Recursively generate subsets with remaining elements
4. Backtrack by removing element

**Time**: $O(2^n \times n)$ (generate $2^n$ subsets, each takes $O(n)$ to copy), **Space**: $O(n)$ (recursion depth)

**Generate all subsets**:
```ruby
def subsets(nums)
  result = []
  backtrack_subsets(nums, 0, [], result)
  result
end

def backtrack_subsets(nums, start, current, result)
  result << current.dup

  (start...nums.length).each do |i|
    current.push(nums[i])
    backtrack_subsets(nums, i + 1, current, result)
    current.pop
  end
end

# Example
nums = [1, 2, 3]
puts subsets(nums).inspect
# => [[], [1], [1, 2], [1, 2, 3], [1, 3], [2], [2, 3], [3]]
```

**Subsets with Duplicates**:
```ruby
def subsets_with_dup(nums)
  nums.sort!
  result = []
  backtrack_subsets_dup(nums, 0, [], result)
  result
end

def backtrack_subsets_dup(nums, start, current, result)
  result << current.dup

  (start...nums.length).each do |i|
    next if i > start && nums[i] == nums[i - 1]

    current.push(nums[i])
    backtrack_subsets_dup(nums, i + 1, current, result)
    current.pop
  end
end
```

---

#### Permutations

**What is Permutations Problem?**

Generate **all possible arrangements** of a given set of elements.

**Example**:
- `nums = [1, 2, 3]`
- Permutations: `[1,2,3], [1,3,2], [2,1,3], [2,3,1], [3,1,2], [3,2,1]`
- Total: $3! = 6$ permutations

**Difference from Subsets**:
- **Subsets**: Choose which elements to include (order doesn't matter)
- **Permutations**: All elements included, **order matters**!

**Backtracking Approach**:
1. For each position, try each unused element
2. Mark element as used
3. Recursively fill remaining positions
4. Backtrack by unmarking element

**Time**: $O(n! \times n)$ (generate $n!$ permutations, each takes $O(n)$ to copy), **Space**: $O(n)$ (recursion depth)

**Generate all permutations**:
```ruby
def permute(nums)
  result = []
  backtrack_permute(nums, [], result)
  result
end

def backtrack_permute(nums, current, result)
  if current.length == nums.length
    result << current.dup
    return
  end

  nums.each do |num|
    next if current.include?(num)

    current.push(num)
    backtrack_permute(nums, current, result)
    current.pop
  end
end

# Example
nums = [1, 2, 3]
puts permute(nums).inspect
# => [[1,2,3], [1,3,2], [2,1,3], [2,3,1], [3,1,2], [3,2,1]]
```

**Permutations with Duplicates**:
```ruby
def permute_unique(nums)
  nums.sort!
  result = []
  used = Array.new(nums.length, false)
  backtrack_permute_unique(nums, [], used, result)
  result
end

def backtrack_permute_unique(nums, current, used, result)
  if current.length == nums.length
    result << current.dup
    return
  end

  nums.each_with_index do |num, i|
    next if used[i]
    next if i > 0 && nums[i] == nums[i - 1] && !used[i - 1]

    current.push(num)
    used[i] = true
    backtrack_permute_unique(nums, current, used, result)
    current.pop
    used[i] = false
  end
end
```

---

#### Combination Sum

**What is Combination Sum?**

Find **all unique combinations** of candidates that sum to a target. **Same number can be used multiple times**.

**Example**:
- `candidates = [2, 3, 6, 7]`, `target = 7`
- Combinations: `[2, 2, 3]` and `[7]`
- Note: `2` can be used multiple times!

**Backtracking Approach**:
1. For each candidate, try including it
2. Recursively find combinations for remaining target
3. **Key**: Can reuse same candidate (pass same index)
4. Prune: If target becomes negative, backtrack

**Time**: $O(2^{target/min})$ (worst case), **Space**: $O(target/min)$ (recursion depth)

```ruby
def combination_sum(candidates, target)
  result = []
  backtrack_combination(candidates, target, 0, [], result)
  result
end

def backtrack_combination(candidates, target, start, current, result)
  if target == 0
    result << current.dup
    return
  end

  return if target < 0

  (start...candidates.length).each do |i|
    current.push(candidates[i])
    backtrack_combination(candidates, target - candidates[i], i, current, result)
    current.pop
  end
end

# Example
candidates = [2, 3, 6, 7]
target = 7
puts combination_sum(candidates, target).inspect
# => [[2, 2, 3], [7]]
```

**Combination Sum II** (Each number used once):
```ruby
def combination_sum2(candidates, target)
  candidates.sort!
  result = []
  backtrack_combination2(candidates, target, 0, [], result)
  result
end

def backtrack_combination2(candidates, target, start, current, result)
  if target == 0
    result << current.dup
    return
  end

  return if target < 0

  (start...candidates.length).each do |i|
    next if i > start && candidates[i] == candidates[i - 1]

    current.push(candidates[i])
    backtrack_combination2(candidates, target - candidates[i], i + 1, current, result)
    current.pop
  end
end
```

---

#### Palindrome Partitioning

**Find all palindrome partitions**:
```ruby
def partition(s)
  result = []
  backtrack_partition(s, 0, [], result)
  result
end

def backtrack_partition(s, start, current, result)
  if start == s.length
    result << current.dup
    return
  end

  (start...s.length).each do |end_idx|
    substring = s[start..end_idx]
    if is_palindrome?(substring)
      current.push(substring)
      backtrack_partition(s, end_idx + 1, current, result)
      current.pop
    end
  end
end

def is_palindrome?(s)
  s == s.reverse
end

# Example
s = "aab"
puts partition(s).inspect
# => [["a", "a", "b"], ["aa", "b"]]
```

---

### 23. Recursion

#### Fundamentals

**Definition**: Function that calls itself to solve smaller instances of the same problem.

**Components**:
1. **Base Case**: Termination condition
2. **Recursive Case**: Problem reduction

**Recursion Tree Example**:
```
fib(4)
├── fib(3)
│   ├── fib(2)
│   │   ├── fib(1) → 1
│   │   └── fib(0) → 0
│   └── fib(1) → 1
└── fib(2)
    ├── fib(1) → 1
    └── fib(0) → 0
```

---

#### Tail Recursion

**Definition**: Recursive call is the last operation

**Non-Tail Recursive**:
```ruby
def factorial(n)
  return 1 if n <= 1
  n * factorial(n - 1)  # Multiplication after recursive call
end
```

**Tail Recursive**:
```ruby
def factorial_tail(n, acc = 1)
  return acc if n <= 1
  factorial_tail(n - 1, n * acc)  # Recursive call is last operation
end

# Example
puts factorial_tail(5)  # => 120
```

**Advantages**:
- Can be optimized to iteration by compiler
- Constant stack space

---

#### Tower of Hanoi

**What is Tower of Hanoi?**

Move $n$ disks from **source peg** to **destination peg** using an **auxiliary peg**.

**Rules**:
1. Only one disk can be moved at a time
2. A disk can only be placed on top of a **larger disk**
3. Only the **top disk** of a stack can be moved

**Example (3 disks)**:
```
Initial:        Goal:
  |               |
 [1]              |
 [2]              |
 [3]             [1]
─────           [2]
  A              [3]
                ─────
                  C
```

**Recursive Strategy**:
1. Move $n-1$ disks from source to auxiliary (using destination)
2. Move largest disk from source to destination
3. Move $n-1$ disks from auxiliary to destination (using source)

**Step-by-Step (3 disks)**:
```
Step 1: Move 2 disks A→B (using C)
  A      B      C          A      B      C
 [1]     |      |          |      |     [1]
 [2]     |      |    →    [2]     |      |
 [3]     |      |         [3]     |      |

Step 2: Move disk 3 A→C
  A      B      C          A      B      C
  |      |     [1]         |      |     [1]
 [2]     |      |    →     |      |      |
 [3]     |      |          |      |     [3]

Step 3: Move 2 disks B→C (using A)
  A      B      C          A      B      C
  |      |     [1]         |      |      |
  |      |      |    →     |      |     [1]
  |      |     [3]         |      |     [2]
                                        [3]
```

**Recurrence**: $T(n) = 2T(n-1) + 1$ → $T(n) = 2^n - 1$ moves

**Time**: $O(2^n)$, **Space**: $O(n)$ (recursion stack)

```ruby
def tower_of_hanoi(n, source = 'A', destination = 'C', auxiliary = 'B')
  if n == 1
    puts "Move disk 1 from #{source} to #{destination}"
    return
  end

  tower_of_hanoi(n - 1, source, auxiliary, destination)
  puts "Move disk #{n} from #{source} to #{destination}"
  tower_of_hanoi(n - 1, auxiliary, destination, source)
end

# Example
tower_of_hanoi(3)
# Move disk 1 from A to C
# Move disk 2 from A to B
# Move disk 1 from C to B
# Move disk 3 from A to C
# Move disk 1 from B to A
# Move disk 2 from B to C
# Move disk 1 from A to C
```

**Time**: O(2^n), **Space**: O(n)

---

#### Generate Parentheses

**Problem**: Generate all valid combinations of n pairs of parentheses

```ruby
def generate_parentheses(n)
  result = []
  backtrack_parens("", 0, 0, n, result)
  result
end

def backtrack_parens(current, open, close, max, result)
  if current.length == max * 2
    result << current
    return
  end

  if open < max
    backtrack_parens(current + "(", open + 1, close, max, result)
  end

  if close < open
    backtrack_parens(current + ")", open, close + 1, max, result)
  end
end

# Example
puts generate_parentheses(3).inspect
# => ["((()))", "(()())", "(())()", "()(())", "()()()"]
```

---

#### Letter Combinations of Phone Number

```ruby
def letter_combinations(digits)
  return [] if digits.empty?

  mapping = {
    '2' => 'abc', '3' => 'def', '4' => 'ghi',
    '5' => 'jkl', '6' => 'mno', '7' => 'pqrs',
    '8' => 'tuv', '9' => 'wxyz'
  }

  result = []
  backtrack_letters(digits, 0, "", mapping, result)
  result
end

def backtrack_letters(digits, index, current, mapping, result)
  if index == digits.length
    result << current
    return
  end

  letters = mapping[digits[index]]
  letters.each_char do |letter|
    backtrack_letters(digits, index + 1, current + letter, mapping, result)
  end
end

# Example
puts letter_combinations("23").inspect
# => ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]
```

---

#### Power Set (All Subsets)

**Recursive Approach**:
```ruby
def power_set(nums)
  return [[]] if nums.empty?

  first = nums[0]
  rest_subsets = power_set(nums[1..-1])

  new_subsets = rest_subsets.map { |subset| [first] + subset }
  rest_subsets + new_subsets
end

# Example
puts power_set([1, 2, 3]).inspect
```

---

#### Recursion Stack Depth Analysis

**Stack Overflow Example**:
```ruby
def deep_recursion(n)
  return 0 if n == 0
  1 + deep_recursion(n - 1)
end

# This will cause stack overflow for large n
begin
  puts deep_recursion(100000)
rescue SystemStackError => e
  puts "Stack overflow: #{e.message}"
end
```

**Iterative Alternative**:
```ruby
def iterative_version(n)
  result = 0
  n.times { result += 1 }
  result
end

puts iterative_version(100000)  # No stack overflow
```

---

## Part V — Searching & Sorting

### 24. Searching Algorithms

#### Linear Search

**Algorithm**: Check each element sequentially

```ruby
def linear_search(arr, target)
  arr.each_with_index do |element, index|
    return index if element == target
  end
  -1
end

# Example
arr = [64, 34, 25, 12, 22, 11, 90]
puts linear_search(arr, 22)  # => 4
```

**Time**: O(n), **Space**: O(1)

---

#### Binary Search

**Iterative**:
```ruby
def binary_search(arr, target)
  left = 0
  right = arr.length - 1

  while left <= right
    mid = left + (right - left) / 2

    return mid if arr[mid] == target

    if arr[mid] < target
      left = mid + 1
    else
      right = mid - 1
    end
  end

  -1
end
```

**Recursive**:
```ruby
def binary_search_recursive(arr, target, left = 0, right = arr.length - 1)
  return -1 if left > right

  mid = left + (right - left) / 2

  return mid if arr[mid] == target

  if arr[mid] < target
    binary_search_recursive(arr, target, mid + 1, right)
  else
    binary_search_recursive(arr, target, left, mid - 1)
  end
end
```

**Time**: O(log n), **Space**: O(1) iterative, O(log n) recursive

---

#### Exponential Search

**Use Case**: Unbounded/infinite arrays

```ruby
def exponential_search(arr, target)
  return 0 if arr[0] == target

  # Find range
  i = 1
  while i < arr.length && arr[i] <= target
    i *= 2
  end

  # Binary search in range
  binary_search_range(arr, target, i / 2, [i, arr.length - 1].min)
end

def binary_search_range(arr, target, left, right)
  while left <= right
    mid = left + (right - left) / 2

    return mid if arr[mid] == target

    if arr[mid] < target
      left = mid + 1
    else
      right = mid - 1
    end
  end

  -1
end

# Example
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 20, 30, 40, 50]
puts exponential_search(arr, 30)  # => 11
```

**Time**: O(log n), **Space**: O(1)

---

#### Ternary Search

**Use Case**: Unimodal functions (find maximum/minimum)

```ruby
def ternary_search(arr, target, left = 0, right = arr.length - 1)
  return -1 if left > right

  mid1 = left + (right - left) / 3
  mid2 = right - (right - left) / 3

  return mid1 if arr[mid1] == target
  return mid2 if arr[mid2] == target

  if target < arr[mid1]
    ternary_search(arr, target, left, mid1 - 1)
  elsif target > arr[mid2]
    ternary_search(arr, target, mid2 + 1, right)
  else
    ternary_search(arr, target, mid1 + 1, mid2 - 1)
  end
end

# Example
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
puts ternary_search(arr, 7)  # => 6
```

**Time**: O(log₃ n), **Space**: O(log n)

---

#### Search Algorithms Comparison

| Algorithm | Time | Space | Use Case |
|:----------|:-----|:------|:---------|
| **Linear** | O(n) | O(1) | Unsorted, small arrays |
| **Binary** | O(log n) | O(1) | Sorted arrays |
| **Exponential** | O(log n) | O(1) | Unbounded/infinite arrays |
| **Ternary** | O(log₃ n) | O(log n) | Unimodal functions |

---

### 25. Sorting Algorithms

#### Bubble Sort

**Algorithm**: Repeatedly swap adjacent elements if in wrong order

```ruby
def bubble_sort(arr)
  n = arr.length

  (n - 1).times do |i|
    swapped = false

    (0...(n - i - 1)).each do |j|
      if arr[j] > arr[j + 1]
        arr[j], arr[j + 1] = arr[j + 1], arr[j]
        swapped = true
      end
    end

    break unless swapped  # Optimization
  end

  arr
end

# Example
arr = [64, 34, 25, 12, 22, 11, 90]
puts bubble_sort(arr).inspect
```

**Time**: O(n²) worst/average, O(n) best
**Space**: O(1)
**Stable**: Yes

---

#### Selection Sort

**Algorithm**: Find minimum and place at beginning

```ruby
def selection_sort(arr)
  n = arr.length

  (0...n - 1).each do |i|
    min_idx = i

    (i + 1...n).each do |j|
      min_idx = j if arr[j] < arr[min_idx]
    end

    arr[i], arr[min_idx] = arr[min_idx], arr[i] if min_idx != i
  end

  arr
end

# Example
arr = [64, 25, 12, 22, 11]
puts selection_sort(arr).inspect
```

**Time**: O(n²) all cases
**Space**: O(1)
**Stable**: No

---

#### Insertion Sort

**Algorithm**: Build sorted array one element at a time

```ruby
def insertion_sort(arr)
  (1...arr.length).each do |i|
    key = arr[i]
    j = i - 1

    while j >= 0 && arr[j] > key
      arr[j + 1] = arr[j]
      j -= 1
    end

    arr[j + 1] = key
  end

  arr
end

# Example
arr = [12, 11, 13, 5, 6]
puts insertion_sort(arr).inspect
```

**Time**: O(n²) worst/average, O(n) best
**Space**: O(1)
**Stable**: Yes

---

#### Merge Sort

**Algorithm**: Divide, sort, merge

```ruby
def merge_sort(arr)
  return arr if arr.length <= 1

  mid = arr.length / 2
  left = merge_sort(arr[0...mid])
  right = merge_sort(arr[mid..-1])

  merge(left, right)
end

def merge(left, right)
  result = []
  i = j = 0

  while i < left.length && j < right.length
    if left[i] <= right[j]
      result << left[i]
      i += 1
    else
      result << right[j]
      j += 1
    end
  end

  result.concat(left[i..-1]) if i < left.length
  result.concat(right[j..-1]) if j < right.length

  result
end

# Example
arr = [38, 27, 43, 3, 9, 82, 10]
puts merge_sort(arr).inspect
```

**Time**: O(n log n) all cases
**Space**: O(n)
**Stable**: Yes

---

#### Quick Sort

**Algorithm**: Choose pivot, partition, recursively sort

```ruby
def quick_sort(arr, low = 0, high = arr.length - 1)
  if low < high
    pi = partition(arr, low, high)
    quick_sort(arr, low, pi - 1)
    quick_sort(arr, pi + 1, high)
  end
  arr
end

def partition(arr, low, high)
  pivot = arr[high]
  i = low - 1

  (low...high).each do |j|
    if arr[j] <= pivot
      i += 1
      arr[i], arr[j] = arr[j], arr[i]
    end
  end

  arr[i + 1], arr[high] = arr[high], arr[i + 1]
  i + 1
end

# Example
arr = [10, 7, 8, 9, 1, 5]
puts quick_sort(arr).inspect
```

**Time**: O(n log n) average, O(n²) worst
**Space**: O(log n)
**Stable**: No

**Randomized Quick Sort** (Better average case):
```ruby
def quick_sort_randomized(arr, low = 0, high = arr.length - 1)
  if low < high
    pi = partition_randomized(arr, low, high)
    quick_sort_randomized(arr, low, pi - 1)
    quick_sort_randomized(arr, pi + 1, high)
  end
  arr
end

def partition_randomized(arr, low, high)
  # Random pivot
  random_index = rand(low..high)
  arr[random_index], arr[high] = arr[high], arr[random_index]

  partition(arr, low, high)
end
```

---

#### Heap Sort

**Algorithm**: Build max heap, extract max repeatedly

```ruby
def heap_sort(arr)
  n = arr.length

  # Build max heap
  ((n / 2) - 1).downto(0) do |i|
    heapify(arr, n, i)
  end

  # Extract elements one by one
  (n - 1).downto(1) do |i|
    arr[0], arr[i] = arr[i], arr[0]
    heapify(arr, i, 0)
  end

  arr
end

def heapify(arr, n, i)
  largest = i
  left = 2 * i + 1
  right = 2 * i + 2

  largest = left if left < n && arr[left] > arr[largest]
  largest = right if right < n && arr[right] > arr[largest]

  if largest != i
    arr[i], arr[largest] = arr[largest], arr[i]
    heapify(arr, n, largest)
  end
end

# Example
arr = [12, 11, 13, 5, 6, 7]
puts heap_sort(arr).inspect
```

**Time**: O(n log n) all cases
**Space**: O(1)
**Stable**: No

---

#### Counting Sort

**Algorithm**: Count occurrences, calculate positions

**Use Case**: Small range of integers

```ruby
def counting_sort(arr)
  return arr if arr.empty?

  max_val = arr.max
  min_val = arr.min
  range = max_val - min_val + 1

  count = Array.new(range, 0)
  output = Array.new(arr.length)

  # Count occurrences
  arr.each do |num|
    count[num - min_val] += 1
  end

  # Calculate cumulative count
  (1...range).each do |i|
    count[i] += count[i - 1]
  end

  # Build output array
  (arr.length - 1).downto(0) do |i|
    output[count[arr[i] - min_val] - 1] = arr[i]
    count[arr[i] - min_val] -= 1
  end

  output
end

# Example
arr = [4, 2, 2, 8, 3, 3, 1]
puts counting_sort(arr).inspect
```

**Time**: O(n + k) where k = range
**Space**: O(n + k)
**Stable**: Yes

---

#### Radix Sort

**Algorithm**: Sort digit by digit using counting sort

```ruby
def radix_sort(arr)
  return arr if arr.empty?

  max_val = arr.max
  exp = 1

  while max_val / exp > 0
    counting_sort_by_digit(arr, exp)
    exp *= 10
  end

  arr
end

def counting_sort_by_digit(arr, exp)
  n = arr.length
  output = Array.new(n)
  count = Array.new(10, 0)

  # Count occurrences
  arr.each do |num|
    index = (num / exp) % 10
    count[index] += 1
  end

  # Calculate cumulative count
  (1...10).each do |i|
    count[i] += count[i - 1]
  end

  # Build output array
  (n - 1).downto(0) do |i|
    index = (arr[i] / exp) % 10
    output[count[index] - 1] = arr[i]
    count[index] -= 1
  end

  # Copy to original array
  arr.replace(output)
end

# Example
arr = [170, 45, 75, 90, 802, 24, 2, 66]
puts radix_sort(arr).inspect
```

**Time**: O(d(n + k)) where d = digits, k = base
**Space**: O(n + k)
**Stable**: Yes

---

#### Bucket Sort

**Algorithm**: Distribute into buckets, sort buckets, concatenate

```ruby
def bucket_sort(arr, bucket_size = 5)
  return arr if arr.length <= 1

  min_val = arr.min
  max_val = arr.max

  bucket_count = ((max_val - min_val) / bucket_size).floor + 1
  buckets = Array.new(bucket_count) { [] }

  # Distribute into buckets
  arr.each do |num|
    index = ((num - min_val) / bucket_size).floor
    buckets[index] << num
  end

  # Sort each bucket and concatenate
  result = []
  buckets.each do |bucket|
    result.concat(bucket.sort)
  end

  result
end

# Example
arr = [0.897, 0.565, 0.656, 0.1234, 0.665, 0.3434]
puts bucket_sort(arr, 0.1).inspect
```

**Time**: O(n + k) average, O(n²) worst
**Space**: O(n + k)
**Stable**: Yes

---

#### Sorting Algorithms Comparison

| Algorithm | Best | Average | Worst | Space | Stable | In-Place |
|:----------|:-----|:--------|:------|:------|:-------|:---------|
| **Bubble** | O(n) | O(n²) | O(n²) | O(1) | Yes | Yes |
| **Selection** | O(n²) | O(n²) | O(n²) | O(1) | No | Yes |
| **Insertion** | O(n) | O(n²) | O(n²) | O(1) | Yes | Yes |
| **Merge** | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes | No |
| **Quick** | O(n log n) | O(n log n) | O(n²) | O(log n) | No | Yes |
| **Heap** | O(n log n) | O(n log n) | O(n log n) | O(1) | No | Yes |
| **Counting** | O(n + k) | O(n + k) | O(n + k) | O(k) | Yes | No |
| **Radix** | O(d(n + k)) | O(d(n + k)) | O(d(n + k)) | O(n + k) | Yes | No |
| **Bucket** | O(n + k) | O(n + k) | O(n²) | O(n) | Yes | No |

**When to Use**:

| Scenario | Algorithm | Reason |
|:---------|:----------|:-------|
| Small dataset | Insertion Sort | Simple, O(n) best case |
| Nearly sorted | Insertion Sort | O(n) for nearly sorted |
| Large dataset | Merge/Quick Sort | O(n log n) guaranteed |
| Memory constrained | Heap Sort | O(1) space |
| Stability required | Merge Sort | Stable O(n log n) |
| Integer range known | Counting/Radix | Linear time |
| Uniformly distributed | Bucket Sort | O(n) average |

---

## Part VI — String Algorithms

### 26. String Basics

#### Pattern Matching (Naive)

```ruby
def naive_pattern_search(text, pattern)
  n = text.length
  m = pattern.length
  positions = []

  (0..n - m).each do |i|
    j = 0

    while j < m && text[i + j] == pattern[j]
      j += 1
    end

    positions << i if j == m
  end

  positions
end

# Example
text = "AABAACAADAABAABA"
pattern = "AABA"
puts naive_pattern_search(text, pattern).inspect  # => [0, 9, 12]
```

**Time**: O(nm), **Space**: O(1)

---

#### Anagram Check

```ruby
def is_anagram?(s1, s2)
  return false if s1.length != s2.length

  s1.chars.sort == s2.chars.sort
end

# Hash-based (O(n))
def is_anagram_hash?(s1, s2)
  return false if s1.length != s2.length

  freq = Hash.new(0)

  s1.each_char { |c| freq[c] += 1 }
  s2.each_char { |c| freq[c] -= 1 }

  freq.values.all?(&:zero?)
end

# Example
puts is_anagram?("listen", "silent")  # => true
puts is_anagram?("hello", "world")    # => false
```

---

#### Longest Palindromic Substring

**Expand Around Center**:
```ruby
def longest_palindrome(s)
  return "" if s.empty?

  start = 0
  max_len = 0

  s.length.times do |i|
    # Odd length palindromes
    len1 = expand_around_center(s, i, i)
    # Even length palindromes
    len2 = expand_around_center(s, i, i + 1)

    len = [len1, len2].max

    if len > max_len
      max_len = len
      start = i - (len - 1) / 2
    end
  end

  s[start, max_len]
end

def expand_around_center(s, left, right)
  while left >= 0 && right < s.length && s[left] == s[right]
    left -= 1
    right += 1
  end

  right - left - 1
end

# Example
puts longest_palindrome("babad")  # => "bab" or "aba"
puts longest_palindrome("cbbd")   # => "bb"
```

**Time**: O(n²), **Space**: O(1)

---

### 27. Advanced String Algorithms

#### KMP (Knuth-Morris-Pratt) Algorithm

**Use Case**: Efficient pattern matching

**Algorithm**: Build LPS (Longest Proper Prefix which is also Suffix) array, use it to skip comparisons

```ruby
def kmp_search(text, pattern)
  n = text.length
  m = pattern.length

  lps = compute_lps(pattern)
  positions = []

  i = 0  # Index for text
  j = 0  # Index for pattern

  while i < n
    if pattern[j] == text[i]
      i += 1
      j += 1
    end

    if j == m
      positions << i - j
      j = lps[j - 1]
    elsif i < n && pattern[j] != text[i]
      if j != 0
        j = lps[j - 1]
      else
        i += 1
      end
    end
  end

  positions
end

def compute_lps(pattern)
  m = pattern.length
  lps = Array.new(m, 0)
  len = 0
  i = 1

  while i < m
    if pattern[i] == pattern[len]
      len += 1
      lps[i] = len
      i += 1
    else
      if len != 0
        len = lps[len - 1]
      else
        lps[i] = 0
        i += 1
      end
    end
  end

  lps
end

# Example
text = "ABABDABACDABABCABAB"
pattern = "ABABCABAB"
puts kmp_search(text, pattern).inspect  # => [10]

# LPS example
puts compute_lps("ABABCABAB").inspect  # => [0, 0, 1, 2, 0, 1, 2, 3, 4]
```

**Time**: O(n + m), **Space**: O(m)

---

#### Rabin-Karp Algorithm

**Use Case**: Multiple pattern matching using hashing

```ruby
def rabin_karp(text, pattern)
  n = text.length
  m = pattern.length
  d = 256  # Number of characters
  q = 101  # Prime number

  positions = []
  h = 1
  p = 0  # Hash value for pattern
  t = 0  # Hash value for text

  # Calculate h = d^(m-1) % q
  (m - 1).times { h = (h * d) % q }

  # Calculate initial hash values
  m.times do |i|
    p = (d * p + pattern[i].ord) % q
    t = (d * t + text[i].ord) % q
  end

  # Slide pattern over text
  (0..n - m).each do |i|
    # Check if hash values match
    if p == t
      # Verify character by character
      if text[i, m] == pattern
        positions << i
      end
    end

    # Calculate hash for next window
    if i < n - m
      t = (d * (t - text[i].ord * h) + text[i + m].ord) % q
      t += q if t < 0
    end
  end

  positions
end

# Example
text = "GEEKS FOR GEEKS"
pattern = "GEEK"
puts rabin_karp(text, pattern).inspect  # => [0, 10]
```

**Time**: O(n + m) average, O(nm) worst
**Space**: O(1)

---

#### Z-Algorithm

**Use Case**: Find all occurrences of pattern in linear time

```ruby
def z_algorithm(text, pattern)
  combined = pattern + "$" + text
  n = combined.length
  z = Array.new(n, 0)

  left = 0
  right = 0

  (1...n).each do |i|
    if i > right
      left = right = i
      while right < n && combined[right] == combined[right - left]
        right += 1
      end
      z[i] = right - left
      right -= 1
    else
      k = i - left
      if z[k] < right - i + 1
        z[i] = z[k]
      else
        left = i
        while right < n && combined[right] == combined[right - left]
          right += 1
        end
        z[i] = right - left
        right -= 1
      end
    end
  end

  # Find positions where z[i] == pattern.length
  positions = []
  m = pattern.length

  z.each_with_index do |val, i|
    positions << i - m - 1 if val == m
  end

  positions
end

# Example
text = "AABAACAADAABAABA"
pattern = "AABA"
puts z_algorithm(text, pattern).inspect  # => [0, 9, 12]
```

**Time**: O(n + m), **Space**: O(n + m)

---

#### Suffix Array

**Definition**: Sorted array of all suffixes of a string

```ruby
def build_suffix_array(text)
  n = text.length
  suffixes = []

  n.times do |i|
    suffixes << [text[i..-1], i]
  end

  suffixes.sort_by! { |suffix, _| suffix }
  suffixes.map { |_, index| index }
end

# Example
text = "banana"
suffix_array = build_suffix_array(text)
puts "Suffix Array: #{suffix_array.inspect}"
# => [5, 3, 1, 0, 4, 2]

puts "\nSuffixes in sorted order:"
suffix_array.each do |i|
  puts "#{i}: #{text[i..-1]}"
end
# 5: a
# 3: ana
# 1: anana
# 0: banana
# 4: na
# 2: nana
```

**Pattern Search using Suffix Array**:
```ruby
def search_with_suffix_array(text, pattern, suffix_array)
  n = text.length
  m = pattern.length

  # Binary search for pattern
  left = 0
  right = n - 1

  while left <= right
    mid = (left + right) / 2
    suffix = text[suffix_array[mid]..-1]

    if suffix.start_with?(pattern)
      return suffix_array[mid]
    elsif pattern < suffix[0, m]
      right = mid - 1
    else
      left = mid + 1
    end
  end

  -1
end

# Example
position = search_with_suffix_array(text, "ana", suffix_array)
puts "Pattern found at position: #{position}"  # => 1 or 3
```

**Time**: O(n² log n) naive, O(n log n) optimized
**Space**: O(n)

---

#### Longest Common Prefix (LCP) Array

**Definition**: LCP[i] = longest common prefix between suffix[i] and suffix[i-1]

```ruby
def build_lcp_array(text, suffix_array)
  n = text.length
  lcp = Array.new(n, 0)
  inv_suffix = Array.new(n)

  # Build inverse suffix array
  n.times do |i|
    inv_suffix[suffix_array[i]] = i
  end

  k = 0

  n.times do |i|
    if inv_suffix[i] == n - 1
      k = 0
      next
    end

    j = suffix_array[inv_suffix[i] + 1]

    while i + k < n && j + k < n && text[i + k] == text[j + k]
      k += 1
    end

    lcp[inv_suffix[i]] = k
    k = [k - 1, 0].max
  end

  lcp
end

# Example
lcp = build_lcp_array(text, suffix_array)
puts "LCP Array: #{lcp.inspect}"
```

---

#### Manacher's Algorithm

**Use Case**: Find longest palindromic substring in O(n)

```ruby
def manacher(s)
  # Transform string: "abc" -> "^#a#b#c#$"
  t = "^#" + s.chars.join("#") + "#$"
  n = t.length
  p = Array.new(n, 0)

  center = 0
  right = 0

  (1...n - 1).each do |i|
    mirror = 2 * center - i

    if i < right
      p[i] = [right - i, p[mirror]].min
    end

    # Expand around center i
    while t[i + p[i] + 1] == t[i - p[i] - 1]
      p[i] += 1
    end

    # Update center and right
    if i + p[i] > right
      center = i
      right = i + p[i]
    end
  end

  # Find maximum length
  max_len = 0
  center_index = 0

  p.each_with_index do |len, i|
    if len > max_len
      max_len = len
      center_index = i
    end
  end

  start = (center_index - max_len) / 2
  s[start, max_len]
end

# Example
puts manacher("babad")  # => "bab" or "aba"
puts manacher("cbbd")   # => "bb"
```

**Time**: O(n), **Space**: O(n)

---

#### String Algorithms Comparison

| Algorithm | Time | Space | Use Case |
|:----------|:-----|:------|:---------|
| **Naive** | O(nm) | O(1) | Simple, small strings |
| **KMP** | O(n + m) | O(m) | Single pattern matching |
| **Rabin-Karp** | O(n + m) avg | O(1) | Multiple patterns |
| **Z-Algorithm** | O(n + m) | O(n + m) | Pattern matching |
| **Suffix Array** | O(n² log n) | O(n) | Multiple queries |
| **Manacher** | O(n) | O(n) | Longest palindrome |

---

## Part VII — Mathematical & Special Algorithms

### 28. Number Theory

#### Sieve of Eratosthenes

**Problem**: Find all primes up to n

```ruby
def sieve_of_eratosthenes(n)
  return [] if n < 2

  is_prime = Array.new(n + 1, true)
  is_prime[0] = is_prime[1] = false

  (2..Math.sqrt(n).to_i).each do |i|
    if is_prime[i]
      (i * i..n).step(i) do |j|
        is_prime[j] = false
      end
    end
  end

  (2..n).select { |i| is_prime[i] }
end

# Example
puts sieve_of_eratosthenes(30).inspect
# => [2, 3, 5, 7, 11, 13, 17, 19, 23, 29]
```

**Time**: O(n log log n), **Space**: O(n)

---

#### GCD (Euclidean Algorithm)

```ruby
def gcd(a, b)
  while b != 0
    a, b = b, a % b
  end
  a
end

# Recursive
def gcd_recursive(a, b)
  return a if b == 0
  gcd_recursive(b, a % b)
end

# LCM
def lcm(a, b)
  (a * b) / gcd(a, b)
end

# Example
puts gcd(48, 18)  # => 6
puts lcm(12, 18)  # => 36
```

**Time**: O(log min(a, b)), **Space**: O(1)

---

#### Modular Arithmetic

**Modular Exponentiation**:
```ruby
def mod_exp(base, exp, mod)
  result = 1
  base = base % mod

  while exp > 0
    if exp.odd?
      result = (result * base) % mod
    end

    exp >>= 1
    base = (base * base) % mod
  end

  result
end

# Example
puts mod_exp(2, 10, 1000)  # => 24 (2^10 % 1000)
```

**Time**: O(log exp), **Space**: O(1)

---

#### Prime Factorization

```ruby
def prime_factors(n)
  factors = []

  # Check for 2
  while n % 2 == 0
    factors << 2
    n /= 2
  end

  # Check odd numbers
  i = 3
  while i * i <= n
    while n % i == 0
      factors << i
      n /= i
    end
    i += 2
  end

  factors << n if n > 2

  factors
end

# Example
puts prime_factors(315).inspect  # => [3, 3, 5, 7]
```

**Time**: O(√n), **Space**: O(log n)

---

#### Fibonacci (Matrix Exponentiation)

**Fast Fibonacci** - O(log n):
```ruby
def fib_matrix(n)
  return n if n <= 1

  matrix = [[1, 1], [1, 0]]
  result = matrix_power(matrix, n - 1)
  result[0][0]
end

def matrix_power(matrix, n)
  return [[1, 0], [0, 1]] if n == 0
  return matrix if n == 1

  if n.even?
    half = matrix_power(matrix, n / 2)
    matrix_multiply(half, half)
  else
    matrix_multiply(matrix, matrix_power(matrix, n - 1))
  end
end

def matrix_multiply(a, b)
  [
    [a[0][0] * b[0][0] + a[0][1] * b[1][0], a[0][0] * b[0][1] + a[0][1] * b[1][1]],
    [a[1][0] * b[0][0] + a[1][1] * b[1][0], a[1][0] * b[0][1] + a[1][1] * b[1][1]]
  ]
end

# Example
puts fib_matrix(10)  # => 55
```

---

### 29. Computational Geometry

#### Convex Hull (Graham Scan)

**Problem**: Find smallest convex polygon containing all points

```ruby
def convex_hull(points)
  return points if points.length < 3

  # Find bottom-most point (or left-most if tie)
  start = points.min_by { |p| [p[1], p[0]] }

  # Sort by polar angle
  sorted = points.sort_by do |p|
    next -Float::INFINITY if p == start
    Math.atan2(p[1] - start[1], p[0] - start[0])
  end

  hull = [sorted[0], sorted[1]]

  (2...sorted.length).each do |i|
    while hull.length > 1 && ccw(hull[-2], hull[-1], sorted[i]) <= 0
      hull.pop
    end
    hull.push(sorted[i])
  end

  hull
end

def ccw(p1, p2, p3)
  (p2[0] - p1[0]) * (p3[1] - p1[1]) - (p2[1] - p1[1]) * (p3[0] - p1[0])
end

# Example
points = [[0, 3], [1, 1], [2, 2], [4, 4], [0, 0], [1, 2], [3, 1], [3, 3]]
hull = convex_hull(points)
puts "Convex Hull: #{hull.inspect}"
```

**Time**: O(n log n), **Space**: O(n)

---

#### Line Intersection

**Check if two line segments intersect**:
```ruby
def segments_intersect?(p1, q1, p2, q2)
  o1 = orientation(p1, q1, p2)
  o2 = orientation(p1, q1, q2)
  o3 = orientation(p2, q2, p1)
  o4 = orientation(p2, q2, q1)

  # General case
  return true if o1 != o2 && o3 != o4

  # Special cases (collinear)
  return true if o1 == 0 && on_segment?(p1, p2, q1)
  return true if o2 == 0 && on_segment?(p1, q2, q1)
  return true if o3 == 0 && on_segment?(p2, p1, q2)
  return true if o4 == 0 && on_segment?(p2, q1, q2)

  false
end

def orientation(p, q, r)
  val = (q[1] - p[1]) * (r[0] - q[0]) - (q[0] - p[0]) * (r[1] - q[1])
  return 0 if val == 0  # Collinear
  val > 0 ? 1 : 2  # Clockwise or Counterclockwise
end

def on_segment?(p, q, r)
  q[0] <= [p[0], r[0]].max && q[0] >= [p[0], r[0]].min &&
  q[1] <= [p[1], r[1]].max && q[1] >= [p[1], r[1]].min
end

# Example
p1 = [1, 1]
q1 = [10, 1]
p2 = [1, 2]
q2 = [10, 2]
puts segments_intersect?(p1, q1, p2, q2)  # => false
```

---

## Part VIII — Complexity & Theory

### 30. Complexity Classes

#### P, NP, NP-Complete, NP-Hard

**Definitions**:

**P (Polynomial Time)**:
- Problems solvable in polynomial time
- Examples: Sorting, Searching, Shortest Path

**NP (Nondeterministic Polynomial)**:
- Problems verifiable in polynomial time
- Solution can be checked quickly
- Examples: Subset Sum, Graph Coloring

**NP-Complete**:
- Hardest problems in NP
- If any NP-Complete problem has polynomial solution, P = NP
- Examples: SAT, Traveling Salesman, Knapsack

**NP-Hard**:
- At least as hard as NP-Complete
- May not be in NP
- Examples: Halting Problem, Optimization versions

**Relationship**:
```
        NP-Hard
           |
    ┌──────┴──────┐
    |             |
NP-Complete      |
    |             |
    └─────┬───────┘
          |
         NP
          |
          P
```

---

#### Traveling Salesman Problem (TSP)

**Brute Force** - O(n!):
```ruby
def tsp_brute_force(graph)
  n = graph.length
  vertices = (1...n).to_a
  min_path = Float::INFINITY

  vertices.permutation.each do |perm|
    current_path = 0
    k = 0

    perm.each do |i|
      current_path += graph[k][i]
      k = i
    end

    current_path += graph[k][0]
    min_path = [min_path, current_path].min
  end

  min_path
end

# Example
graph = [
  [0, 10, 15, 20],
  [10, 0, 35, 25],
  [15, 35, 0, 30],
  [20, 25, 30, 0]
]
puts tsp_brute_force(graph)  # => 80
```

**Dynamic Programming** - O(n² 2^n):
```ruby
def tsp_dp(graph)
  n = graph.length
  all_visited = (1 << n) - 1
  memo = {}

  def tsp_helper(graph, mask, pos, memo, n)
    return graph[pos][0] if mask == (1 << n) - 1

    key = [mask, pos]
    return memo[key] if memo[key]

    ans = Float::INFINITY

    n.times do |city|
      if (mask & (1 << city)) == 0
        new_ans = graph[pos][city] + tsp_helper(graph, mask | (1 << city), city, memo, n)
        ans = [ans, new_ans].min
      end
    end

    memo[key] = ans
  end

  tsp_helper(graph, 1, 0, memo, n)
end
```

---

## Part IX — Practical Patterns & System-Level Data Structures

### 31. Problem-Solving Patterns

#### Two Pointers

**Use Cases**: Sorted arrays, linked lists, palindromes

**Examples**:

**Pair with Target Sum**:
```ruby
def two_sum_sorted(arr, target)
  left = 0
  right = arr.length - 1

  while left < right
    sum = arr[left] + arr[right]

    return [left, right] if sum == target

    if sum < target
      left += 1
    else
      right -= 1
    end
  end

  nil
end
```

**Remove Duplicates**:
```ruby
def remove_duplicates(arr)
  return 0 if arr.empty?

  i = 0

  (1...arr.length).each do |j|
    if arr[j] != arr[i]
      i += 1
      arr[i] = arr[j]
    end
  end

  i + 1
end
```

---

#### Sliding Window

**Fixed Size Window**:
```ruby
def max_sum_subarray(arr, k)
  return nil if arr.length < k

  window_sum = arr[0...k].sum
  max_sum = window_sum

  (k...arr.length).each do |i|
    window_sum = window_sum - arr[i - k] + arr[i]
    max_sum = [max_sum, window_sum].max
  end

  max_sum
end
```

**Variable Size Window**:
```ruby
def longest_substring_k_distinct(s, k)
  return 0 if s.empty? || k == 0

  char_freq = Hash.new(0)
  max_length = 0
  window_start = 0

  s.each_char.with_index do |char, window_end|
    char_freq[char] += 1

    while char_freq.length > k
      left_char = s[window_start]
      char_freq[left_char] -= 1
      char_freq.delete(left_char) if char_freq[left_char] == 0
      window_start += 1
    end

    max_length = [max_length, window_end - window_start + 1].max
  end

  max_length
end
```

---

#### Fast & Slow Pointers

**Cycle Detection**:
```ruby
def has_cycle?(head)
  return false if head.nil?

  slow = head
  fast = head

  while fast && fast.next
    slow = slow.next
    fast = fast.next.next

    return true if slow == fast
  end

  false
end
```

**Find Cycle Start**:
```ruby
def find_cycle_start(head)
  slow = head
  fast = head

  # Find meeting point
  while fast && fast.next
    slow = slow.next
    fast = fast.next.next
    break if slow == fast
  end

  return nil unless fast && fast.next

  # Find start of cycle
  slow = head
  while slow != fast
    slow = slow.next
    fast = fast.next
  end

  slow
end
```

---

### 32. System-Level Data Structures

#### LRU Cache

**Implementation using Hash + Doubly Linked List**:
```ruby
class LRUNode
  attr_accessor :key, :value, :prev, :next

  def initialize(key, value)
    @key = key
    @value = value
    @prev = nil
    @next = nil
  end
end

class LRUCache
  def initialize(capacity)
    @capacity = capacity
    @cache = {}
    @head = LRUNode.new(0, 0)
    @tail = LRUNode.new(0, 0)
    @head.next = @tail
    @tail.prev = @head
  end

  def get(key)
    return -1 unless @cache[key]

    node = @cache[key]
    remove_node(node)
    add_to_head(node)
    node.value
  end

  def put(key, value)
    if @cache[key]
      node = @cache[key]
      node.value = value
      remove_node(node)
      add_to_head(node)
    else
      node = LRUNode.new(key, value)
      @cache[key] = node
      add_to_head(node)

      if @cache.size > @capacity
        lru = @tail.prev
        remove_node(lru)
        @cache.delete(lru.key)
      end
    end
  end

  private

  def add_to_head(node)
    node.next = @head.next
    node.prev = @head
    @head.next.prev = node
    @head.next = node
  end

  def remove_node(node)
    node.prev.next = node.next
    node.next.prev = node.prev
  end
end

# Example
cache = LRUCache.new(2)
cache.put(1, 1)
cache.put(2, 2)
puts cache.get(1)     # => 1
cache.put(3, 3)       # Evicts key 2
puts cache.get(2)     # => -1 (not found)
cache.put(4, 4)       # Evicts key 1
puts cache.get(1)     # => -1 (not found)
puts cache.get(3)     # => 3
puts cache.get(4)     # => 4
```

---

#### LFU Cache

**Least Frequently Used Cache**:
```ruby
class LFUCache
  def initialize(capacity)
    @capacity = capacity
    @min_freq = 0
    @key_to_val = {}
    @key_to_freq = {}
    @freq_to_keys = Hash.new { |h, k| h[k] = [] }
  end

  def get(key)
    return -1 unless @key_to_val[key]

    update_freq(key)
    @key_to_val[key]
  end

  def put(key, value)
    return if @capacity <= 0

    if @key_to_val[key]
      @key_to_val[key] = value
      update_freq(key)
      return
    end

    if @key_to_val.size >= @capacity
      evict
    end

    @key_to_val[key] = value
    @key_to_freq[key] = 1
    @freq_to_keys[1] << key
    @min_freq = 1
  end

  private

  def update_freq(key)
    freq = @key_to_freq[key]
    @key_to_freq[key] = freq + 1

    @freq_to_keys[freq].delete(key)
    @freq_to_keys[freq + 1] << key

    if @freq_to_keys[freq].empty? && freq == @min_freq
      @min_freq += 1
    end
  end

  def evict
    key = @freq_to_keys[@min_freq].shift
    @key_to_val.delete(key)
    @key_to_freq.delete(key)
  end
end
```

---

#### Consistent Hashing

**Use Case**: Distributed systems, load balancing

```ruby
class ConsistentHash
  def initialize(replicas = 3)
    @replicas = replicas
    @ring = {}
    @sorted_keys = []
  end

  def add_node(node)
    @replicas.times do |i|
      key = hash_key("#{node}:#{i}")
      @ring[key] = node
      @sorted_keys << key
    end
    @sorted_keys.sort!
  end

  def remove_node(node)
    @replicas.times do |i|
      key = hash_key("#{node}:#{i}")
      @ring.delete(key)
      @sorted_keys.delete(key)
    end
  end

  def get_node(key)
    return nil if @ring.empty?

    hash = hash_key(key)

    # Binary search for first node >= hash
    idx = @sorted_keys.bsearch_index { |k| k >= hash }
    idx ||= 0

    @ring[@sorted_keys[idx]]
  end

  private

  def hash_key(key)
    key.hash % (2**32)
  end
end

# Example
ch = ConsistentHash.new(3)
ch.add_node("server1")
ch.add_node("server2")
ch.add_node("server3")

puts ch.get_node("user123")  # => server2 (example)
puts ch.get_node("user456")  # => server1 (example)
```

---

#### Bloom Filter

**Use Case**: Membership testing with false positives allowed

```ruby
class BloomFilter
  def initialize(size, num_hashes)
    @size = size
    @num_hashes = num_hashes
    @bit_array = Array.new(size, false)
  end

  def add(item)
    @num_hashes.times do |i|
      index = hash(item, i) % @size
      @bit_array[index] = true
    end
  end

  def contains?(item)
    @num_hashes.times do |i|
      index = hash(item, i) % @size
      return false unless @bit_array[index]
    end
    true
  end

  private

  def hash(item, seed)
    (item.hash + seed * 31) % @size
  end
end

# Example
bf = BloomFilter.new(100, 3)
bf.add("apple")
bf.add("banana")

puts bf.contains?("apple")   # => true
puts bf.contains?("orange")  # => false (probably)
```

---

## Conclusion

This comprehensive Data Structures & Algorithms guide covers:

✅ **Part 0**: Foundations (Mathematical, Algorithm Analysis, Memory Models)
✅ **Part I**: Core Data Structures (Arrays, Linked Lists, Stack, Queue, Hashing)
✅ **Part II**: Trees (Binary Trees, BST, AVL, Red-Black, B-Trees, Heaps, Trie, Segment Tree, Fenwick Tree)
✅ **Part III**: Graphs (BFS/DFS, Shortest Paths, MST, Topological Sort, SCC, Network Flow)
✅ **Part IV**: Algorithm Paradigms (Divide & Conquer, Greedy, DP, Backtracking, Recursion)
✅ **Part V**: Searching & Sorting (All major algorithms with comparisons)
✅ **Part VI**: String Algorithms (KMP, Rabin-Karp, Z-Algorithm, Suffix Array, Manacher)
✅ **Part VII**: Mathematical Algorithms (Number Theory, Computational Geometry)
✅ **Part VIII**: Complexity Theory (P, NP, NP-Complete, TSP)
✅ **Part IX**: Practical Patterns (Two Pointers, Sliding Window, Fast & Slow Pointers, LRU/LFU Cache, Consistent Hashing, Bloom Filter)

---

