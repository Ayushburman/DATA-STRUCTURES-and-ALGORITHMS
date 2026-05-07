# ALGORITHMS & COMPUTATION

```bash
MIT OpenCourseWare — 6.006 Introduction to Algorithms
Step-by-step notes with diagrams and visual understanding
```

---

# TOPICS COVERED

```bash
- Problem Solving
- Correctness Proofs
- Asymptotic Analysis
- Complexity Classes
- Data Structures
- Word-RAM Model
```

---

# WHAT IS AN ALGORITHM?

```bash
> The best definition of an algorithm is:

A well-defined, step-by-step computational procedure
that takes an input (or set of inputs),
processes it,
and produces an output to solve a given problem.
```

---

# ALGORITHM AS A RECIPE

```bash
An algorithm behaves like a recipe:

Input  → Processing Steps → Output

Same input
+
Same steps
=
Same output
```

---

# EXAMPLE

```bash
Problem:
Find the largest number.

Input:
[3, 8, 2, 10, 5]

Algorithm:
1. Assume first number is largest
2. Compare with next number
3. Replace if bigger found
4. Repeat until end

Output:
10
```

---

# CORE IDEA

```bash
Algorithms are NOT just code.

Algorithms are:

- logical problem solving
- mathematical reasoning
- correctness proofs
- efficiency analysis
- communication
```

---

# WHAT BEGINNERS THINK

```bash
Algorithms = writing code
```

---

# WHAT COMPUTER SCIENCE ACTUALLY DEMANDS

```bash
Problem Solving
+
Correctness Proofs
+
Efficiency Analysis
+
Human Communication
```

---

# FULL COMPUTATIONAL WORKFLOW

```bash
Problem
   ↓
Thinking
   ↓
Algorithm
   ↓
Proof of Correctness
   ↓
Efficiency Analysis
   ↓
Implementation (Code)
```

---

# FORMAL PROPERTIES OF AN ALGORITHM

---

## 1. PRECISION & CLARITY

```bash
Each step must be:

- clear
- specific
- unambiguous
```

Bad Example:

```bash
"Do something smart"
```

Good Example:

```bash
"Compare adjacent numbers and swap if needed"
```

---

## 2. CORRECTNESS

```bash
An algorithm is correct if:

For EVERY valid input,
it produces the correct output.
```

Not:

```bash
"Works on examples I tested"
```

---

## 3. FINITENESS

```bash
An algorithm must terminate.

It cannot run forever.
```

Example of BAD algorithm:

```bash
while(true)
{
    // infinite loop
}
```

---

## 4. PREDICTABILITY

```bash
Same Input
+
Same Algorithm
=
Same Output
```

Always deterministic.

---

# ALGORITHM VS PROGRAM

```bash
Algorithm:
Abstract logic/design.

Program:
Concrete implementation in a programming language.
```

---

# EXAMPLE

```bash
Algorithm:
Sort numbers using comparisons and swaps.

Program:
Bubble Sort written in C or Python.
```

---

# WHY ALGORITHMS MATTER

```bash
Fast hardware alone is NOT enough.

Efficient algorithms are equally important.
```

---

# EXAMPLE

```bash
Bad Algorithm + Supercomputer
may still fail at huge scale.

Good Algorithm + Normal Computer
can outperform it.
```

---

# WHAT IS A COMPUTATIONAL PROBLEM?

```bash
A computational problem is:

A clearly defined task that can be solved
using an algorithm and executed by a computer.
```

---

# INPUT AND OUTPUT

```bash
Input  = data given to solve the problem
Output = final processed result
```

---

# EXAMPLE

```bash
Input:
[5, 1, 9, 3]

Problem:
Sort numbers

Output:
[1, 3, 5, 9]
```

---

# VISUAL REPRESENTATION

```bash
INPUT ─────► PROBLEM ─────► VALID OUTPUT
```

---

# IMPORTANT UNDERSTANDING

```bash
Problem = WHAT to solve
Algorithm = HOW to solve
```

---

# BINARY RELATION

```bash
A problem is formally:

A binary relation between inputs and outputs.
```

Meaning:

```bash
Each input maps to a set of allowed outputs.
```

