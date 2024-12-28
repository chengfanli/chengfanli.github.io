---
title: Finite Element Simulation
summary: Developed deformable solid objects simulation based on tetrahedral meshes using FEM.
tags:
  - CG
date: 2024-03-20
# external_link: https://github.com/chengfanli/ProjectsCollection/blob/master/fem.md
---

Developed deformable solid objects simulation based on tetrahedral meshes using FEM.

### Code Logic

+ Extracting the surface mesh

  For each face, sort the vertex indices and store to the map `<index, index, index>` to `<count>`. Loop through all the tets to build the map and surface meshes is faces with `count == 1`. 

+ Computing and applying internal forces

  Calculate `F` and `stress` for each tet and loop through particles to update internal forces based on `f = F * stress * area * normal`. Detailed calculation of `F` and `stress` is shown on `utils.cpp`.

+ Collision resolution

  When a particle hits the collider, apply a penalty force to the tet in the direction of the normal of the collider. The magnitude of the penalty force is calculated by `f = k * |v|`. Any particle that is inside the collider will be projected out later.

+ Explicit integration method

  Store the original state and update the position and velocity of particles on midpoint. Then calculate one step `dx` and `dv` on the midpoint state and apply them to the original state.

### Extra Features

* Runge-Kutta 4 Integrator

  Store the original state. Take one step from original state and store `dx, dv` to `k1`. Take half step from original state and store `dx, dv` to `k2`.  Take half step from `k2` and store `dx, dv` to `k3`. Take one step from `k3` and store `dx, dv` to `k4`. Update from original state with `delta = 1 / 6 * (k1 + 2k2 + 2k3 + k4)`.

* Adaptive time stepping

  Take one step from original state to get state `xa`. Take two half step from original state to get state `xb`. Calculate the error based on `xa` and `xb`. Update the time step `t` to `t' = sqrt(max_error / error) * t`.

### Demo Video

* Single tetrahedron falling on the floor (`./inis/tet.ini` $\rightarrow$ `./demo-video/tet.mp4`)

  <video src="../../about/src/graphics/demo-video/tet.mp4" style="width: 62%;"></video>

* Cube falling on the floor (`./inis/cube.ini` $\rightarrow$ `./demo-video/cube.mp4`)

  <video src="../../about/graphics/demo-video/cube.mp4" style="width: 62%;"></video>

* Ellipsoid falling on the floor with fixed sphere (`./inis/ellipsoid.ini` $\rightarrow$ `./demo-video/ellipsoid.mp4`)

  <video src="../../about/src/graphics/demo-video/ellipsoid.mp4" style="width: 62%;"></video>

* Higher-order explicit integrator

  * With Runge-Kutta 4 Integrator (`./inis/rk4_on.ini` $\rightarrow$ `./demo-video/rk4_on.mp4`)

    <video src="../../about/src/graphics/demo-video/rk4_on.mp4" style="width: 62%;"></video>

  * Without Runge-Kutta 4 Integrator (`./inis/rk4_off.ini` $\rightarrow$ `./demo-video/rk4_off.mp4`)

    <video src="../../about/src/graphics/demo-video/rk4_off.mp4" style="width: 62%;"></video>

* Adaptive time stepping

  * With Adaptive time stepping (`./inis/adapt_on.ini` $\rightarrow$ `./demo-video/adapt_on.mp4`)

    <video src="../../about/src/graphics/demo-video/adapt_on.mp4" style="width: 62%;"></video>

  * Without Adaptive time stepping (`./inis/adapt_off.ini` $\rightarrow$ `./demo-video/adapt_off.mp4`)