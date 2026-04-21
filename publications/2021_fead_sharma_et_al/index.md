---
title: Space-Time Finite Element Method for Transient and Unconfined Seepage Flow Analysis
tags: [Space-time FEM, Unconfined seepage flow, Moving boundary problem]
keywords: [Space-time FEM, Unconfined seepage flow, Moving boundary problem]
categories: [Journal paper, year 2021]
authors: [Vikas Sharma, Kazunori Fujisawa, Akira Murakami]
doi: https://doi.org/10.1016/j.finel.2021.103632
date: "07/06/2021"
image: ./figures/thumbnail.svg
abstract: >
  This paper aims to develop a moving-mesh type Finite Element Method for the computation of the transient unconfined seepage flow through the porous medium. The proposed method is based on the time discontinuous Galerkin Space-Time Finite Element Method (ST/FEM). It solves the seepage problem in the saturated region. The primary unknown in ST/FEM is piezometric pressure. Fluid velocities are derived from the pressure using Darcy's law. Further, an iterative algorithm has been proposed in this paper to implement the proposed method. In each iteration step, the computation domain is updated according to the flow velocity on the phreatic boundary. Subsequently, internal nodes are moved using the mesh moving technique to accommodate the newly updated computation domain. The mesh moving technique, which is discussed in this paper, is based on an elasticity problem. ST/FEM is employed to analyze several unconfined seepage flow problems, and results of steady state solutions are compared with those available in the literature to demonstrate the efficacy of the proposed scheme.
---

## Executive Summary

This paper aims to develop a moving-mesh type Finite Element Method for the computation of the transient unconfined seepage flow through the porous medium. The proposed method is based on the time discontinuous Galerkin Space-Time Finite Element Method (ST/FEM). It solves the seepage problem in the saturated region. The primary unknown in ST/FEM is piezometric pressure. Fluid velocities are derived from the pressure using Darcy's law. Further, an iterative algorithm has been proposed in this paper to implement the proposed method. In each iteration step, the computation domain is updated according to the flow velocity on the phreatic boundary. Subsequently, internal nodes are moved using the mesh moving technique to accommodate the newly updated computation domain. The mesh moving technique, which is discussed in this paper, is based on an elasticity problem. ST/FEM is employed to analyze several unconfined seepage flow problems, and results of steady state solutions are compared with those available in the literature to demonstrate the efficacy of the proposed scheme.
