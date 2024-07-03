---
title: Ray Tracer
summary: Implemented an efficient ray intersection algorithms, complex lighting effects, shinier surfaces, realistic shadows, and texture mapping for highly realistic 3D rendering.
tags:
  - CG
date: 2023-11-02
# external_link: https://github.com/lllllcf/LuminaryStudio
---

## Output Comparison

Run the program with the specified `.ini` file to compare your output (it should automatically save to the correct path).

> If your program can't find certain files or you aren't seeing your output images appear, make sure to:<br/>
>
> 1. Set your working directory to the project directory
> 2. Set the command-line argument in Qt Creator to `template_inis/illuminate/<ini_file_name>.ini`
> 3. Clone the `scenefiles` submodule. If you forgot to do this when initially cloning this repository, run `git submodule update --init --recursive` in the project directory

> Note: once all images are filled in, the images will be the same size in the expected and student outputs.

| File/Method To Produce Output |                       Expected Output                        |                         Your Output                          |
| :---------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
|       point_light_1.ini       | ![](https://raw.githubusercontent.com/BrownCSCI1230/scenefiles/main/illuminate/required_outputs/point_light/point_light_1.png) | ![Place point_light_1.png in student_outputs/illuminate/required folder](https://lllllcf.github.io/src/graphics/student_outputs/illuminate/required/point_light_1.png) |
|       point_light_2.ini       | ![](https://raw.githubusercontent.com/BrownCSCI1230/scenefiles/main/illuminate/required_outputs/point_light/point_light_2.png) | ![Place point_light_2.png in student_outputs/illuminate/required folder](https://lllllcf.github.io/src/graphics/student_outputs/illuminate/required/point_light_2.png) |
|       spot_light_1.ini        | ![](https://raw.githubusercontent.com/BrownCSCI1230/scenefiles/main/illuminate/required_outputs/spot_light/spot_light_1.png) | ![Place spot_light_1.png in student_outputs/illuminate/required folder](https://lllllcf.github.io/src/graphics/student_outputs/illuminate/required/spot_light_1.png) |
|       spot_light_2.ini        | ![](https://raw.githubusercontent.com/BrownCSCI1230/scenefiles/main/illuminate/required_outputs/spot_light/spot_light_2.png) | ![Place spot_light_2.png in student_outputs/illuminate/required folder](https://lllllcf.github.io/src/graphics/student_outputs/illuminate/required/spot_light_2.png) |
|       simple_shadow.ini       | ![](https://raw.githubusercontent.com/BrownCSCI1230/scenefiles/main/illuminate/required_outputs/shadow/simple_shadow.png) | ![Place simple_shadow.png in student_outputs/illuminate/required folder](https://lllllcf.github.io/src/graphics/student_outputs/illuminate/required/simple_shadow.png) |
|        shadow_test.ini        | ![](https://raw.githubusercontent.com/BrownCSCI1230/scenefiles/main/illuminate/required_outputs/shadow/shadow_test.png) | ![Place shadow_test.png in student_outputs/illuminate/required folder](https://lllllcf.github.io/src/graphics/student_outputs/illuminate/required/shadow_test.png) |
|    shadow_special_case.ini    | ![](https://raw.githubusercontent.com/BrownCSCI1230/scenefiles/main/illuminate/required_outputs/shadow/shadow_special_case.png) | ![Place shadow_special_case.png in student_outputs/illuminate/required folder](https://lllllcf.github.io/src/graphics/student_outputs/illuminate/required/shadow_special_case.png) |
|     reflections_basic.ini     | ![](https://raw.githubusercontent.com/BrownCSCI1230/scenefiles/main/illuminate/required_outputs/reflection/reflections_basic.png) | ![Place reflections_basic.png in student_outputs/illuminate/required folder](https://lllllcf.github.io/src/graphics/student_outputs/illuminate/required/reflections_basic.png) |
|    reflections_complex.ini    | ![](https://raw.githubusercontent.com/BrownCSCI1230/scenefiles/main/illuminate/required_outputs/reflection/reflections_complex.png) | ![Place reflections_complex.png in student_outputs/illuminate/required folder](https://lllllcf.github.io/src/graphics/student_outputs/illuminate/required/reflections_complex.png) |
|       texture_cone.ini        | ![](https://raw.githubusercontent.com/BrownCSCI1230/scenefiles/main/illuminate/required_outputs/texture_tests/texture_cone.png) | ![Place texture_cone.png in student_outputs/illuminate/required folder](https://lllllcf.github.io/src/graphics/student_outputs/illuminate/required/texture_cone.png) |
|       texture_cone2.ini       | ![](https://raw.githubusercontent.com/BrownCSCI1230/scenefiles/main/illuminate/required_outputs/texture_tests/texture_cone2.png) | ![Place texture_cone2.png in student_outputs/illuminate/required folder](student_outputs/illuminate/required/texture_cone2.png) |
|       texture_cube.ini        | ![](https://raw.githubusercontent.com/BrownCSCI1230/scenefiles/main/illuminate/required_outputs/texture_tests/texture_cube.png) | ![Place texture_cube.png in student_outputs/illuminate/required folder](https://lllllcf.github.io/src/graphics/student_outputs/illuminate/required/texture_cube.png) |
|       texture_cube2.ini       | ![](https://raw.githubusercontent.com/BrownCSCI1230/scenefiles/main/illuminate/required_outputs/texture_tests/texture_cube2.png) | ![Place texture_cube2.png in student_outputs/illuminate/required folder](https://lllllcf.github.io/src/graphics/student_outputs/illuminate/required/texture_cube2.png) |
|        texture_cyl.ini        | ![](https://raw.githubusercontent.com/BrownCSCI1230/scenefiles/main/illuminate/required_outputs/texture_tests/texture_cyl.png) | ![Place texture_cyl.png in student_outputs/illuminate/required folder](https://lllllcf.github.io/src/graphics/student_outputs/illuminate/required/texture_cyl.png) |
|       texture_cyl2.ini        | ![](https://raw.githubusercontent.com/BrownCSCI1230/scenefiles/main/illuminate/required_outputs/texture_tests/texture_cyl2.png) | ![Place texture_cyl2.png in student_outputs/illuminate/required folder](https://lllllcf.github.io/src/graphics/student_outputs/illuminate/required/texture_cyl2.png) |
|      texture_sphere.ini       | ![](https://raw.githubusercontent.com/BrownCSCI1230/scenefiles/main/illuminate/required_outputs/texture_tests/texture_sphere.png) | ![Place texture_sphere.png in student_outputs/illuminate/required folder](https://lllllcf.github.io/src/graphics/student_outputs/illuminate/required/texture_sphere.png) |
|      texture_sphere2.ini      | ![](https://raw.githubusercontent.com/BrownCSCI1230/scenefiles/main/illuminate/required_outputs/texture_tests/texture_sphere2.png) | ![Place texture_sphere2.png in student_outputs/illuminate/required folder](https://lllllcf.github.io/src/graphics/student_outputs/illuminate/required/texture_sphere2.png) |

## Design Choices

#### Texture

Calculate the `diffuse` value using blending and pass it to the light to calculate the final effect.

#### Texture Bilinear Filtering

Find the four nearest pixels in the four corners around the intersected point and use the bilinear interpolation similar to `lab7`.

#### Refraction

Use the following formula to calculate the refracted direction and a similar code as `reflection` to recursively calculate the refraction effect.

$\vec{\omega_o} = \sqrt{1 - \frac{1}{\mu^2} [1 - (\vec{n} \cdot \vec{\omega_i})^2]} + \frac{1}{\mu}[-\vec{\omega_i} + (\vec{n} \cdot \vec{\omega_i})\vec{n}]$

#### Soft Shadow

Use a new type of light `LightType::LIGHT_SOFT` with a finite area `length x length`. Sample a random location on the light source for `soft-samples` times and use the average value to be the color of the shadow.

## Collaboration/References

N/A



## Known Bugs

* Refraction does not achieve the expected result for `refract2.png`

* When the sample number of the soft shadow is large (i.e. set a large `soft-samples` in the `.ini` file), the speed of the ray tracer is slow.

  

## Extra Credit

#### Texture Bilinear Filtering

Set `bi-filtering = true` inside the `.ini` file.

Use the following two command line arguments to compare the output.

`template_inis/illuminate/extra_credit/bilinear.ini`

`template_inis/illuminate/extra_credit/bilinear_off.ini`

<img src="https://lllllcf.github.io/src/graphics/student_outputs/illuminate/extra/bilinear.png" alt="softshadow" style="zoom:35%;" /> <img src="https://lllllcf.github.io/src/graphics/student_outputs/illuminate/extra/bilinear_off.png" alt="softshadow" style="zoom:35%;" />



#### Refraction

`light.cpp`  -> `refraction`

Set `refract = true` inside the `.ini` file.

Use the following two command line arguments to see the output.

`template_inis/illuminate/extra_credit/refract1.ini`

`template_inis/illuminate/extra_credit/refract2.ini`

<img src="https://lllllcf.github.io/src/graphics/student_outputs/illuminate/extra/refract1.png" alt="softshadow" style="zoom:35%;" />

The output for `refract1` is similar to the expected output.

<img src="https://lllllcf.github.io/src/graphics/student_outputs/illuminate/extra/refract2.png" alt="softshadow" style="zoom:35%;" />

but the output for `refract2` does not achieve the expected results.



#### Soft Shadow

`light.cpp` and `sceneparser.cpp`

+ Add a new type of light `LightType::LIGHT_SOFT` with a new parameter `length` that specifies the side length for the light, and reuse other parameters and code for `LightType::LIGHT_SPOT`.

+ Example usage for `.json` file to create `LightType::LIGHT_SOFT`

```json
"lights": [
        {
          "type": "soft",
          "color": [1.0, 1.0, 1.0],
          "direction": [0.0, -1.0, 0.0],
          "angle": 30.0,
          "penumbra": 20.0,
          "attenuationCoeff": [0.8, 0.05, 0.0],
	 	  "length": 0.3
        }
    ]
```

+ Set `soft-samples = 50`  inside the `.ini` file to specify sample points.

+ Use the following two command line arguments to compare the output.

  `template_inis/illuminate/extra_credit/softshadow.ini`

  `template_inis/illuminate/extra_credit/softshadow_off.ini`

  <img src="https://lllllcf.github.io/src/graphics/student_outputs/illuminate/extra/softshadow.png" alt="softshadow" style="zoom:35%;" /> <img src="https://lllllcf.github.io/src/graphics/student_outputs/illuminate/extra/softshadow_off.png" alt="softshadow" style="zoom:35%;" />

+ Use the following two command line arguments to compare the output.

  `template_inis/illuminate/extra_credit/softshadow2.ini`

  `template_inis/illuminate/extra_credit/softshadow2_off.ini`

  <img src="https://lllllcf.github.io/src/graphics/student_outputs/illuminate/extra/softshadow2.png" alt="softshadow" style="zoom:35%;" /> <img src="https://lllllcf.github.io/src/graphics/student_outputs/illuminate/extra/softshadow2_off.png" alt="softshadow" style="zoom:35%;" />

### Output Comparison

Run the program with the specified `.ini` file to compare your output (it should automatically save to the correct path).

> If your program can't find certain files or you aren't seeing your output images appear, make sure to:<br/>
>
> 1. Set your working directory to the project directory
> 2. Set the command-line argument in Qt Creator to `template_inis/intersect/<ini_file_name>.ini`
> 3. Clone the `scenefiles` submodule. If you forgot to do this when initially cloning this repository, run `git submodule update --init --recursive` in the project directory

> Note: once all images are filled in, the images will be the same size in the expected and student outputs.

| File/Method To Produce Output |                       Expected Output                        |                         Your Output                          |
| :---------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
|         unit_cone.ini         | ![](https://raw.githubusercontent.com/BrownCSCI1230/scenefiles/main/intersect/required_outputs/unit_cone.png) | ![Place unit_cone.png in student_outputs/intersect/required folder](https://lllllcf.github.io/src/graphics/student_outputs/intersect/required/unit_cone.png) |
|       unit_cone_cap.ini       | ![](https://raw.githubusercontent.com/BrownCSCI1230/scenefiles/main/intersect/required_outputs/unit_cone_cap.png) | ![Place unit_cone_cap.png in student_outputs/intersect/required folder](https://lllllcf.github.io/src/graphics/student_outputs/intersect/required/unit_cone_cap.png) |
|         unit_cube.ini         | ![](https://raw.githubusercontent.com/BrownCSCI1230/scenefiles/main/intersect/required_outputs/unit_cube.png) | ![Place unit_cube.png in student_outputs/intersect/required folder](https://lllllcf.github.io/src/graphics/student_outputs/intersect/required/unit_cube.png) |
|       unit_cylinder.ini       | ![](https://raw.githubusercontent.com/BrownCSCI1230/scenefiles/main/intersect/required_outputs/unit_cylinder.png) | ![Place unit_cylinder.png in student_outputs/intersect/required folder](https://lllllcf.github.io/src/graphics/student_outputs/intersect/required/unit_cylinder.png) |
|        unit_sphere.ini        | ![](https://raw.githubusercontent.com/BrownCSCI1230/scenefiles/main/intersect/required_outputs/unit_sphere.png) | ![Place unit_sphere.png in student_outputs/intersect/required folder](https://lllllcf.github.io/src/graphics/student_outputs/intersect/required/unit_sphere.png) |
|       parse_matrix.ini        | ![](https://raw.githubusercontent.com/BrownCSCI1230/scenefiles/main/intersect/required_outputs/parse_matrix.png) | ![Place parse_matrix.png in student_outputs/intersect/required folder](https://lllllcf.github.io/src/graphics/student_outputs/intersect/required/parse_matrix.png) |
|       ambient_total.ini       | ![](https://raw.githubusercontent.com/BrownCSCI1230/scenefiles/main/intersect/required_outputs/ambient_total.png) | ![Place ambient_total.png in student_outputs/intersect/required folder](https://lllllcf.github.io/src/graphics/student_outputs/intersect/required/ambient_total.png) |
|       diffuse_total.ini       | ![](https://raw.githubusercontent.com/BrownCSCI1230/scenefiles/main/intersect/required_outputs/diffuse_total.png) | ![Place diffuse_total.png in student_outputs/intersect/required folder](https://lllllcf.github.io/src/graphics/student_outputs/intersect/required/diffuse_total.png) |
|      specular_total.ini       | ![](https://raw.githubusercontent.com/BrownCSCI1230/scenefiles/main/intersect/required_outputs/specular_total.png) | ![Place specular_total.png in student_outputs/intersect/required folder](https://lllllcf.github.io/src/graphics/student_outputs/intersect/required/specular_total.png) |
|        phong_total.ini        | ![](https://raw.githubusercontent.com/BrownCSCI1230/scenefiles/main/intersect/required_outputs/phong_total.png) | ![Place phong_total.png in student_outputs/intersect/required folder](https://lllllcf.github.io/src/graphics/student_outputs/intersect/required/phong_total.png) |
|    directional_light_1.ini    | ![](https://raw.githubusercontent.com/BrownCSCI1230/scenefiles/main/intersect/required_outputs/directional_light_1.png) | ![Place directional_light_1.png in student_outputs/intersect/required folder](https://lllllcf.github.io/src/graphics/student_outputs/intersect/required/directional_light_1.png) |
|    directional_light_2.ini    | ![](https://raw.githubusercontent.com/BrownCSCI1230/scenefiles/main/intersect/required_outputs/directional_light_2.png) | ![Place directional_light_2.png in student_outputs/intersect/required folder](https://lllllcf.github.io/src/graphics/student_outputs/intersect/required/directional_light_2.png) |

### Design Choices

#### KD-Tree

`BoundingBox` class, uses two vectors to measure the AABB.

`KDNode` class represents each node of the tree.

`buildKDTree` function constructs the tree. For choosing the split axis, I cycle through three axes instead of choosing the best axis because the latter approach is time consuming.

`traverse_kd_tree` function traverses the tree and if meets the leaf node, then calculate the intersected shape.

#### OpenMP

use `#pragma omp parallel for collapse(2)` before the main loop of pixels.

#### Anti-Aliasing Post-filter

Apply the blur filter from Project 2 with radius 5 as the post filter. The definition of the blur filter is in `filterutils.cpp`.

#### Super-Sampling

Apply `traceRay` function for the four corners of the aimed pixel and calculate the mean.

### Collaboration/References

N/A

### Known Bugs

There will be some black spots on the edges of objects due to inaccurate float comparisons.

### Extra Credit

#### Acceleration data structure: KD-Tree

`kdtree.cpp` and `boundingbox.cpp` 

Set `acceleration = true` inside the `.ini` file.

Use the following two command line arguments to compare the speed.

`template_inis/intersect/extra_credit/kdtree_false.ini`

`template_inis/intersect/extra_credit/kdtree_true.ini`

(use recursive_sphere_6.json)

<img src="https://lllllcf.github.io/src/graphics/student_outputs/intersect/extra_credit/recursive_sphere_6.png" alt="recursive_sphere_6" style="width:62%;" />

#### Parallelization: Level1: OpenMP

Use `#pragma omp parallel for collapse(2)` before the main loop of pixels.

Set `parallel = true` inside the `.ini` file.

Use the following two command line arguments to compare the speed.

`template_inis/intersect/extra_credit/parallel_false.ini`

`template_inis/intersect/extra_credit/parallel_true.ini`

(use primitive_salad_2.json)

<img src="https://lllllcf.github.io/src/graphics/student_outputs/intersect/extra_credit/primitive_salad_2.png" alt="primitive_salad_2.png" style="width:62%;" />

#### Anti-Aliasing: Blurring Post-filter

`filterutil.cpp`

Set `anti-aliasing = true` inside the `.ini` file.

Use the following two command line arguments to compare the output.

`template_inis/intersect/extra_credit/antialising_false.ini`

`template_inis/intersect/extra_credit/antialising_true.ini`

(use directional_light_2.json)

<img src="https://lllllcf.github.io/src/graphics/student_outputs/intersect/extra_credit/original_directional_light_2.png" alt="original_directional_light_2" style="width:62%;" /> <img src="https://lllllcf.github.io/src/graphics/student_outputs/intersect/extra_credit/antialising_directional_light_2.png" alt="antialising_directional_light_2" style="width:62%;" />

#### Super-Sampling: Stochastic Super-Sampling

Set `super-sample = true` inside the `.ini` file and `num-samples = 10` to specify sample points.

Use the following two command line arguments to compare the output.

`template_inis/intersect/extra_credit/supersample_false.ini`

`template_inis/intersect/extra_credit/supersample_true.ini`

(use primitive_salad_1.json)

<img src="https://lllllcf.github.io/src/graphics/student_outputs/intersect/extra_credit/original_primitive_salad_1.png" alt="original_primitive_salad_1" style="width:62%;" /> <img src="https://lllllcf.github.io/src/graphics/student_outputs/intersect/extra_credit/supersample_primitive_salad_1.png" alt="supersample_primitive_salad_1" style="width:62%;" />

#### Create your own scene file

Use the following command line argument.

`template_inis/intersect/extra_credit/customize.ini`

(use torii.json)<img src="https://lllllcf.github.io/src/graphics/student_outputs/intersect/extra_credit/torii.png" alt="torii" style="width:62%;" />