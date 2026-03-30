---
title: NSD Algorithm Overview
tags: [nsd, decomposition, algorithm]
aliases: [Nonlinear Sensitivity-based Decomposition]
---

# NSD Algorithm Overview

This note collects the full algorithmic picture.

## Problem structure

The problem is split into:

- an upper-level problem in global variables $x$,
- many lower-level subproblems indexed by $i$.

Each lower subproblem contains local process variables and an artificial local copy $\delta_i$ of the upper-level quantity seen in period $i$.

The coupling is imposed through the dummy constraint

$$
\delta_i-G_i x = C_{d,i}(q_{+,i}-q_{-,i}).
$$

## What each lower problem returns

After solving lower problem $i$ at the current upper iterate, we extract:

1. the lower optimal value $\Phi_i$,
2. the dummy-constraint dual $\gamma_i$,
3. the local KKT matrices needed to form $K_i$ and $E_i$,
4. the reduced curvature operator via the [[08 - Schur Complement]].

## Extract / reduce / inject pattern

The workflow can be summarized as:

1. extract first- and second-order information from each solved lower problem,
2. reduce the lower KKT sensitivity system into dummy space,
3. inject the resulting gradient and Hessian contributions into the upper
   problem.

This is why the method keeps lower problems independent while still giving the
upper solver derivative-quality information.

## What the implementation needs from each lower solve

To build the reduced sensitivity system, the lower solve must provide:

- primal values for the local variables,
- dual values, especially the dummy multipliers $\gamma_i$,
- the Hessian blocks of the lower Lagrangian,
- Jacobians of the local constraints and dummy constraints,
- diagonal barrier/bound terms coming from the NLP solver formulation.

## What gets added and what gets stacked

Two different algebraic patterns appear in NSD:

- the upper objective, gradient, and Hessian are **added** in upper-variable
  space,
- the lower Newton variables are **stacked** inside bordered linear systems
  before elimination.

If

$$
x\in\mathbb{R}^{n_x},
$$

then

$$
\nabla f_0(x),\ m \in \mathbb{R}^{n_x},
\qquad
\nabla^2 f_0(x),\ M \in \mathbb{R}^{n_x\times n_x}.
$$

So the upper augmentation is ordinary same-shape addition:

$$
\nabla \Phi_0(x)=\nabla f_0(x)+m,
\qquad
\nabla^2 \Phi_0(x)=\nabla^2 f_0(x)+M.
$$

Concatenation appears only in the lower linearized KKT systems, where variables
such as $\Delta y_i$, $\Delta \gamma_i$, and $\Delta x$ are stacked into block
vectors.

## Gradient contribution

The lower contribution to the upper gradient is

$$
m=-\sum_i G_i^T \gamma_i.
$$

## Hessian contribution

The reduced Schur operator is

$$
P_i=E_i^T K_i^{-1}E_i,
$$

and the lower contribution to the upper Hessian is

$$
M=\sum_i G_i^T P_i^{-1}G_i.
$$

## Upper-level augmented derivatives

The upper solver then uses

$$
\nabla \Phi_0(x)=\nabla f_0(x)+m,
$$

and

$$
\nabla^2 \Phi_0(x)=\nabla^2 f_0(x)+M.
$$

So the upper-level optimizer behaves as if it had access to the derivatives of the embedded lower optimal-value function.

## Objective contribution

The augmented upper objective value is

$$
\Phi_0(x)=f_0(x)+\sum_i \Phi_i^*(x),
$$

so each lower problem contributes not only sensitivity information but also its
optimal scalar objective value.

## One outer iteration

1. Choose current upper iterate $x^l$.
2. Solve all lower subproblems in parallel or independently.
3. Extract each $\gamma_i^l$.
4. Build each reduced operator $P_i$ from the linearized lower KKT system.
5. Assemble
   $$
   m^l=-\sum_i G_i^T \gamma_i^l.
   $$
6. Assemble
   $$
   M^l=\sum_i G_i^T P_i^{-1} G_i.
   $$
7. Give the augmented gradient and Hessian to the upper-level NLP solver.
8. Update $x$ and repeat until convergence.

## Why this should work

Because the method is computing local first- and second-order derivatives of the true upper value function:

- first order from [[07 - Dummy Constraints and Dummy-Constraint Duals]],
- second order from [[08 - Schur Complement]] and lower KKT sensitivity.

See [[09 - Value Function Sensitivity]].

## Why this scales

The expensive lower linear algebra stays inside each subproblem, and the reduced
Schur operators live in the smaller coupling space rather than the full lower
variable space. That is what makes the method compatible with decomposition and
parallel lower solves.

## Global bordered-system view

Before the Schur complement is taken period by period, the global Newton picture
can be read as:

- each $K_i$ sits on a block diagonal for period $i$,
- each $E_i$ connects internal lower variables to the corresponding dummy dual,
- each $G_i$ maps the dummy-dual space back to the upper variable space.

So the global bordered system stacks all lower-period sensitivity blocks first,
then couples them to the upper step through the dummy-constraint structure.

## Links

- [[07 - Dummy Constraints and Dummy-Constraint Duals]]
- [[08 - Schur Complement]]
- [[09 - Value Function Sensitivity]]
- [[06 - Interior-Point Methods]]
- [[00 - MOC - NSD and Decomposition]]
- [[Reduced KKT System]]
- [[Barrier and Bound Sigma Terms]]
