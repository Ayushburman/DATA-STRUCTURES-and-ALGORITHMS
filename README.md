# ALGORITHMS
```bash
The best definition of an **algorithm**, is a well-defined, step-by-step computational procedure that
takes a value or set of values as input and transforms them into a specific output to solve a given problem
>  It can be viewed as a tool for solving a well-specified computational problem, acting
as a recipe or a sequence of instructions that a computer or person follows to achieve a desired result
> To be considered a formal algorithm in computer science, a procedure should generally meet several key criteria:
. **Precision** and **Clarity**: The steps must be specific, distinct, and not breakable into further subtasks

. **Correctness**: The procedure is considered correct if it halts with the right output for every possible input instance

. **Finiteness**: An algorithm must complete its task and cannot take an infinite amount of time; it must always terminate

. **Predictability**: Executing the same algorithm on the same set of values must result in the same output every time

. While the terms are often used interchangeably, the sources distinguish an algorithm from a program: an algorithm is
  the abstract design or logic created at "design time," whereas a  program is the concrete implementation of that logic
  in a specific programming language at "implementation time"
. Ultimately, algorithms are considered a form of technology because total system performance depends as much on
 choosing efficient **algorithms** as it does on having fast hardware




```



----
```bash

> A computational problem is:
. A clearly defined task that can be solved using an algorithm and executed by a computer.

```

---
```
**Input**  = the data given to solve the 'problem'.
**Output** = the final result produced after processing the input using an algorithm.

```
-----
Algorithms &
Computation
MIT OpenCourseWare — 6.006 Introduction to Algorithms. Step-by-step notes with diagrams and visual understanding.

Problem Solving
Correctness Proofs
Asymptotic Analysis
Complexity Classes
Data Structures
Word-RAM Model

What is the Goal of Studying Algorithms?
Most beginners assume algorithms = writing code. That is incorrect. In computer science, algorithms are fundamentally about logical problem solving, proving a solution is correct, analysing its efficiency, and communicating it clearly to other humans.


Core Insight
A computer only executes instructions. But a computer scientist must convince professors, engineers, researchers, and teammates that: the solution works, it always works, and it is fast enough.

What Beginners Think
Algorithms = writing code to produce output.
✓ What CS Actually Demands
Solving problems logically + proving correctness + demonstrating efficiency + explaining to humans.

Problem ↓ Thinking ↓ Algorithm ↓ Proof of Correctness ↓ Efficiency Analysis ↓ Implementation (Code)

When you claim "I made a sorting algorithm," people will immediately ask: Does it always sort correctly? What about huge inputs? How fast is it? Why is it correct? This is why proofs and analysis are first-class concerns — not afterthoughts.


What is a Computational Problem?
A problem is not code. A problem is a formal rule describing valid inputs and the set of correct outputs for each input.



INPUT ──────► PROBLEM ──────► VALID OUTPUTS Example: [5, 1, 9, 3] ──► Sort ──► [1, 3, 5, 9] ✔ └────► [5, 1, 9, 3] ✘
Binary Relation
A problem is formally a binary relation between inputs and outputs. 
Each input maps to a set of allowed outputs. Some outputs are valid; others are not.

Predicate (Checker)
A predicate answers TRUE or FALSE.
For sorting, is_sorted(output) returns TRUE if the output satisfies the problem's constraint, FALSE otherwise.


Critical Property — Arbitrary Input Size
An algorithm must work for 10 users, 10⁶ users, 10¹² users — not just small examples.
Scalability is baked into the definition of a correct algorithm.


What is an Algorithm?
A problem defines what must be solved.
An algorithm defines how to solve it — a finite, deterministic sequence of
steps that transforms any valid input into a correct output.

Problem
"Sort numbers."
Specifies only the goal — the input/output relationship.

Algorithm
"Compare, swap, repeat."
Specifies the precise steps used to achieve that goal.


An algorithm behaves like a function f(input) = output.
The output must satisfy the problem's predicate for every valid input.
Same input + same steps → guaranteed predictable output.
Deterministic
Finite Steps
Correct on All Valid Inputs
Not Just "Code That Works on Examples"

----
# Algorithms & Computation

> MIT OpenCourseWare — 6.006 Introduction to Algorithms  
> Step-by-step notes with diagrams and visual understanding.

---

# Topics Covered

- Problem Solving
- Correctness Proofs
- Asymptotic Analysis
- Complexity Classes
- Data Structures
- Word-RAM Model

---

# Table of Contents

1. Goal of Studying Algorithms
2. Computational Problems
3. Algorithms
4. Problems vs Algorithms
5. Binary Relations
6. Predicates
7. Arbitrary Input Size
8. Deterministic Algorithms
9. Mathematical View of Algorithms
10. Core Philosophy

---

# 1. What is the Goal of Studying Algorithms?

Most beginners think:

```text
Algorithms = Writing Code
```

This is incomplete.

In computer science, algorithms are primarily about:

- logical problem solving
- correctness proofs
- efficiency analysis
- communication

---

# Core Insight

A computer only executes instructions.

But a computer scientist must convince humans that:

- the solution works
- it always works
- it is efficient
- it scales to huge inputs

---

# What Beginners Think

```text
Algorithms = code that produces output
```

---

# What Computer Science Actually Requires

```text
Problem Solving
+
Mathematical Reasoning
+
Correctness Proofs
+
Efficiency Analysis
+
Human Communication
```

---

# Full Computational Workflow

