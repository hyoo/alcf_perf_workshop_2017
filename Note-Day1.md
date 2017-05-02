# Intro 

- INCITE proposal
  - http://www.doeleadershipcomputing.org/2017-incite-proposal-writing-webinar/
- Getting Started
  - [Slides](http://www.alcf.anl.gov/files/ALCF_GettingStarted_2016_1.pdf)
  - [Video](https://www.youtube.com/watch?v=RqKjLNJ3A-0&feature=youtu.be)
- [ALCF Many-Core Tools & Technologies Video Series](https://www.youtube.com/playlist?list=PLGj2a3KTwhRa__pANkWixmIZWBLQkEhZD)



# System Architecture - Hardware 

- Sytems
  - Mira/Cetus/Vesta: Blue Gene, 10PF
  - Cooley : 126 Teslka K80, Haswell
  - Theta : KNL (Cray), 10PF
  - Storage
    - home: 1.4PB
    - scratch: mira-fs0, mira-fs1,,,
- Blue Gene
  - Blue Gene/Q (3rd) - 2012. LLNL (#4), ANL(#9)
  - Low speed, low power but Massive parallelism
  - Programming Models
    - Fortran, C, C++, Python
    - MPI, OpenMP, Pthreads
  - 5D torus network
- Cray XC40
  - Theta
  - Intel Xeon Phi 2g
  - Aurora 2018
- Cooley

# Software & Job Submission

- [Presentation files](http://www.alcf.anl.gov/presentations)

## Outline

### Mira (Blue Gene Q)

#### Software & SoftEnv

- Available softwares:  see [/user-guides/software-and-libraries](https://www.alcf.anl.gov/user-guides/software-and-libraries)
- SoftEnv:
  - For more detail see [softenv-intro](www.mcs.anl.gov/hs/software/systems/softenv/softenv-intro.html)
  - config files locates at `~/.soft`
  - `soft add/remove keyword` to change env
  - @default should be very end in the .soft file
  - use .bash_profile for env settings. not .soft
  - after modifying ~/.soft, run `resoft`
- Compiler Wraps
  - `+mpiwrapper-xl` : IBM XL (mpixlc, mpixlc++, mpixlf77, mpixlf90, etc)
  - `+mpiwrapper-gcc` : GNU (mpicc, mpicxx, mpif77, mpif90)
  - `+mpiwrapper-bgclang` : CLANG (mpiclang, mpiclang++, mpiclang++11)

#### Building your code

#### Preparing

- See more details at [/user-guides/allocation-accounting-sbank](https://www.alcf.anl.gov/user-guides/allocation-accounting-sbank)
- Disk quota
  - `myquota`
  - `myprojectquotas`
- Computing hour allocations
  - `sbank`
  - `sbank l a -p <project_name>`: Allocation available to project
  - `sbank l u -p <project_name> -u <user>`: Charges against user 
- Queues
  - To get list of queues available `qstat -Q`
  - status of my jobs `qstat -u hsyoo`
  - queue details `qstat -f(l) <jobId>`

#### Queing

- Cobalt Scheduler


- submit: `qsub`
- minimum info to submit a job
  - `qsub -A <project> -t <wall-time> -n <node size> -O <output prefix> <executable> <args>`
- For more detail, see [/user-guides/cobalt-job-control](https://www.alcf.anl.gov/user-guides/cobalt-job-control) 
- standard files
  - <jobid>.cobalt error, <jobid>.error, <jobid>.output
- `/soft/cobalt/examples/` contains examples for each system

#### Optimizing for queue throughput

For better system throughput, admin will reallocate queues based on node size and walltime.

- prod-long queue: < 4k, long (6-12h)
- prod-short: <4k, <6h
- prod-capability: >4k
- Consider chaining jobs (dependencies) in order to boost job score

### THETA

#### software & libraries

- /soft/compilers
- /soft/debuggers
- /soft/libraries
- /soft/perftools
- /soft/visualization

#### modules

- `help` `list` `avail` `load` `unload` `switch|swap` `display|show`

#### compilers

- Use Cray wrappers
  - use cc, CC, ftn
- Select compilers
  - module swap <old_env> <new_env>
  - `module swap PrgEnv-intel PrgEnv-llvm` or `module swap PrgEnv-intel PrgEnv-gnu`

#### Submitting script

- `aprun`
- example: 2 nodes, 64 ranks/node, 1 thread/rank, 1 rank/core
  - `aprun -n 128 -N 64 -d 1 -j 1 -cc depth -e OMP_NUM_THREADS=1 <exe>`
- `numactl`



### Checking Status 

- [Mira Status View](http://status.alcf.anl.gov/mira/activity)


- to see all reservations: `showres`
- list status of partitions on Mira: `partlist`
- list status of nodes on Theta: `nodelist



## Login

```
$ssh (id)@(resource).alcf.anl.gov
// for password
[4 digit pin]+[authentication token]
```



## Reference

- [User Guide](https://www.alcf.anl.gov/user-guides/new-user-guide)

 