# Dashboard
This program can be used to quickly prototype and deploy CNN and FCNN architectures. It preferentially uses the Cuda capable GPU and if no GPU is provided will fallback to using the CPU. The backend uses Pytorch for building and training a neural network. The program is easily editable and can be changed to support more layers if the user desires. 

## Supported Layers & Parameters

| Layer Type        | Input Dimension (`in_dim`) | Output Dimension (`out_dim`) | Kernel Size | Padding | Stride | Extra Parameters | Defaults |
|------------------|----------------------------|-----------------------------|-------------|---------|--------|-----------------|-----------|
| **Conv2d**       | ✅ Required                | ✅ Required                 | Optional    | Optional | Optional | `bias` (bool)   | `kernel=3`, `padding=1`, `stride=1`, `bias=True` |
| **Linear**       | ✅ Required                | ✅ Required                 | –           | –       | –      | –               | None |
| **Dropout**      | ✅ Dropout probability     | Same as `in_dim`            | –           | –       | –      | –               | Provide probability (default= `0.5`) |
| **LeakyReLU**    | Used for `negative_slope`  | Same as `in_dim`            | –           | –       | –      | `negative_slope` (float) | `negative_slope=0.01` |
| **ELU**          | Used for `alpha`           | Same as `in_dim`            | –           | –       | –      | `alpha` (float)         | `alpha=1.0` |
| **ReLU**         | –                          | –                           | –           | –       | –      | –               | No parameters |
| **Tanh**         | –                          | –                           | –           | –       | –      | –               | No parameters |
| **Sigmoid**      | –                          | –                           | –           | –       | –      | –               | No parameters |
| **Flatten**      | –                          | –                           | –           | –       | –      | –               | No parameters |
| **GELU**         | –                          | –                           | –           | –       | –      | –               | No parameters |
| **Softmax**      | –                          | –                           | –           | –       | –      | `dim=1`         | Hardcoded: `dim=1` |
| **MaxPool2d**    | –                          | –                           | Optional    | Optional | Optional | –               | `kernel=2`, `padding=0`, `stride=2` |
| **AvgPool2d**    | –                          | –                           | Optional    | Optional | Optional | –               | `kernel=2`, `padding=0`, `stride=2` |

**Notes:**  
> - All layers use a consistent internal config structure for backend handling.  
> - `in_dim` and `out_dim` are mandatory for layers like `Conv2d` and `Linear`.  
> - For `Dropout`, the probability is entered via the `in_dim` field. Consider updating for clarity.  
> - Layers like `ReLU`, `Tanh`, `Sigmoid`, `Flatten`, `GELU`, and `Softmax` have no user-configurable parameters (except `Softmax`, which is hardcoded to `dim=1`).  
> - Pooling layers accept optional parameters with sensible defaults.


