# IvI GPU cluster

There is a channel `#ivi_cluster` in the IvI slack.  
Read the pinned posts for more info, this readme only provides the basics.

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

When submitting a job, you need to specify the number of GPU, the ram, the number of CPUs and the duration. Please adjust these arguments according to your needs.  
Each node has 4 GPUs, 128GB of ram, 48 CPU threads (but 2 are used for slurm), and 2x10 TB local HDD (/hddstore). Maximum run time is 7 days.

Here is an example on how to get an interactive session with 1 GPU for 2h30:  
`srun -u --pty --gres=gpu:1 --mem=30G --cpus-per-task=10 --time=2:30:00 bash -i`

Same but with 4 GPUs for 1 day and 8 hours:  
`srun -u --pty --gres=gpu:4 --mem=120G --cpus-per-task=40 --time=1-8 bash -i`  

Ideally you should submit a job instead of using an interactive session:  
`srun --gres=gpu:1 --mem=30G --cpus-per-task=10 --time=2:30:00 python myscript.py --myargument=foo`

Quoting a wise man. Priority of a job will depend on the size of the job (smaller jobs have higher priority) and the amount of resources used in the past (if you have consumed less resources in the past you will have a higher priority).

slurm will provide a job id. Use that id if you want to remove yourself from the queue with `scancel [job id]`.

## Monitor node usage

Either use `squeue` or `mywatch` (see last line of [.bashrc](#useful-things-to-have-in-your-bashrc))


## Jupyter notebook on a node
1. Get an interactive session on a GPU node.
2. Run `jupyter notebook --no-browser --port=20105` on GPU node. And you'll get a token like this `http://localhost:20105/?token=31427b811f3f3fdaef9d5da5cce8c81ba4df2f2ed4535960`.
3. Run `ssh -L 20103:localhost:20104 UvAnetID@ivi-h0.science.uva.nl ssh -L 20104:localhost:20105 ivi-cn009` on your local machine. Here you project the local port `20103` to IvI port `20104` and project IvI port `20104` to GPU node port `20105`.
4. Open your browser and go to http://localhost:20103 and paste the token in step 2 `31427b811f3f3fdaef9d5da5cce8c81ba4df2f2ed4535960`.

## Data storage

1 TB on your home directory.  
Move your data to /hddstore or /sddstore for faster compute.

## Change GCC version

The default GCC version is 4.8.  
Use GCC 6 with
`source /opt/rh/devtoolset-6/enable`
or GCC 7 with
`source /opt/rh/devtoolset-7/enable`
