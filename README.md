# nodes-info

Resources on how to use the GPU clusters: [das5](das5.md) and [LISA](lisa.md).

## General things to know

* DO NOT stay idle on a GPU node.

* Learn on how to create sessions with either `screen` or `tmux`. Opening a session and then submitting your job allows you to disconnect and then later resume (from a different location) and monitor the progress. `tmux` is not available on lisa.

* `nvidia-smi` is useful to check the usage of GPUs on a node.

* `CUDA_VISIBLE_DEVICES=0 python myscript.py` will only make the GPU:0 visible to python. Alternatively, you can specify it within your python script.

* You can create a bash script with multiple parallel jobs that you will submit via `slurm` or `torque`. Here is an example:

```bash
CUDA_VISIBLE_DEVICES=0 python exp1.py & \
    CUDA_VISIBLE_DEVICES=1,2 python exp2.py & \
    CUDA_VISIBLE_DEVICES=3 python exp3.py & \
    wait
```

A quick tutorial on how to use das4 is available [here](https://goo.gl/Atq9Za).
