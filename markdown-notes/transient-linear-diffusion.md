# Transient diffusion
	- Strong form in terms of $u$, where $f$ is the source density.
	- $$\frac{\partial\rho u}{\partial t}-\nabla\cdot\mathbf{k}\nabla u=f\left(\mathbf{x},t\right)$$
	- The mixed form of the problem is given in the form of flux $\mathbf{q}$ and $u$.
	- $$\frac{\partial\rho u}{\partial t}+\nabla\cdot\mathbf{q}=f\left(\mathbf{x},t\right)$$
	- $$\mathbf{q}=-\mathbf{k}\nabla u$$
	- Dirichlet boundary condition is given as:
		- $$u=u_{0}$$
	- Neumann boundary condition in terms of outgoing flux given in by
	  
	  $$\mathbf{q}\cdot\mathbf{n}=h_{out}$$
	  
	  or
	  
	  $$-\mathbf{k}\nabla u\cdot\mathbf{n}=h_{out}$$
	  
	  Neumann boundary condition in terms of incoming flux is given by
	  
	  $$-\mathbf{q}\cdot\mathbf{n}=h_{in}$$
	  
	  or
	  
	  $$\mathbf{k}\nabla u\cdot\mathbf{n}=h_{in}$$
-
- ## Semi discrete FEM
  
  Variation form
  
  $$B\left(\delta u,u\right)=L\left(\delta u\right)$$
  
  $$B\left(\delta u,u\right)=a\left(\delta u,u\right)+\left(\delta u,\frac{\partial\rho u}{\partial t}\right)$$
  
  $$L\left(\delta u\right)=\left(\delta u,f\right)+\left\langle \delta u,h_{in}\right\rangle$$
  
  $$a\left(\delta u,u\right)=\int_{\Omega}\frac{\partial\delta u}{\partial x_{i}}k_{ij}\frac{\partial u}{\partial x_{j}}d\Omega$$
  
  $$\left(\delta u,\frac{\partial\rho u}{\partial t}\right)=\int_{\Omega}\delta u\frac{\partial\rho u}{\partial t}d\Omega$$
  
  Discrete form
  
  $$\begin{align*}
  \mathbf{M}\frac{d\mathbf{U}}{dt}+\mathbf{K}\mathbf{U} & =\mathbf{F}\left(t\right)\\
  \end{align*}$$
  
  Semi-discrete finite element method
  
  $$MV_{n+1}+KU_{n+1}=F_{n+1}$$
  
  $$U_{n+1}=U_{n}+a_{1}\Delta tV_{n}+a_{2}\Delta tV_{n+1}$$
  
  $$a_{1}=\left(1-\alpha\right)$$
  
  $$a_{2}=\alpha$$
- $\alpha=0$ Forward difference (forward Euler), first order accurate, explicit method, conditionally stable.
- $\alpha=1$, Backward difference (backward Euler), first order accurate, implicit method, unconditionally stable
- $\alpha=0.5$, Trapezoidal rule, midpoint rule, Crank-Nicolson, second order accurate, implicit method, unconditionally stable
  
  $$U_{n+1}=U_{n}+a_{1}\Delta tV_{n}+a_{2}\Delta tV_{n+1}$$
  
  $$V_{n+1}=-\frac{1}{a_{2}\Delta t}U_{n}-\frac{a_{1}}{a_{2}\Delta t}V_{n}\Delta t+\frac{1}{a_{2}\Delta t}U_{n+1}$$