---
title: MOC - NSD and Decomposition
tags: [optimization, decomposition, nsd, moc]
aliases: [Map of Content, NSD Map]
---
# MOC - NSD and Decomposition

This vault is a concept map for the ideas we discussed around constrained optimization, KKT systems, Newton's method, interior-point methods, dummy constraints, dummy-constraint duals, Schur complements, and the NSD-style decomposition logic. HELLLLLLLLLLO!

## Start here

- [[01 - Optimization Problem Basics]]
- [[02 - Lagrangian and Multipliers]]
- [[03 - KKT Conditions]]
- [[04 - Newton's Method for Equations]]
- [[05 - Newton for Constrained Optimization]]
- [[06 - Interior-Point Methods]]
- [[07 - Dummy Constraints and Dummy-Constraint Duals]]
- [[08 - Schur Complement]]
- [[09 - Value Function Sensitivity]]
- [[10 - NSD Algorithm Overview]]

## Fast mental model

The upper-level problem does not directly solve all lower-level physics at once. Instead, it uses lower subproblems to return:

1. an optimal lower-level objective value,
2. a first-order signal through [[07 - Dummy Constraints and Dummy-Constraint Duals]], and
3. a second-order signal through [[08 - Schur Complement]].

Those are injected into the upper-level derivatives, which makes the upper solver behave as if it had differentiated the full embedded lower problem.

## Main chain of ideas

```text
Optimization problem
-> Lagrangian
-> KKT conditions
-> Newton on KKT system
-> interior-point / NLP solver structure
-> lower-level KKT linearization
-> dummy-constraint duals for gradient information
-> Schur complement for reduced curvature information
-> upper-level gradient/Hessian augmentation
```

## Suggested reading order

1. [[01 - Optimization Problem Basics]]
2. [[02 - Lagrangian and Multipliers]]
3. [[03 - KKT Conditions]]
4. [[04 - Newton's Method for Equations]]
5. [[05 - Newton for Constrained Optimization]]
6. [[06 - Interior-Point Methods]]
7. [[07 - Dummy Constraints and Dummy-Constraint Duals]]
8. [[08 - Schur Complement]]
9. [[09 - Value Function Sensitivity]]
10. [[10 - NSD Algorithm Overview]]

## One-page summary

- The [[02 - Lagrangian and Multipliers|Lagrangian]] combines the objective and constraints into one expression.
- The [[03 - KKT Conditions|KKT conditions]] describe local optimality for constrained problems.
- [[04 - Newton's Method for Equations|Newton's method]] solves nonlinear equations by linearizing them locally.
- [[05 - Newton for Constrained Optimization]] applies Newton to the KKT system.
- [[06 - Interior-Point Methods]] are a practical way to solve constrained NLPs by using perturbed complementarity / barrier logic.
- [[07 - Dummy Constraints and Dummy-Constraint Duals]] explain how an upper-level variable is copied into a lower problem and why the dual of that artificial link contains sensitivity information.
- [[08 - Schur Complement]] explains how a large linear KKT system is reduced to a smaller system in the coupling space.
- [[09 - Value Function Sensitivity]] explains why the duals and reduced matrices should work at all.
- [[10 - NSD Algorithm Overview]] ties the whole workflow together.

## Links

- [[11 - Derivatives Gradient Jacobian Hessian]]
- [[12 - Glossary]]
- [[Reduced KKT System]]
- [[Barrier and Bound Sigma Terms]]
