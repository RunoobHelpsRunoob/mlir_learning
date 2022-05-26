*5/25/2022*
From the [author's comments](https://github.com/llvm/llvm-project/issues/51654#issuecomment-1074259839), I think the problems remains how to deal with ```Reduce```, since all ```Parallel``` will check whether the results dims equal to reduction dims, but for SparseTensor, things may change somehow.

