# Neural Network Dashboard Manual

This program is used to quickly prototype and deploy CNN and FCNN architectures.  
It automatically uses the CUDA-capable GPU when available; if no GPU is found, it falls back to CPU.

The backend uses **PyTorch** to build and train neural networks.  
The program is fully editable and should be easily extendable; you can easily add more layers if you want to extend it.

---

## 📖 Table of Contents
- [Supported Layers & Parameters](#-supported-layers--parameters)
- [Architecture Validation](#️-architecture-validation)
- [CUDA Errors](#-cuda-errors)
- [File Handling System](#-file-handling-system)
  - [CSV Format](#csv-format)
  - [ZIP Format (Image Dataset)](#zip-format-image-dataset)
- [Extendability](#-extendability)
- [Final Note](#-final-note)

---

## Supported Layers & Parameters

| Layer Type        | Input Dimension (`in_dim`) | Output Dimension (`out_dim`) | Kernel Size | Padding | Stride | Extra Parameters | Defaults |
|------------------|----------------------------|-----------------------------|-------------|---------|--------|-----------------|-----------|
| **Conv2d**       | ✅ Required                | ✅ Required                 | Optional    | Optional | Optional | `bias` (bool)   | `kernel=3`, `padding=1`, `stride=1`, `bias=True` |
| **Linear**       | ✅ Required                | ✅ Required                 | –           | –       | –      | –               | None |
| **Dropout**      | ✅ Probability (use `in_dim`) | Same as `in_dim`          | –           | –       | –      | –               | `0.5` (recommend specifying explicitly) |
| **LeakyReLU**    | ✅ Use `in_dim` for slope  | Same as `in_dim`            | –           | –       | –      | `negative_slope` (float) | `negative_slope=0.01` |
| **ELU**          | ✅ Use `in_dim` for alpha  | Same as `in_dim`            | –           | –       | –      | `alpha` (float)         | `alpha=1.0` |
| **ReLU**         | –                          | –                           | –           | –       | –      | –               | No parameters |
| **Tanh**         | –                          | –                           | –           | –       | –      | –               | No parameters |
| **Sigmoid**      | –                          | –                           | –           | –       | –      | –               | No parameters |
| **Flatten**      | –                          | –                           | –           | –       | –      | –               | No parameters |
| **GELU**         | –                          | –                           | –           | –       | –      | –               | No parameters |
| **Softmax**      | –                          | –                           | –           | –       | –      | `dim=1` (fixed) | Hardcoded: `dim=1` |
| **MaxPool2d**    | –                          | –                           | Optional    | Optional | Optional | –               | `kernel=2`, `padding=0`, `stride=2` |
| **AvgPool2d**    | –                          | –                           | Optional    | Optional | Optional | –               | `kernel=2`, `padding=0`, `stride=2` |

**Notes:**
- `in_dim` and `out_dim` are mandatory for layers like **Conv2d** and **Linear**.
- For **Dropout**, enter the probability into the `in_dim` field. (Example: `0.5` for 50% dropout.)
- Layers like **ReLU**, **Tanh**, **Sigmoid**, **Flatten**, **GELU**, and **Softmax** have no user-configurable parameters (except `Softmax`, which uses `dim=1` by default).
- Pooling layers accept optional parameters but work well with defaults.

---

## Architecture Validation

If you build an invalid architecture, the program will stop **before training** begins.

You’ll see a ⚠️ icon next to the problematic layer in the UI.  
You can then edit or delete the layer using the **Edit Layer** tab.

---

## CUDA Errors

If the program encounters a CUDA error:
- The error will appear in the GPU section at the bottom of the UI.
- OR, a warning will appear advising you to restart the app or kernel.

*Note:*  
- CUDA errors require a full kernel or app restart to clear.

---

## File Handling System

The app accepts **CSV** files for tabular data and **ZIP** files for image datasets.

### CSV Format

Your CSV should look like this (headers must match exactly):

dataset.csv
├── x1, x2, x3, ..., y
├── 0.5, 1.2, 3.4, ..., 0
├── 0.7, 0.8, 2.1, ..., 1
└── ...

- `x1, x2, ..., xn` are your features.
- `y` is the label.
- *Headers are case-sensitive.*
- Make sure to include all headers, or training will not start.

---

### ZIP Format (Image Dataset)

Organize your `.zip` file like this:

dataset.zip
├── class1
│   ├── image1.jpg
│   ├── image2.jpg
│   └── ...
├── class2
│   ├── image1.jpg
│   ├── image2.jpg
│   └── ...
└── ...


- Each folder represents a class label.
- Inside folders, use image formats like `.jpg`, `.png`.
- Non-image files inside folders will be ignored.
- The app automatically extracts and deletes temporary files after training.
- The program **only accepts zip** files. Make sure the file is zipped!

---

## Extendability

The program is built to be modular:
- You can easily add more layers to the backend.
- All layers follow a consistent internal config for easy expansion.

---

## Final Note

If you think of improvements or want to extend the features, feel free to hack away!

---


