## Issue description

* *demo.py* fails to run with the error below

```
ImportError: cannot import name 'pa_sfd_match'
```

## Code example

*  Command to reproduce the bug:

```
root@68e19c8a175f:/swook/repos/tencent/dsfd# python demo.py --trained_model /swook/model/dsfd/WIDERFace_DSFD_RES152.pth \
> --img_root /swook/dataset/wider-face-WIDER_val \
> --save_folder ./save \
> --visual_threshold 0.1
```

* Error messages:

```
ImportError: cannot import name 'pa_sfd_match'
```

* Whole stack traces:

```
Traceback (most recent call last):
  File "demo.py", line 27, in <module>
    from face_ssd import build_ssd
  File "/swook/repos/tencent/dsfd/face_ssd.py", line 13, in <module>
    from layers import *
  File "/swook/repos/tencent/dsfd/layers/__init__.py", line 2, in <module>
    from .modules import *
  File "/swook/repos/tencent/dsfd/layers/modules/__init__.py", line 2, in <module>
    from .multibox_loss import MultiBoxLoss, focalLoss
  File "/swook/repos/tencent/dsfd/layers/modules/multibox_loss.py", line 13, in <module>
    from ..box_utils import (log_sum_exp, match, pa_sfd_match, refine_match,
ImportError: cannot import name 'pa_sfd_match'
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

1. [ImportError: cannot import name 'pa_sfd_match' from 'layers.box_utils' · Issue #69 · Tencent/FaceDetection-DSFD (github.com)](https://github.com/Tencent/FaceDetection-DSFD/issues/69)
2. [ImportError: cannot import name 'pa_sfd_match' · Issue #65 · Tencent/FaceDetection-DSFD (github.com)](https://github.com/Tencent/FaceDetection-DSFD/issues/65#issuecomment-653732608)

* *\${DSFD_DIR}/layers/modules/mulltibox_loss.py* tries to import `pa_sfd_match` from `..box_utils`

```python
from ..box_utils import (log_sum_exp, match, pa_sfd_match, refine_match,
                         sfd_match)
```

* However, *\${DSFD_DIR}/layers/box_utils.py* doesn't declare `pa_sfd_match` at all
* Remove `pa_sfd_match` as suggested in the issue above