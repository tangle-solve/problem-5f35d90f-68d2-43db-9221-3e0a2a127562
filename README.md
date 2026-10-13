<!-- solve-problem:5f35d90f-68d2-43db-9221-3e0a2a127562 -->
# Efficient distribution-free PAC learning of DNF

A [Tangle Solve problem](https://solve.tangle.tools/problems/5f35d90f-68d2-43db-9221-3e0a2a127562).

## What is the problem?

In the PAC model (Valiant, 1984), fix the class of DNF formulas of size *s* over *n* Boolean variables (i.e., ORs of at most *s* ANDs of literals). The goal: give an algorithm that, given i.i.d. samples (x, f(x)) where x is drawn from an **arbitrary, unknown** distribution D over {0,1}ⁿ and f is any DNF of size s, and given accuracy ε and confidence δ parameters, outputs a hypothesis h (in **any** representation — improper learning is allowed) such that Pr_{x~D}[h(x) ≠ f(x)] ≤ ε, with probability ≥ 1−δ, in time poly(n, s, 1/ε, log 1/δ). The hypothesis must merely compute the function approximately; it need not be a DNF. This is the general-distribution version of learning polynomial-size DNF; the uniform-distribution version was resolved (see below), but distribution-free learnability remains open.

Precise interpretation note: "polynomial-size" means s = poly(n) with the runtime polynomial in n and s jointly. Membership queries are *not* assumed (though that variant is interesting; see Warnings).

## Why does it matter?

This is one of the central open problems in computational learning theory, essentially equivalent in difficulty to weak learnability of DNF and closely tied to learning intersections of halfspaces, depth-2 circuits, and to long-standing lower-bound questions in complexity theory. A positive result would give efficient symbolic concept learning with wide AI applications (rule-based classifiers from unlabeled-distribution assumptions); a negative result would likely require breakthrough circuit lower bounds. It also gates the broader program of understanding which natural concept classes are learnable without distributional assumptions.

## What's already known?

- **Uniform distribution:** Jackson (1997), via the Fourier-based "harmonic sieve" boosting Gács's/Kalai's weak learners, gave a poly-time algorithm for learning poly-size DNF under the **uniform** distribution with membership queries; later refinements (e.g., Feldman) removed the need for queries under uniform. This does **not** address arbitrary D.
- **Best runtime for distribution-free (agnostic-agnostic) learning:** Klivans and Servedio (2004) give 2^{Õ(n^{1/3})} for DNF of poly size — subexponential but not polynomial. (Verify the exact exponent; subsequent minor improvements may exist.)
- **Why approaches fail:** Under arbitrary distributions, the Fourier/low-degree paradigm behind the harmonic sieve collapses — Fourier coefficients are distribution-dependent and membership-query membership-query efficient weak learning is not available. The Kolmogorov-complexity/mansour-style concentration arguments fail.
- **Hardness:** DNFs of poly size contain, and are contained in, classes near known hardness frontiers: learning intersections of halfspaces is crypto-hard (under assumptions), and DNF learning is known to be at least as hard as learning noisy parity-type tasks in some formulations. No unconditional hardness is known; hardness would imply circuit lower bounds.

## What would count as solving it?

**Positive (main):** An algorithm with runtime poly(n, s, 1/ε, log 1/δ) achieving error ≤ ε w.r.t. arbitrary unknown D over {0,1}ⁿ for DNF of size s, improper hypotheses allowed, using only random examples (no queries). 
**Negative/barrier:** A proof that no such algorithm exists — e.g., via a reduction showing it would imply a major circuit lower bound (like NP ⊄ P/poly) or a cryptographic construction based on standard assumptions. 
**Partial:** polynomial time for s up to some super-constant (currently even s = ω(1) distribution-free seems hard); or poly-time with membership queries.

## How to start

1. Read Kearns–Vazirani's *An Introduction to Computational Learning Theory*, ch. 3 and the DNF sections, for the framework; then Jackson (1997) and Klivans–Servedio (2004) to understand the uniform-distribution and subexponential frontiers.
2. Identify precisely where the uniform-distribution argument breaks: the harmonic sieve needs the target's Fourier spectrum under the sampling distribution; under unknown D this spectrum is inaccessible without query access. Ask what surrogate weak-learner survives.
3. Consider the boosting perspective: distribution-free DNF learning reduces to weakly learning DNF; study whether any known weak-learning primitive (e.g., via regression, kernel methods, or smooth boosting) can be made query-free.
4. Main obstacle: no known poly-time weak learner for DNF under arbitrary distributions exists even with queries (verify current status); any query-free result seems strictly harder.

## Key references

- L. Valiant, "A Theory of the Learnable," CACM 27(11), 1984. Introduces the PAC model and poses DNF learnability. https://dl.acm.org/doi/10.1145/358056.358050
- J. Jackson, "An Efficient Membership-Query Algorithm for Learning DNF with Respect to the Uniform Distribution," JCSS 55(3), 1997. Proves poly-size DNF is learnable in poly time under the uniform distribution with membership queries (harmonic sieve).
- A. Klivans and R. Servedio, "Learning DNF in Time 2^{Õ(n^{1/3})}," JCSS 68(2), 2004. Gives the best subexponential distribution-free algorithm via a boosting-based reduction to halfspace counting. (Verify link.) https://www.sciencedirect.com/science/article/pii/S0022000003001859
- M. Kearns and U. Vazirani, *An Introduction to Computational Learning Theory*, MIT Press, 1994. Standard reference for PAC learning, weak learning, and boosting reductions relevant to this problem.

## Warnings

- The membership-query-free vs. membership-query distinction is critical: Jackson's result uses queries; do not conflate. Decide upfront which variant you target.
- "Improper" learning is genuinely allowed — requiring a DNF hypothesis makes the problem hard for information-theoretic reasons (hardness of DNF minimization), so don't restrict to proper hypotheses.
- Weak DNF learning (constant advantage) suffices via boosting — focus effort there rather than strong learning directly.
- Beware claimed reductions: learning DNF distribution-free is *related* to but not settled by results on juntas, parities, or agnostic learning; several folklore "equivalences" are imprecise (verify any reduction you plan to invoke).

---
*`ALGO-000196` · unverified*

## Acceptance guidance

**Positive (main):** An algorithm with runtime poly(n, s, 1/ε, log 1/δ) achieving error ≤ ε w.r.t. arbitrary unknown D over {0,1}ⁿ for DNF of size s, improper hypotheses allowed, using only random examples (no queries). 
**Negative/barrier:** A proof that no such algorithm exists — e.g., via a reduction showing it would imply a major circuit lower bound (like NP ⊄ P/poly) or a cryptographic construction based on standard assumptions. 
**Partial:** polynomial time for s up to some super-constant (currently even s = ω(1) distribution-free seems hard); or poly-time with membership queries.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/5f35d90f-68d2-43db-9221-3e0a2a127562?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000196.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000196)
