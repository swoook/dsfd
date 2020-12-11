## Validation: WIDER FACE $\mathrm{val}$

* *\${DSFD_DIR}/widerface_val.py* evaluates DSFD on WIDER FACE $\mathrm{val}$

| flags          | description                                                  |
| -------------- | ------------------------------------------------------------ |
| trained_model  | Path to the DSFD model                                       |
| widerface_root | Directory of WIDER Face<br />E.g. *\${WIDERFACE_DIR}*        |
| save_folder    | Path to write results                                        |
| cuda           | Whether to use CUDA<br />Pass CUDA if you'd like to use CUDA |

* Be cautious that `widerface_root` is different from the same flag in demo
* `widerface_root` looks like:

```
.
├── Submission_example.zip
├── wider_face_split.zip
├── WIDER_test.zip
├── WIDER_train.zip
├── WIDER_val.zip
.
.
.
```

1. Download [eval_tools](http://mmlab.ie.cuhk.edu.hk/projects/WIDERFace/support/eval_script/eval_tools.zip) to *\${DSFD_DIR}* and unzip it

2. Typical command for evaluation is written below:

   ```
   root@501243bba88b:${DSFD_DIR}# python widerface_val.py --trained_model ${PTH_DIR}/WIDERFace_DSFD_RES152.pth --widerface_root ${WIDERFACE_DIR} --save_folder ./val-res/wider-face-val --cuda CUDA
   ```