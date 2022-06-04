# Contrastive Self-Supervised Learning on CIFAR-10

    
[![Platform](https://img.shields.io/badge/platform-pytorch-blue)](https://pytorch.org/get-started/locally/)
[![Top Language](https://img.shields.io/github/languages/top/huang-research-group/contrastive2021)](https://github.com/huang-research-group/contrastive2021/search?l=python)
[![Latest Release](https://img.shields.io/github/v/release/huang-research-group/contrastive2021)](https://github.com/huang-research-group/contrastive2021/releases)

## Description

[Weiran Huang](https://www.weiranhuang.com), Mingyang Yi and Xuyang Zhao, "[Towards the Generalization of Contrastive Self-Supervised Learning](https://arxiv.org/abs/2111.00743)", arXiv:2111.00743, 2021.

This repository is used to verify how data augmentations will affect the performance of contrastive self-supervised learning algorithms.

## Supported Models

- SimCLR
- Barlow Twins
- MoCo
- SimSiam

## Supported Augmentations

- (a) Random Cropping
- (b) Random Gaussian Blur
- (c) Color Dropping (i.e., randomly convert images to grayscale)
- (d) Color Distortion
- (e) Random Horizontal Flipping

## Installation
```bash
python -m venv venv                 # create a virtual environment named venv
source venv/bin/activate            # activate the environment
pip install -r requirements.txt     # install the dependencies
```

Code is tested in the following environment:
- torch==1.4.0
- torchvision==0.5.0
- torchmetrics==0.4.0
- pytorch-lightning==1.3.8
- hydra-core==1.0.0
- lightly==1.0.8 **(important!)**

## Script and Sample Code

```console
├── contrastive2021
    ├── README.md                  // descriptions about the repo
    ├── requirements.txt           // dependencies
    ├── scripts
        ├── run_train_eval.sh      // shell script for training and evaluation
    ├── src
        ├── models.py              // models
        ├── util.py                // utilities
    ├── train_eval.py              // training and evaluation script
```

## Evaluation
KNN evaluation protocol. Code from [here](https://colab.research.google.com/github/facebookresearch/moco/blob/colab-notebook/colab/moco_cifar10_demo.ipynb).

## Results

### Richer data augmentations result in better performance

Usage: `python train_eval.py --model=simclr --epoch=800 --augs=abcde --num_runs=3`

| (a)  | (b)  | (c)  | (d)  | (e)  |    SimCLR    | Barlow Twins |
| :--: | :--: | :--: | :--: | :--: | :----------: | :----------: |
|  ✓   |  ✓   |  ✓   |  ✓   |  ✓   | 89.92 ± 0.05 | 83.93 ± 0.57 |
|  ✓   |  ✓   |  ✓   |  ✓   |  ×   | 88.41 ± 0.11 | 83.37 ± 0.43 |
|  ✓   |  ✓   |  ✓   |  ×   |  ×   | 83.62 ± 0.19 | 73.70 ± 0.99 |
|  ✓   |  ✓   |  ×   |  ×   |  ×   | 62.91 ± 0.25 | 49.56 ± 0.11 |
|  ✓   |  ×   |  ×   |  ×   |  ×   | 62.37 ± 0.09 | 48.54 ± 0.29 |

### Stronger data augmentations result in better performance

Usage: `python train_eval.py --model=twins --epoch=800 --augs=color --color_strength=0.5 --num_runs=3`

| Color Distortion Strength |    SimCLR    | Barlow Twins |
| :-----------------------: | :----------: | :----------: |
|             1             | 82.64 ± 0.57 | 78.79 ± 0.54 |
|            1/2            | 78.49 ± 0.09 | 72.76 ± 1.50 |
|            1/4            | 76.25 ± 0.16 | 68.30 ± 0.15 |
|            1/8            | 73.60 ± 0.11 | 61.13 ± 2.81 |


## Acknowledgement

This code is based on:

- [IgorSusmelj/barlowtwins](https://github.com/IgorSusmelj/barlowtwins)
- [lightly/imagenette_benchmark.py](https://github.com/lightly-ai/lightly/blob/v1.1.19/docs/source/getting_started/benchmarks/imagenette_benchmark.py)

## Citation

If you find our work useful in your research, please consider citing:

```
@misc{huang2021towards,
      title={Towards the Generalization of Contrastive Self-Supervised Learning}, 
      author={Weiran Huang and Mingyang Yi and Xuyang Zhao},
      year={2021},
      eprint={2111.00743},
      archivePrefix={arXiv}
}
```
