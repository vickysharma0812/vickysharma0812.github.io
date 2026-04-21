---
title: An Energy-based Overset Finite Element Method for Pseudo-static Structural Analysis
authors: [Haruka Tomobe, Vikas Sharma, Harusato Kimura, Hitoshi Morikawa]
doi: https://doi.org/10.1007/s10915-023-02113-9
keywords: [Overset mesh method, Finite element method, Composite structures, Civil engineering, Agricultural Engineering]
categories: [Journal paper]
date: "01/28/2023"
image: ./figures/thumbnail.png
abstract: >
  This paper addresses a simple energy-based overset finite element method (EbO-FEM) to solve pseudo-static deformation problems consisting of overlapped meshes based on the domain composition method (DCM). This scheme is a non-iterative equation-based method for enforcing the continuity of the displacement field. Hence, the scheme consumes possible minimal computational costs for deformation problems with non-conforming overlapping meshes. The system’s total energy is augmented with continuity constraint energy (CCE) which is a function of the gaps in the displacement field between two overlapping regions. Subsequently, two conventional integration schemes, the Gauss-point projection, and the point-to-point projection, are utilized to discretize the CCE. It is confirmed that both schemes can yield accurate and unique solutions in the overlapped region of the finite element meshes. Further, we proposed a dimensionless relative penalty parameter (DRP). We found that DRP ranging between 1 to 10 is appropriate to robustly obtain accurate solutions for a wide range of scales, stiffness, and geometries, which is supported by three numerical simulations without increasing computational costs after assembling the global matrices and vectors.
---

## Executive Summary

This paper addresses a simple energy-based overset finite element method (EbO-FEM) to solve pseudo-static deformation problems consisting of overlapped meshes based on the domain composition method (DCM). This scheme is a non-iterative equation-based method for enforcing the continuity of the displacement field. Hence, the scheme consumes possible minimal computational costs for deformation problems with non-conforming overlapping meshes. The system’s total energy is augmented with continuity constraint energy (CCE) which is a function of the gaps in the displacement field between two overlapping regions. Subsequently, two conventional integration schemes, the Gauss-point projection, and the point-to-point projection, are utilized to discretize the CCE. It is confirmed that both schemes can yield accurate and unique solutions in the overlapped region of the finite element meshes. Further, we proposed a dimensionless relative penalty parameter (DRP). We found that DRP ranging between 1 to 10 is appropriate to robustly obtain accurate solutions for a wide range of scales, stiffness, and geometries, which is supported by three numerical simulations without increasing computational costs after assembling the global matrices and vectors.
