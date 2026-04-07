# Towards Stable and Storage-efficient Dataset Distillation: Matching Convexified Trajectory (CVPR 2025)

> **Official implementation of MCT**, a stable and storage-efficient dataset distillation method presented at CVPR 2025.

## Authors

**Wenliang Zhong**<sup>1</sup>, **Haoyu Tang**<sup>1</sup>*, **Qinghai Zheng**<sup>2</sup>, **Mingzhu Xu**<sup>1</sup>, **Yupeng Hu**<sup>1</sup>, **Weili Guan**<sup>3</sup>

<sup>1</sup> Shandong University  
<sup>2</sup> Fuzhou University  
<sup>3</sup> Harbin Institute of Technology (Shenzhen)  
\* Corresponding author: `tanghao258@sdu.edu.cn`

## Links

- **Paper**: [https://openaccess.thecvf.com/content/CVPR2025/papers/Zhong_Towards_Stable_and_Storage-efficient_Dataset_Distillation_Matching_Convexified_Trajectory_CVPR_2025_paper.pdf](https://openaccess.thecvf.com/content/CVPR2025/papers/Zhong_Towards_Stable_and_Storage-efficient_Dataset_Distillation_Matching_Convexified_Trajectory_CVPR_2025_paper.pdf)
- **Project Page**: [GitHub (iLearn-Lab/CVPR25-MCT)](https://github.com/iLearn-Lab/CVPR25-MCT)
- **CVPR 2025 Virtual Page**: [Poster 34469](https://cvpr.thecvf.com/virtual/2025/poster/34469)

---

## Table of Contents

- [Updates](#updates)
- [Introduction](#introduction)
- [Highlights](#highlights)
- [Method / Framework](#method--framework)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Visualization](#visualization)
- [TODO](#todo)
- [Citation](#citation)
- [Acknowledgement](#acknowledgement)
- [License](#license)

---

## Updates

- [03/2025] Initial release of the CVPR 2025 official code
- [06/2024] Initial release on arXiv

---

## Introduction

本项目是论文 **Towards Stable and Storage-efficient Dataset Distillation: Matching Convexified Trajectory (CVPR 2025)** 的官方实现。

### Summary
Dataset Distillation (DD) aims to synthesize a small dataset to replace a large one for efficient training. However, traditional trajectory matching methods often suffer from training instability and high storage costs for expert trajectories. 

**Matching Convexified Trajectory (MCT)** addresses these issues by:
- **Convexifying Trajectories**: Transforming jagged expert trajectories into smooth, convex ones for more stable matching.
- **Storage-efficient Interpolation**: Storing only a few key waypoints and reconstructing trajectories via interpolation, dramatically reducing storage requirements.

This repository provides:
- Training code for generating expert buffers.
- Trajectory convexification and compression scripts.
- Core distillation scripts for synthesizing high-quality datasets.

---

## Highlights

- **Stable Training**: Convexified trajectories lead to more consistent distillation performance.
- **Storage Efficient**: Reduces repository/storage footprint compared to full trajectory storage.
- **Support for Multiple Datasets**: CIFAR-10, CIFAR-100, and Tiny-ImageNet.
- **CVPR 2025**: Official code for reproducing the results in the paper.

---

## Method / Framework

![Framework](./CVPR_MCT_POSTER.png)

**Figure 1.** Comparison of Traditional Trajectory Matching vs. Matching Convexified Trajectory (MCT).

---

## Project Structure

```text
.
├── exps/                  # Ablation and visualization scripts
│   ├── trajectory_compression.py  # Logic for waypoint interpolation and compression
│   ├── visualize_synthetic.py     # Results visualization
│   └── ...
├── buffer.py              # Script to generate expert trajectory buffers
├── convexify.py           # Core logic for trajectory convexification
├── distill_compressed.py   # Main distillation script using MCT
├── networks.py            # Neural network architectures (ConvNet, ResNet, etc.)
├── utils.py               # Evaluation, data augmentation, and helper functions
├── reparam_module.py      # Module for gradient-through-parameters
├── requirements.txt       # Dependencies
└── CVPR_MCT_POSTER.png     # Poster overview
```

---

## Installation

### 1. Clone the repository
```bash
git clone https://github.com/iLearn-Lab/CVPR25-MCT.git
cd CVPR25-MCT
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

---

## Usage

### 1. Generate Expert Buffer
First, generate the expert trajectories for the target dataset:
```bash
python buffer.py --dataset=CIFAR10 --zca
```

### 2. Compress Trajectory
Generate the convexified and compressed trajectories:
```bash
python exps/trajectory_compression.py --num_interpolation=4 --zca --dataset=CIFAR10
```

### 3. Dataset Distillation
Run the main distillation script using the compressed trajectories:
```bash
# CIFAR-10, IPC=1, with ZCA
python distill_compressed.py --dataset=CIFAR10 --ipc=1 --syn_steps=60 --expert_epochs=6 --max_start_epoch=4 --lr_img=1e3 --lr_lr=1e-07 --lr_init=1e-2 --zca
```

---

## Visualization

You can find the presentation poster below:
![CVPR_MCT_POSTER](./CVPR_MCT_POSTER.png)

---

## Citation

If you find this work useful, please cite our paper:

```bibtex
@InProceedings{Zhong_2025_CVPR,
    author    = {Zhong, Wenliang and Tang, Haoyu and Zheng, Qinghai and Xu, Mingzhu and Hu, Yupeng and Guan, Weili},
    title     = {Towards Stable and Storage-efficient Dataset Distillation: Matching Convexified Trajectory},
    booktitle = {Proceedings of the Computer Vision and Pattern Recognition Conference (CVPR)},
    month     = {June},
    year      = {2025},
    pages     = {25581-25589}
}
```

---

## Acknowledgement

- This work was supported by the **iLearn-Lab** at Shandong University and collaborators.
- Code style and foundations are built upon previous works in Trajectory Matching.

---

## License

This project is released under the **Apache License 2.0**.
