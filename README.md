# DAAS

## Datasets

Download from https://zenodo.org/record/4365954#.X-2s8nVKiZQ

- sssp-int.zip contains the int graph inputs.
- sssp-float.zip contains the float graph inputs.
- put the sssp-int and sssp-float directories in the inputs directory, e.g. the input file structure should be
inputs/sssp-int/graph.gr

## Requirements

- cmake >=3.16.3
- LLVM >= 9.0.0
- Boost C++ Libraries
- NVIDIA graph library
- Cuda >= 9.2 && < 11.0
- LonestarGPU Benchmark Suite v3
- CUB v1.3.1
- ModernGPU v1.1
