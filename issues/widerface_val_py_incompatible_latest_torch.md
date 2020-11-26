* **Is your feature request related to a problem? Please describe.**
* It seems *\${DSFD_DIR}/widerface_val.py* is also only compatible with `torch==0.3.1` or below
* Refer to this [commit](https://github.com/swoook/dsfd/blob/5066cf38a736d7730451b4fcd7c60512e7834e57/demo-latest-torch.py) for more details about incompatible codes
* It'd be better to add validation script for the `torch` i use
* **Describe the solution you'd like**
* *\${DSFD_DIR}/widerface_val.py* supports the `torch==1.4.0a`
* **Describe alternatives you've considered**
* Using a docker for `torch==0.3.1`
* However, PyTorch or NVIDIA doesn't provide a docker for `torch==0.3.1`
* So, i should build it myself if i'd like to use it
* **Additional context**
* None

# Comment 1

