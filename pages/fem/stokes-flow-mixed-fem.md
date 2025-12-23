---
title: 'Mixed finite element method for stokes flow'
tags: [FEM, Stokes flow, Mixed FEM]
summary: In this post formulation and implementation procedure of mixed finite element method for stationary Stokes flow is presented.
authors:
  - Vikas Sharma
date: 2022-04-22
---


# Mixed finite element method for Stokes flow

## Flow characteristics:

- Creeping flow
- Convective acceleration is negligible
- Incompressible

## Strong form:

$$
\rho\frac{\partial\mathbf{v}}{\partial t}+\nabla p-\mu\nabla^{2}\mathbf{v}-\rho\mathbf{b}=\mathbf{0},
$$

$$
\nabla \cdot \mathbf{v} = 0
$$

Essential boundary condition:

$$
v_{i} = v_{ig}, \text{ on } \Gamma_{i}^{g}
$$

Neumann boundary condition:

$$
-pn_{i}+\mu \frac{\partial v_i}{\partial x_j} n_{j}=h_i, \text{ on } \Gamma_{i}^{h}
$$

here, note that $h_{i}$ is not the real traction, it is called the pseudo traction.

## Weak form:

Find $\mathbf{v}$ and $p$ such that for all $\delta \mathbf{v}$ and $\delta p$ following is true:

$$
B_{G}\left(\delta\mathbf{v},\delta p;\mathbf{v},p\right)=L_{G}(\delta\mathbf{v},\delta p)
$$

where,

$$
B_{G}\left(\delta\boldsymbol{v},\delta p;\boldsymbol{v},p\right)=\int_{\Omega}\left(-\frac{\partial\delta v_{i}}{\partial x_{i}}p+\frac{\partial\delta v_{i}}{\partial x_{j}}\mu\frac{\partial v_{i}}{\partial x_{j}}+\delta p\frac{\partial v_{j}}{\partial x_{j}}\right)d\Omega
$$

$$
L_{G}(\delta\mathbf{v},\delta p)=\int_{\Omega}\delta v_{i}\rho b_{i}d\Omega+\int_{\Gamma_{i}^{h}}\delta v_{i}h_{i}d\Omega
$$

## Proof of weak form:

The process of getting the above mentioned weak form is given below.

First, multiple the residual of momentum equation with the test function $\delta v$ and the continuity equation with the $\delta p$, and integrate over the entire domain.


$$
\int_{\Omega}\delta v_{i}\left\{ \frac{\partial p}{\partial x_{i}}-\mu\frac{\partial^{2}v_{i}}{\partial x_{j}\partial x_{j}}-\rho b_{i}\right\} d\Omega+\int_{\Omega}\delta p\frac{\partial v_{j}}{\partial x_{j}}d\Omega=0
$$

Now we use integration by parts and Green's divergence theorem to pressure and shear stress gradient terms. Then we obtain the following

$$
\begin{split}-\int_{\Omega}\frac{\partial\delta v_{i}}{\partial x_{i}}pd\Omega+\int_{\Omega}\frac{\partial\delta v_{i}}{\partial x_{j}}\mu\frac{\partial v_{i}}{\partial x_{j}}d\Omega\\ -\int_{\Gamma}\delta v_{i}\left(-pn_{i}+\mu\frac{\partial v_{i}}{\partial x_{j}}\right)n_{j}d\Omega\\ -\int_{\Omega}\delta v_{i}\rho b_{i}d\Omega+\int_{\Omega}\delta p\frac{\partial v_{j}}{\partial x_{j}}d\Omega\\ =0 \end{split}
$$

now noting that

$$
\delta v_{i}=0 \text{ on } \Gamma_{i}^{g}
$$

and

$$
-pn_{i}+\mu \frac{\partial v_i}{\partial x_j} n_{j}=h_i, \text{ on } \Gamma_{i}^{h}
$$

then,

$$
\begin{split}-\int_{\Omega}\frac{\partial\delta v_{i}}{\partial x_{i}}pd\Omega+\int_{\Omega}\frac{\partial\delta v_{i}}{\partial x_{j}}\mu\frac{\partial v_{i}}{\partial x_{j}}d\Omega\\ +\int_{\Omega}\delta p\frac{\partial v_{j}}{\partial x_{j}}d\Omega\\ -\int_{\Omega}\delta v_{i}\rho b_{i}d\Omega-\int_{\Gamma_{i}^{h}}\delta v_{i}h_{i}d\Omega\\ =0 \end{split}
$$

or,

