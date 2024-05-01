# System Info.
<dl>
<dt> Compute node</dt> 
<dd>NEC SX-Aurora TSUBASA C401-8

|Item | Description |
|:---------------|:---------------|
|Processing Units|8 VE (Vector Engines) + 1 VH (Host)|
|VE Processor    |NEC VE Type 30A|
|VE Peak (FP64)  |4.91TF / VE|
|VE Memory       |96GB HBM2E / VE|
|VE Memory Speed |2.45TB/s / VE|
|VH Processor    |AMD EPYC 7763 (2.45GHz, 64cores)|
|VH Peak (FP64)  |2.5TF / VH|
|VH Memory</dt>  |256GB DDR4-3200 / VH|
|VH Memory Speed |0.2TB/s / VH|
</dd>

<dt> OS</dt>
<dd> Rocky Linux 8.8</dd>
<dt> Job scheduler</dt>
<dd>NEC Network QUeuing System V</dd>
<dt> Interconnect </dt>
<dd>NVIDIA InfiniBand NDR 

|Item | Version |
|:----|:----|
|MLNX_OFED   | 23.04-1.1.3|
|HCA firmware| 20.37.1014|
|SHARP       | 3.3.0|
</dd>
</dl>

# Installed development tools

|Tool name |Latest version | Commands | Module name | Description |
|:---------|:--------------|:---------|:------------|:------------|
| NEC SDK  | 5.2.0 | `ncc` / `nc++` / `nfort` |  | for VE|
| NEC MPI | 3.6.0 | `mpincc` / `mpinc++` / `mpinfort` |  | for VE |
| Intel oneAPI | 2024.0.2 | `icx` / `icpx` / `ifx` | `compiler/latest` | for VH |
| Intel MPI | 2021.11 | `mpiicx` / `mpiicpx` / `mpiifx` | `compiler/latest`<br>`mpi/latest` | for VH |
| GNU Compiler | 8.5.0 | `gcc` / `g++` / `gfortran` |   | for VH |

# Batch job
## Job queues

| Name | Number of VEs | Max elapsed time | Memory | Description |
|:-----|:--------------|:-----------------|:-------|:------------|
| `sxsf` | 1 | 1h | 96GB | Free of charge |
| `sxs` | 1 to 2048 | 720h | 96GB x Num VEs | Charged |

## Job script samples

### Serial
```
#!/bin/sh
#PBS -q sxsf
#PBS --venode 1
#PBS -l elapstim_req=00:10:00
cd $PBS_O_WORKDIR
./a.out
```

### OpenMP
```
#!/bin/sh
#PBS -q sxs
#PBS --venode 1
#PBS -l elapstim_req=00:10:00
#PBS -v VE_OMP_NUM_THREADS=16  
cd $PBS_O_WORKDIR
./a.out
```

### MPI+OpenMP
```
#!/bin/sh
#PBS -q sxs
#PBS --venode 8  # Number of VEs 
#PBS -l elapstim_req=00:10:00
#PBS -v VE_OMP_NUM_THREADS=16  
cd $PBS_O_WORKDIR
mpirun -np 8 ./a.out
```

## Job options

| Option | Description|
|:-------|:-----------|
| `--venode` | Number of VEs to use |
| `-l elapstim_req` | Time limit for this job |
| `-v VE_OMP_NUM_THREADS=`*num* | Use *num* cores per VE to use (Each VE has 16 cores) |
| `-jo` | Save both stdout and stderr to the same file |

## Job commands
|Command | Description |
|:-------|:--------|
|`qsub`  | Submit a job |
|`reqstat` | Check statuses of jobs |
|`qdel` | Cancel a job |

## Check resource usage
Login to the portal: <https://www.ss.cc.tohoku.ac.jp/portal>

Choose "Details of Project Billing" or "Details of User Billing"

# Preparation

## User ID
For foreign users, the ID will be notified by the project leader.
For Japanese users, a paper of the ID will be sent by mail.

## Public key 
Login to the portal: <https://sportal.ss.cc.tohoku.ac.jp/thkportal/riyosha_login>

Choose "Create and Register Keys for SSH Login" to create a new key-pair.
A new private key will be saved in your PC.
Use it to login to AOBA-S.
After logging in, you can add your public keys to `.ssh/authorized_keys` .

## Login node
 `sfront.cc.tohoku.ac.jp`

# Documents
## Web site
<https://www.ss.cc.tohoku.ac.jp>
(Japanese)

## Usage
<https://www.ss.cc.tohoku.ac.jp/aoba-s>
(Japanese)

## Manuals from the system vendor
<https://sxauroratsubasa.sakura.ne.jp/Documentation>
(English)

