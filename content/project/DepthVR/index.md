---
title: Real-Time Temporally Consistent Depth Completion for VR-Teleoperated Robots
summary: Real-time depth completion and 3D reconstruction system for enhanced VR-based robot control. Temporally consistent point cloud reconstruction.
tags:
  - CV
date: 2024-07-01

links:
- name: Unity
  url: https://github.com/h2r/GHOST/tree/optical_flow
- name: Model
  url: https://github.com/chengfanli/Realtime-Depth-Estimation-Nconv
- name: Abstract
  url: https://chengfanli.github.io/about/src/VRteleop/TeleNetAbstract.pdf
---


<!-- <img src="https://chengfanli.github.io/about/src/VRteleop/system.png" alt="teaser" style="zoom:50%;" /> -->

## Real-Time Temporally Consistent Depth Completion for VR-Teleoperated Robots

High-quality visual perception is essential for precise control and interaction in VR-teleoperated robotics. Existing systems are often challenged by sparse, noisy inputs and high latency, emphasizing the need for real-time, temporally consistent, and dense point cloud reconstruction. 

\[[Unity Repo](https://github.com/h2r/GHOST/tree/optical_flow)\]
\[[Model Repo](https://github.com/chengfanli/Realtime-Depth-Estimation-Nconv)\]
\[[Abstract](https://chengfanli.github.io/about/src/VRteleop/TeleNetAbstract.pdf)\]

## Overview

<img src="https://chengfanli.github.io/about/src/VRteleop/overview.png" alt="teaser" style="zoom:50%;" />

In this project, we present a real-time depth completion and point cloud reconstruction system specifically designed for VR-teleoperated spot robots. We employ an algebraically-constrained, normalized CNN to propagate depth and confidence through multi-modal fusion within a multi-scale network regulated by a gradient matching loss. 

Additionally, we implement a spatial-temporal geometry-aware filter that leverages online optical flow and pose estimation to ensure temporally consistent point cloud reconstruction. 

This system achieves a rendering speed of 50 FPS, enhancing the visual quality and teleoperation experience.

## Demo

### Point Cloud Demo

Real-time depth completion

Spatial-temporal geometry-aware filter

Temporally consistent point cloud reconstruction

<video width="640" height="360" controls>
  <source src="https://chengfanli.github.io/about/src/VRteleop/final.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

### VR Teleoperation Demo

<video width="640" height="360" controls>
  <source src="https://chengfanli.github.io/about/src/VRteleop/telenet_small.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>


## Experiments

### Depth Completion
Unguided propagation model + RGB guided multi-scale multi-modal fusion

Left Camera: Sparse Depth

Right Camera: Depth completion Result

<video width="640" height="360" controls>
  <source src="https://chengfanli.github.io/about/src/VRteleop/s-d.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

### Temporally Consistent Depth Refinement
Pose estimation + Optical flow estimation + Spatial-temporal geometry-aware filter

Left Camera: Depth completion + native frame mean averaging

Right Camera: Depth completion + Temporally Consistent Depth Refinement (now the transition become smoother! and it is also effective for static scene) 

<video width="640" height="360" controls>
  <source src="https://chengfanli.github.io/about/src/VRteleop/cvd.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>


<!-- 
<video width="640" height="360" controls>
  <source src="https://chengfanli.github.io/about/src/VRteleop/final.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

Video4
Left/Right Camera: Depth completion +Temporally Consistent Depth Refinement + Point Cloud Inpainting -->