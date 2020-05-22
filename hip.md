# HIP Status

- [AMReX Test Problems](#AMReX-Test-Problems)
  * [Basic](#Basic)

# AMReX Test Problems

All tests are compiled with `make USE_MPI=FALSE USE_CUDA=FALSE USE_HIP=TRUE DIM=<DIM>`.  They are run with `./<executable> <Inputs>`.

## Basic

| Directory | DIM | Compile | Run | Inputs |
| ------ | --- | ---------- | ---------- | ---------- |
| Tutorials/Basic/HelloWorld_C  | 3 | OK | OK |        |
| Tutorials/HeatEquation_EX1_C/Exec | 2 | fail |  | inputs |
| Tutorials/HeatEquation_EX1_C/Exec | 3 | OK | NaN | inputs |
| Tutorials/HeatEquation_EX2_C/Exec | 3 | OK | OK | inputs nsteps=1000 |
| Tutorials/GPU/Launch | 3 | OK | OK | |
| Tutorials/GPU/ParallelReduce | 3 | OK | OK |  |
| Tutorials/GPU/ParallelScan | 3 | OK | OK | |
| Tests/GPU/Vector | 3 | OK | OK | inputs |

