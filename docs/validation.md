## Validation: WIDER FACE $\mathrm{val}$

* *\${REPO-ROOT}/widerface_val.py* evaluates DSFD on WIDER FACE val
* Use *\${REPO-ROOT}/widerface_val_torch140.py* if you use `torch > 1.4`

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

2. Execute the command below to evaluate DSFD on WIDER FACE val

   ```
   root@501243bba88b:${DSFD_DIR}# python widerface_val.py --trained_model ${PTH_DIR}/WIDERFace_DSFD_RES152.pth --widerface_root ${WIDERFACE_DIR} --save_folder ./val-res/wider-face-val --cuda CUDA
   ```
   
3. Calculate APs by using [swoook/widerface-evaluation](https://github.com/swoook/widerface-evaluation)