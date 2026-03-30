---
title: Reduced KKT System
tags: [kkt, decomposition, reduction]
aliases: [Reduced Newton System]
---

# Reduced KKT System

In the NSD derivation, the phrase "reduced KKT system" does **not** mean the
final Schur-complement system yet. It means the lower Newton/KKT system after
the interior-point complementarity clutter has already been condensed out.

## Three levels of the same sensitivity system

For one lower period problem, it helps to distinguish:

1. the raw primal-dual interior-point KKT system,
2. the reduced KKT system,
3. the Schur-reduced system in dummy-dual space.

These are not three different theories. They are three algebraic views of the
same local lower sensitivity equations after more and more variables are
eliminated.

## Raw primal-dual interior-point system

Before any reduction, the lower Newton system contains:

- primal lower variables,
- equality-constraint multipliers,
- slack or inequality-related multipliers,
- complementarity or barrier equations,
- the dummy-constraint multiplier $\gamma_i$.

So this is the most detailed solver-oriented form of the lower sensitivity
equations.

## First reduction

The first reduction eliminates variables and equations that are only present
because of the interior-point treatment of inequalities and bounds.

After that elimination, the lower Newton system is rewritten as

$$
\begin{bmatrix} K_i & E_i\\ E_i^T & 0 \end{bmatrix}
\begin{bmatrix} \Delta y_i\\ \Delta \gamma_i \end{bmatrix}
=
-\begin{bmatrix} r_i\\ u_i \end{bmatrix}.
$$

Here:

- $y_i$ collects all remaining lower Newton variables except $\gamma_i$,
- $K_i$ is the reduced lower KKT block for those variables,
- $E_i$ is the Jacobian of the dummy constraint with respect to $y_i$.

This is already a **reduced** KKT system relative to the raw primal-dual one.

## What is inside $y_i$?

$y_i$ is not the full original NLP variable list. It is the remaining lower
Newton variable block after slack/complementarity-related updates have been
condensed out.

So $y_i$ contains the meaningful internal lower sensitivity variables, while
$\gamma_i$ is kept separate as the coupling dual the upper problem actually
cares about.

## Second reduction

The Schur complement performs a second reduction by eliminating $\Delta y_i$:

$$
K_i\Delta y_i + E_i\Delta\gamma_i = -r_i,
$$

$$
E_i^T\Delta y_i = -u_i.
$$

From the first equation,

$$
\Delta y_i = -K_i^{-1}r_i - K_i^{-1}E_i\Delta\gamma_i.
$$

Substitute into the second to get

$$
\bigl(E_i^T K_i^{-1} E_i\bigr)\Delta\gamma_i
=
u_i - E_i^T K_i^{-1}r_i.
$$

Define

$$
P_i = E_i^T K_i^{-1}E_i.
$$

Then the Schur-reduced system becomes

$$
P_i\Delta\gamma_i = u_i - E_i^T K_i^{-1}r_i.
$$

Now only the dummy-dual increment remains.

## Why the reductions happen in this order

The two eliminations serve different purposes:

- first reduction: remove solver artifacts from interior-point handling,
- second reduction: remove internal lower variables the upper level does not
  need to carry.

So the progression is

$$
\text{raw solver system}
\to
\text{reduced KKT system in }(y_i,\gamma_i)
\to
\text{Schur-reduced system in }\gamma_i.
$$

## Why the upper problem cares

The upper problem does not need the full lower Newton step. It needs the lower
behavior as seen through the dummy coupling.

That is why the first-order signal uses

$$
m=-\sum_i G_i^T\gamma_i,
$$

and the second-order signal uses

$$
M=\sum_i G_i^T P_i^{-1}G_i.
$$

The reduced KKT system is the algebraic bridge between the raw lower solver
structure and these upper-level derivative contributions.

## Links

- [[05 - Newton for Constrained Optimization]]
- [[06 - Interior-Point Methods]]
- [[08 - Schur Complement]]
- [[10 - NSD Algorithm Overview]]
- [[Barrier and Bound Sigma Terms]]
