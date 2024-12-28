---
title: Real-Time Temporally Consistent Depth Completion for VR-Teleoperated Robots
summary: Real-time depth completion and 3D reconstruction system for enhanced VR-based robot control. Temporally consistent point cloud reconstruction.
tags:
  - CV
date: 2024-11-11

links:
- name: Unity
  url: https://github.com/h2r/GHOST/tree/faisals-tests
- name: Model
  url: https://github.com/chengfanli/Realtime-Depth-Estimation-Nconv
- name: Abstract
  url: https://chengfanli.github.io/about/src/VRteleop/TeleNetAbstract.pdf
---


<!-- <img src="https://chengfanli.github.io/about/src/VRteleop/system.png" alt="teaser" style="zoom:50%;" /> -->

## Real-Time Temporally Consistent Depth Completion for VR-Teleoperated Robots

High-quality visual perception is essential for precise control and interaction in VR-teleoperated robotics. Existing systems are often challenged by sparse, noisy inputs and high latency, emphasizing the need for real-time, temporally consistent, and dense point cloud reconstruction. 

\[[Unity Repo](https://github.com/h2r/GHOST/tree/faisals-tests)\]
\[[Model Repo](https://github.com/chengfanli/Realtime-Depth-Estimation-Nconv)\]
\[[Abstract](https://chengfanli.github.io/about/src/VRteleop/TeleNetAbstract.pdf)\]

### Overview

<img src="https://chengfanli.github.io/about/src/VRteleop/overview.png" alt="teaser" style="zoom:50%;" />

In this project, we present a real-time depth completion and point cloud reconstruction system specifically designed for VR-teleoperated spot robots. We employ an algebraically-constrained, normalized CNN to propagate depth and confidence through multi-modal fusion within a multi-scale network regulated by a gradient matching loss. 

Additionally, we implement a spatial-temporal geometry-aware filter that leverages online optical flow and pose estimation to ensure temporally consistent point cloud reconstruction. 

This system achieves a rendering speed of 40 FPS, enhancing the visual quality and teleoperation experience.

### Demo

#### VR Teleoperation

<video width="640" height="360" controls>
  <source src="https://chengfanli.github.io/about/src/VRteleop/telenet_small.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

#### Point Cloud Demo

Real-time depth completion and point cloud reconstruction

<video width="640" height="360" controls>
  <source src="https://chengfanli.github.io/about/src/VRteleop/final.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

### Qualitative Comparison
#### Depth Completion

<img src="https://chengfanli.github.io/about/src/VRteleop/depth.png" alt="teaser" style="zoom:50%;" />

#### Consistent Point Cloud
The top row shows the final rendering results of the Spot moving through the dynamic scene, the middle row shows the result after frame averaging, and the last row shows the result after applying temporally consistent point cloud denoising. We can observe that the geometry of the chair is preserved when the Spot is moving.
<img src="https://chengfanli.github.io/about/src/VRteleop/consistent.png" alt="teaser" style="zoom:50%;" />

### More Results

#### Depth Completion Video
Unguided propagation model + RGB guided multi-scale multi-modal fusion

Left Camera: Sparse Depth

Right Camera: Depth completion Result

<video width="640" height="360" controls>
  <source src="https://chengfanli.github.io/about/src/VRteleop/s-d.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

#### Point Cloud Comparison
The top row shows the input RGB images, followed by depth maps and 3D reconstructions from DepthAnything-v2-Metric, BP-NET, and Ours.

<img src="https://chengfanli.github.io/about/src/VRteleop/pointcloud.png" alt="teaser" style="zoom:50%;" />

#### Quantitative Comparison

We evaluate the quantitative performance of five models using the dataset collected by the robot.
<img src="https://chengfanli.github.io/about/src/VRteleop/quantitative.png" alt="teaser" style="zoom:50%;" />
