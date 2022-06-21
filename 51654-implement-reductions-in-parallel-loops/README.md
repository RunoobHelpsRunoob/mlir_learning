*5/25/2022*
From the [author's comments](https://github.com/llvm/llvm-project/issues/51654#issuecomment-1074259839), I think the problems remains how to deal with ```Reduce```, since all ```Parallel``` will check whether the results dims equal to reduction dims, but for SparseTensor, things may change somehow.


```
(base) [hengyume@mlp-spr-03 bin]$ ./mlir-opt /home/hengyume/mlir/llvm-project/mlir/test/Integration/Dialect/SparseTensor/CPU/sparse_reductions.mlir --sparse-compiler="parallelization-strategy=3 vectorization-strategy=2" | ./mlir-cpu-runner -e entry  -entry-point-result=void --shared-libs=/home/hengyume/mlir/llvm-project/debug/lib/libmlir_c_runner_utils.so
/home/hengyume/mlir/llvm-project/mlir/test/Integration/Dialect/SparseTensor/CPU/sparse_reductions.mlir:30:10: error: 'arith.addi' op requires the same type for all operands and results
    %0 = linalg.generic #trait_reduction
         ^
/home/hengyume/mlir/llvm-project/mlir/test/Integration/Dialect/SparseTensor/CPU/sparse_reductions.mlir:30:10: note: see current operation: %15 = "arith.addi"(%arg3, %14) : (vector<1xi32>, i32) -> vector<1xi32>
Error: entry point not found
(base) [hengyume@mlp-spr-03 bin]$ ./mlir-opt /home/hengyume/mlir/llvm-project/mlir/test/Integration/Dialect/SparseTensor/CPU/sparse_reductions.mlir --sparse-compiler="parallelization-strategy=3 vectorization-strategy=3" | ./mlir-cpu-runner -e entry  -entry-point-result=void --shared-libs=/home/hengyume/mlir/llvm-project/debug/lib/libmlir_c_runner_utils.so
26
(base) [hengyume@mlp-spr-03 bin]$ ./mlir-opt /home/hengyume/mlir/llvm-project/mlir/test/Integration/Dialect/SparseTensor/CPU/sparse_reductions.mlir --sparse-compiler="parallelization-strategy=3 vectorization-strategy=4" | ./mlir-cpu-runner -e entry  -entry-point-result=void --shared-libs=/home/hengyume/mlir/llvm-project/debug/lib/libmlir_c_runner_utils.so
26
(base) [hengyume@mlp-spr-03 bin]$ ./mlir-opt /home/hengyume/mlir/llvm-project/mlir/test/Integration/Dialect/SparseTensor/CPU/sparse_reductions.mlir --sparse-compiler="parallelization-strategy=3 vectorization-strategy=2" | ./mlir-cpu-runner -e entry  -entry-point-result=void --shared-libs=/home/hengyume/mlir/llvm-project/debug/lib/libmlir_c_runner_utils.so
/home/hengyume/mlir/llvm-project/mlir/test/Integration/Dialect/SparseTensor/CPU/sparse_reductions.mlir:30:10: error: 'arith.addi' op requires the same type for all operands and results
    %0 = linalg.generic #trait_reduction
         ^
/home/hengyume/mlir/llvm-project/mlir/test/Integration/Dialect/SparseTensor/CPU/sparse_reductions.mlir:30:10: note: see current operation: %15 = "arith.addi"(%arg3, %14) : (vector<1xi32>, i32) -> vector<1xi32>
Error: entry point not found
```