```text
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

# Example

Suppose someone says:

```text
"I made a sorting algorithm."
```

Immediately, people ask:

- Does it always sort correctly?
- What happens for massive inputs?
- How fast is it?
- Why is it correct?
- What is its complexity?

This is why proofs and analysis are first-class concerns.

---

# 2. What is a Computational Problem?

A problem is NOT code.

A problem is:

> A formal rule describing:
>
> - valid inputs
> - correct outputs

---

# Visual Representation

```text
INPUT ─────► PROBLEM ─────► VALID OUTPUTS
```

---

# Example — Sorting Problem

## Input

```text
[5, 1, 9, 3]
```

---

## Correct Output

```text
[1, 3, 5, 9]
```

✔ Correct

---

## Incorrect Output

```text
[5, 1, 9, 3]
```

✘ Not sorted

---

# Important Understanding

The problem only specifies:

```text
WHAT must happen
```

It does NOT specify:

```text
HOW to do it
```

That is the algorithm's responsibility.

---

# 3. What is an Algorithm?

An algorithm defines:

```text
HOW to solve the problem
```

It is:

> A finite, deterministic sequence of steps that transforms valid input into correct output.

---

# Problem vs Algorithm

---

## Problem

```text
"Sort numbers."
```

Defines the goal.

---

## Algorithm

```text
1. Compare numbers
2. Swap if needed
3. Repeat
```

Defines the process.

---

# Visual Comparison

```text
PROBLEM
   ↓
Desired Result

ALGORITHM
   ↓
Step-by-Step Method
```

---

# 4. Algorithm as a Function

Mathematically:

```text
f(input) = output
```

The output must satisfy the problem's rules.

---

# Example

Input:

```text
[4, 2, 8]
```

Algorithm:

```text
Bubble Sort
```

Output:

```text
[2, 4, 8]
```

The output satisfies the sorting condition.

---

# 5. Binary Relation

A computational problem is formally:

# A Binary Relation

between:

- inputs
- outputs

---

# Meaning

Each input maps to:

```text
Allowed Outputs
```

Some outputs are valid.
Others are invalid.

---

# Visual

```text
Input A ─────► Output 1 ✔
         └──► Output 2 ✘
```

---

# Example — Sorting

Input:

```text
[3, 1, 2]
```

---

Valid Output:

```text
[1, 2, 3]
```

---

Invalid Output:

```text
[3, 1, 2]
```

because it is not sorted.

---

# 6. Predicates (Checkers)

A predicate is a checker.

It answers:

```text
TRUE or FALSE
```

---

# Example — Sorting Predicate

```text
is_sorted(output)
```

---

If output is:

```text
[1, 2, 3]
```

Result:

```text
TRUE
```

---

If output is:

```text
[3, 1, 2]
```

Result:

```text
FALSE
```

---

# Why Predicates Matter

Predicates formally define correctness.

They mathematically determine whether:

```text
Output is valid
```

---

# 7. Arbitrary Input Size

A real algorithm must work for:

```text
10 elements
1000 elements
10⁶ elements
10¹² elements
```

NOT just tiny examples.

---

# Critical Idea

Scalability is built into the definition of an algorithm.

An algorithm that works only for small cases is NOT truly correct.

---

# Visual Growth

```text
Small Input
      ↓
Large Input
      ↓
Massive Input
```

The algorithm must still work correctly.

---

# Example

A sorting algorithm should work for:

- 5 numbers
- 500 numbers
- 500 million numbers

without changing its logic.

---

# 8. Deterministic Algorithms

A deterministic algorithm means:

```text
Same Input
+
Same Steps
=
Same Output
```

Always predictable.

---

# Example

Input:

```text
[3, 2, 1]
```

Every execution produces:

```text
[1, 2, 3]
```

not random outputs.

---

# Key Properties of Algorithms

---

## Deterministic

Predictable behavior.

---

## Finite

Must finish eventually.

---

## Correct

Works for ALL valid inputs.

---

## General

Not just hardcoded examples.

---

# 9. Why "Code That Works Once" is NOT Enough

Many beginners test:

```text
2 or 3 examples
```

and assume algorithm is correct.

That is dangerous.

---

# Example

Suppose a sorting program works for:

```text
[3, 1, 2]
```

but fails for:

```text
[5, 5, 1]
```

Then the algorithm is incorrect.

---

# Computer Science Standard

Correctness means:

```text
Works for EVERY valid input
```

not:

```text
Works on examples I tried
```

---

# 10. Core Philosophy of Algorithms

Algorithms are NOT just programming.

They are:

```text
Problem Solving
+
Mathematical Reasoning
+
Efficiency Analysis
+
Communication
```

---

# Final Big Picture

```text
COMPUTATIONAL THINKING

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

# Most Important Takeaways

---

## 1. Problems and Algorithms are Different

```text
Problem = WHAT
Algorithm = HOW
```

---

## 2. Correctness Matters

An algorithm must work for ALL valid inputs.

---

## 3. Efficiency Matters

Good algorithms scale well.

Bad algorithms collapse for huge input sizes.

---

## 4. Proofs Matter

Computer science depends on mathematical guarantees.

---

## 5. Communication Matters

You must explain and justify your solution clearly.

---

# Final Summary

Algorithms are not merely code.

They are:

```text
Logical Problem Solving
+
Correctness Guarantees
+
Efficiency at Scale
+
Mathematical Communication
```

The code itself is often the final step — not the central idea.

