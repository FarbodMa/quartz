---
title: KKT Conditions
tags: [optimization, kkt]
aliases: [Karush-Kuhn-Tucker Conditions]
---

# KKT Conditions

For a nonlinear program

$$
\min_x f(x)
$$

subject to

$$
c(x)=0,\qquad g(x)\ge 0,
$$

a Lagrangian can be written as

$$
L(x,\lambda,\nu)=f(x)+\lambda^T c(x)-\nu^T g(x).
$$

The KKT conditions combine feasibility, stationarity, and complementarity.

## Equality-constrained case

If there are only equalities,

$$
\min_x f(x)\quad \text{s.t.}\quad c(x)=0,
$$

then the KKT conditions are

$$
\nabla_x L(x,\lambda)=0,\qquad c(x)=0.
$$

## With inequalities

The full KKT conditions are typically written as:

### Primal feasibility

$$
c(x)=0,\qquad g(x)\ge 0
$$

### Dual feasibility

$$
\nu \ge 0
$$

### Stationarity

$$
\nabla f(x)+J_c(x)^T\lambda-J_g(x)^T\nu=0
$$

### Complementarity

$$
\nu_j g_j(x)=0 \quad \forall j
$$

This means each inequality is either:

- inactive, with $g_j(x)>0$ and $\nu_j=0$,
- active, with $g_j(x)=0$ and typically $\nu_j>0$.

That active/inactive switching is what makes inequality-constrained problems
more delicate numerically than equality-constrained ones.

## Interior-point connection

Interior-point methods replace exact complementarity

$$
\nu_j g_j(x)=0
$$

with the perturbed condition

$$
\nu_j g_j(x)=\mu,\qquad \mu>0,
$$

so both $g_j(x)$ and $\nu_j$ stay positive during the iteration. As
$\mu \to 0$, the perturbed system approaches the true KKT system.

## Why KKT matters

A constrained NLP solver is usually trying to satisfy the KKT system.

That is why [[04 - Newton's Method for Equations|Newton's method]] is applied to KKT residuals, producing linear systems that involve:

- Hessians of the [[02 - Lagrangian and Multipliers|Lagrangian]],
- Jacobians of constraints,
- complementarity or barrier terms.

## In the NSD context

The lower-level subproblem is assumed to be solved to a KKT point. Then the NSD derivation differentiates the lower KKT system with respect to upper-level variables. That is the foundation for both:

- gradient extraction through [[07 - Dummy Constraints and Dummy-Constraint Duals]],
- curvature extraction through [[08 - Schur Complement]].

## Links

- [[02 - Lagrangian and Multipliers]]
- [[04 - Newton's Method for Equations]]
- [[05 - Newton for Constrained Optimization]]
- [[06 - Interior-Point Methods]]
