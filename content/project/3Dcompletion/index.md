---
title: Open-ended Example-Based Shape Modeling
summary: Developed an autoregressive transformer decoder for precise part selection, leveraging extrinsic and intrinsic implicit representations to to facilitate 3D shape generation and synthesis based on a small set of example shapes.
tags:
  - CG
date: 2024-11-10
# external_link: https://github.com/chengfanli/eecs494-p3
links:
- name: Github
  url: https://github.com/dinhanhtruong/implicit-transformer-shape-synthesis
# - name: Devlog
#   url: https://www.indiedb.com/games/biology-452-field-ecology-of-snail-fungus-interaction
# - name: Github
#   url: https://github.com/chengfanli/eecs494-p3
# - name: Trailer
#   url: https://chengfanli.github.io/about/src/Trailer452.mp4

---

Our group explored the challenging field of open-ended example-based 3D shape generation and synthesis. We developed an autoregressive transformer decoder that leverages the extrinsic (GMM) and intrinsic (surface geometry) representations to automatically complete the part selection process based on a small set of example shapes.

Left: input example shapes

Right: Generated shapes 

<img src="https://chengfanli.github.io/about/src/3Dcompletion/res1.jpg" alt="teaser" style="zoom:50%;" />

<img src="https://chengfanli.github.io/about/src/3Dcompletion/res2.jpg" alt="teaser" style="zoom:50%;" />

Training the decoder requires enormous 3D data. I solved this limitation by constructing a dataset of meaningful combinations of example shapes and their corresponding "ideal" parts to compose. Because high-quality 3D mesh data is challenging to obtain, I used a cascaded diffusion model to complete and reconstruct part-level shapes. I split the existing shapes into parts and reconstructed complete shapes for each part, creating a meaningful training dataset containing more than 60,000 3D shapes. 

<img src="https://chengfanli.github.io/about/src/3Dcompletion/completion0.jpg" alt="teaser" style="zoom:50%;" />

<img src="https://chengfanli.github.io/about/src/3Dcompletion/completion1.jpg" alt="teaser" style="zoom:50%;" />

The example shapes are partially identical to the ground truth while maintaining diversity across each other. Partially identical completion maintains intrinsic and extrinsic features of the incomplete shape by using preserved priors in the diffusion model's denoising process, ensuring consistent surface geometry. Additionally, introducing a diversity of example shapes measured by Bhattacharyya distance and supported by introducing bias in the diffusion model enhances the transformer decoder's generalization ability.

