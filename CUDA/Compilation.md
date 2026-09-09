```
.cu → (cicc) → PTX → (ptxas) → SASS
```
- cicc: Device compiler.
- PTX: Virtual GPU assembly language.
- ptxas: PTX optimizing assembler.
- SASS: Architecture specific assembly language.

pixas optimization levels:
- `-O0`: Optimization disabled.
- `-O1`/`-O2`/`-O3`: Optimization enabled. `-O03` is default.

# Translation Unit
A **translation unit** is one source file after preprocessing.

E.g. `main.cu`
```cpp
#include "utils.cuh"

__global__ void kernel() {}
```

Its translation unit contains:
- The content of `main.cu`.
- The content inserted by `#include "untils.cuh"`
- The results of expanding macros and conditional compilation.

It does not contain function definitions in `utils.cu`.

**By default, CUDA expects all device code to be resolved within the same translation unit.**

NVCC separates host code and device code, compiles them through different toolchain paths, and embeds the generated device image into a host object. 

**Host code uses separate compilation and host linking.**

# RDC
With RDC (Relocatable Device Code) enabled:
```bash
nvcc -rdc=true main.cu functions.cu -o program
```
CUDA can compile multiple compilation units separately, then **device link** them.

**RDC restricts optimization** because compilation units are optimized separately.