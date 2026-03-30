---
title: Optimization Problem Basics
tags: [optimization, basics]
---

# Optimization Problem Basics

A generic nonlinear optimization problem can be written as

$$
\min_x f(x)
$$

subject to

$$
c(x)=0,\qquad g(x)\ge 0.
$$

Here:

- $x$ is the vector of decision variables.
- $f(x)$ is the objective.
- $c(x)=0$ are equality constraints.
- $g(x)\ge 0$ are inequality constraints.

## Unconstrained vs constrained

### Unconstrained

$$
\min_x f(x)
$$

A local optimum often satisfies

$$
\nabla f(x)=0.
$$

### Constrained

The optimum must balance two things:

1. make the objective small,
2. stay feasible.

That balance is described using the [[02 - Lagrangian and Multipliers|Lagrangian]] and then the [[03 - KKT Conditions|KKT conditions]].

## Derivatives language

For a scalar function $f(x)$:

- in one variable, the first derivative is $\frac{df}{dx}$ and the second derivative is $\frac{d^2f}{dx^2}$,
- in many variables, the first derivative is usually represented by the gradient,
- in many variables, the second derivative is usually represented by the Hessian.

See also [[11 - Derivatives Gradient Jacobian Hessian]].

## Why this matters for NSD

The NSD decomposition ultimately needs derivatives of an upper-level objective that includes lower-level optimal-value functions. That is why so much of the method revolves around gradients, Hessians, and linearized KKT systems.

## Links

- [[02 - Lagrangian and Multipliers]]
- [[03 - KKT Conditions]]
- [[11 - Derivatives Gradient Jacobian Hessian]]
