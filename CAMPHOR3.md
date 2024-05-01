# System Info.
<dl>
<dt> Compute node</dt> 
<dd>Dell PowerEdge C6620

|Item | Description |
|:---------------|:---------------|
|Processing units| 2 CPUs |
|CPU     | Intel Xeon CPU Max 9480 (1.9GHz, 56cores) |
|CPU Peak (FP64)  | 3.4TF / CPU |
|CPU Memory       | 128GB HBM2e |
|CPU Memory Speed | 1.6TB/s / CPU |
</dd>

<dt> OS</dt>
<dd> Red Hat Enterprise Linux 8.9</dd>
<dt> Job scheduler</dt>
<dd> Slurm</dd>
<dt> Interconnect </dt>
<dd> NVIDIA InfiniBand NDR +HDR

|Item | Version |
|:----|:----|
|MLNX_OFED   | 23.10-2.1.3.1 |
|HCA firmware| 20.39.1002 |
|SHARP       | 3.5.1 |
</dd>
</dl>

# Installed development tools

|Tool name |Latest version | Commands | Module name | Description |
|:---------|:--------------|:---------|:------------|:------------|
| Intel oneAPI + MPI | 2023.1 | `icx` / `icpx` / `ifx` / `mpiicx` / `mpiicpx` / `mpiifx` |  |  |
| GNU compiler | 8.5.0 | `gcc` / `g++` / `gfortran` |   |  |
| Open MPI | 4.1.5 | `mpicc` / `mpicxx` / `mpifort` | `openmpi/4.1.5_intel2022.3` |  |

# Batch job
## Job queues

| Name | Number of cores | Max elapsed time | Memory | Description |
|:-----|:--------------|:-----------------|:-------|:------------|
| `jha` | 1 to 2912 (112cores / node) | 14 days | 120GB x nodes |  |

## Job script samples
Note: 
 - `srun` is needed to run programs on compute nodes

### Serial
```
#!/bin/bash
#SBATCH -p jha
#SBATCH -t 00:05:00
#SBATCH --rsc p=1:t=1:c=1
#SBATCH -o %x.%j.out
srun ./a.out
```

### OpenMP
```
#!/bin/bash
#SBATCH -p jha
#SBATCH -t 00:05:00
#SBATCH --rsc p=1:t=12:c=12
#SBATCH -o %x.%j.out
srun ./a.out
```

### MPI+OpenMP
```
#!/bin/bash
#SBATCH -p jha
#SBATCH -t 00:05:00
#SBATCH --rsc p=4:t=8:c=8
#SBATCH -o %x.%j.out
srun a.out
```

## Job options

| Command &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; | Description |
|:--------------------|:--------|
|`-p ` *name*  | Queue name to submit (Only `jha` is available for our project) |
|`-t ` *time* | Limit time (hh:mm:ss) to execute |
|`--rsc p=`*pr*`:t=`*th*`:c=`*co*`:m=`*mem* | Resources to use:   *pr* (Number of processes), *th* (Number of threads / process),   *co* (Number of cores / process), *mem* (Memory / process (default=1142M, max=120G)) |

## Job commands

|Command | Description |
|:-------|:--------|
|`sbatch`  | Submit a job |
|`squeue` | Check statuses of jobs |
|`scancel` | Cancel a job |

## Check resource usage

Login to the portal: <https://web.kudpc.kyoto-u.ac.jp/portal>

# Preparation

## User ID

Will be sent by Email.

## Public key 

Login to the portal: <https://web.kudpc.kyoto-u.ac.jp/portal>

Choose "SSH public key" in "User Information"

## Login node
`camphor.kudpc.kyoto-u.ac.jp`

# Documents

## Web site
<https://web.kudpc.kyoto-u.ac.jp/manual/en>

