# gpu-burn
Multi-GPU CUDA stress test
http://wili.cc/blog/gpu-burn.html

# Easy docker build and run

```
git clone https://github.com/wilicc/gpu-burn
cd gpu-burn
docker build -t gpu_burn .
docker run --rm --gpus all gpu_burn
```

# Binary packages

https://repology.org/project/gpu-burn/versions

# Building
To build GPU Burn:

`make`

To remove artifacts built by GPU Burn:

`make clean`

GPU Burn builds with a default Compute Capability of 5.0.
To override this with a different value:

`make COMPUTE=<compute capability value>`

CFLAGS can be added when invoking make to add to the default
list of compiler flags:

`make CFLAGS=-Wall`

LDFLAGS can be added when invoking make to add to the default
list of linker flags:

`make LDFLAGS=-lmylib`

NVCCFLAGS can be added when invoking make to add to the default
list of nvcc flags:

`make NVCCFLAGS=-ccbin <path to host compiler>`

CUDAPATH can be added to point to a non standard install or
specific version of the cuda toolkit (default is 
/usr/local/cuda):

`make CUDAPATH=/usr/local/cuda-<version>`

CCPATH can be specified to point to a specific gcc (default is
/usr/bin):

`make CCPATH=/usr/local/bin`

CUDA_VERSION and IMAGE_DISTRO can be used to override the base
images used when building the Docker `image` target, while IMAGE_NAME
can be set to change the resulting image tag:

`make IMAGE_NAME=myregistry.private.com/gpu-burn CUDA_VERSION=12.0.1 IMAGE_DISTRO=ubuntu22.04 image`

# Usage

    GPU Burn
    Usage: gpu-burn [OPTIONS] [TIME]

    -m X    Use X MB of memory.
    -m N%   Use N% of the available GPU memory.  Default is 90%
    -d      Use doubles
    -tc     Try to use Tensor cores
    -l      Lists all GPUs in the system
    -i N    Execute only on GPU N
    -c FILE Use FILE as compare kernel.  Default is compare.ptx
    -stts T Set timeout threshold to T seconds for using SIGTERM to abort child processes before using SIGKILL.  Default is 30
    -u N    Set GPU utilization threshold to N%. Default is 40%
    -h      Show this help message

    Examples:
    gpu-burn -d 3600 # burns all GPUs with doubles for an hour
    gpu-burn -m 50% # burns using 50% of the available GPU memory
    gpu-burn -l # list GPUs
    gpu-burn -i 2 # burns only GPU of index 2
    gpu-burn -u 60 # sets GPU utilization threshold to 60%
