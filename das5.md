# DAS-5 cluster

## Account creation

Ask for an account by sending an email to <das-account@cs.vu.nl>. Use your `@uva.nl` email address.  
It should normally take 1-2 days.

## Hostname

`fs4.das5.science.uva.nl` to access GPU nodes.

## Useful things to have in your `.bashrc`

```bash
module load gcc
module load slurm
module load cuda80
module load cuDNN
alias mywatch='/home/koelma/bin/mywatch'
```

Other modules are also available, full list is avaible with `module avail`.

Pick the version you want for CUDA by looking at what's available `module avail cuda`.

## Get a node with slurm

`srun -u --pty bash -i` Get an interactive session on a *CPU* node  
`srun -u --pty --gres=gpu:1 bash -i` Get an interactive session on a *GPU* node  
`srun -u --pty -w node404 bash -i`  Get an interactive session on `node404`  
`srun -u --pty -p fatq bash -i`  Get an interactive session on the fatq node (more RAM)

Ideally you should submit a job instead of using an interactive session:

`srun --gres=gpu:1  python myscript.py --myargument=foo`

`srun --gres=gpu:4 bash mybashscript.sh`

## Jupyter notebook on a node

For those who want to play with jupyter notebook on a node, here is the procedure.

1. Get an interective session on a CPU or GPU node
2. Record which node you got (e.g. `node401`)
3. On the obtained node, run `jupyter notebook --no-browser --port=8888`
4. From your local machine, run `ssh -t -t username@fs4.das5.science.uva.nl -L 8888:localhost:8888 ssh node401 -L 8888:localhost:8888`
5. Open a browser on your local machine and go to http://localhost:8888
6. You should now have access to a jupyter notebook that is running on a node on das5
7. Do **NOT** forget to kill both sessions once you are done

*Note:* if you run into issues to launch jupyter notebook on the GPU node, you might want to remove the following environment variable `unset XDG_RUNTIME_DIR`

## Monitor node usage

Either use `squeue` or `mywatch` (see last line of [.bashrc](#useful-things-to-have-in-your-bashrc))

## Data storage

Your homefolder space is quite limited. Only use it for scripts.

Install your own python or other stuff on `/var/scratch/` (there is already a directory for each user). Also store your data on `/var/scratch/`. If you run out of space, ask Dennis.

Check your current quota with `quota -sv`.

## More info

Read more on the [das-5 website](https://www.cs.vu.nl/das5/jobs.shtml).
