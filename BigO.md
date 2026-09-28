# Big O Notation

Sequence-wise notes: read 1 → 13 in order, then repeat the practice loop at the end.

**Study sequence**

1. [What Big O measures](#s1)
2. [Formal definition](#s2)
3. [O, Ω, Θ and cases](#s3)
4. [Growth-rate hierarchy](#s4)
5. [Simplification rules](#s5)
6. [Analysing loops](#s6)
7. [Analysing recursion](#s7)
8. [Amortized analysis](#s8)
9. [Space complexity](#s9)
10. [Reference tables](#s10)
11. [Input size → complexity](#s11)
12. [Common pitfalls](#s12)
13. [Practice with answers](#s13)

## **1**What Big O measures

Big O describes how the work (time) or memory (space) of an algorithm *grows* as the input size `n` grows. It counts basic operations, not seconds, so it is independent of hardware and language.

- It is an **upper bound on growth rate** for large `n`.
- It ignores constant factors and lower-order terms: `3n² + 5n + 2` grows like `n²`.
- Always state what `n` is (array length, number of nodes, digits, ...).

## **2**Formal definition

`f(n) = O(g(n))` if there exist constants `c > 0` and `n₀` such that `0 ≤ f(n) ≤ c·g(n)` for all `n ≥ n₀`.

```
Prove 3n² + 5n + 2 = O(n²)
For n ≥ 1:  5n ≤ 5n²  and  2 ≤ 2n²
So 3n² + 5n + 2 ≤ 3n² + 5n² + 2n² = 10n²
Choose c = 10, n₀ = 1.  Done.
```

Proof recipe: bound every term by the dominant term, add the coefficients to get `c`, then pick `n₀` where the bounds hold.

That function is also `O(n³)`, which is true but loose. Always give the **tightest** bound you can prove.

## **3**O, Ω, Θ and cases

| Symbol | Meaning | Analogy |
| --- | --- | --- |
| `O(g)` | Upper bound: grows no faster than g | ≤ |
| `Ω(g)` | Lower bound: grows at least as fast as g | ≥ |
| `Θ(g)` | Tight bound: both O(g) and Ω(g) | = |
| `o(g)` | Strictly slower than g | \< |
| `ω(g)` | Strictly faster than g | > |

**Bound and case are different things.** A case is an input scenario (best, average, worst). A bound (O, Ω, Θ) is a function class. You can put any bound on any case.

```
Linear search
best case  (target at index 0): Θ(1)
worst case (absent):            Θ(n)
Whole algorithm:                O(n), Ω(1)
```

In interviews "the complexity" normally means the tight *worst-case* bound, unless you are told average or amortized.

## **4**Growth-rate hierarchy

`1 < log n < √n < n < n log n < n² < n³ < 2ⁿ < n! < nⁿ`

| Class | Typical example | Ops at n = 1000 |
| --- | --- | --- |
| O(1) | array index, hash lookup (avg) | 1 |
| O(log n) | binary search | ≈ 10 |
| O(√n) | trial-division primality | ≈ 32 |
| O(n) | single scan | 10³ |
| O(n log n) | merge sort | ≈ 10⁴ |
| O(n²) | nested loops, bubble sort | 10⁶ |
| O(n³) | naive matrix multiply | 10⁹ |
| O(2ⁿ) | all subsets | ≈ 10³⁰¹ |
| O(n!) | all permutations | ≈ 10²⁵⁶⁷ |

Any polynomial beats any exponential eventually, and any power of `log n` loses to any positive power of `n`.

## **5**Simplification rules

1. **Drop constants:** `O(5n) = O(n)`.
2. **Drop lower-order terms:** `O(n² + n) = O(n²)`.
3. **Sequential steps add, keep the max:** `O(n) + O(n²) = O(n²)`.
4. **Nested steps multiply:** a loop of `n` around a loop of `m` is `O(n·m)`.
5. **Different inputs, different variables:** two arrays give `O(a + b)` or `O(a·b)`, never `O(n)`.
6. **Log bases don't matter:** `log₂ n = log₁₀ n / log₁₀ 2`, a constant factor.
7. **Calls cost what they cost:** a library call inside a loop (sort, slice, `in` on a list) multiplies in its own complexity.

## **6**Analysing loops

Ask two questions for each loop: how many iterations, and how much work per iteration.

```
for i in range(n): ...                     # O(n)

for i in range(n):
    for j in range(n): ...                 # O(n²)

for i in range(n):
    for j in range(i): ...                 # 0+1+...+(n-1) = n(n-1)/2 → O(n²)

i = 1
while i < n: i *= 2                       # doubles each time → O(log n)

for i in range(n):
    j = 1
    while j < n: j *= 2                   # n × log n → O(n log n)

i = 1
while i * i <= n: i += 1                  # O(√n)

for i in range(1, n + 1):
    for j in range(i, n + 1, i): ...       # n/1 + n/2 + ... + n/n = n·Hₙ → O(n log n)
```

Sums to remember: `1+2+...+n = n(n+1)/2` (quadratic), `1+2+4+...+n = 2n-1` (linear), `1+1/2+...+1/n ≈ ln n` (harmonic).

## **7**Analysing recursion

Write the recurrence, then solve it by unrolling, by a recursion tree (levels × work per level), or by the Master theorem.

| Recurrence | Result | Example |
| --- | --- | --- |
| T(n) = T(n−1) + O(1) | O(n) | recursive factorial |
| T(n) = T(n−1) + O(n) | O(n²) | recursive selection sort |
| T(n) = 2T(n−1) + O(1) | O(2ⁿ) | naive Fibonacci (tight: O(φⁿ)) |
| T(n) = T(n/2) + O(1) | O(log n) | binary search |
| T(n) = T(n/2) + O(n) | O(n) | quickselect (average) |
| T(n) = 2T(n/2) + O(1) | O(n) | tree traversal |
| T(n) = 2T(n/2) + O(n) | O(n log n) | merge sort |

**Master theorem.** For `T(n) = a·T(n/b) + f(n)` with `a ≥ 1, b > 1`, let `c = log_b a` and compare `f(n)` with `n^c`:

- **Case 1:** `f(n) = O(n^(c−ε))` → `Θ(n^c)` (leaves dominate).
- **Case 2:** `f(n) = Θ(n^c · log^k n)` → `Θ(n^c · log^(k+1) n)` (all levels equal; k = 0 gives an extra log factor).
- **Case 3:** `f(n) = Ω(n^(c+ε))` and `a·f(n/b) ≤ k·f(n)` for some k \< 1 → `Θ(f(n))` (root dominates).

Merge sort: a = 2, b = 2, c = 1, f(n) = n = n^c, so Case 2 gives `Θ(n log n)`. The Master theorem does not cover unequal splits like `T(n−1)` or non-polynomial gaps; use the tree method there.

## **8**Amortized analysis

Amortized cost is the average cost per operation over a worst-case *sequence*. There is no probability involved, unlike average-case analysis.

Dynamic array append: one append can cost `O(n)` when the array doubles, but across `n` appends the copies total `1 + 2 + 4 + ... + n < 2n`. Total work is under `3n`, so each append is `O(1)` amortized.

Same idea in sliding window and two-pointer loops: an inner `while` that never resets moves each pointer at most `n` times, so the whole loop is `O(n)`, not `O(n²)`.

## **9**Space complexity

Count **auxiliary** memory (extra space beyond the input) and include the **recursion stack**.

| Case | Space |
| --- | --- |
| Iterative sum over an array | O(1) |
| Recursive sum (depth n) | O(n) stack |
| Merge sort | O(n) buffer |
| Quicksort | O(log n) stack average, O(n) worst |
| DFS / BFS on a graph | O(V) |
| DP table n × m | O(n·m), or O(m) with a rolling row |

## **10**Reference tables

| Structure / algorithm | Operation | Complexity |
| --- | --- | --- |
| Array | access / search / insert middle / append | O(1) / O(n) / O(n) / O(1) amortized |
| Linked list | search / insert at known node | O(n) / O(1) |
| Hash table | insert, lookup, delete | O(1) average, O(n) worst |
| Balanced BST | insert, search, delete | O(log n); O(n) if unbalanced |
| Binary heap | push, pop / peek / build | O(log n) / O(1) / O(n) |
| Binary search | on sorted array | O(log n) |
| Merge sort | all cases | O(n log n), O(n) space |
| Quicksort | average / worst | O(n log n) / O(n²) |
| Heap sort | all cases, in place | O(n log n) |
| Insertion sort | best / worst | O(n) / O(n²) |
| Counting sort | keys in range k | O(n + k) |
| BFS, DFS, topological sort | graph with V, E | O(V + E) |
| Dijkstra (binary heap) | shortest paths | O((V + E) log V) |
| Bellman–Ford / Floyd–Warshall | shortest paths | O(V·E) / O(V³) |

Any comparison-based sort needs `Ω(n log n)` comparisons in the worst case.

## **11**Input size → target complexity

Rule of thumb: about 10⁸ simple operations per second in C++/Java, closer to 10⁷ in Python. Read the constraint, then pick the complexity that fits.

| Constraint on n | Aim for |
| --- | --- |
| n ≤ 10–11 | O(n!) |
| n ≤ 20–25 | O(2ⁿ) |
| n ≤ 500 | O(n³) |
| n ≤ 5,000 | O(n²) |
| n ≤ 10⁵–10⁶ | O(n log n) |
| n ≤ 10⁷–10⁸ | O(n) |
| n larger, or n up to 10¹⁸ | O(log n) or O(1) |

## **12**Common pitfalls

- **Big O is not "worst case".** See section 3.
- **Nested loops are not automatically O(n²).** Check the bounds: `j` may halve, or the inner loop may be amortized.
- **Hidden costs:** `x in list` is O(n); `list.insert(0, x)` and `pop(0)` are O(n); slicing copies O(k); repeated `s += t` can be O(n²); `sorted()` inside a loop multiplies by `n log n`.
- **String comparison costs length.** Sorting `n` strings of length `L` is `O(L · n log n)`.
- **Memoization:** complexity = (number of distinct states) × (work per state). Memoized Fibonacci is `O(n)`.
- **Pseudo-polynomial time:** trial-division primality is `O(√n)` in the *value* n, but exponential in the number of bits. Knapsack's `O(n·W)` has the same issue.
- **Constants still matter for small n.** An O(n²) insertion sort can beat O(n log n) sorts on tiny arrays.
- **Hash tables are O(1) on average only,** assuming a good hash function.

## **13**Practice with answers

Work each one on paper first, then open the answer.

1\. Three nested loops: `n`, `n`, then a fixed `10`

O(10·n²) = **O(n²)**.

2\. `while n > 0: n //= 3`

**O(log n)**; the base 3 is a constant factor.

3\. `for i in range(1, n): for j in range(1, n, i)`

Inner runs about n/i times: n·Hₙ = **O(n log n)**.

4\. `f(n)` calls `f(n/2)` twice and does an O(n) loop

T(n) = 2T(n/2) + n → **O(n log n)**.

5\. `f(n)` calls `f(n−1)` twice, O(1) extra work

T(n) = 2T(n−1) + 1 → **O(2ⁿ)**.

6\. Build a set from `n` items, then answer `m` membership queries

**O(n + m)** average.

7\. `for i in range(n): sorted(arr)` where `len(arr) = n`

n × n log n = **O(n² log n)**.

8\. Recursive DFS on a path-shaped tree of n nodes: time and space?

Time **O(n)**, space **O(n)** for the recursion stack (O(h) in general).

**Mastery loop:** before running any code you write, state its time and space complexity in terms of named variables, then justify it in one sentence. Do this for 20 loop problems and 10 recurrences and the notation becomes automatic.
