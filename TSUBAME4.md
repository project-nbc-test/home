# System Info.
<dl>
<dt> Compute node</dt> 
<dd> Cray XD665

|Item | Description |
|:---------------|:---------------|
|Processing units| 2 CPUs + 4 GPUs |
|CPU    | AMD EPYC 9654 (2.4GHz, 96cores) |
|CPU Peak (FP64)  | 3.69TF / CPU |
|CPU Memory       | 768GB DDR5-4800 |
|CPU Memory Speed | 460.8GB/s / CPU |
|GPU    | NVIDIA H100 SXM5 |
|GPU Peak (FP64)  | 33.5TF / GPU |
|GPU Memory       | 94GB HBM2e |
|GPU Memory Speed | 2.4TB/s / GPU |
</dd>

<dt> OS</dt>
<dd> Red Hat Enterprise Linux 9.3 </dd>
<dt> Job scheduler</dt>
<dd> Altair Grid Engine</dd>
<dd> NVIDIA InfiniBand NDR

|Item | Version |
|:----|:----|
|MLNX_OFED   | 23.10-0.5.5|
|HCA firmware| 20.39.2048 |
|SHARP       | 3.5.1 |
</dd>
</dl>

# Installed development tools

|Tool name |Latest version | Commands | Module name | Description |
|:---------|:--------------|:---------|:------------|:------------|
| Intel oneAPI | 2024.0.2 | `icx` / `icpx` / `ifx` | `intel/2024.0.2` |  |
| Intel MPI | 2021.11 | `mpiicx` / `mpiicpx` / `mpiifx` | `intel-mpi/2021.11` |  |
| GNU compiler | 11.4.1 | `gcc` / `g++` / `gfortran` |   |  |
| Open MPI | 5.0.2 | `mpicc` / `mpicxx` / `mpifort` | `openmpi/5.0.2-gcc` | There are modules for other compilers: `openmpi/5.0.2-intel`, `openmpi/5.0.2-nvhpc` |
| NVIDIA HPC SDK + HPCX | 24.1 | | `nvhpc/24.1` | CUDA 12.3|

# Batch job
## Job queues

| Name | Number of Nodes | Max elapsed time | Memory | Description |
|:-----|:--------------|:-----------------|:-------|:------------|
| `node_f` | 1 | 24h | 768GB  | 192cores + 4GPUs |
| `node_h` | 1/2 | 24h | 384GB  | 96cores + 2GPUs |
| `node_q` | 1/4 | 24h | 192GB  | 48cores + 1GPU |
| `node_o` | 1/8 | 24h | 96GB  | 24cores + 1/2GPU |
| `gpu_1` |  | 24h | 96GB  | 8cores + 1GPUs |
| `gpu_h` |  | 24h | 48GB  | 4cores + 1/2GPUs |
| `cpu_160` |  | 24h | 368GB  | 160cores + 0GPU |
| `cpu_80` |  | 24h | 184GB  | 80cores + 0GPU |
| `cpu_40` |  | 24h | 92GB  | 40cores + 0GPU |
| `cpu_16` |  | 24h | 36.8GB  | 16cores + 0GPU |
| `cpu_8` |  | 24h | 18.4GB  | 8cores + 0GPU |
| `cpu_4` |  | 24h | 9.2GB  | 4cores + 0GPU |

## Job script samples

### Serial
```
#!/bin/sh
#$ -cwd
#$ -l cpu_4=1
#$ -l h_rt=00:05:00
./a.out
```

### OpenMP
```
#!/bin/sh
#$ -cwd
#$ -l cpu_4=1
#$ -l h_rt=00:05:00
export OMP_NUM_THREADS=4
./a.out
```

### MPI+OpenMP
```
#!/bin/sh
#$ -cwd
#$ -l node_f=4
#$ -l h_rt=00:05:00
module load openmpi/5.0.2-gcc
export OMP_NUM_THREADS=96
mpirun -npernode 2 -n 8 -x LD_LIBRARY_PATH ./a.out
```

## Job options

| Option | Description|
|:-------|:-----------|
| `-l ` *type*`=`*num* | Submit for *num* instances of *type* resource |
| `-l h_rt=`*time* | Limit time (hh:mm:ss) to execute |
| `-j y` | Save both stdout and stderr to the same file |
| `-p ` *num* | Set job priority to *num*: `-5` (default), `-4` (higher), `-3` (highest) |

## Job commands
Note:
Without `-g` option to qsub, the job is assumed to be experimental (free of charge) with limitation of parallelism (2 nodes or less), elapsed time (10 min or less) and priority (lowest).

|Command | Description |
|:-------|:--------|
|`qsub`  | Submit an experimental job |
|`qsub -g jh240058`  | Submit a job |
|`qstat` | Check statuses of jobs |
|`qdel` | Cancel a job |

## Check resource usage

Command: `t4-user-info group point -g jh240058`

# Preparation

## User ID
Will be sent by Email.

## Public key 
Login to: <https://portal.t4.gsic.titech.ac.jp/ptl>

Click "Register SSH public key"

## Login node
 `login.t4.gsic.titech.ac.jp`

# Documents
## Web site
<https://www.t4.gsic.titech.ac.jp/docs/handbook.en>


