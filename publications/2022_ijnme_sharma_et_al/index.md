---
title: A methodology to control numerical dissipation characteristics of velocity based time discontinuous Galerkin space‐time finite element method
authors: [Vikas Sharma, Kazunori Fujisawa, Akira Murakami, Shuto Sasakawa]
author: Sharma et al.
doi: https://doi.org/10.1002/nme.7078
keywords: [controlled numerical dissipation, discontinuous Galerkin method, space-time FEM,
unconditional-stable, v-ST/FEM]
categories: [Journal paper, year 2022]
date: "07/14/2022"
image: ./figures/thumbnail.svg
abstract: >
  Direct time integration schemes are an integral part of the FEM simulation of structural dynamics problems. Such schemes should be at least second-order accurate, unconditionally stable, and numerically dissipates the high-frequency components. To this end, this paper develops a time integration scheme, called modified v-ST/FEM, which is based on the time-discontinuous Galerkin method. The proposed method employs an unsymmetric triangular bubble function for relating the displacement field to the velocity field. The modified v-ST/FEM contains two-parameter $\alpha \in (0, 0.5)$ and  $\beta \in (-1, \beta_{c})$ for controlling the dissipation of high-frequency components. A comprehensive study of the influence of $\alpha$ and $\beta$ on the numerical performance of the proposed method is conducted. It is found that the error in the solution increases when the value of $\alpha$ increases. However, for all practical purposes, $\beta$ has a negligible influence on the accuracy of the proposed method. The modified v-ST/FEM is second-order accurate for $\alpha \ne 0.0$, and third-order accurate for $\alpha=0.0$. The numerical efficacy of the modified v-ST/FEM is demonstrated by solving some benchmark problems and comparing its result to those obtained by other popular methods such as Trapezoidal rule, HHT-$\alpha$, and Bathe's scheme.
---

## Executive Summary

Direct time integration schemes are an integral part of the FEM simulation of structural dynamics problems. Such schemes should be at least second-order accurate, unconditionally stable, and numerically dissipates the high-frequency components. To this end, this paper develops a time integration scheme, called modified v-ST/FEM, which is based on the time-discontinuous Galerkin method. The proposed method employs an unsymmetric triangular bubble function for relating the displacement field to the velocity field. The modified v-ST/FEM contains two-parameter $\alpha \in (0, 0.5)$ and  $\beta \in (-1, \beta_{c})$ for controlling the dissipation of high-frequency components. A comprehensive study of the influence of $\alpha$ and $\beta$ on the numerical performance of the proposed method is conducted. It is found that the error in the solution increases when the value of $\alpha$ increases. However, for all practical purposes, $\beta$ has a negligible influence on the accuracy of the proposed method. The modified v-ST/FEM is second-order accurate for $\alpha \ne 0.0$, and third-order accurate for $\alpha=0.0$. The numerical efficacy of the modified v-ST/FEM is demonstrated by solving some benchmark problems and comparing its result to those obtained by other popular methods such as Trapezoidal rule, HHT-$\alpha$, and Bathe's scheme.
