---
title: Arbitrary mesh‐moving velocity‐based space‐time finite element method for large deformation analysis of solids
authors: [Shion Shimizu, Vikas Sharma, Kazunori Fujisawa]
author: Shimizu et al.
doi: https://doi.org/10.1002/nme.7352
keywords: [Velocity-based space-time finite element method, Large deformation analysis of solids, Arbitrary moving mesh, Stress update, Geometrical nonlinearity, Iterative method]
date: "09/13/2023"
categories: [Journal paper]
image: ./figures/thumbnail.svg
---

## Abstract

This paper presents a new velocity-based space-time finite element method for computing the large deformation of solids over arbitrary Lagrange/Eulerian moving meshes. The proposed method is oriented toward quasi-static deformation problems with hypoelastic and neo-Hookean hyperelastic constitutive models. The Cauchy stress in the weak form of the linear momentum equation is explicitly described in terms of deformation velocity through consistent time integration of objective stress rates transferred in the arbitrary moving mesh. Consequently, the resultant system equation only contains the space-time nodal velocity as the primary unknown. An iterative algorithm for solving the discretized system equation is implemented, whereby the nonlinearities induced by geometrical change in the computational domain as well as nonlinear constitutive equations are computed in an iterative manner updating the stress and the strain over the moving mesh of the deforming domain. Three benchmark problems, such as uniform beam compression, thick-cylinder compression with superimposed rigid body rotation and extrusion of a column involving material loss, have been solved in order to examine the accuracy of the proposed numerical scheme. The numerical results have revealed the proper computation of the stress and the displacement of the solids undergoing the large deformation and rotation over the arbitrary Lagrange/Eulerian moving meshes, and have shown the validity and applicability of the proposed method with linear convergence of the iterative algorithm.
