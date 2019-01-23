# IvI GPU cluster

## Hostname

`ivi-h0.science.uva.nl` to access the cluster. Use your UvAnetID as credentials.

## Useful things to have in your `.bashrc`

```bash
export LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:/usr/local/cuda-8.0/lib64
export LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:/usr/local/cuda-8.0/cudnn/cuda/lib64
alias mywatch='/home/dkoelma1/bin/mywatch'
```

Pick the version you want for CUDA by looking at what's available in `/usr/local/`.

## Get a node with slurm

When submitting a job, you need to specify the number of GPU, the ram, the number of CPUs and the duration.  
Each node has 4 GPUs, 128GB of ram, 48 CPU threads (but 2 are used for slurm) and a time limit of 7 days.

Here is an example on how to get an interactive session with 1 GPU for one day:  
`srun -u --pty --gres=gpu:1 --mem=32G --cpus-per-task=12 --time=1-0 bash -i`  

Same but with 4 GPUs:  
`srun -u --pty --gres=gpu:4 --mem=0 --cpus-per-task=46 --time=1-0 bash -i`  
(`--mem=0` books all the memory)

Ideally you should submit a job instead of using an interactive session:  
`srun --gres=gpu:1 --mem=32G --cpus-per-task=12 --time=1-0 python myscript.py --myargument=foo`

## Monitor node usage

Either use `squeue` or `mywatch` (see last line of [.bashrc](#useful-things-to-have-in-your-bashrc))

## Data storage

TBA

## Change GCC version

The default GCC version is 4.8.

Use GCC 6 with
`source /opt/rh/devtoolset-6/enable`

or GCC 7 with
`source /opt/rh/devtoolset-7/enable`
