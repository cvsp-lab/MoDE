<div align="center">
  <h2>MoDE: Mixture of Deformation Experts for Dynamic Gaussian Splatting</h2>
  <h3 style="font-size:1.5em; margin-top: 15px;"><strong style="letter-spacing: -0.5px">IEEE TPAMI 2026</strong></h3>
  <a href="TPAMI-2026-03-0704.R1_Kong.pdf"><img src="https://img.shields.io/badge/Paper-TPAMI_2026-b31b1b" alt="Paper"></a>
  <a href="https://github.com/cvsp-lab/MoE-GS-studio"><img src="https://img.shields.io/badge/MoE--GS_Studio-blue" alt="MoE-GS Studio"></a>

  <p>
    <a href="https://www.pnu-cvsp.com/members/inhwan"><strong>In-Hwan Jin</strong></a><sup style="margin-right: -3px;">1*</sup>
    ·
    <a href="https://www.pnu-cvsp.com/members/hyeong-ju"><strong>Hyeongju Mun</strong></a><sup style="margin-right: -3px;">1*</sup>
    ·
    <strong>Joonsoo Kim</strong><sup style="margin-right: -3px;">2</sup>
    ·
    <strong>Kugjin Yun</strong><sup style="margin-right: -3px;">2</sup>
    ·
    <a href="https://www.pnu-cvsp.com/prof"><strong>Kyeongbo Kong</strong></a><sup style="margin-right: -3px;">1†</sup>
    <br>
    <sup style="margin-right: -3px;">1</sup> Pusan National University  <sup style="margin-left: 5px; margin-right: -3px;">2</sup> Electronics and Telecommunications Research Institute
    <br>
    <sup>*</sup> Equal contribution &nbsp;&nbsp;&nbsp; <sup>†</sup> Corresponding author
  </p>

  <br>
  <img src="main.gif" width=70%>
  <br>
  <b>Summary</b>: <b>Mixture of Deformation Experts</b> framework for dynamic Gaussian Splatting with
            multiple deformation experts jointly optimized on a shared canonical Gaussian representation.
  <br><br>
  <b>MoE-GS Series</b>: MoDE is part of
  <a href="https://github.com/cvsp-lab/MoE-GS-studio"><b>MoE-GS Studio</b></a>,
  a research series on Mixture-of-Experts architectures for Dynamic Gaussian Splatting.
</div>


## 🚧 TODO List

- [x] Data Preprocessing Scripts
- [x] Training Scripts
- [x] Rendering Scripts
- [x] Deformation Expert Configurations
- [x] Related Project Links

<br><br>

## Contents

1. [Setup](#setup)
2. [Preprocess Datasets](#preprocess-datasets)
3. [Training and Rendering](#training-and-rendering)
4. [Related Projects](#related-projects)
5. [BibTeX](#bibtex)

<br><br>

## Setup

### Download Repository and Thirdparty Modules
```shell
git clone https://github.com/cvsp-lab/MoDE.git
```

### Environment Setup
Install the required packages and submodules:

```bash
pip install -r requirements.txt
pip install -e submodules/diff-gaussian-rasterization/
pip install -e submodules/simple-knn/
```

<br><br>

## Preprocess Datasets

### Neural 3D Video Dataset
For the Neural 3D Video dataset, extract frames and reorganize the scene directory:

```bash
python script/pre_n3v.py --videopath <dataset>/<scene>
```

Downsample dense point clouds:

```bash
python script/downsample_point.py \
    <location>/<scene>/colmap/dense/workspace/fused.ply \
    <location>/<scene>/points3D_downsample.ply
```

<br><br>

## Training and Rendering

### MoDE with 4DGaussians and E-D3DGS

Train on the Neural 3D Video dataset:

```bash
python train_emb.py \
    -s <N3V_DATASET_ROOT>/coffee_martini \
    --expname <SAVE_PATH> \
    --configs "arguments_MoDE/dynerf/config_rot_0/coffee_martini.py"
```

Render:

```bash
python render_emb.py --skip_test --skip_train \
    --model_path <SAVE_PATH> \
    --configs "arguments_MoDE/emb/config_0/coffee_martini.py" \
    --iteration 30000
```

### MoDE with 4DGaussians and Grid4D

Train on the Neural 3D Video dataset:

```bash
python train_hash.py \
    -s <N3V_DATASET_ROOT>/coffee_martini \
    --expname <SAVE_PATH> \
    --configs "arguments_MoDE/dynerf/config_rot_0/coffee_martini.py"
```

Render:

```bash
python render_hash.py --skip_train --skip_test \
    --model_path <SAVE_PATH> \
    --configs "arguments_MoDE/hash/config_0/coffee_martini.py" \
    --iteration 30000
```

<br>

## Related Projects

- [MoE-GS Studio](https://github.com/cvsp-lab/MoE-GS-studio): Overview of our MoE-based 4DGS research series.
- [MoE-GS](https://github.com/cvsp-lab/MoE-GS): Mixture of Experts for Dynamic Gaussian Splatting.

<br>

## BibTeX
```bibtex
@article{jinmode2026,
    title={On the Design of Mixture-of-Experts for Dynamic Gaussian Splatting},
    author={In-Hwan Jin and Hyeongju Mun and Joonsoo Kim and Kugjin Yun and Kyeongbo Kong},
    journal={IEEE Transactions on Pattern Analysis and Machine Intelligence},
    year={2026},
    note={Accepted}
}
```
