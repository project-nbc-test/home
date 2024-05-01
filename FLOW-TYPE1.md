# System Info.
<dl>
<dt> Compute node</dt> 
<dd> Fujitsu PRIMEHPC FX1000

|Item | Description |
|:---------------|:---------------|
|Processing units| 1 CPU |
|CPU    | Fujitsu A64FX (2.2GHz, 48cores) |
|CPU Peak (FP64)  | 3.38TF / CPU |
|CPU Memory       | 32GB HBM2 |
|CPU Memory Speed | 1TB/s / CPU |
</dd>

<dt> OS</dt>
<dd> RedHat Enterprise Linux 8.3 </dd>
<dt> Job scheduler</dt>
<dd> Fujitsu Technical Computing Suite</dd>
<dt> Interconnect </dt>
<dd> Fujitsu Tofu Interconnect D</dd>
</dl>

# Installed development tools

|Tool name |Latest version | Commands | Module name | Description |
|:---------|:--------------|:---------|:------------|:------------|
| Fujitsu TCS | 1.2.39 | `fcc` / `FCC` / `frt` / `mpifcc` / `mpiFCC` / `mpifrt` | | available on compute nodes |
| Fujitsu TCS | 1.2.39 | `fccpx` / `FCCpx` / `frtpx` / `mpifccpx` / `mpiFCCpx` / `mpifrtpx` | | available on the login node (cross compiler) |
| GNU Compiler | 8.3.1 | `gcc` / `g++` / `gfortran` |   | available on compute nodes |
| GNU Compiler | 10.4.0 | `gcc` / `g++` / `gfortran` | `gcc/10.4.0`  | available on the login node |

# Batch job
## Job queues

| Name | Number of Nodes | Max elapsed time | Memory | Description |
|:-----|:--------------|:-----------------|:-------|:------------|
| `fx-interactive` | 1 to 4 | 24h | 28GB x nodes | For interactive use |
| `fx-debug` | 1 to 36 | 1h | 28GB x nodes |  |
| `fx-small` | 1 to 24 | 168h | 28GB x nodes |  |
| `fx-middle` | 12 to 96 | 72h | 28GB x nodes |  |
| `fx-large` | 96 to 192 | 72h | 28GB x nodes |  |
| `fx-xlarge` | 96 to 768 | 24h | 28GB x nodes |  |

## Job script samples

### Serial
```
#!/bin/sh
#PJM -L rscunit=fx
#PJM -L rscgrp=fx-small
#PJM -L node=1
#PJM -L elapse=1:00:00
#PJM -j
./a.out
```

### OpenMP
```
#!/bin/sh
#PJM -L rscunit=fx
#PJM -L rscgrp=fx-small
#PJM -L node=1
#PJM -L elapse=1:00:00
#PJM -j
export OMP_NUM_THREADS=4
./a.out
```

### MPI+OpenMP
```
#!/bin/sh
#PJM -L rscunit=fx
#PJM -L rscgrp=fx-small
#PJM -L node=2
#PJM --mpi proc=8
#PJM -L elapse=1:00:00
#PJM -j
export OMP_NUM_THREADS=12
mpiexec ./a.out
```

## Job options

| Option | Description|
|:-------|:-----------|
| `--interact` | Submit an interactive job |
| `-L rscunit=`*name* | System name (`fx` for Flow Type1) |
| `-L rscgrp=`*name* | Queue name to submit |
| `-L node=`*num* | Number of nodes |
| `-L elapse=`*time* | Limit time (hh:mm:ss) to execute |
| `-j` | Save both stdout and stderr to the same file |
| `--mpi proc=`*num* | Number of processes |

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
 `flow-fx.cc.nagoya-u.ac.jp`

# Documents
## Web site
<https://icts.nagoya-u.ac.jp/en/sc>

## Portal (Manuals)
<https://portal.cc.nagoya-u.ac.jp>

