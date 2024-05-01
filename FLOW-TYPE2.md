# System Info.
<dl>
<dt> Compute node</dt> 
<dd> Fujitsu Server PRIMERGY CX2570 M5

|Item | Description |
|:---------------|:---------------|
|Processing units| 2 CPUs + 4 GPUs |
|CPU    | Intel Xeon Gold 6230 (2.1GHz, 20cores) |
|CPU Peak (FP64)  | 1.34TF / CPU |
|CPU Memory       | 384GB DDR4 2933MHz |
|CPU Memory Speed | 141GB/s / CPU |
|GPU    | NVIDIA Tesla V100 |
|GPU Peak (FP64)  | 7.8TF / GPU |
|GPU Memory       | 32GB HBM2 |
|GPU Memory Speed | 0.9TB/s / GPU |
</dd>

<dt> OS</dt>
<dd> CentOS Linux 7.7.1908 </dd>
<dt> Job scheduler</dt>
<dd> Fujitsu Technical Computing Suite</dd>
<dd> NVIDIA InfiniBand EDR + HDR

|Item | Version |
|:----|:----|
|MLNX_OFED   | 5.1-0.6.6.0 |
|HCA firmware| 16.28.1002 |
|SHARP       | 2.2.0 |
</dd>
</dl>

# Installed development tools

|Tool name |Latest version | Commands | Module name | Description |
|:---------|:--------------|:---------|:------------|:------------|
| Intel oneAPI + MPI | 2023.2 | `icx` / `icpx` / `ifx` / `mpiicx` / `mpiicpx` / `mpiifx` | `oneapi/2023.2.0` |  |
| GNU compiler | 11.3.0 | `gcc` / `g++` / `gfortran` |  `gcc/11.3.0` |  |
| Open MPI | 4.1.5 | `mpicc` / `mpicxx` / `mpifort` | `gcc/11.3.0` `openmpi/4.1.5` |  |
| NVIDIA HPC SDK | 23.1 | | `hpc_sdk/23.1` | CUDA 12.0|
| NVIDIA HPCX | 2.9.0 | | `hpcx/2.9.0` | |

# Batch job
## Job queues

| Name | Number of Nodes | Max elapsed time | Memory | Description |
|:-----|:--------------|:-----------------|:-------|:------------|
| `cx-interactive` | 1 | 24h | 338GB x nodes | For interactive use |
| `cx-debug` | 1 to 4 | 1h | 338GB x nodes |  |
| `cx-share` | 1/4 | 168h | 84GB |  |
| `cx-single` | 1  | 336h | 338GB x nodes |  |
| `cx-small` | 1 to 8 | 168h | 338GB x nodes |  |
| `cx-middle` | 4 to 16 | 72h | 338GB x nodes |  |
| `cx-large` | 16 to 64 | 72h | 338GB x nodes |  |

## Job script samples

### Serial
```
#!/bin/sh
#PJM -L rscunit=cx
#PJM -L rscgrp=cx-small
#PJM -L node=1
#PJM -L elapse=00:05:00
#PJM -j
./a.out
```

### OpenMP
```
#!/bin/sh
#PJM -L rscunit=cx
#PJM -L rscgrp=cx-small
#PJM -L node=1
#PJM -L elapse=00:05:00
#PJM -j
export OMP_NUM_THREADS=4
./a.out
```

### MPI+OpenMP
```
#!/bin/sh
#PJM -L rscunit=cx
#PJM -L rscgrp=cx-small
#PJM -L node=2
#PJM --mpi proc=8
#PJM -L elapse=00:05:00
#PJM -j
module load oneapi
export OMP_NUM_THREADS=10
mpiexec -machinefile $PJM_O_NODEINF -n $PJM_MPI_PROC ./a.out
```

## Job options

| Option | Description|
|:-------|:-----------|
| `--interact` | Submit an interactive job |
| `-L rscunit=`*name* | System name (`cx` for Flow Type2) |
| `-L rscgrp=`*name* | Queue name to submit |
| `-L node=`*num* | Number of nodes |
| `-L gpu=`*num* | Number of GPUs |
| `-L elapse=`*time* | Limit time (hh:mm:ss) to execute |
| `-j` | Save both stdout and stderr to the same file |

## Job commands
|Command | Description |
|:-------|:--------|
|`pjsub`  | Submit a job |
|`pjstat` | Check statuses of jobs |
|`pjdel` | Cancel a job |

## Check resource usage
### Group usage
Command: `/home/center/local/bin/charge`

### User usage
Command: `/home/center/local/bin/charge2`

# Preparation

## User ID
A paper of the ID will be sent by mail.

## Public key 
Login to: <https://portal.cc.nagoya-u.ac.jp>

Click "SSHpublicKey", and paste your public key and click "Register a new key"

## Login node
 `flow-cx.cc.nagoya-u.ac.jp`

# Documents
## Web site
<https://icts.nagoya-u.ac.jp/en/sc>

## Portal (Manuals)
<https://portal.cc.nagoya-u.ac.jp>

