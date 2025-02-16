<div align=center>
  <h1>
    NeRF Applications
  </h1>
  <p>
    <a href=https://mhsung.github.io/kaist-cs479-spring-2025/ target="_blank"><b>KAIST CS479: Machine Learning for 3D Data</b></a><br>
  </p>
</div>

<div align=center>
  <p>
    Instructor: <a href=https://mhsung.github.io target="_blank"><b>Minhyuk Sung</b></a> (mhsung [at] kaist.ac.kr)<br>
    TA: <a href=https://github.com/phillipinseoul target="_blank"><b>Yuseung Lee</b></a>  (phillip0701 [at] kaist.ac.kr)<br>      
    Credit: <a href=https://github.com/jh27kim target="_blank"><b>Jaihoon Kim</b></a>  (jh27kim [at] kaist.ac.kr)      
  </p>
</div>

<div align=center>
  <img src="./fig/teaser.gif" width="1000" />
</div>

## Abstract

NOTE: Most of the materials we provide here are heavily dependent on opensource framework. 
- [NeRFStudio](https://docs.nerf.studio/en/latest/): NeRFStudio is a opensource framework where you can try out various NeRF models
- [SDFStudio](https://docs.nerf.studio/en/latest/extensions/sdfstudio.html): SDFStudio is built on top of NeRFStudio and provides various neural implicit surface reconstruction models.
- [ThreeStudio](https://github.com/threestudio-project/threestudio): ThreeStudio is a framework for creating 3D contetns. They provide zero-shot, one-shot and few-shot generation models. 

The goal of this task is for you to get familar with opensource NeRF based frameworks. 
The scope of NeRF research is too large to cover and here we have listed a few. 
Most of the tasks in this week are focused on installation, training and visualizing the results, and we left the most challenging task at the end, feel free to check out. 

<details>
<summary><b>Table of Content</b></summary>
  
- [Abstract](#abstract)
- [Setup](#setup)
- [Tasks](#tasks)
  - [Task 0. Run NeRFacto](#task-0-Run-NeRFacto)
  - [Task 1. Try your own data](#task-1-Try-your-own-data)
  - [Task 2. Try other methods: `Instant-NGP`, `Mip-NeRF`, `TensoRF`](#task-2-try-other-methods)
  - [Task 3. Run NeuS](#task-3-Run-NeuS)
  - [Task 4. Export mesh](#task-4-Export-mesh)
  - [Task 5. Run `DreamFusion`](#task-5-Run-DreamFusion)
  - [Task 6. Try other methods: `Magic3D`, `ProlificDreamer` ](#task-6-try-other-methods)
  - [Task 7. Extend framework](#task-4-Extend-framework)
- [Further Readings](#further-readings)
</details>

## Setup

If you have troubles with the latest version please refer to the commit ID which we employed. 
- [NeRFStudio](https://github.com/nerfstudio-project/nerfstudio): d78af5b5699cb343cb46b5163d464e455524040f
- [SDFStudio](https://github.com/autonomousvision/sdfstudio): ef14f965296a8e3b37ce21e51f1256be4868038f
- [ThreeStudio](https://github.com/threestudio-project/threestudio): 74ff18a3810cdea39a5341ef8652d4fdc3ffde9f

For task 7, we advise you to make your own environment. 
```
conda create --name {ENVIRONMENT_NAME} -y python=3.8
conda activate {ENVIRONMENT_NAME}
python -m pip install --upgrade pip
```

```
# torch1.12.1+cu113
pip install torch==1.12.1+cu113 torchvision==0.13.1+cu113 --extra-index-url https://download.pytorch.org/whl/cu113
# or torch2.0.0+cu118
pip install torch torchvision --index-url https://download.pytorch.org/whl/cu118
```

Optioanlly, install ninja for faster build
```
pip install ninja
```
Install required packages
```
pip install -r requirements.txt
```

## Tasks

### Task 0. Run NeRFacto

Installation and training steps can be found at [NeRFStudio github](https://github.com/nerfstudio-project/nerfstudio).
After installation, you can run NeRFacto by running this command

```
# You can try different data 
ns-download-data nerfstudio --capture-name=poster
# Train model
ns-train nerfacto --data data/nerfstudio/poster
```

`NeRFStudio` has a variety of `NeRF` implementations and you can visualize the training process online. [NeRFStudio project page](https://docs.nerf.studio/en/latest/index.html)
More explanation of NeRFacto can be found at [here](https://docs.nerf.studio/en/latest/nerfology/methods/nerfacto.html)

Once you successfully execute their code, you will be provided with a viewer link where you can navigate around the scene online. 
<p align="center">
  <img width="300" src="./fig/viewer_1.png" width="500" />
  <img width="300" src="./fig/viewer_2.png" width="500" /> 
</p>

### Task 1. Try your own data

Run `NeRFacto` using your own data [Use custom data on NeRFStudio](https://docs.nerf.studio/en/latest/quickstart/custom_dataset.html)
We recommend using `COLMAP` with images or video. Note that when taking images they should overlap densely over each other. 

### Task 2. Try other methods: `Instant-NGP`, `Mip-NeRF`, `TensoRF`

Theoretical background and training examples can be found at [InstantNGP](https://docs.nerf.studio/en/latest/nerfology/methods/instant_ngp.html), [Mip-NeRF](https://docs.nerf.studio/en/latest/nerfology/methods/mipnerf.html) and [TensoRF](https://docs.nerf.studio/en/latest/nerfology/methods/tensorf.html).

### Task 3. Run NeuS
You can check available methods at [SDFStudio project page](https://docs.nerf.studio/en/latest/extensions/sdfstudio.html#).

We recommend creating a new environment at a separate directory.
Follow the instructions to install required packages. [SDFStudio github](https://github.com/autonomousvision/sdfstudio)

You can check available dataset at [SDFStudio dataset](https://github.com/autonomousvision/sdfstudio/blob/master/docs/sdfstudio-data.md)
Select any dataset you prefer and train NeuSFacto. 

### Task 4. Export mesh
Once you have completed training, you can visualize implicit function by mesh extraction. 
Use the following command. 
```
ns-extract-mesh --load-config outputs/neus-facto-dtu65/neus-facto/XXX/config.yml --output-path meshes/neus-facto-dtu65.ply
```

Example mesh of Brandenburg gate (takes ~12 hours using 8 GPUs)
<p align="center">
  <img width="400" src="./fig/export_mesh.png">
</p>

### Task 5. Run `DreamFusion`
Follow the instructions to install prerequisites. You can find more details at [ThreeStudio github](https://github.com/threestudio-project/threestudio).

Run DreamFusion using either Stable Diffusion model or DeepFloy IF. 
Freely select text prompt you prefer and train the model.

Here's an example of DreamFusion output.

<p align="center">
  <img width="800" src="./fig/dreamfusion.gif">
</p>

### Task 6. (Optional) Try other methods: `Magic3D`, `ProlificDreamer` 
(⚠ High VRAM usage)
Train other methods available on ThreeStudio. 

How do the results differ to vanilla DreamFusion ?

Example outputs of `Magic3D` and `ProlificDreamer`.

<p align="center">
  <img width="600" src="./fig/magic3d.gif">

  <img width="600" src="./fig/prolific.gif">
</p>

### Task 7. (Optional) Extend framework
Pick any paper from [here](https://www.notion.so/geometry-kaist/Tutorial-3-NeRF-Applications-12aad39d9dec4d22b17475fd25bc0f17?pvs=4) and extend NeRFStudio/SDFStudio/ThreeStudio. 


### Further Readings

If you are interested in this topic, we encourage you to check out the papers listed below.
- [NeuS: Learning Neural Implicit Surfaces by Volume Rendering for Multi-view Reconstruction (NeurIPS 2021)](https://arxiv.org/abs/2106.10689)
- [Volume Rendering of Neural Implicit Surfaces (NeurIPS 2021)](https://arxiv.org/abs/2106.12052)
- [DreamFusion: Text-to-3D using 2D Diffusion (ICLR 2023)](https://arxiv.org/abs/2209.14988)
- [Magic3D: High-Resolution Text-to-3D Content Creation (CVPR 2023)](https://arxiv.org/abs/2211.10440)
- [Nerfstudio: A Modular Framework for Neural Radiance Field Development (SIGGRAPH 2023)](https://arxiv.org/abs/2302.04264)
- [Zero-1-to-3: Zero-shot One Image to 3D Object (ICCV 2023)](https://arxiv.org/abs/2303.11328)
- [ProlificDreamer: High-Fidelity and Diverse Text-to-3D Generation with Variational Score Distillation (arXiv 2023)](https://arxiv.org/abs/2305.16213)
