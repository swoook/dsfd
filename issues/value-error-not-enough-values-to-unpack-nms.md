## Issue description

* *widerface_val_torch140.py* fails to run with the error below

```
ValueError: not enough values to unpack (expected 2, got 0)
```

## Code example

*  Command to reproduce the bug:

```
python widerface_val_torch140.py --trained_model /swook/model/dsfd/WIDERFace_DSFD_RES152.pth --widerface_root /swook/dataset/wider-face --save_folder ./val-res/wider-face-val --cuda CUDA
```

* Error messages:

```
ValueError: not enough values to unpack (expected 2, got 0)
```

* Whole stack traces:

```
Traceback (most recent call last):
  File "widerface_val_torch140.py", line 311, in <module>
    test_widerface()
  File "widerface_val_torch140.py", line 296, in test_widerface
    det0 = detect_face(image, shrink)  # origin test
  File "widerface_val_torch140.py", line 66, in detect_face
    y = net(x)
  File "/opt/conda/lib/python3.6/site-packages/torch/nn/modules/module.py", line 541, in __call__
    result = self.forward(*input, **kwargs)
  File "/swook/repos/tencent/dsfd/face_ssd.py", line 348, in forward
    self.priors.type(type(x.data))                  # default boxes
  File "/swook/repos/tencent/dsfd/layers/functions/detection.py", line 75, in forward
    ids, count = nms(boxes, scores, self.nms_thresh, self.top_k)
ValueError: not enough values to unpack (expected 2, got 0)
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

* Succeeded to reproduce same error
* The error always occurred while testing *0_Parade_marchingband_1_356.jpg*

```
Testing image 82/3226 0_Parade_marchingband_1_356.jpg....
```

* *0_Parade_marchingband_1_356.jpg* looks like:

![](issue-05/0_Parade_marchingband_1_356.jpg)

* It seems that DSFD can't detect any face from this image
* *demo.py* also fails on *0_Parade_marchingband_1_356.jpg* with same error
* 