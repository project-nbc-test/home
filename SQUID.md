# System Info.
<dl>
<dt> Compute node</dt> 
<dd> 

|Item | Description |
|:---------------|:---------------|
|Processing units| 2 CPUs |
|CPU     | Intel Xeon Platinum 8368 (2.4GHz, 38cores) |
|CPU Peak (FP64)  | 2.92TF / CPU |
|CPU Memory       | 256GB DDR4-3200 |
|CPU Memory Speed | 205GB/s / CPU |
</dd>

<dt> OS</dt>
<dd> Rocky Linux 8.8</dd>
<dt> Job scheduler</dt>
<dd> PBSpro</dd>
<dt> Interconnect </dt>
<dd> NVIDIA InfiniBand HDR

|Item | Version |
|:----|:----|
|MLNX_OFED   | 23.04-1.1.3.0 |
|HCA firmware| 20.37.1014 |
|SHARP       | 3.3.0 |
</dd>
</dl>

# Installed development tools

|Tool name |Latest version | Commands | Module name | Description |
|:---------|:--------------|:---------|:------------|:------------|
| Intel oneAPI + MPI | 2023.2 | `icx` / `icpx` / `ifx` / `mpiicx` / `mpiicpx` / `mpiifx` | `BaseCPU` |  |
| GNU compiler / Open MPI| GCC 8.5.0 + Open MPI 4.1.5 | `gcc` / `g++` / `gfortran` / `mpicc` / `mpicxx` / `mpifort` | `BaseGCC`  |  |

# Batch job
## Job queues

| Name &nbsp; &nbsp; &nbsp; &nbsp; | Number of cores | Max elapsed time | Memory | Description |
|:-----|:--------------|:-----------------|:-------|:------------|
| `SQUID` | 1 to 38912 (76 cores / node) | 120h | 248GB x nodes |  |
| `SQUID-R` | 1 to 38912 | 120h | 248GB x nodes | Allow non-full-bisection-bandwidth node allocation |
| `SQUID-S` | 38 cores | 120h | 124GB |  |
| `DBG` | 152 cores| 10m | 248GB x nodes |  |
| `INTC` | 152 cores | 10m | 248GB x nodes | For interactive use |

## Job script samples

### Serial
```
#!/bin/bash
#PBS -q DBG
#PBS --group=jh240058
#PBS -l cpunum_job=1
#PBS -l elapstim_req=00:05:00
cd $PBS_O_WORKDIR ./a.out
```

### OpenMP
```
#!/bin/bash
#PBS -q DBG
#PBS --group=jh240058
#PBS -l cpunum_job=12
#PBS -l elapstim_req=00:05:00 
#PBS -v OMP_NUM_THREADS=12
cd $PBS_O_WORKDIR
./a.out
```

### MPI+OpenMP
```
#!/bin/bash
#PBS -q DBG
#PBS --group=jh240058
#PBS -l cpunum_job=38
#PBS -l elapstim_req=00:05:00 
#PBS -T intmpi  # use Intel MPI             
#PBS -b 2       
#PBS -v OMP_NUM_THREADS=38
cd $PBS_O_WORKDIR
mpirun ${NQSV_MPIOPTS} -np 4 ./a.out 
```

## Job options

| Command  | Description |
|:--------------------|:--------|
|`-q ` *name*  | Queue name to submit |
|`-l elapstim_req=`*time* | Limit time (hh:mm:ss) to execute |
|`--group jh240058` | Group name |
|`-l cpunum_job=`*num* | Number of CPU cores per node |
|`-T ` *type* | Type of MPI: `intmpi` (Intel MPI), `openmpi` (Open MPI) |
|`-v OMP_NUM_THREADS=`*threads* | Number of threads per process |
|`-b ` *num* | Number of nodes |

## Job commands

|Command | Description |
|:-------|:--------|
|`qsub`  | Submit a job |
|`qstat` | Check statuses of jobs |
|`qdel` | Cancel a job |

## Check resource usage

Command: `usage_view`

(0.2998 SQUID point = 1 node * hour)

# Preparation

## User ID

Will be sent by Email.
Login via the specified URL and change the password

## Two factor quthentication

### For portal

Login to: <https://squidportal.hpc.cmc.osaka-u.ac.jp>

Register QR code to your authenticator

### For SSH to the login node

Login to: <http://www.hpc.cmc.osaka-u.ac.jp/system/manual/squid-use/login>

Register QR code to your authenticator

## Login node
`squidhpc.hpc.cmc.osaka-u.ac.jp`

Enter password, and enter the verification code of the authenticator

# Documents

## Web site
<http://www.hpc.cmc.osaka-u.ac.jp/en/system/manual/squid-use>

