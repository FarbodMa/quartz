---
title: Newton for Constrained Optimization
tags: [optimization, newton, kkt]
---

# Newton for Constrained Optimization

For an equality-constrained problem

$$
\min_x f(x)\quad \text{s.t.}\quad c(x)=0,
$$

the KKT system is

$$
\nabla_x L(x,\lambda)=0,\qquad c(x)=0.
$$

Define the residual function

$$
F(x,\lambda)=
\begin{bmatrix}
\nabla_x L(x,\lambda)\\
c(x)
\end{bmatrix}.
$$

Newton is applied to

$$
F(x,\lambda)=0.
$$

## Linearization

At the current iterate $(x^k,\lambda^k)$,

$$
F(x^k+\Delta x,\lambda^k+\Delta \lambda)
\approx
F(x^k,\lambda^k)+J_F(x^k,\lambda^k)
\begin{bmatrix}
\Delta x\\
\Delta \lambda
\end{bmatrix}.
$$

Setting this approximation to zero gives the Newton system

$$
\begin{bmatrix}
\nabla_{xx}^2 L(x,\lambda) & J_c(x)^T\\
J_c(x) & 0
\end{bmatrix}
\begin{bmatrix}
\Delta x\\
\Delta \lambda
\end{bmatrix}
=
-
\begin{bmatrix}
\nabla_x L(x,\lambda)\\
c(x)
\end{bmatrix}.
$$

## Why the Hessian of the Lagrangian appears

Because Newton differentiates the stationarity residual

$$
\nabla_x L(x,\lambda)=0.
$$

Its derivative with respect to $x$ is

$$
\nabla_{xx}^2 L(x,\lambda).
$$

So the Hessian of the Lagrangian is not an arbitrary choice. It is the Jacobian block of the stationarity equation.

For nonlinear constraints, this block can be written as

$$
\nabla_{xx}^2 L(x,\lambda)=\nabla^2 f(x)+\sum_j \lambda_j \nabla^2 c_j(x),
$$

so constraint curvature contributes directly to the Newton system.

## Practical interpretation

Each iteration does:

1. evaluate the KKT residual,
2. build the linearized KKT system,
3. solve for $(\Delta x,\Delta \lambda)$,
4. update the iterate.

In practice, solvers usually do not take the full step blindly. They combine
this Newton system with line search or trust-region logic so that the residuals
decrease reliably.

This same pattern extends to [[06 - Interior-Point Methods]], except there the residual also includes slack/complementarity equations.

## With inequalities

When inequalities are present, the residual includes additional slack or
barrier/complementarity equations. The Newton idea is unchanged: write the full
residual system, take its Jacobian, solve the linearized system for the step,
and update the iterate.

## Why this matters for NSD

The NSD derivation builds a reduced linearized KKT system for each lower problem. Its block form is the same kind of Newton system, only with more structure. That reduced system is later compressed by the [[08 - Schur Complement]].

## Links

- [[03 - KKT Conditions]]
- [[04 - Newton's Method for Equations]]
- [[06 - Interior-Point Methods]]
- [[08 - Schur Complement]]