---

# EXAMPLE

```bash
Input:
[3,1,2]

Valid Output:
[1,2,3] ✔

Invalid Output:
[3,1,2] ✘
```

---

# PREDICATE (CHECKER)

```bash
A predicate checks whether an output is valid.
```

Example:

```bash
is_sorted(output)
```

Returns:

```bash
TRUE  → correctly sorted
FALSE → incorrect
```

---

# ARBITRARY INPUT SIZE

```bash
A real algorithm must work for:

10 inputs
1000 inputs
10^6 inputs
10^12 inputs
```

NOT just tiny examples.

---

# SCALABILITY

```bash
Algorithms must remain correct
even when input becomes massive.
```

---

# DETERMINISTIC ALGORITHMS

```bash
Deterministic means:

Same input
+
Same steps
=
Same output
```

Always predictable.

---

# MATHEMATICAL VIEW

```bash
Algorithm behaves like a function:

f(input) = output
```

Output must satisfy problem constraints.

---

# BIRTHDAY PROBLEM

```bash
Goal:
Determine whether two people share the same birthday.
```

---

# ❌ NAIVE APPROACH — O(n²)

```bash
Compare everyone with everyone.

A vs B
A vs C
A vs D
B vs C
...
```

Very slow for large n.

---

# ✓ BETTER APPROACH — O(n)

```bash
Maintain a record of birthdays already seen.

For each new person:
1. Check record
2. If found → MATCH
3. Else → add to record
```

---

# STEP-BY-STEP EXAMPLE

```bash
Student 1:
Birthday = Jan 5
Record = {}

Not found → Add

Record = {Jan 5}
```

---

```bash
Student 2:
Birthday = Mar 2
Record = {Jan 5}

Not found → Add

Record = {Jan 5, Mar 2}
```

---

```bash
Student 3:
Birthday = Jan 5
Record = {Jan 5, Mar 2}

MATCH FOUND ✓
```

---

# FLOW

```bash
Read birthday
      ↓
Already exists?
   ↓        ↓
 YES        NO
 ↓           ↓
MATCH      Add to record
```

---

# KEY INSIGHT

```bash
Data structures improve efficiency.

O(n²) → O(n)
```

---

# PROVING CORRECTNESS

```bash
Testing examples is NOT enough.

We must prove algorithms work
for ALL valid inputs.
```

---

# MATHEMATICAL INDUCTION

---

## BASE CASE

```bash
Prove smallest case works.
```

---

## INDUCTIVE HYPOTHESIS

```bash
Assume algorithm works for size K.
```

---

## INDUCTIVE STEP

```bash
Prove:
If it works for K,
it also works for K+1.
```

---

# EFFICIENCY ANALYSIS

```bash
Wrong Question:
"How many seconds?"

Correct Question:
"How many operations?"
```

---

# WHY SECONDS ARE WRONG

```bash
Seconds depend on:

- CPU speed
- RAM
- hardware
- operating system
```

Not purely algorithm quality.

---

# WHAT COMPUTER SCIENCE COUNTS

```bash
Operations:

- comparisons
- additions
- swaps
- memory accesses
```

---

# INPUT SIZE (n)

```bash
n = amount of input
```

Examples:

```bash
Sorting → number of elements
Graphs  → number of nodes
```

---

# BUBBLE SORT GROWTH

```bash
n = 10
operations ≈ 10² = 100
```

---

```bash
n = 1000
operations ≈ 1000² = 1,000,000
```

---

```bash
n = 1,000,000
operations ≈ (10^6)^2 = 10^12
```

Explodes rapidly.

---

# CORE IDEA

```bash
Hardware changes.

Algorithmic growth laws do NOT.
```

---

# ASYMPTOTIC ANALYSIS

```bash
Studies how operations grow
as n becomes huge.
```

---

# BIG-O NOTATION

```bash
O(f(n))

Upper bound:
Algorithm grows no worse than f(n)
```

---

# OMEGA NOTATION

```bash
Ω(f(n))

Lower bound:
Algorithm needs at least f(n) work
```

---

# THETA NOTATION

