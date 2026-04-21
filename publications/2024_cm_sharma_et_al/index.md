---
title: Velocity-based space-time FEMs for solid dynamics problem generalized framework for linear basis functions in time
author: Sharma et al.
authors: [Vikas Sharma, Kazunori Fujisawa, Yuki Kuroda]
doi: https://doi.org/10.1007/s00466-024-02461-9
keywords: [Space-time, FEM, Unconditionally stable, Third order accurate, Discontinuous Galerkin method,
Elastodynamics]
date: "03/11/2024"
image: ./figures/thumbnail.svg
---

## Abstract

Time discontinuous Galerkin Space-Time Finite Element Method (ST/FEM) can be used for developing arbitrary high-order accurate and unconditionally stable time integration schemes for elastodynamics problems. The existing ST/FEMs can be classified as the single-field and two-field ST/FEM: in the former method, either displacement or velocity, is independent and discontinuous in time. In contrast, in the latter method, both displacement and velocity fields are independent and discontinuous in time. Both methods have third-order accuracy for linear interpolation in time, higher than typical time integration schemes used in semi-discretized. However, these methods currently lack a unified computational framework, so each method requires a separate implementation. Therefore, the main goal of the present study is to develop a generalized computational framework that can facilitate the derivation and implementation of the existing linear-in-time ST/FEMs in a unified manner. This framework is developed by realizing that existing methods differ through the treatments of displacement-velocity relationships, which can be unified through displacement functions. In addition, by employing this framework, a new ST/FEM, which is designated as LC v-ST/FEM, is derived from the linear combination of displacement functions of single-field and two-field ST/FEMs. LC v-ST/FEM contains a user-defined parameter $\alpha \in [0,1]$, which can be used for controlling the high-frequency dissipation characteristics. From finite difference analysis and numerical solutions of benchmark problems, it is demonstrated that the proposed method is the third order accurate in time, unconditionally stable, and contains negligible numerical dispersion error for all $0 \le \alpha \le 1$. Moreover, for $\alpha \ne 0$, the method can attenuate the spurious high-frequency components from the velocity and displacement fields.
