## Issue description

* *demo.py* fails to run with the error below

```
RuntimeError: CUDA out of memory. Tried to allocate 62.00 MiB (GPU 0; 10.76 GiB total capacity; 9.65 GiB already allocated; 45.94 MiB free; 9.91 GiB reserved in total by PyTorch)
```

## Code example

*  Command to reproduce the bug:

```
python demo.py --trained_model /swook/model/dsfd/WIDERFace_DSFD_RES152.pth --widerface_root /swook/dataset/wider-face/WIDER_val --save_folder ./save --visual_threshold 0.1 --cuda CUDA
```

* Error messages:

```
RuntimeError: CUDA out of memory. Tried to allocate 62.00 MiB (GPU 0; 10.76 GiB total capacity; 9.65 GiB already allocated; 45.94 MiB free; 9.91 GiB reserved in total by PyTorch)
```

* Whole stack traces:

```
Traceback (most recent call last):
  File "demo.py", line 222, in <module>
    test_oneimage()
  File "demo.py", line 201, in test_oneimage
    det_b = infer(net , img , transform , thresh , cuda , bt)
  File "demo.py", line 72, in infer
    y = net(x)      # forward pass
  File "/opt/conda/lib/python3.6/site-packages/torch/nn/modules/module.py", line 541, in __call__
    result = self.forward(*input, **kwargs)
  File "/swook/repos/tencent/dsfd/face_ssd.py", line 240, in forward
    conv5_3_x = self.layer3(conv4_3_x)
  File "/opt/conda/lib/python3.6/site-packages/torch/nn/modules/module.py", line 541, in __call__
    result = self.forward(*input, **kwargs)
  File "/opt/conda/lib/python3.6/site-packages/torch/nn/modules/container.py", line 92, in forward
    input = module(input)
  File "/opt/conda/lib/python3.6/site-packages/torch/nn/modules/module.py", line 541, in __call__
    result = self.forward(*input, **kwargs)
  File "/opt/conda/lib/python3.6/site-packages/torch/nn/modules/container.py", line 92, in forward
    input = module(input)
  File "/opt/conda/lib/python3.6/site-packages/torch/nn/modules/module.py", line 541, in __call__
    result = self.forward(*input, **kwargs)
  File "/opt/conda/lib/python3.6/site-packages/torchvision/models/resnet.py", line 109, in forward
    out = self.bn3(out)
  File "/opt/conda/lib/python3.6/site-packages/torch/nn/modules/module.py", line 541, in __call__
    result = self.forward(*input, **kwargs)
  File "/opt/conda/lib/python3.6/site-packages/torch/nn/modules/batchnorm.py", line 79, in forward
    exponential_average_factor, self.eps)
  File "/opt/conda/lib/python3.6/site-packages/torch/nn/functional.py", line 1670, in batch_norm
    training, momentum, eps, torch.backends.cudnn.enabled
RuntimeError: CUDA out of memory. Tried to allocate 62.00 MiB (GPU 0; 10.76 GiB total capacity; 9.65 GiB already allocated; 45.94 MiB free; 9.91 GiB reserved in total by PyTorch)
```

## System Info

