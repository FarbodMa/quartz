---
title: Interior-Point Methods
tags: [optimization, interior-point, ipopt]
aliases: [Barrier Methods]
---

# Interior-Point Methods

Interior-point methods are practical NLP algorithms for problems with inequality constraints.

## Original constrained problem

$$
\min_x f(x)
$$

subject to

$$
c(x)=0,\qquad g(x)\ge 0.
$$

## Why inequalities are harder

An inequality can be:

- inactive: $g_j(x)>0$,
- active: $g_j(x)=0$.

The raw KKT condition for each inequality is

$$
\nu_j g_j(x)=0.
$$

This is complementarity, and it creates active-set switching behavior.

## Barrier viewpoint

Interior-point methods stay inside the feasible region by solving a barrier problem such as

$$
\min_x f(x)-\mu \sum_j \ln g_j(x)
\quad \text{s.t.}\quad c(x)=0.
$$

The term $-\ln g_j(x)$ becomes very large near $g_j(x)=0^+$, so the iterates stay in the interior.

## Primal-dual viewpoint

A primal-dual interior-point method solves a perturbed KKT system like

$$
\nabla_x L(x,\lambda,\nu)=0,
$$

$$
c(x)=0,
$$

$$
g(x)>0,\qquad \nu>0,
$$

$$
\nu_j g_j(x)=\mu.
$$

As $\mu \to 0$, this approaches the true KKT complementarity condition

$$
\nu_j g_j(x)=0.
$$

## Simple barrier example

Consider

$$
\min_x x^2 \quad \text{s.t.}\quad x \ge 1.
$$

Using the convention $g(x)=x-1 \ge 0$, the barrier problem becomes

$$
\min_x x^2-\mu \ln(x-1).
$$

For a fixed $\mu>0$, the minimizer stays strictly inside the feasible region,
so $x>1$. As $\mu \to 0$, the minimizer approaches the true constrained
solution at the boundary.

## Central path intuition

The perturbed complementarity condition

$$
\nu_j g_j(x)=\mu
$$

keeps both $g_j(x)$ and $\nu_j$ positive during the iteration. The path traced
as $\mu$ decreases is the central path that interior-point methods follow
toward the true KKT point.

## Newton inside interior-point

Interior-point methods still use Newton. The difference is that Newton is applied to a *perturbed* KKT system that includes barrier/complementarity equations.

That is why practical NLP solvers often produce linear systems containing:

- Hessians of the [[02 - Lagrangian and Multipliers|Lagrangian]],
- constraint Jacobians,
- diagonal terms related to slacks, bounds, and complementarity.

## NSD connection

The lower-level KKT matrix used in NSD reflects exactly this kind of Newton/IP structure. The extra diagonal terms in the reduced system come from barrier/bound treatment. Then the [[08 - Schur Complement]] is applied to compress the system.

## Links

- [[02 - Lagrangian and Multipliers]]
- [[03 - KKT Conditions]]
- [[05 - Newton for Constrained Optimization]]
- [[08 - Schur Complement]]
- [[10 - NSD Algorithm Overview]]
- [[Barrier and Bound Sigma Terms]]
