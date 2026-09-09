CUDA doesn't support C++ `rand()`. Use **cuRAND** library to generate random numbers on GPU. 

1. Include headers.
```c++
#include <curand_kernel.h>
```

2. Initialize random states.  
Each GPU thread needs its own random state. You typically set them up in a kernel.  
```c++
__global__ void initRand(curandState *states, unsigned long seed) {
    int idx = blockIdx.x * blockDim.x + threadIdx.x;
    curand_init(seed, idx, 0, &states[idx]);
}
```

3. Generate random numbers in kernels.  
```c++
__global__ void generateRand(curandState *states) {
    int idx = blockIdx.x * blockDim.x + threadIdx.x;
    curandState localState = states[idx];

    // generate random number
    float r = curand_uniform(&localState);

    // write state back
    states[idx] = localState;
}
```

Available generators:  
- `curand_uniform(&state)` → float from Uniform(0,1]
- `curand_uniform_double(&state)` → double from Uniform(0,1]
- `curand_normal(&state)` → float from Normal(0,1)
- `curand(&state)` → unsigned int

These functions are only callable by `__global__` or `__device__` kernels.