---
title: Barrier and Bound Sigma Terms
tags: [interior-point, bounds, kkt]
aliases: [Sigma Terms]
---

# Barrier and Bound Sigma Terms

The $\Sigma$ matrices are the diagonal remnants of the barrier, bound, and
complementarity equations after their associated multiplier updates are
eliminated from the raw lower Newton system.

## Where they come from

In a primal-dual interior-point lower solve, complementarity-style equations
appear for slacks, relaxations, and variable bounds. Schematically:

$$
\mathcal{A}_{s,i}s_i-\mu e=0,\qquad \mathcal{A}_{q,i}q_i-\mu e=0,
$$

$$
\mathcal{A}_{z,i}^{U}(z^U-z_i)-\mu e=0,\qquad
\mathcal{A}_{z,i}^{L}(z_i-z^L)-\mu e=0.
$$

If the multiplier updates associated with these equations are eliminated, they
do not disappear without a trace. Their effect is folded into diagonal terms in
the remaining reduced KKT matrix.

## Standard sigma definitions

The chapter introduces diagonal matrices such as

$$
\Sigma_i^L=(Z_i-Z^L)^{-1}\mathcal A_i^L,\qquad
\Sigma_i^U=(Z^U-Z_i)^{-1}\mathcal A_i^U,
$$

$$
\Sigma_{s,i}=S_i^{-1}\mathcal A_{s,i},\qquad
\Sigma_{q,i}=Q_i^{-1}\mathcal A_{q,i}.
$$

These are barrier/bound curvature terms that remain after the corresponding
multiplier variables have been condensed out.

## Why they are diagonal

Each bound or slack acts componentwise.

For one lower-bound complementarity equation,

$$
\alpha^L(z-z^L)-\mu=0,
$$

the multiplier $\alpha^L$ interacts only with the same scalar variable $z$, not
with every other coordinate. So after linearization and elimination, the
resulting correction affects only the corresponding diagonal entry.

## Tiny scalar derivation

Take

$$
\alpha^L(z-z^L)-\mu=0.
$$

Linearizing gives

$$
(z-z^L)\Delta \alpha^L + \alpha^L\Delta z
=
-\bigl(\alpha^L(z-z^L)-\mu\bigr).
$$

Solving for $\Delta \alpha^L$ yields a term proportional to

$$
\frac{\alpha^L}{z-z^L}\Delta z.
$$

That coefficient is the scalar version of the diagonal contribution stored in
$\Sigma_i^L$.

## Why they end up inside $K_i$

After complementarity-related variables are eliminated, the reduced Newton
matrix for the lower period no longer uses explicit bound-multiplier updates.
Instead, the remaining primal block is modified by diagonal terms such as

$$
\tilde W_{zz}=W_{zz}+\Sigma_i^L+\Sigma_i^U.
$$

Similarly, slack and relaxed-variable rows carry $\Sigma_{s,i}$ and
$\Sigma_{q,i}$.

When the remaining reduced system is grouped into

$$
\begin{bmatrix} K_i & E_i\\ E_i^T & 0 \end{bmatrix},
$$

those diagonal $\Sigma$ blocks are already part of the reduced internal block
$K_i$.

## Intuition

Without elimination, the lower Newton system would carry many extra variables to
represent barrier and bound mechanics explicitly.

With elimination:

- the explicit multiplier-update variables disappear,
- their local curvature effect remains,
- that effect is stored as diagonal "stiffness" terms in the reduced matrix.

So the bounds still push back on the lower Newton step, but in compressed form.

## Links

- [[06 - Interior-Point Methods]]
- [[Reduced KKT System]]
- [[08 - Schur Complement]]
- [[10 - NSD Algorithm Overview]]
