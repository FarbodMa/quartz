---
title: Value Function Sensitivity
tags: [sensitivity, envelope-theorem, decomposition]
---

# Value Function Sensitivity

This note answers the question:

> Why should the dummy duals and Schur complement work at all?

## The real upper objective

The true upper objective has the form

$$
\Phi_0(x)=f_0(x)+\sum_i \Phi_i^*(x),
$$

where $\Phi_i^*(x)$ is the optimal value of lower problem $i$ when $x$ is fixed.

So the upper solver needs derivatives of a value function, not just derivatives of a simple explicit formula.

## First-order sensitivity

Because the lower problem is solved at a KKT point, the derivative of the lower optimal value with respect to $x$ comes from the explicit appearance of $x$ in the lower Lagrangian.

For the dummy-coupling term, this gives

$$
m=-\sum_i G_i^T \gamma_i.
$$

This is the lower-level contribution to the upper gradient.

This is a constrained version of envelope-theorem logic.

## Why first-order chain-rule terms disappear

At the lower optimum, the internal lower variables already satisfy stationarity.
So when the lower optimal value is differentiated with respect to $x$, the
indirect dependence through $z_i(x)$, $\delta_i(x)$, and other lower variables
is canceled by the KKT stationarity conditions. What remains at first order is
the explicit $x$-dependence of the lower Lagrangian, which is why the dummy
duals determine the gradient contribution.

## Linearized KKT sensitivity equation

Let $\xi_i$ stack the lower primal and dual variables, and let

$$
F_i(\xi_i;x)=0
$$

denote the lower KKT equations at fixed upper variable $x$.

At a solved lower optimum for the current upper iterate $x^l$, we have

$$
F_i(\xi_i^*;x^l)=0.
$$

If the upper variable is perturbed by $\Delta x$, the lower optimum also moves
by $\Delta \xi_i$. First-order Taylor expansion gives

$$
\frac{\partial F_i}{\partial \xi_i}\Delta \xi_i
+
\frac{\partial F_i}{\partial x}\Delta x
=
0.
$$

The right-hand side is zero because the base point is already a KKT point, so
there is no residual term left after linearization. This linearized KKT system
is the starting point for the reduced $(y_i,\gamma_i)$ system and the later
Schur-complement reduction.

## Second-order sensitivity

To get second-order information, differentiate the lower KKT system itself.

That produces a linearized lower KKT/Newton system. Eliminating the lower internal variables gives the reduced operator

$$
P_i = E_i^T K_i^{-1} E_i.
$$

From this, the lower contribution to the upper Hessian becomes

$$
M=\sum_i G_i^T P_i^{-1} G_i.
$$

## Why this is not arbitrary

- Using $\gamma_i$ for the gradient is not a guess; it comes from differentiating the lower Lagrangian with respect to $x$.
- Using $P_i^{-1}$ for curvature is not a guess; it comes from implicit differentiation of the lower KKT system.
- Using the Schur complement is not an approximation by itself; it is exact block elimination.

## When this can become delicate

This logic depends on local sensitivity assumptions such as:

- the lower problem is solved successfully,
- the multipliers are meaningful and stable,
- KKT regularity is good enough, for example so multipliers are locally unique,
- the local linearization is informative.

So the method is local, not a universal guarantee under arbitrary degeneracy.

## Links

- [[02 - Lagrangian and Multipliers]]
- [[03 - KKT Conditions]]
- [[07 - Dummy Constraints and Dummy-Constraint Duals]]
- [[08 - Schur Complement]]
- [[10 - NSD Algorithm Overview]]
- [[12 - Glossary]]
- [[Reduced KKT System]]
