---
title: Derivatives Gradient Jacobian Hessian
tags: [calculus, optimization, notation]
aliases: [Derivative Notation]
---

# Derivatives Gradient Jacobian Hessian

This note cleans up the notation that often gets mixed together.

## Scalar function of one variable

If

$$
f:\mathbb{R}\to\mathbb{R},
$$

then

- first derivative: $\frac{df}{dx}$,
- second derivative: $\frac{d^2f}{dx^2}$.

In this case, "gradient" and "first derivative" are basically the same idea, and "Hessian" and "second derivative" are also basically the same idea.

## Scalar function of many variables

If

$$
f:\mathbb{R}^n \to \mathbb{R},
$$

then the first derivative is usually represented as the gradient

$$
\nabla f(x)=
\begin{bmatrix}
\frac{\partial f}{\partial x_1}\\
\vdots\\
\frac{\partial f}{\partial x_n}
\end{bmatrix}.
$$

The second derivative is usually represented as the Hessian

$$
\nabla^2 f(x)=
\begin{bmatrix}
\frac{\partial^2 f}{\partial x_1^2} & \cdots & \frac{\partial^2 f}{\partial x_1 \partial x_n}\\
\vdots & \ddots & \vdots\\
\frac{\partial^2 f}{\partial x_n \partial x_1} & \cdots & \frac{\partial^2 f}{\partial x_n^2}
\end{bmatrix}.
$$

## Vector-valued functions

If

$$
F:\mathbb{R}^n\to\mathbb{R}^m,
$$

then the first derivative is usually represented by the Jacobian

$$
J_F(x)=\frac{\partial F}{\partial x}.
$$

This is the matrix that appears in [[04 - Newton's Method for Equations|Newton's method]] when solving a system $F(w)=0$.

## Optimization relevance

- gradient: first derivative of a scalar objective,
- Hessian: second derivative / curvature of a scalar objective,
- Jacobian: first derivative of a vector residual such as a KKT system.

In constrained optimization, the Newton system is built from the Jacobian of the KKT residual. One block of that Jacobian is the Hessian of the [[02 - Lagrangian and Multipliers|Lagrangian]].

## Subtle language point

Strictly speaking, the first derivative is a linear map, while the gradient is
the vector that represents that map after choosing coordinates and an inner
product. Likewise, the second derivative can be viewed as a bilinear operator,
while the Hessian is its matrix representation.

In optimization practice, people usually identify these pairs and simply say
"gradient = first derivative" and "Hessian = second derivative." That shorthand
is usually fine as long as the scalar-vs-vector distinction stays clear.

## Links

- [[01 - Optimization Problem Basics]]
- [[03 - KKT Conditions]]
- [[04 - Newton's Method for Equations]]
- [[05 - Newton for Constrained Optimization]]
