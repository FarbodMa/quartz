---
title: Schur Complement
tags: [linear-algebra, decomposition, kkt]
---

# Schur Complement

The Schur complement is a way to eliminate some variables from a block linear system and keep only the reduced effect on the variables you care about.

## Generic block system

Suppose

$$
\begin{bmatrix}
K & E\\
E^T & 0
\end{bmatrix}
\begin{bmatrix}
\Delta y\\
\Delta \gamma
\end{bmatrix}
=
-
\begin{bmatrix}
r\\
u
\end{bmatrix}.
$$

From the first block row,

$$
K\Delta y + E\Delta \gamma = -r,
$$

so

$$
\Delta y = -K^{-1}r - K^{-1}E\Delta \gamma.
$$

Substitute into the second block row:

$$
E^T\Delta y = -u.
$$

Then

$$
-E^T K^{-1}r - E^T K^{-1}E \Delta \gamma = -u.
$$

So

$$
(E^T K^{-1}E)\Delta \gamma = u - E^T K^{-1}r.
$$

Define

$$
P=E^T K^{-1}E.
$$

This $P$ is the Schur complement seen in the reduced $\gamma$-space.

## Sensitivity view

In the NSD setting, the reduced system is driven by upper-level perturbations.
After eliminating the internal lower variables, one gets

$$
P_i \Delta \gamma_i = -G_i \Delta x,
$$

so

$$
\Delta \gamma_i = -P_i^{-1} G_i \Delta x.
$$

This makes $P_i^{-1}G_i$ the local sensitivity of the dummy duals to
upper-level perturbations.

## Why it is useful

If the full system is large but the coupling dimension is small, solving in the reduced space can be much cheaper.

## NSD interpretation

In the lower-level Newton/KKT system:

- $K_i$ describes the internal lower-problem response,
- $E_i$ links the internal variables to the dummy-constraint dual space,
- the Schur complement

$$
P_i = E_i^T K_i^{-1} E_i
$$

compresses the internal lower structure into a reduced operator in the coupling space.

This bordered system is already **reduced** relative to the raw primal-dual
interior-point KKT system. The Schur complement is a further reduction that
removes the remaining internal lower variables. See [[Reduced KKT System]].

## Why the Hessian contribution looks like

$$
M=\sum_i G_i^T P_i^{-1}G_i
$$

Because:

1. the upper perturbation $\Delta x$ affects the dummy space through $G_i\Delta x$,
2. the reduced dummy-dual response is governed by $P_i^{-1}$,
3. mapping back to upper space gives $G_i^T P_i^{-1} G_i$.

## Exactness vs implementation shortcut

Forming the Schur complement is not "changing the problem" in an arbitrary way.
It is exact block elimination. The reduced system is mathematically equivalent
to the original bordered KKT system, assuming the required inverses exist.

An implementation may then compute $P_i^{-1}$ directly in dummy space and only
afterward assemble

$$
\hat M_i = G_i^T P_i^{-1} G_i.
$$

That changes the computational route, not the final quadratic form.

## Why replacing $G_i$ by an identity can still be valid

Sometimes the implementation solves for $P_i^{-1}$ directly in the reduced
dummy space using an identity right-hand side, then reconstructs

$$
\hat M_i = G_i^T P_i^{-1} G_i.
$$

This changes **how** the reduced operator is computed, not **what** the final quadratic form is.

## Links

- [[05 - Newton for Constrained Optimization]]
- [[07 - Dummy Constraints and Dummy-Constraint Duals]]
- [[09 - Value Function Sensitivity]]
- [[10 - NSD Algorithm Overview]]
- [[12 - Glossary]]
- [[Reduced KKT System]]
