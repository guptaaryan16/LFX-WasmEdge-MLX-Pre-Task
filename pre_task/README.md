## PreTask for the LFX Proposal

The pre-task included building framework and examples related to the issue I want to contribute to during the LFX mentroship.


1. **Compiling MLX Project on Python and C++ portions**

I have compiled the projects on both the python and C++ portions of MLX package v0.1.0 on my M1 Macbook Air with the following env and versions for my device.

```
OS: macOS 14.1.1 23B81 arm64 
Host: MacBookAir10,1 
Kernel: 23.1.0 
Terminal: Warp

Python version: 3.9.6
Homebrew 4.2.6
cmake version 3.28.2
GNU Make 3.81
```
I still have to figure out the `make install` command for running Metal build files on my machine but so far so good.
The build logs for the same are [here](./mlx_install_logs.txt)

My OSS Contribtions to MLX community:
1. https://github.com/ml-explore/mlx/pull/620
2. https://github.com/ml-explore/mlx/issues/10

I also have some experience working with PyTorch and other ML frameworks (both for personal projects and in terms of contributions). This will really help me make understand and get started on the requirements of the project.


2. **Compiling WasmEdge and LLAMA.cpp example**

I compiled the WasmEdge with LLAMA plugin on my system, and it works natively on my device. I used the following commands as defined here:
```
cmake -GNinja -Bbuild -DCMAKE_BUILD_TYPE=Release \
  -DWASMEDGE_PLUGIN_WASI_NN_BACKEND="GGML" \
  -DWASMEDGE_PLUGIN_WASI_NN_GGML_LLAMA_METAL=ON \
  -DWASMEDGE_PLUGIN_WASI_NN_GGML_LLAMA_BLAS=OFF \
  .
cmake --build build
# For the WASI-NN plugin, you should install this project.
sudo cmake --install build
```
The build logs can be found [here](wasm_build_logs.txt)

Then I proceeded to compile the LLAMA example and since the requirements of LLAMA model are huge, my system gets stuck on running the same. So as a hack, I used the same script written in Rust for LLAMA, compiled it and passedMicrosoft/Phi-2 model (in GGUF format) downloaded from HF. It worked perfectly and the example is shown below. 

Here is the example for the same,
<img src="./images/Screenshot 2024-02-05 at 2.27.02 AM.png">