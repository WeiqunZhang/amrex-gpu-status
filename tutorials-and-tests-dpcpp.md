All tests are compiled with `make USE_MPI=FALSE USE_DPCPP=TRUE DIM=<DIM>`.  They are run with `./<executable> <Inputs>`.

Many particle tests are not listed here because they require device API for random number generator.

## amrex/Tutorials

| Directory | DIM | Compile | Run | Inputs |
| ------ | --- | ---------- | ---------- | ---------- |
| HeatEquation_EX1_C/Exec | 3 | OK | OK | inputs |
| HeatEquation_EX2_C/Exec | 3 | OK | OK | inputs nsteps=1000 |
| HeatEquation_EX3_C/Exec | 2 | OK | OK | inputs_2d nsteps=100 |
| HeatEquation_EX3_C/Exec | 3 | OK | kernel arguments size 1248 | inputs_3d |
| Basic/HelloWorld_C  | 3 | OK | OK |        |
| Amr/Advection_AmrCore/Exec/SingleVortex | 2 | OK | OK | inputs |
| Amr/Advection_AmrCore/Exec/SingleVortex | 3 | OK | OK | inputs max_step=100 |
| Amr/Advection_AmrLevel/Exec/SingleVortex | 2 | OK | abort | inputs.tracers |
| LinearSolvers/ABecLaplacian_C | 3 | OK | OK | inputs-rt-poisson-lev |
| LinearSolvers/ABecLaplacian_C | 3 | OK | kernel arguments size 1248 | inputs-rt-abeclap-com |
| LinearSolvers/NodalPoisson | 3 | OK | OK | inputs-rt |
| EB/CNS/Exec/Combustor | 3 | OK | kernel arguments size 1212 | inputs.regt |
| EB/MacProj | 2 | OK | kernel argumens size 1480 | inputs amrex.fpe_trap_invalid=0 |
| EB/MacProj | 3 | OK | kernel argumens size 1212 | inputs amrex.fpe_trap_invalid=0 |
| GPU/Advection_AmrCore/Exec/SingleVortex | 3 | OK | OK | inputs |
| GPU/CNS/Exec/RT | 3 | OK | OK | inputs-rt amrex.fpe_trap_invalid=0 |
| GPU/Launch | 3 | OK | OK | |
| GPU/ParallelReduce | 3 | OK | OK |  |
| GPU/ParallelScan | 3 | OK | OK | |

## amrex/Tests

| Directory | DIM | Compile | Run | Inputs |
| ------ | --- | ---------- | ---------- | ---------- |
| LinearSolvers/EBTensor | 3 | OK | kernel arguments size 1212 | inputs.rt.3d |
| LinearSolvers/NodeEB | 2 | OK | kernel arguments size 1480 | inputs.rt.2d |
| LinearSolvers/NodeEB | 3 | OK | kernel arguments size 1212 | inputs.rt.3d.y |
| Particles/ParticleMesh | 3 | OK | OK | inputs nx=64 ny=64 nz=64 nppc=4 |
| Particles/ParticleReduce | 3 | OK | OK | inputs |
| Particles/ParticleTransformations | 3 | OK | abort | inputs |
| Particles/Redistribute | 3 | OK | abort | inputs.rt.cuda redistribute.do_random=0 |
| Particles/Redistribute | 3 | OK | abort | inputs.rt.cuda.sort redistribute.do_random=0 |
| Particles/Redistribute | 3 | OK | abort | inputs.rt.cuda.nonperiodic redistribute.do_random=0 |
| Particles/Redistribute | 3 | OK | abort | inputs.rt.cuda.mr redistribute.do_random=0 |
| Particles/NeighborParticles | 3 | ADL | | inputs |
| GPU/Vector | 3 | OK | OK | inputs |
