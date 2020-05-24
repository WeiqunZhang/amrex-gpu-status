# DPC++ Status

- [AMReX Test Problems](#AMReX-Test-Problems)
  * [Basic](#Basic)
  * [AMR](#AMR)
  * [Linear Solvers](#Linear-Solvers)
  * [EB](#EB)
  * [Particles](#Particles)

- [Incflo](#Incflo)
  * [No EB](#No-EB)
  * [With EB](#With-EB)

- [MFiX-Exa](#MFix-Exa)
  * [BENCH01-Size0001](#BENCH01-Size0001)

- [WarpX](#WarpX)
  * [Langmuir 2d](#Langmuir-2d)


# AMReX Test Problems

All tests are compiled with `make USE_MPI=FALSE USE_DPCPP=TRUE DIM=<DIM>`.  They are run with `./<executable> <Inputs>`.

## Basic

| Directory | DIM | Compile | Run | Inputs |
| ------ | --- | ---------- | ---------- | ---------- |
| Tutorials/Basic/HelloWorld_C  | 3 | OK | OK |        |
| Tutorials/HeatEquation_EX1_C/Exec | 2 | OK | OK | inputs |
| Tutorials/HeatEquation_EX1_C/Exec | 3 | OK | OK | inputs |
| Tutorials/HeatEquation_EX2_C/Exec | 3 | OK | OK | inputs nsteps=1000 |
| Tutorials/GPU/Launch | 3 | OK | OK | |
| Tutorials/GPU/ParallelReduce | 3 | OK | OK |  |
| Tutorials/GPU/ParallelScan | 3 | OK | OK | |
| Tests/GPU/Vector | 3 | OK | OK | inputs |

## AMR

| Directory | DIM | Compile | Run | Inputs |
| ------ | --- | ---------- | ---------- | ---------- |
| Tutorials/Amr/Advection_AmrCore/Exec/SingleVortex | 2 | OK | OK | inputs |
| Tutorials/Amr/Advection_AmrCore/Exec/SingleVortex | 3 | OK | OK | inputs max_step=100 |
| Tutorials/GPU/Advection_AmrCore/Exec/SingleVortex | 3 | OK | OK | inputs |
| Tutorials/GPU/CNS/Exec/RT | 3 | OK | OK | inputs-rt amrex.fpe_trap_invalid=0 |

## Linear Solvers

| Directory | DIM | Compile | Run | Inputs |
| ------ | --- | ---------- | ---------- | ---------- |
| Tutorials/LinearSolvers/ABecLaplacian_C | 3 | OK | OK | inputs-rt-poisson-lev |
| Tutorials/LinearSolvers/ABecLaplacian_C | 3 | OK | OK | inputs-rt-abeclap-com |
| Tutorials/LinearSolvers/NodalPoisson | 3 | OK | OK | inputs-rt |
| Tutorials/HeatEquation_EX3_C/Exec | 2 | OK | OK | inputs_2d nsteps=100 |
| Tutorials/HeatEquation_EX3_C/Exec | 3 | OK | OK | inputs_3d |

## EB

| Directory | DIM | Compile | Run | Inputs |
| ------ | --- | ---------- | ---------- | ---------- |
| Tutorials/EB/CNS/Exec/Combustor | 3 | OK | OK | inputs.regt |
| Tutorials/EB/MacProj | 2 | OK | OK | inputs amrex.fpe_trap_invalid=0 |
| Tutorials/EB/MacProj | 3 | OK | OK | inputs amrex.fpe_trap_invalid=0 |
| Tests/LinearSolvers/EBTensor | 3 | OK | OK <sup>[1](#footnote1)</sup> | inputs.rt.3d |
| Tests/LinearSolvers/NodeEB | 2 | OK | OK | inputs.rt.2d |
| Tests/LinearSolvers/NodeEB | 3 | OK | OK <sup>[2](#footnote2)</sup> | inputs.rt.3d.y |

<a name="footnote1">[1]</a>: We have to dsable GPU launch in
`MLEBTensorOp::apply`, othewise the run hangs.

<a name="footnote1">[2]</a>: The compiler has trouble JIT-compiling
the `mlndlap_stencil_rap` function.  We have to disable GPU launch for
that function.

## Particles

| Directory | DIM | Compile | Run | Inputs |
| ------ | --- | ---------- | ---------- | ---------- |
| Tests/Particles/ParticleMesh | 3 | OK | OK | inputs nx=64 ny=64 nz=64 nppc=4 |
| Tests/Particles/ParticleReduce | 3 | OK | OK | inputs |
| Tests/Particles/ParticleTransformations | 3 | OK | OK | inputs |
| Tests/Particles/Redistribute | 3 | OK | OK | inputs.rt.cuda redistribute.do_random=0 |
| Tests/Particles/Redistribute | 3 | OK | OK | inputs.rt.cuda.sort redistribute.do_random=0 |
| Tests/Particles/Redistribute | 3 | OK | OK | inputs.rt.cuda.nonperiodic redistribute.do_random=0 |
| Tests/Particles/Redistribute | 3 | OK | OK | inputs.rt.cuda.mr redistribute.do_random=0 |
| Tests/Particles/NeighborParticles | 3 | OK | OK | inputs |
| Tutorials/Amr/Advection_AmrLevel/Exec/SingleVortex | 2 | OK | OK | inputs.tracers particles.do_tiling=0 |


# [Incflo](https://github.com/AMReX-Codes/incflo)

The `development` branch of `incflo` is used.

## No EB

This compiles and runs to completion.
```
cd test_no_eb
make -j 16 USE_MPI=FALSE USE_DPCPP=TRUE
./incflo3d.dpcpp.ex benchmark.double_shear_layer_x
```

## With EB

This compiles and runs to completion.
```
cd test
make -j16 USE_MPI=FALSE USE_CUDA=FALSE USE_DPCPP=TRUE
./incflo3d.dpcpp.ex benchmark.channel_cylinder-x
```


# [MFiX-Exa](https://amrex-codes.github.io/MFIX-Exa/)

Some EB types do not work with DPC++ yet.  Due to the lack of device
API for random number generator in oneAPI, those particle
initialization methods using RNG do not work.

## BENCH01-Size0001

This test compiles and produces correct results.
```
cd exec
make -j16 USE_MPI=FALSE USE_DPCPP=TRUE
cd ../benchmarks/01-HCS/Size0001
../../../exec/mfix3d.gnu.ex inputs
```


# [WarpX](https://github.com/ECP-WarpX/WarpX/)

WarpX is not fully functional with DPC++ yet, because DPC++ does not
yet support recursive device function and device API for random number
generation.  The spectral solver using FFT also has not been ported.

## Langmuir 2d

This test compiles and produces correct results.
```
make -j16 USE_MPI=FALSE USE_OMP=FALSE USE_CUDA=FALSE USE_DPCPP=TRUE DIM=2
Bin/main2d.dpcpp.TPROF.ex Examples/Tests/Langmuir/inputs_3d_rt electrons.ux=0.01 electrons.xmax=0.e-6
```

