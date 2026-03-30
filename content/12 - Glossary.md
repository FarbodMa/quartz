---
title: Glossary
tags: [glossary, definitions]
---

# Glossary

## Dummy constraint
An artificial equality used to tie a local lower-level copy $\delta_i$ to an upper-level quantity $G_i x$. See [[07 - Dummy Constraints and Dummy-Constraint Duals]].

## Dummy variable
An artificial local copy such as $\delta_i$ introduced so a lower subproblem can
be solved independently while still representing an upper-level quantity. See
[[07 - Dummy Constraints and Dummy-Constraint Duals]].

## Dummy-constraint dual
The multiplier $\gamma_i$ of the dummy constraint. It acts like a sensitivity or shadow price of the coupling. See [[07 - Dummy Constraints and Dummy-Constraint Duals]].

## Complementarity
The KKT condition that a multiplier and its associated inequality slack cannot
both be strictly positive at the solution. See [[03 - KKT Conditions]] and
[[06 - Interior-Point Methods]].

## Central path
The smooth path defined by perturbed complementarity equations such as
$\nu_j g_j(x)=\mu$ in interior-point methods. See [[06 - Interior-Point Methods]].

## Gradient
The vector of first derivatives of a scalar function of many variables. See [[11 - Derivatives Gradient Jacobian Hessian]].

## Hessian
The matrix of second derivatives of a scalar function of many variables. See [[11 - Derivatives Gradient Jacobian Hessian]].

## Jacobian
The matrix of first derivatives of a vector-valued function. See [[11 - Derivatives Gradient Jacobian Hessian]].

## KKT system
The first-order optimality conditions for a constrained optimization problem. See [[03 - KKT Conditions]].

## Lagrangian
The function that combines the objective and constraints using multipliers. See [[02 - Lagrangian and Multipliers]].

## Multiplier
Another name for a dual variable or shadow price attached to a constraint in the
Lagrangian. See [[02 - Lagrangian and Multipliers]].

## Newton linearization
Replacing a nonlinear equation by its local first-order Taylor approximation and solving the resulting linear system. See [[04 - Newton's Method for Equations]].

## Reduced KKT system
The lower Newton/KKT system after barrier/complementarity-related variables have
been condensed out, but before the Schur complement eliminates the remaining
internal lower variables. See [[Reduced KKT System]].

## Schur-reduced system
The further reduced dummy-dual-space system obtained after eliminating the
remaining internal lower variables from the reduced KKT system. See
[[08 - Schur Complement]] and [[Reduced KKT System]].

## Schur complement
A reduced matrix obtained by eliminating part of a block linear system. See [[08 - Schur Complement]].

## Sigma terms
Diagonal barrier/bound curvature terms such as $\Sigma_i^L$, $\Sigma_i^U$,
$\Sigma_{s,i}$, and $\Sigma_{q,i}$ that remain after complementary variables
are eliminated from the raw lower Newton system. See
[[Barrier and Bound Sigma Terms]].

## Value function
The optimal objective value of a lower problem as a function of parameters such as upper-level variables. See [[09 - Value Function Sensitivity]].

## Links

- [[00 - MOC - NSD and Decomposition]]
- [[03 - KKT Conditions]]
- [[06 - Interior-Point Methods]]
- [[11 - Derivatives Gradient Jacobian Hessian]]
- [[Reduced KKT System]]
- [[Barrier and Bound Sigma Terms]]