$$
\begin{aligned}\int_{\Omega}\left(-\frac{\partial\delta v_{i}}{\partial x_{i}}p+\frac{\partial\delta v_{i}}{\partial x_{j}}\mu\frac{\partial v_{i}}{\partial x_{j}}+\delta p\frac{\partial v_{j}}{\partial x_{j}}\right)d\Omega\\ =\int_{\Omega}\delta v_{i}\rho b_{i}d\Omega+\int_{\Gamma_{i}^{h}}\delta v_{i}h_{i}d\Omega \end{aligned}
$$

This completes the proof.

## Finite element approximation

For test and trial function of pressure field use the following finite element approximation:

$$
\delta p=\sum_{I=1}^{n_{n}}\delta p_{I}N_{p}^{I}
$$

$$
p=\sum_{I=1}^{n_{n}} p_{I}N_{p}^{I}
$$

where, $\delta p_I$ and $p_I$ are the nodal values of $\delta p$ and $p$, and $N^I_p$ is the shape function.

For test and trial function of velocity field we use the following finite element approximation:

$$
\delta v_{iI}=\sum_{I=1}^{n_{n}}\delta v_{iI}N_{v}^{I}
$$

$$
v_{iI}=\sum_{I=1}^{n_{n}} v_{iI}N_{v}^{I}
$$

where, $\delta v_{iI}$ and $v_{iI}$ are the nodal value of $i$th component of velocity field, and $N_{v}^I$ is the shape function of velocity field.

## Finite element discretization

$$
\begin{aligned}\int_{\Omega}-\frac{\partial\delta v_{i}}{\partial x_{i}}pd\Omega & =-\delta v_{iI}\left[\int_{\Omega}\frac{\partial N_{v}^{I}}{\partial x_{i}}N_{p}^{J}d\Omega\right]p_{J}\\ & =\delta v_{iI}\left[G_{i1}^{IJ}\right]p_{J} \end{aligned}
$$

$$
\begin{aligned}\int_{\Omega}\frac{\partial\delta v_{i}}{\partial x_{j}}\mu\frac{\partial v_{i}}{\partial x_{j}}d\Omega & =\delta v_{iI}\int_{\Omega}\frac{\partial N_{v}^{I}}{\partial x_{j}}\mu\frac{\partial v_{i}}{\partial x_{j}}d\Omega\\ & =\delta v_{iI}\left[\int_{\Omega}\frac{\partial N_{v}^{I}}{\partial x_{j}}\mu\frac{\partial N_{v}^{J}}{\partial x_{j}}d\Omega\right]v_{iJ}\\ & =\delta v_{iI}\left[K_{ij}^{IJ}\right]v_{jJ} \end{aligned}
$$

$$
\begin{aligned}\int_{\Omega}\delta p\frac{\partial v_{i}}{\partial x_{i}}d\Omega & =\delta p_{I}\left[\int_{\Omega}N_{p}^{I}\frac{\partial N_{v}^{J}}{\partial x_{i}}d\Omega\right]v_{iJ}\\ & =\delta p_{I}\left[-G_{1i}^{JI}\right]v_{iJ} \end{aligned}
$$

$$
\begin{aligned}\int_{\Omega}\delta v_{i}\rho b_{i}d\Omega+\int_{\Gamma_{i}^{h}}\delta v_{i}h_{i}d\Omega & =\delta v_{iI}\left\{ \int_{\Omega}N_{v}^{I}\rho b_{i}d\Omega+\int_{\Gamma_{i}^{h}}N_{v}^{I}h_{i}ds\right\} \\ & =\delta v_{iI}\left\{ F_{iI}\right\} \end{aligned}
$$

where,

$$
G_{i1}^{IJ}=-\int_{\Omega}\frac{\partial N_{v}^{I}}{\partial x_{i}}N_{p}^{J}d\Omega
$$

$$
K_{ij}^{IJ}=\delta_{ij}\int_{\Omega}\frac{\partial N_{v}^{I}}{\partial x_{k}}\mu\frac{\partial N_{v}^{J}}{\partial x_{k}}d\Omega
$$

$$
F_{iI}=\int_{\Omega}N_{v}^{I}\rho b_{i}d\Omega+\int_{\Gamma_{i}^{h}}N_{v}^{I}h_{i}ds
$$

## System of linear equation

The system of linear equation is given by following.
$$
\left[\begin{array}{cc} \mathbf{K} & \mathbf{G}\\ \mathbf{G}^{T} & \mathbf{0} \end{array}\right]\left\{ \begin{array}{c} \mathbf{V}\\ \mathbf{P} \end{array}\right\} =\left\{ \begin{array}{c} \mathbf{F}\\ \mathbf{0} \end{array}\right\}
$$

