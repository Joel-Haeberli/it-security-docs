tags: #cryptocurrency #bitcoin #pow #consens #proof-of-work

# Proof-of-Work (PoW)

links: [[402 DSS TOC - Preliminaries|DSS TOC - Preliminaries]] - [[themes/000 Index|Index]]

---

## Concept

The idea of a **Proof of Work** (PoW) is to be able to proof that some work has been done. I can proof to the teacher that I did some work by giving her an answer to a question she gave me.

The **Proof of Work** scheme looks as follows:

- $solve(p,d,f)$ $\rightarrow$ $s$:
	- $p$ for puzzle: This is the problem to be solved which shall demonstrate that work was done.
	- $d$ for difficulty: The problems difficulty must be adjustable, so that the PoW remains usable in the future. It's a requirement regarding the solution.
	- $f$ for function: The underlying function of the puzzle which helps to solve it. $f$ must take the puzzle and the solution as input. The result must be equal to the difficulty $d$.
- $verify(p,d,s,f)$ $\rightarrow$ $True | False$:
	- $p$ for puzzle: The puzzle which was to be solved.
	- $d$ for difficulty: The problems difficulty.
	- $s$ for solution: The solution obtained by solve.
	- $f$ for function: The function which defines the problem to be solved.

Given this scheme we can say that:
$verify(p,d,solve(p,d,f),f) = True$, iff $f$ solves the problem such that given $p$ and $s$ as input result in $d$
The PoW therefore lies in finding a solution $s$ which as parameter of the function $f$ results in a definable difficulty $d$ when combined with puzzle $p$.

## Hashcash

Hashcash was the first implementation of a PoW which works as follows:

$f$ = SHA-256($p$ | $s$), (| is the concatenation operation)
$p$ = bit string
$d$ = number of leading zero bits in solution

When we want to solve the following problem:

$d = 2$
$p = 01001100011$

we would try to find a solution $s$, so that:

001... = SHA-256(01001100011 | $s$)

## Puzzle-Friendliness

The PoW is predestinated to use hash functions. Especially if the hash function is puzzle-friendly. A hash function is puzzle-friendly if there is **no better way of solving the puzzle** $d = hash(p | s)$, **than just randomly trying**. This comes because a hash is easy to calculate but hard (or impossible) to invert. This makes verification easy but solving the puzzle hard.

---
links: [[402 DSS TOC - Preliminaries|DSS TOC - Preliminaries]] - [[themes/000 Index|Index]]