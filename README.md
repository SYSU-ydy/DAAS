# DAAS

## Datasets

Download from https://zenodo.org/record/4365954#.X-2s8nVKiZQ

- sssp-int.zip contains the int graph inputs.
- sssp-float.zip contains the float graph inputs.
- put the sssp-int and sssp-float directories in the inputs directory, e.g. the input file structure should be
inputs/sssp-int/graph.gr

The graph files are in binary GR format (http://users.diag.uniroma1.it/challenge9/format.shtml). This format is used by Galois as well as ADDS.
Most of our input graphs are from SuiteSparse Matrix Collection (https://sparse.tamu.edu). The website provides MTX format graphs in text files. We converted them to GR binaries. The remain graphs are inputs that come with Galois (e.g. rmat*.gr and road-*.gr), which are already in an appropriate format.

## Requirements

- cmake >=3.16.3
- LLVM with Clang >= 9.0.0
- Boost C++ Libraries
- NVIDIA graph library
- Cuda >= 9.2 && < 11.0
- LonestarGPU Benchmark Suite v3
- CUB v1.3.1
- ModernGPU v1.1

## Usage

### Building project

Inside code directory, run ./build_all.sh

There are int and float implementations of the solution and of prior solutions (taking int or float graphs)

a. ads_* is the proposed solution
b. nf_* is an optimized implementation of Near-Far,
which is the prior state-of-the-art GPU solution
c. nv_* is an nvGRAPH library implementation
d. cpu_sss_* are implementations of Dijkstra’s algorithm and a CPU delta-stepping algorithm.
e. Note: nf_* and cpu_sssp_* are from their git repository. The build_all.sh script performs the git clone
command and applies patches.

### Running project

Inside the code directory, run ./run_all.sh, and each implementation will produces 2 outputs.
Using ads_int as an example:
a. ads_int_result contains timing and work count results. Each line has 3 fields separated by a space: Graph_name run_time (in seconds) work_count
b. ads_int_final_dist is a directory that has the final distance (i.e. SSSP result) for all graphs (used in the next step)

### validating results

To validate performance results, the correctness of SSSP results can be checked by comparing whether two implementations produce the same final node distances.

a. run ./verify_against_*
This will check the SSSP result (*_final_dist) between our solution and the target implementation.
b. The script verify.py will compare files and report a “mismatch” for any lines that differ.
c. Note: nv_graph uses float data types internally, so wesometimes get conversion problems for int graphs,
with the distances differing by 1 between NV and other implementations (ours and prior solutions).
We commented out the int version’s verification for NV.
