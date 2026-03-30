---
title: Dummy Constraints and Dummy-Constraint Duals
tags: [decomposition, sensitivity, duals]
aliases: [Dummy Duals]
---

# Dummy Constraints and Dummy-Constraint Duals

This is the key coupling idea in the decomposition.

## Why introduce a dummy constraint?

The upper-level problem has shared variables $x$, while lower-level subproblem $i$ wants a local variable it can optimize with directly.

So introduce a local copy $\delta_i$ and connect it to $x$ using

$$
\delta_i-G_i x = C_{d,i}(q_{+,i}-q_{-,i}).
$$

Ignoring the relaxation variables, the core idea is just

$$
\delta_i=G_i x.
$$

This is called a dummy constraint because $\delta_i$ is an artificial local copy, not a new physical law.

## Lower-level Lagrangian term

The lower Lagrangian contains a term

$$
\gamma_i^T(\delta_i-G_i x-C_{d,i}(q_{+,i}-q_{-,i})).
$$

The vector $\gamma_i$ is the multiplier of the dummy constraint.

## Meaning of $\gamma_i$

$\gamma_i$ is a sensitivity or shadow price of enforcing the artificial coupling.

Intuitively:

- if period $i$ can satisfy the upper request easily, $\gamma_i$ is small,
- if satisfying the requested target is expensive or restrictive, $\gamma_i$ is large in magnitude.

## Constraint perturbation view

If the dummy constraint were written as

$$
\delta_i-G_i x=b_i,
$$

then the multiplier $\gamma_i$ would describe how the lower optimal value
changes under a small perturbation $\Delta b_i$. That is why $\gamma_i$ can be
read as the shadow price of the coupling requirement, not just as an algebraic
multiplier.

## Why $G_i$ is there

$G_i$ maps the global upper-level vector $x$ into the smaller coupling space
seen by period $i$. If period $i$ only depends on a few components of $x$, then
$G_i$ acts like a selector matrix that picks those components and builds the
local target $G_i x$.

## Why does it enter the upper gradient?

Differentiate the dummy term with respect to $x$:

$$
\frac{\partial}{\partial x}\left[\gamma_i^T(\delta_i-G_i x-\cdots)\right]
=
-G_i^T\gamma_i.
$$

Summing across periods gives the lower-level contribution to the upper gradient:

$$
m=-\sum_i G_i^T\gamma_i.
$$

So the dummy dual is the first-order feedback signal from lower subproblems to the upper-level optimizer.

## Tiny toy model

Consider

$$
\min_\delta (\delta-80)^2\quad \text{s.t.}\quad \delta-x=0.
$$

The Lagrangian is

$$
L(\delta,\gamma)=(\delta-80)^2+\gamma(\delta-x).
$$

Stationarity gives

$$
2(\delta-80)+\gamma=0.
$$

Since $\delta=x$, we get

$$
\gamma=-2(x-80).
$$

The optimal-value function is

$$
\Phi(x)=(x-80)^2,
$$

so

$$
\frac{d\Phi}{dx}=2(x-80)=-\gamma.
$$

This is the simplest demonstration of why the multiplier of the coupling constraint becomes a gradient signal.

## Links

- [[02 - Lagrangian and Multipliers]]
- [[09 - Value Function Sensitivity]]
- [[10 - NSD Algorithm Overview]]
- [[08 - Schur Complement]]
- [[12 - Glossary]]