- PyTorch or Caffe2: PyTorch
- How you installed PyTorch (conda, pip, source): docker ([nvcr.io/nvidia/pytorch](https://ngc.nvidia.com/catalog/containers/nvidia:pytorch))
- Build command you used (if compiling from source): None
- OS: Ubuntu 16.04 LTS
- PyTorch version: 1.4.0
- Python version: 3.6
- CUDA/cuDNN version: 10.2
- GPU models and configuration: 2080 Ti
- GCC version (if compiling from source): None
- CMake version: None
- Versions of any other relevant libraries: None

# Comment 1

* Refer to the issues below

1. [RuntimeError: CUDA out of memory. · Issue #60 · Tencent/FaceDetection-DSFD (github.com)](https://github.com/Tencent/FaceDetection-DSFD/issues/60)
2. [RuntimeError: CUDA out of memory · Issue #44 · Tencent/FaceDetection-DSFD (github.com)](https://github.com/Tencent/FaceDetection-DSFD/issues/44)

* Recall the required version of PyTorch is 0.3.1

* However, ours is 1.4.0
* *Tencent/FaceDetection-DSFD* uses some deprecated methods
* Trying to replace them with latest methods

# Comment 2

The suggestions i referred are also too old for the latest version.
Using different docker for `torch==0.3.1` would be much easier.

# Comment 3

* NVIDIA says the **nvidia:pytorch** for `torch==0.3.1` is *nvcr.io/nvidia/pytorch:18.04-py3* [[here]](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel_18-04.html#rel_18-04)
* However, it actually contains `torch==0.4.0a0`
* *nvcr.io/nvidia/pytorch:18.03-py3* also contains `torch==0.4.0a0`

# Comment 4

* *demo.py* fails to run with the error below

```
ModuleNotFoundError: No module named 'cv2'
```

* Installation for `opencv-python` fails with the error below

```
root@7feda172152c:/swook/repos/tencent/dsfd# pip install opencv-python
Collecting opencv-python
  Using cached https://files.pythonhosted.org/packages/30/46/821920986c7ce5bae5518c1d490e520a9ab4cef51e3e54e35094dadf0d68/opencv-python-4.4.0.46.tar.gz
    Complete output from command python setup.py egg_info:
    Traceback (most recent call last):
      File "<string>", line 1, in <module>
      File "/tmp/pip-build-zqpvc4be/opencv-python/setup.py", line 9, in <module>
        import skbuild
    ModuleNotFoundError: No module named 'skbuild'
```

* Installation for `opencv-python` succeeded after updating pip to latest version

```
 pip install --upgrade pip
```

* *demo.py* fails to run with the error below

```
Traceback (most recent call last):
  File "demo.py", line 11, in <module>
    import cv2
  File "/opt/conda/envs/pytorch-py3.6/lib/python3.6/site-packages/cv2/__init__.py", line 5, in <module>
    from .cv2 import *
ImportError: libGL.so.1: cannot open shared object file: No such file or directory
```

* Confirmed it's solved after executing the commands below [[here]](https://github.com/conda-forge/pygridgen-feedstock/issues/10#issuecomment-365914605)

```
apt update
apt install libgl1-mesa-glx
```

* Confirmed similar error

```
Traceback (most recent call last):
  File "demo.py", line 11, in <module>
    import cv2
  File "/opt/conda/envs/pytorch-py3.6/lib/python3.6/site-packages/cv2/__init__.py", line 5, in <module>
    from .cv2 import *
ImportError: libgthread-2.0.so.0: cannot open shared object file: No such file or directory
```

* Confirmed it's solved after executing the commands below [[here]](https://github.com/conda-forge/pygridgen-feedstock/issues/10#issuecomment-365914605)

```
apt install libglib2.0-0
```

* *demo.py* fails to run with the error below

```
Traceback (most recent call last):
  File "/swook/repos/tencent/dsfd/demo.py", line 12, in <module>
    import matplotlib.pyplot as plt
ModuleNotFoundError: No module named 'matplotlib'
```

* Install matplotlib

```
pip install matplotlib
```

* *demo.py* fails to run with the error below

```
root@d2260ec17b65:/swook/repos/tencent/dsfd# python demo.py --trained_model /swook/model/dsfd/WIDERFace_DSFD_RES152.pth --widerface_root /swook/dataset/
wider-face/WIDER_val --save_folder ./save --visual_threshold 0.1 --cuda CUDA
loading pretrained resnet model
Downloading: "https://download.pytorch.org/models/resnet152-b121ed2d.pth" to /root/.torch/models/resnet152-b121ed2d.pth
100%|███████████████████████████████████████████████████████████████████████████████████████████████| 241530880/241530880 [00:19<00:00, 12666725.32it/s]
Finished loading model!
Segmentation fault (core dumped)
```

* Maybe it would be better to find other docker images for `torch==0.3.1`

## Recap

_nvcr.io/nvidia/pytorch:18.04-py3_ and _nvcr.io/nvidia/pytorch:18.03-py3_ both have the same issues.

* *demo.py* fails to run with the error below

```

```

* 