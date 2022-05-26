# Evaluate sparse runtime support library performance

```shell

git checkout a7ac120a9ad784998a5527fc0a71b2d0fd55eccb
git apply patch
# I add an environment variable here "BENCHMARK_SPARSE"
./mlir-opt ../../mlir/test/Integration/Dialect/SparseTensor/CPU/sparse_storage.mlir --sparse-compiler |BENCHMARK_SPARSE=true TENSOR0="../../mlir/test/Integration/data/wide.mtx" ./mlir-cpu-runner -e entry -entry-point-result=void -shared-libs="../lib/libmlir_c_runner_utils.so.15git"
```


```shell
SUPPORTLIB=/home/hengyume/mlir/llvm-project/build/lib/libmlir_c_runner_utils.so python unit_test_tensor_utils.py
```
