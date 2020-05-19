All tests are compiled with `make USE_MPI=FALSE USE_DPCPP=TRUE DIM=<DIM>`.  They are run with `./<executable> <Inputs>`.

Many particle tests are not listed here because they require device API for random number generator.

## Basic

| Directory | DIM | Compile | Run | Inputs |
| ------ | --- | ---------- | ---------- | ---------- |
| Tutorials/Basic/HelloWorld_C  | 3 | OK | OK |        |
| Tutorials/HeatEquation_EX1_C/Exec | 3 | OK | OK | inputs |
| Tutorials/HeatEquation_EX2_C/Exec | 3 | OK | OK | inputs nsteps=1000 |
| Tutorials/HeatEquation_EX3_C/Exec | 2 | OK | OK | inputs_2d nsteps=100 |
| Tutorials/GPU/Launch | 3 | OK | OK | |
| Tutorials/GPU/ParallelReduce | 3 | OK | OK |  |
| Tutorials/GPU/ParallelScan | 3 | OK | OK | |
| Tests/GPU/Vector | 3 | OK | OK | inputs |

# AMR

| Directory | DIM | Compile | Run | Inputs |
| ------ | --- | ---------- | ---------- | ---------- |
| Tutorials/Amr/Advection_AmrCore/Exec/SingleVortex | 2 | OK | OK | inputs |
| Tutorials/Amr/Advection_AmrCore/Exec/SingleVortex | 3 | OK | OK | inputs max_step=100 |
| Tutorials/GPU/Advection_AmrCore/Exec/SingleVortex | 3 | OK | OK | inputs |
| Tutorials/GPU/CNS/Exec/RT | 3 | OK | OK | inputs-rt amrex.fpe_trap_invalid=0 |

# Linear Solvers

| Directory | DIM | Compile | Run | Inputs |
| ------ | --- | ---------- | ---------- | ---------- |
| Tutorials/LinearSolvers/ABecLaplacian_C | 3 | OK | OK | inputs-rt-poisson-lev |
| Tutorials/LinearSolvers/ABecLaplacian_C | 3 | OK | kernel arguments size 1248 | inputs-rt-abeclap-com |
| Tutorials/LinearSolvers/NodalPoisson | 3 | OK | OK | inputs-rt |
| Tutorials/HeatEquation_EX3_C/Exec | 3 | OK | kernel arguments size 1248 | inputs_3d |

# EB

| Directory | DIM | Compile | Run | Inputs |
| ------ | --- | ---------- | ---------- | ---------- |
| Tutorials/EB/CNS/Exec/Combustor | 3 | OK | kernel arguments size 1212 | inputs.regt |
| Tutorials/EB/MacProj | 2 | OK | kernel argumens size 1480 | inputs amrex.fpe_trap_invalid=0 |
| Tutorials/EB/MacProj | 3 | OK | kernel argumens size 1212 | inputs amrex.fpe_trap_invalid=0 |
| Tests/LinearSolvers/EBTensor | 3 | OK | kernel arguments size 1212 | inputs.rt.3d |
| Tests/LinearSolvers/NodeEB | 2 | OK | kernel arguments size 1480 | inputs.rt.2d |
| Tests/LinearSolvers/NodeEB | 3 | OK | kernel arguments size 1212 | inputs.rt.3d.y |

# Particles

| Directory | DIM | Compile | Run | Inputs |
| ------ | --- | ---------- | ---------- | ---------- |
| Tests/Particles/ParticleMesh | 3 | OK | OK | inputs nx=64 ny=64 nz=64 nppc=4 |
| Tests/Particles/ParticleReduce | 3 | OK | OK | inputs |
| Tests/Particles/ParticleTransformations | 3 | OK | abort | inputs |
| Tests/Particles/Redistribute | 3 | OK | abort | inputs.rt.cuda redistribute.do_random=0 |
| Tests/Particles/Redistribute | 3 | OK | abort | inputs.rt.cuda.sort redistribute.do_random=0 |
| Tests/Particles/Redistribute | 3 | OK | abort | inputs.rt.cuda.nonperiodic redistribute.do_random=0 |
| Tests/Particles/Redistribute | 3 | OK | abort | inputs.rt.cuda.mr redistribute.do_random=0 |
| Tests/Particles/NeighborParticles | 3 | ADL | | inputs |
| Tutorials/Amr/Advection_AmrLevel/Exec/SingleVortex | 2 | OK | abort | inputs.tracers |
