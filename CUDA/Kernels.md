# Functions
`__global__`: A **kernel** function.
- Executed on device.
- Called on host.
- Must return `void`.

`__device__`: A device function.
- Executed on device.
- Called on device.

`__host__`: A host function.
- Executed on host.
- Called on host.

# Grid, Block and Warp
CUDA GPUs have many parallel processors grouped into **Streaming Multiprocessors**, or SMs. 

**Grid**: all threads launched by a kernel.
- A grid is made up of multiple blocks.

**Block**: a group of threads that must fit on one SM.
- The number of threads per block cannot exceed the number of threads an SM can host.
- A block is made up of multiple warps.
- The number of threads per block is a multiple of 32.

**Warp**: 32 threads that the SM actually schedules together.

Relation:  
- Each SM can run **multiple** concurrent thread blocks.
- Multiple threads from the same block must run on a **single** SM.
- Multiple blocks from the same grid can run on **different** SMs.

# One Thread Per Item
- `blockIdx.x`: Id of the block.
- `blockDim.x`: Number of threads in each block.
- `threadIdx.x`: Id of the thread.

```cpp
__global__ void add(int n, float *x, float *y)
{
    int index = blockIdx.x * blockDim.x + threadIdx.x;

    if (i < n)
        y[i] = x[i] + y[i];
}
```
- `index` is the starting index of the thread.

# Grid-Stride Loops
- `gridDim.x`: number of blocks in each grid

Grid-stride loops
- Separates the amount of data from the number of threads.
- Supports data larger than the grid.

```cpp
__global__ void add(int n, float *x, float *y)
{
	int index = blockIdx.x * blockDim.x + threadIdx.x;
	int stride = blockDim.x * gridDim.x;
	for (int i = index; i < n; i += stride)
		y[i] = x[i] + y[i];
}
```
- `stride` is the total number of threads in the grid.