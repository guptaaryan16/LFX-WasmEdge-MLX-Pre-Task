## My Experiments on Plugin ecosystem in WasmEdge

I have been trying to work out with the initial setup of the WasmEdge-MLX project plugin files which will be added directly to the project. 
I have added sample files for the project as well.

### Initial Headers for the plugin
After exploring the MLX project and compiling the same on my system, I came to know that all of the code seems to reside in `#include <mlx.h>` header and so I added it here similar to the design of the other plugin. Then I proceeded to understand how the plugins work for NN libraries.

Also like most of the plugins, I added a `#include <plugin.h>` borrowed from the project.

### The WasmEdge `WasiNNEnvironment` struct 

This struct seems to handle all the env variables for the NN library. I saw the setup of pytorch, which seems to expose a struct `Graph` (although within flag `WASMEDGE_PLUGIN_WASI_NN_BACKEND_TORCH` which seems ok), which handle objects like torch graph and the device API.
This `Graph` struct also seems to be used in the implementation of llama plugin in the `ggml` files. 

```
struct Graph {
  torch::jit::Module TorchModel;
  torch::DeviceType TorchDevice = at::kCPU;
};
```
We may need to create a similar struct for mlx although first I may need to understand the behaviour of MLX because for the shared memory between CPU and Metal-GPU for this. 

This `Graph` struct will help in loading the torch object in the WasmEdge env and thus connects the two project together.

### Rest of the functions
The rest of the functions seem to provide API to control the model and help in loading results to and from the Graph struct i.e. the NN model.

### My Experiments with WasmEdge and Initial Benchmarking 

WIP

### Differences between llama ggml plugin and MLX plugin 

WIP