```bash
Θ(f(n))

Tight bound:
Upper bound = Lower bound
```

---

# RELATIONSHIP

```bash
Ω(f(n)) ≤ Θ(f(n)) ≤ O(f(n))
```

---

# COMPLEXITY CLASSES

---

## Θ(1) — CONSTANT

```bash
Same work always.

Example:
arr[5]
```

---

## Θ(log n) — LOGARITHMIC

```bash
Very slow growth.

Binary Search
Balanced Trees
```

---

## BINARY SEARCH VISUAL

```bash
1024
 ↓
512
 ↓
256
 ↓
128
 ...
```

---

## Θ(n) — LINEAR

```bash
Work grows directly with input.
```

---

## Θ(n log n)

```bash
Efficient sorting algorithms.

Merge Sort
Heap Sort
```

---

## Θ(n²) — QUADRATIC

```bash
Nested loops.

for(i)
{
    for(j)
    {
    }
}
```

---

## Θ(2^n) — EXPONENTIAL

```bash
Catastrophic growth.

n = 50 becomes practically impossible.
```

---

# COMPLEXITY RANKING

```bash
Θ(1)
Θ(log n)
Θ(n)
Θ(n log n)
Θ(n²)
Θ(2^n)
```

Best → Worst

---

# WORD-RAM MODEL

```bash
Abstract machine model used to analyze algorithms fairly.
```

---

# MEMORY STRUCTURE

```bash
[0][1][2][3][4][5][6]
```

CPU accesses any cell directly.

---

# RANDOM ACCESS

```bash
arr[4]
```

takes constant time.

---

# WORD SIZE

```bash
Modern systems commonly use 64-bit words.
```

---

# IMPORTANT FORMULA

```bash
w ≥ log₂(n)

w = word size
n = number of memory locations
```

---

# CONSTANT-TIME OPERATIONS

```bash
- addition
- subtraction
- multiplication
- bit operations
- memory access
```

---

# FUNDAMENTAL LOWER BOUND

```bash
To process n elements,
you must at least read n elements.

Therefore:

Ω(n)
```

---

# DATA STRUCTURES

```bash
Data structures organize information efficiently.
```

---

# COMMON DATA STRUCTURES

```bash
Array       → sequential storage
Linked List → dynamic storage
Stack       → LIFO
Queue       → FIFO
Hash Table  → fast lookup
Tree        → hierarchy
Graph       → relationships
```

---

# GRAPH EXAMPLE

```bash
A ─── B
│     │
│     │
C ─── D
```

Used in:

```bash
- GPS
- social networks
- shortest paths
```

---

# COURSE ROADMAP

---

## PART 1

```bash
Arrays
Hash Tables
Heaps
Sorting
```

---

## PART 2

```bash
Graphs
BFS
DFS
Dijkstra
Topological Sort
```

---

## PART 3

```bash
Dynamic Programming
```

---

# COMPUTATIONAL THINKING

```bash
Problem
   ↓
Algorithm
   ↓
Correctness Proof
   ↓
Efficiency Analysis
   ↓
Data Structures
   ↓
Implementation
   ↓
Scalable Systems
```

---

# MOST IMPORTANT TAKEAWAYS

---

## 1. PROBLEM ≠ ALGORITHM

```bash
Problem = WHAT
Algorithm = HOW
```

---

## 2. CORRECTNESS MATTERS

```bash
Algorithms must work
for ALL valid inputs.
```

---

## 3. EFFICIENCY MATTERS

```bash
Good algorithms scale.
Bad algorithms collapse.
```

---

## 4. ASYMPTOTIC ANALYSIS MATTERS

```bash
We study growth,
not machine timing.
```

---

## 5. DATA STRUCTURES MATTER

```bash
Good organization
dramatically improves speed.
```

---

## 6. COMPUTER SCIENCE IS COMMUNICATION

```bash
You must explain:

- correctness
- efficiency
- reasoning
```

clearly to humans.

---

# FINAL PHILOSOPHY

```bash
Algorithms are NOT merely code.

They are:

Problem Solving
+
Mathematical Reasoning
+
Efficiency Analysis
+
Communication
```

Code is usually the final step —
not the central idea.
