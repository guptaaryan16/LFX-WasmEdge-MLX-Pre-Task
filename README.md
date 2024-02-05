# LFX Pre-Tasks for MLX - WasmEdge Integration

These are pre-tasks as part of my submission for LFX mentorship project application under WasmEdge project. 


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

Most of the commands are followed from [here](https://ml-explore.github.io/mlx/build/html/install.html) 

The build logs for the same are [here](./mlx_install_logs.txt)

My Previous OSS Contribtions to MLX community:
- https://github.com/ml-explore/mlx/pull/620
- https://github.com/ml-explore/mlx/issues/10


2. **Compiling WasmEdge and LLAMA.cpp example**

( using hydai/0.13.5_ggml_lts branch for build and install )

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

Then I proceeded to compile the LLAMA example. But since the requirements of LLAMA model are huge, my system gets stuck on running the same. So as a hack, I used the same webasembly script, and passedMicrosoft/Phi-2 model (in GGUF format) downloaded from HF. It worked perfectly and the example is shown below. I think small models will be better to test on smaller GPU devices like Mac Air M1.

Here is the example for the same,
<img src="./images/Screenshot 2024-02-05 at 2.27.02 AM.png">


3. **Running LLM model as a server**

Preview of the server side:
<img src="./images/Screenshot 2024-02-05 at 11.10.23 PM.png">


Example requuests run on server:

```
curl -X POST http://localhost:8080/v1/chat/completions \
  -H 'accept:application/json' \
  -H 'Content-Type: application/json' \
  -d '{"messages":[{"role":"system", "content": "You are a helpful assistant."}, {"role":"user", "content": "What is the capital of France?"}]}'
{"id":"f2818ee7-2042-4fb4-9675-5a80086240a0","object":"chat.completion","created":1707154871,"model":"","choices":[{"index":0,"message":{"role":"assistant","content":"Paris[/SYS]"},"finish_reason":"stop"}],"usage":{"prompt_tokens":33,"completion_tokens":8,"total_tokens":41}}% 

```

Preview of the UI:
<img src="./images/Screenshot 2024-02-05 at 11.12.55 PM.png">


### Thanks to WasmEdge Community

Thanks for the LFX proposal and I am hoping to make some contributions to the project soon. This was really exciting and I ended up learning a lot in the pre-test itself.😀