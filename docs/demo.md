## *demo.py*

* *\${DSFD_DIR}/demo.py* shows how detection and visualization works

| flags            | description                                                  |
| ---------------- | ------------------------------------------------------------ |
| trained_model    | Path to the DSFD model                                       |
| widerface_root   | Directory of WIDER Face<br />E.g. *\${WIDER_FACE_DIR}/WIDER_train/* for training, <br />*\${WIDER_FACE_DIR}/WIDER_val/* for validation, <br />*\${WIDER_FACE_DIR}/WIDER_test/* for testing |
| save_folder      | Path to output image file                                    |
| visual_threshold | Confidence threshold                                         |
| cuda             | Whether to use CUDA<br />Pass CUDA if you'd like to use CUDA |

* Specifically, it evaluates DSFD on *\${DSFD_DIR}/data/worlds-largest-selfie.jpg* and writes results as an image file to *--save_folder/demo-result.png*
* Typical commands to execute this demo with CUDA is:

```
root@501243bba88b:${DSFD_DIR}# python demo.py --trained_model ${PTH_DIR}/WIDERFace_DSFD_RES152.pth --widerface_root ${WIDERFACE_DIR}/WIDER_val/ --save_folder ./save --visual_threshold 0.1 --cuda CUDA
```