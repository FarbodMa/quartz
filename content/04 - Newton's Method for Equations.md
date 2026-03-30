---
title: Newton's Method for Equations
tags: [numerical-methods, newton]
aliases: [Newton Method]
---

# Newton's Method for Equations

Newton's method is fundamentally a method for solving

$$
F(w)=0.
$$

## Core idea

At a current guess $w^k$, approximate $F$ using its first-order Taylor expansion:

$$
F(w^k+\Delta w)\approx F(w^k)+J_F(w^k)\Delta w.
$$

Then choose $\Delta w$ so the linearized model becomes zero:

$$
F(w^k)+J_F(w^k)\Delta w=0.
$$

So the Newton step solves

$$
J_F(w^k)\Delta w=-F(w^k).
$$

Then update:

$$
w^{k+1}=w^k+\Delta w.
$$

## 1D version

If $F(x)=0$, then

$$
F(x^k+\Delta x)\approx F(x^k)+F'(x^k)\Delta x.
$$

Set this to zero:

$$
\Delta x=-\frac{F(x^k)}{F'(x^k)}.
$$

That is the classical Newton formula.

## Why people say "Newton linearizes"

Because each iteration replaces the nonlinear equation by a locally linear equation.

This is the exact idea later used for the [[03 - KKT Conditions|KKT system]] in constrained optimization. See [[05 - Newton for Constrained Optimization]].

## Optimization connection

For unconstrained minimization,

$$
\nabla f(x)=0
$$

is the first-order optimality equation. Applying Newton gives

$$
\nabla^2 f(x^k)\Delta x=-\nabla f(x^k).
$$

So unconstrained Newton optimization is just Newton's method applied to the gradient equation.

## How one Newton iteration works

1. write the residual equation $F(w)=0$,
2. evaluate the residual at the current guess,
3. linearize the residual with a first-order Taylor expansion,
4. solve the resulting linear system for $\Delta w$,
5. update the iterate,
6. repeat until the residual is small.

This is why Newton-based optimization repeatedly turns nonlinear equations into
local linear algebra problems.

## Why Newton is local

The linearized model is only reliable near the current guess. If the iterate is
close enough to the true solution and the system is well behaved, Newton can
converge very fast. If not, practical solvers add line search or trust-region
logic to keep the iteration stable.

## Links

- [[03 - KKT Conditions]]
- [[05 - Newton for Constrained Optimization]]
- [[11 - Derivatives Gradient Jacobian Hessian]]
