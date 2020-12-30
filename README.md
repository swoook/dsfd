## :loudspeaker: This is cloned repository!

This repository is cloned from [Tencent/FaceDetection-DSFD](https://github.com/Tencent/FaceDetection-DSFD) and modified for research, compatibility, functionality and convenience.

<img src="imgs/DSFD_logo.PNG" title="Logo" width="300" /> 

## Update

* 2019.04: Release pytorch-version DSFD inference code.
* 2019.03: DSFD is accepted by CVPR2019.
* 2018.10: Our DSFD ranks No.1 on [WIDER FACE](http://mmlab.ie.cuhk.edu.hk/projects/WIDERFace/WiderFace_Results.html) and [FDDB](http://vis-www.cs.umass.edu/fddb/results.html)


## Introduction
<p align='center'>
  <img src='./imgs/dsfd_video.gif' width=1000'/>
</p>

In this repo, we propose a novel face detection network, named DSFD, with superior performance over the state-of-the-art face detectors. You can use the code to evaluate our DSFD for face detection. 

For more details, please refer to our paper [DSFD: Dual Shot Face Detector](https://arxiv.org/abs/1810.10220)! or poster [slide](./imgs/DSFD_CVPR2019_poster.pdf)!

<p align='center'>
<img src='./imgs/DSFD_framework.PNG' alt='DSFD Framework' width='1000px'>
</p>

Our DSFD face detector achieves state-of-the-art performance on [WIDER FACE](http://mmlab.ie.cuhk.edu.hk/projects/WIDERFace/WiderFace_Results.html) and [FDDB](http://vis-www.cs.umass.edu/fddb/results.html) benchmark.

### WIDER FACE

<p align='center'>
<img src='./imgs/DSFD_widerface.PNG' alt='DSFD Widerface Performance' width='1000px'>
</p>


|  Backbone  | Easy  | Medium | Hard  | E2E latency (s) |                           Download                           |
| :--------: | :---: | :----: | :---: | --------------- | :----------------------------------------------------------: |
| ResNet-152 | 0.967 | 0.952  | 0.905 | 6.26            | [here](https://s3.amazonaws.com/pytorch/models/resnet152-b121ed2d.pth) |

**Easy**, **Medium** and **Hard** denote AP on WIDER FACE validation set Easy, Medium and Hard, respectively.

**E2E latency** denotes an end-to-end latency (= preprocess + network + TTA + postprocess).

Latency is measured with batch size **1** on **RTX 2080Ti GPU** and **Threadripper 2950X CPU**.

Confidence thresholds were set to **0.01** for both AP and latency benchmark.

### FDDB

<p align='center'>
<img src='./imgs/DSFD_fddb.PNG' alt='DSFD FDDB Performance' width='1000px'>
</p>

## Requirements

- `cudatoolkit==10.2`
- `cudnn==7.6`
- `python==3.6`
- `torch==1.4.0`
- `torchvision==0.5.0`

## Development Environments

### Conda

* [*conda-py36torch14.yml*](dev-envs/conda-py36torch14.yml) is appropriate if you'd like to use this repository on conda environment
* Please refer to [Managing environments — conda documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html?highlight=yml%20file#creating-an-environment-from-an-environment-yml-file) for more details

### Docker

* *nvcr.io/nvidia/pytorch:19.11-py3* is appropriate if you'd like to use this repository on docker container
* Please refer to [PyTorch | NVIDIA NGC](https://ngc.nvidia.com/catalog/containers/nvidia:pytorch) for more details

## Getting Started

### Installation
* Clone this repository

```bash
> git clone https://github.com/swoook/dsfd.git
> cd ${DSFD_DIR}/dsfd
```

### Demo

* Refer to [*demo.md*](docs/demo.md) for detailed instructions

### WIDER FACE Validation

1. Data Preparation : Refer to [*data-preparation.md*](docs/data-preparation.md) for detailed instructions
2. Evaluation: Refer to [*validation.md*](docs/validation.md) for detailed instructions

## Qualitative Results
<p align='center'>
  <img src='./imgs/DSFD_demo1.PNG' width='1000'/>
</p>

<p align='center'>
  <img src='./imgs/DSFD_demo2.PNG' width='1000'/>
</p>
### Citation
If you find DSFD useful in your research, please consider citing: 
```
@inproceedings{li2018dsfd,
  title={DSFD: Dual Shot Face Detector},
  author={Li, Jian and Wang, Yabiao and Wang, Changan and Tai, Ying and Qian, Jianjun and Yang, Jian and Wang, Chengjie and Li, Jilin and Huang, Feiyue},
  booktitle={Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition},
  year={2019}
}
```
## Contact
For any question, please file an issue or contact
```
Jian Li: swordli@tencent.com
```
