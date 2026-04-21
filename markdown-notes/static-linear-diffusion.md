# Static Diffusion Problem

Strong form in terms of $u$, where $f$ is the source density.

$$
-\nabla\cdot\mathbf{k}\nabla u=f
$$

The mixed form of the problem is given in the form of flux $\mathbf{q}$ and $u$.

$$
\nabla\cdot\mathbf{q}=f
$$

$$
\mathbf{q}=-\mathbf{k}\nabla u
$$

Dirichlet boundary condition is given as:

$$
u=u_{0}
$$

Neumann boundary condition in terms of outgoing flux given in by

$$
\mathbf{q}\cdot\mathbf{n}=h_{out}
$$

or

$$
-\mathbf{k}\nabla u\cdot\mathbf{n}=h_{out}
$$

Neumann boundary condition in terms of incoming flux is given by

$$
-\mathbf{q}\cdot\mathbf{n}=h_{in}
$$

or

$$
\mathbf{k}\nabla u\cdot\mathbf{n}=h_{in}
$$

Integral form

$$\int_{\Omega}fd\Omega-\int_{\Omega}\nabla\cdot\mathbf{q}d\Omega=0$$

$$\int_{\Omega}fd\Omega-\int_{\Gamma_{h}}\mathbf{q}\cdot\mathbf{n}ds=0$$

## Dirichlet problem

In the case of Dirichlet problem, the strong form is given as follows.

$$-\nabla\cdot\mathbf{k}\nabla u=f$$

$$u=u_{0}\text{ on }\partial\Omega$$

## Neumann problem

In the case of Neumann problem, the strong form is given as follows:

$$-\nabla\cdot\mathbf{k}\nabla u=f$$

$$\mathbf{k}\nabla u\cdot\mathbf{n}=h_{in}$$

## Example 1

- Dirichlet problem
- Domain is unit square.
- Exact solution is given by$u=x_{1}x_{2}$
- Boundary condition:
  - Bottom, $y_{1}=0$, u=0
  - Right, $x_{1}=1$, $u=x_{2}$
  - Top, $x_{2}=1$, $u=x_{1}$
  - Left, $x_{1}=0$, $u=0$

## Example 2

- Dirichlet problem
- Domain is unit square.
- Exact solution is given by

$$
\begin{aligned}u & =16x_{1}x_{2}\left(1-x_{1}\right)\left(1-x_{2}\right)\\
& =16\left(x_{1}-x_{1}^{2}\right)\left(x_{2}-x_{2}^{2}\right)
\end{aligned}
$$

$$
\frac{\partial u}{\partial x_{1}}=16\left(1-2x_{1}\right)\left(x_{2}-x_{2}^{2}\right)
$$

$$
\frac{\partial^{2}u}{\partial x_{1}\partial x_{1}}=-32\left(x_{2}-x_{2}^{2}\right)
$$

$$
\frac{\partial u}{\partial x_{2}}=16\left(1-2x_{2}\right)\left(x_{1}-x_{1}^{2}\right)
$$

$$
\frac{\partial^{2}u}{\partial x_{2}\partial x_{2}}=-32\left(x_{1}-x_{1}^{2}\right)
$$

$$
f\left(x_{1},x_{2}\right)=32\left(x_{1}-x_{1}^{2}\right)+32\left(x_{2}-x_{2}^{2}\right)
$$

- Boundary condition:
  - Bottom, u=0
  - Right, $u=0$
  - Top, $u=0$
  - Left, $u=0$

## Example 3

- Dirichlet-Neumann Problem
- Domain is unit square
- Exact solution is given by

$$
\begin{aligned}u & =16x_{1}x_{2}\left(1-x_{1}\right)\left(1-x_{2}\right)\\
& =16\left(x_{1}-x_{1}^{2}\right)\left(x_{2}-x_{2}^{2}\right)
\end{aligned}
$$

$$\frac{\partial u}{\partial x_{1}}=16\left(1-2x_{1}\right)\left(x_{2}-x_{2}^{2}\right)$$

$$\frac{\partial u}{\partial x_{2}}=16\left(1-2x_{2}\right)\left(x_{1}-x_{1}^{2}\right)$$

Body force is given by:

$$f\left(x_{1},x_{2}\right)=32\left(x_{1}-x_{1}^{2}\right)+32\left(x_{2}-x_{2}^{2}\right)$$

- Neumann boundary condition at left (x=0)

$$h_{in}:=\mathbf{k}\nabla u\cdot\mathbf{n}=-16\left(x_{2}-x_{2}^{2}\right)$$

- Neumann boundary condition at bottom (y=0)

$$h_{in}:=\mathbf{k}\nabla u\cdot\mathbf{n}=-\frac{\partial u}{\partial x_{2}}=-16\left(x_{1}-x_{1}^{2}\right)$$

## Example 4

- Dirichlet-Neumann Problem
- Domain is unit square
- Exact solution is given by

$$\begin{aligned}u & =16x_{1}x_{2}\left(1-x_{1}\right)\left(1-x_{2}\right)\\
& =16\left(x_{1}-x_{1}^{2}\right)\left(x_{2}-x_{2}^{2}\right)
\end{aligned}$$

$$\frac{\partial u}{\partial x_{1}}=16\left(1-2x_{1}\right)\left(x_{2}-x_{2}^{2}\right)$$

$$\frac{\partial u}{\partial x_{2}}=16\left(1-2x_{2}\right)\left(x_{1}-x_{1}^{2}\right)$$

Body force is given by:

$$f\left(x_{1},x_{2}\right)=32\left(x_{1}-x_{1}^{2}\right)+32\left(x_{2}-x_{2}^{2}\right)$$
- Neumann boundary condition at left

$$h_{in}:=\mathbf{k}\nabla u\cdot\mathbf{n}=-16\left(x_{2}-x_{2}^{2}\right)$$

So the incoming flux on the left boundary is positive and varies along the vertical direction $16x_{2}(1-x_{2})$.
