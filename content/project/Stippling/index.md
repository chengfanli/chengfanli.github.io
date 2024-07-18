---
title: Stippling
summary: Generating stippled versions of images and videos based on [MLBG](https://kops.uni-konstanz.de/bitstreams/21672707-75c4-410b-a4ff-87b21c2ed630/download) and [WLGB](https://graphics.uni-konstanz.de/publikationen/Deussen2017LindeBuzoGray/index.html).
tags:
  - CG
date: 2024-04-01
# external_link: https://github.com/lllllcf/StipplingStudio

links:
- name: Trailer
  url: https://lllllcf.github.io/about/src/stippling.mp4
- name: Github
  url: https://github.com/lllllcf/StipplingStudio
---

<img src="../../about/src/Gallery/teaser.png" alt="teaser" style="zoom:50%;" />

# Stippling

CSCI 2240 Final Project for the Spring 2024 by Stippling Studio ([Chengfan Li](https://github.com/lllllcf), [Wendi Liao](https://github.com/wendi-liao) and [Yixuan Liu](https://github.com/Ahhhh2016))

Special thanks to the papers "[Weighted Linde-Buzo-Gray Stippling](https://graphics.uni-konstanz.de/publikationen/Deussen2017LindeBuzoGray/index.html)" and "[Multi-class Inverted Stippling](https://kops.uni-konstanz.de/bitstreams/21672707-75c4-410b-a4ff-87b21c2ed630/download)" that inspired this project.

\[[Demo Video](https://drive.google.com/file/d/1Hk2hPs_mVhhbz9oe8zTLfxnnQoMRPXu8/view?usp=drive_link)\]



## Overview

Based on the research and exploration of stippling, we have implemented the following features.

+ Weighted LBG algorithm based stippling that can convert grayscale image to stippling.

+ Visualization of Voronoi diagrams, as well as splitting and merging of points.

+ Video stippling with low noise and minimal flickering using WLGB.

+ Multi-class Inverted Stippling for grayscale image.

+ Color Stippling with palette extraction.

+ UNet-based reconstruction model to restore stippling to grayscale images.



## WLBG

### Voronoi Diagram

<img src="https://lllllcf.github.io/about/src/Gallery/voronoi2.png" width="400">

Voronoi diagrams can be used to create a variety of amazing visual effects including stippling. In this project, we use [jc_voronoi](https://github.com/JCash/voronoi) to calculate voronoi diagram efficiently and assign pixels to voronoi cell based on edges and site position.

### Video Stippling

<img src="https://lllllcf.github.io/about/src/Gallery/tiger.gif" width="400">
We haven't integrated video stippling on the master branch yet, but there are some helpful python scripts included in the [VideoStippling](./VideoStippling) folder.

## MLBG

<img src="https://lllllcf.github.io/about/src/Gallery/monroe_with_ordering.png" width="200">


## Color Stippling

<img src="https://lllllcf.github.io/about/src/Gallery/color_with_filling.jpg" width="300">


## Reconstruction

<img src="https://lllllcf.github.io/about/src/Gallery/model.png" width="500">

### Data

[Pre-trained model](https://drive.google.com/file/d/1wNgoFfu8BveQth--_sxytfBQHz6F83pZ/view?usp=drive_link): download from gdrive and put into [checkpoints](./Reconstruction/checkpoints) folder.

[Processed data for training](https://drive.google.com/drive/folders/1WmYop4yAKnwpcS6ffFvmi2NawybhoEtK?usp=drive_link): download from gdrive and put into [data](./Reconstruction/data) folder.

[Raw data](https://drive.google.com/file/d/1ddujNdD7BLoh5h58VGwizlL-kDieatXy/view?usp=drive_link): contains all color images and grayscale images without preprocessing.

### Results

<img src="https://lllllcf.github.io/about/src/Gallery/77_stippling.png" width="300"> <img src="https://lllllcf.github.io/about/src/Gallery/77_reconstruction.png" width="300">

Use [this link](https://drive.google.com/file/d/1rNqYqDoWK2uVU3JlxZ1rmFFiMoJb_Uys/view?usp=drive_link) to download the results of all images in the test set.

### Stippling-Reconstruction Iterations

<img src="https://lllllcf.github.io/about/src/Gallery/S-L.png" width="500">

Here is the result obtained after using our model to continuously perform the Stippling-Reconstruction cycle on the grayscale image. Detailed results can be found [here](./Reconstruction/repeat_test/data).



## Gallery

<img src="https://lllllcf.github.io/about/src/Gallery/book.gif" width="500">

<img src="https://lllllcf.github.io/about/src/Gallery/monroe_with_ordering.png" width="200">    <img src="https://lllllcf.github.io/about/src/Gallery/filling.jpg" width="400">

<img src="https://lllllcf.github.io/about/src/Gallery/s_0378.png" width="300">    <img src="https://lllllcf.github.io/about/src/Gallery/s_1547.png" width="300">

<img src="https://lllllcf.github.io/about/src/Gallery/color_with_filling.jpg" width="500">

 <img src="https://lllllcf.github.io/about/src/Gallery/s_0019.png" width="300"> <img src="https://lllllcf.github.io/about/src/Gallery/s_1503.png" width="300">



## References

Deussen, Oliver, Marc Spicker, and Qian Zheng. "Weighted linde-buzo-gray stippling." *ACM Transactions on Graphics (TOG)* 36.6 (2017): 1-12.

Christoph Schulz, Kin Chung Kwan, Michael Becher, Daniel Baumgartner, Guido Reina, Oliver Deussen, and Daniel Weiskopf. 2021. Multi-Class Inverted Stippling. *ACM Trans*. Graph. 40, 6 (2021)

Tan, J., Echevarria, J. and Gingold, Y., 2018. Efficient palette-based decomposition and recoloring of images via RGBXY-space geometry. ACM Transactions on Graphics (TOG), 37(6), pp.1-10.

