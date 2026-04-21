---
title: Velocity-based space-time finite element method for large deformation analysis of solids incorporating arbitrary moving mesh and hypoelastic constitutive model
authors: [Shion Shimizu, Vikas Sharma, Kazunori Fujisawa]
author: Shimizu et al.
doi: https://doi.org/10.11421/jsces.2023.20230004
keywords: [Velocity-based space-time finite element method, Large deformation analysis of solids, Arbitrary moving mesh, Stress update, Geometrical nonlinearity, Iterative method]
date: "04/28/2023"
image: ./figures/thumbnail.png
abstract: >
  本論文は，任意のメッシュ移動を伴う固体の大変形解析を可能とする速度型Space-time有限要素法（v-ST/FEM）を提案するものである．v-ST/FEMの特徴は時空間領域での簡潔かつ厳密な定式法にあり，ここでは亜弾性構成式を導入した準静的問題を対象とする．移動メッシュ上で計算されるCauchy応力の更新には，メッシュと固体変形の相対速度による移流を考慮した微分形を利用することで，速度のみを未知数とする弱形式が得られる．離散化された方程式に対して，メッシュと応力を更新する繰り返し計算を行い，それにより幾何学的非線形性を考慮するアルゴリズムを提示する．提案手法を一様な引張変形，回転する円筒の圧縮変形，および非一様な引張変形の3つの問題に適用した結果，AMMを用いた場合であっても，ラグランジュ型のメッシュ更新を行う場合と同等の計算精度を示し，AMMを利用できる同手法の大回転／大変形問題への適用性を明らかにした．
---

## Abstract

本論文は，任意のメッシュ移動を伴う固体の大変形解析を可能とする速度型Space-time有限要素法（v-ST/FEM）を提案するものである．v-ST/FEMの特徴は時空間領域での簡潔かつ厳密な定式法にあり，ここでは亜弾性構成式を導入した準静的問題を対象とする．移動メッシュ上で計算されるCauchy応力の更新には，メッシュと固体変形の相対速度による移流を考慮した微分形を利用することで，速度のみを未知数とする弱形式が得られる．離散化された方程式に対して，メッシュと応力を更新する繰り返し計算を行い，それにより幾何学的非線形性を考慮するアルゴリズムを提示する．提案手法を一様な引張変形，回転する円筒の圧縮変形，および非一様な引張変形の3つの問題に適用した結果，AMMを用いた場合であっても，ラグランジュ型のメッシュ更新を行う場合と同等の計算精度を示し，AMMを利用できる同手法の大回転／大変形問題への適用性を明らかにした．

