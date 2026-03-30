---
title: Lagrangian and Multipliers
tags: [optimization, lagrangian, duality]
aliases: [Lagrange Multipliers]
---

# Lagrangian and Multipliers

For an equality-constrained problem

$$
\min_x f(x)\quad \text{s.t.}\quad c(x)=0,
$$

the Lagrangian is

$$
L(x,\lambda)=f(x)+\lambda^T c(x).
$$

## Why use the Lagrangian?

Without constraints, an optimum is often characterized by

$$
\nabla f(x)=0.
$$

With constraints, the optimum generally does **not** occur where $\nabla f(x)=0$. Instead, it occurs where the objective gradient is balanced by constraint gradients:

$$
\nabla_x L(x,\lambda)=\nabla f(x)+J_c(x)^T\lambda=0.
$$

So the Lagrangian is the object that packages:

- the objective,
- the constraints,
- the strength with which constraints "push back" through the multipliers $\lambda$.

## Geometric meaning

For one equality constraint $c(x)=0$, the feasible set is a surface. At a
constrained optimum, you cannot move in any feasible direction and still
decrease the objective. So the objective gradient must line up with the
constraint gradients:

$$
\nabla f(x^*) = -J_c(x^*)^T \lambda^*.
$$

That is the stationarity condition written geometrically.

## Meaning of multipliers

A multiplier is a sensitivity or shadow price.

If the problem is

$$
\min_x f(x)\quad \text{s.t.}\quad c(x)=b,
$$

then the multiplier roughly tells you how the optimal objective changes when $b$ is perturbed.

That is the same idea later used for [[07 - Dummy Constraints and Dummy-Constraint Duals|dummy-constraint duals]].

## Derivatives of the Lagrangian

### First derivative

$$
\nabla_x L(x,\lambda)
$$

This gives the stationarity condition used in the [[03 - KKT Conditions|KKT conditions]].

### Second derivative

$$
\nabla_{xx}^2 L(x,\lambda)
$$

This gives the relevant constrained curvature. In constrained Newton methods, the Hessian of the Lagrangian appears instead of only the Hessian of $f$. See [[05 - Newton for Constrained Optimization]].

## Tiny example

Consider

$$
\min_{x,y} x^2+y^2 \quad \text{s.t.}\quad x+y-1=0.
$$

The Lagrangian is

$$
L(x,y,\lambda)=x^2+y^2+\lambda(x+y-1).
$$

Its first-order conditions are

$$
2x+\lambda=0,\qquad 2y+\lambda=0,\qquad x+y-1=0.
$$

So the Lagrangian turns the constrained optimum conditions into a system of
equations in the primal variables and the multiplier.

## Why not only differentiate the objective?

Because the lower-level optimum depends on both:

- objective terms,
- constraint terms.

When differentiating an optimal-value function with respect to a parameter, the Lagrangian is the correct object to use, not just the raw objective. See [[09 - Value Function Sensitivity]].

## Links

- [[03 - KKT Conditions]]
- [[05 - Newton for Constrained Optimization]]
- [[07 - Dummy Constraints and Dummy-Constraint Duals]]
- [[09 - Value Function Sensitivity]]
