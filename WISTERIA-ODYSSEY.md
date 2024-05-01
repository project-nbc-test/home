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
| GNU Compiler | 8.3.1 | `gcc` / `g++` / `gfortran` |  `gcc/8.3.1` | available on compute nodes |
| GNU Compiler | 12.2.0 | `gcc` / `g++` / `gfortran` | `gcc/12.2.0`  | available on the login node |

# Batch job
## Job queues

| Name | Number of Nodes | Max elapsed time | Memory | Description |
|:-----|:--------------|:-----------------|:-------|:------------|
| `debug-o` | 1 to 144 | 30m | 28GB x nodes |  |
| `short-o` | 1 to 72 | 8h | 28GB x nodes |  |
| `regular-o` | 12 to 1152 | 48h | 28GB x nodes |  |
| `regular-o` | 1153 to 2304 | 24h | 28GB x nodes | Same name for larger number of node with shorter time |

## Job script samples

### Serial
```
#!/bin/sh
#PJM -L rscgrp=debug-o
#PJM -L node=1
#PJM -L elapse=00:05:00
#PJM -g jh240058o
#PJM -j
./a.out
```

### OpenMP
```
#!/bin/sh
#PJM -L rscgrp=debug-o
#PJM -L node=1
#PJM --omp thread=12
#PJM -L elapse=00:05:00
#PJM -g jh240058o
#PJM -j
./a.out
```

### MPI+OpenMP
```
#!/bin/sh
#PJM -L rscgrp=debug-o
#PJM -L node=2
#PJM --mpi proc=8
#PJM --omp thread=12
#PJM -L elapse=00:05:00
#PJM -g jh240058o
#PJM -j
mpiexec ./a.out
```

## Job options

| Option | Description|
|:-------|:-----------|
| `-g jh240058o` | Group name of this project |
| `--interact` | Submit an interactive job |
| `-L rscunit=`*name* | System name (`fx` for Flow Type1) |
| `-L rscgrp=`*name* | Queue name to submit |
| `-L node=`*num* | Number of nodes |
| `-L elapse=`*time* | Limit time (hh:mm:ss) to execute |
| `-j` | Save both stdout and stderr to the same file |
| `--mpi proc=`*num* | Number of processes |
| `--omp thread=`*num* | Number of threads per process |

## Job commands
|Command | Description |
|:-------|:--------|
|`pjsub`  | Submit a job |
|`pjstat` | Check statuses of jobs |
|`pjdel` | Cancel a job |

## Check resource usage

Command: `show_token`

# Preparation

## User ID
Will be sent by Email.

## Public key 
Login to: <https://wisteria-www.cc.u-tokyo.ac.jp>

Click "SSH PublicKey", and paste your public key and click "Register a new key"

## Login node
 `wisteria.cc.u-tokyo.ac.jp`

# Documents
## Web site
<https://www.cc.u-tokyo.ac.jp/supercomputer/wisteria/service>

## Portal (Manuals)
<https://wisteria-www.cc.u-tokyo.ac.jp>

