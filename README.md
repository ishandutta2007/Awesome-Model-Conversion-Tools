# Awesome-Model-Conversion-Tools

## Top Model Conversion Tools Ecosystem

**Curated List of SaaS Products & Open-Source GitHub Projects**  
*Focused on Format Interoperability, Quantization-Aware Conversion & Hardware-Specific Compilation*  
**Last updated: March 2026**

This repository tracks notable **SaaS platforms** and **open-source projects** for **Model Conversion Tools**. These tools translate trained models between formats — PyTorch to ONNX, ONNX to TensorRT, ONNX to OpenVINO IR, and onward to TFLite, Core ML, and Qualcomm DLC — enabling deployment on hardware that the original training framework never targeted.

**Examples** include ONNX, ONNX Runtime, OpenVINO, TensorRT, Core ML Tools, TFLite Converter, TVM, Treelite, and Qualcomm SNPE (the category leaders).

**Open-source emphasis**: This section is heavily expanded with every major active project for self-hosting, format validation, and transparent conversion pipelines — ideal for ML engineers deploying the same model across NVIDIA GPUs, Intel CPUs, Apple Neural Engine, and Qualcomm NPUs without maintaining separate training code per target.

Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.

## Table of Contents
- [SaaS/Hosted Platforms](#saas-hosted-platforms)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## SaaS/Hosted Platforms

- **Qualcomm AI Model Optimizer (AIMO)** — **Web-based zero-code conversion platform** for edge chipsets. **Converts models to TFLite, ONNX, DLC, and more** with automatic quantization, network simplification, and optional custom operator libraries for Qualcomm platforms [citation:4][citation:10]. **SaaS cloud service (AIMO Online) or private Docker deployment**. **Best for teams targeting Qualcomm Snapdragon NPUs** without writing conversion scripts.

- **NVIDIA TensorRT** — **The reference converter for NVIDIA GPUs.** Compiles ONNX or framework-native models into optimized TensorRT engines with layer fusion, kernel auto-tuning, and precision calibration (FP16, INT8, FP8). **The `trtexec` CLI** builds engines from ONNX with static or dynamic shapes [citation:2][citation:8]. **Best for any model that will run on NVIDIA hardware** — the conversion step is mandatory for maximum GPU throughput.

## Open-Source GitHub Projects

- **[ONNX](https://github.com/onnx/onnx)** — **The universal intermediate representation and conversion hub.** Apache 2.0 licensed. **The central format that most conversion pipelines pass through** — PyTorch exports to ONNX, then ONNX converts to TensorRT, OpenVINO, Core ML, or TFLite [citation:2]. **`onnxmltools`** converts scikit-learn, LightGBM, XGBoost, and other traditional ML models to ONNX . **Best for teams wanting a stable intermediate format** that decouples training frameworks from deployment targets.

- **[OpenVINO](https://github.com/openvinotoolkit/openvino)** — **Intel's inference toolkit with `ovc` (OpenVINO Converter).** Apache 2.0 licensed. **Converts ONNX, TensorFlow, and PaddlePaddle models to OpenVINO IR (.xml + .bin)** with FP16 compression by default [citation:1][citation:2]. **`benchmark_app`** validates throughput after conversion. **The actively maintained CPU acceleration path** for Intel hardware. **Best for self-hosted Intel CPU/iGPU/NPU deployments.**

- **[Core ML Tools](https://github.com/apple/coremltools)** — **Apple's conversion toolkit for the Apple Neural Engine.** **The Unified Conversion API directly converts PyTorch models** — the old two-step PyTorch → ONNX → Core ML workflow is no longer required [citation:3][citation:9]. **Keras and ONNX converters are deprecated in coremltools 6** — migrate to the TensorFlow/PyTorch unified converter. **Best for iOS and macOS deployments** wanting native Neural Engine acceleration.

- **[TensorFlow Lite Converter](https://github.com/tensorflow/tensorflow)** — **The standard conversion path for mobile and embedded deployment.** Converts TensorFlow, Keras, and SavedModel formats to `.tflite` with post-training quantization (dynamic range, full integer, float16). **Best for Android and microcontroller targets** where the TFLite runtime is the deployment standard.

- **[Apache TVM](https://github.com/apache/tvm)** — **The open-source compiler stack for diverse hardware.** Compiles models from ONNX, TensorFlow, and PyTorch to optimized code for CPUs, GPUs, and custom accelerators. **Best for teams targeting non-mainstream hardware** or building custom compilation pipelines.

- **[Treelite](https://github.com/dmlc/treelite)** — **The model compiler for decision tree ensembles.** Converts scikit-learn, XGBoost, and LightGBM tree models into optimized C code for fast inference. **Best for deploying gradient-boosted trees** to production without Python runtime overhead.

- **[Hummingbird](https://github.com/microsoft/hummingbird)** — **Microsoft's traditional ML to tensor compiler.** **Converts scikit-learn, LightGBM, and XGBoost models to PyTorch, TorchScript, ONNX, and TVM** . **Tree traversal compiled to GEMM operations** for GPU acceleration. **Best for teams wanting to accelerate traditional ML models** using neural network runtimes.

### Additional Strong Open-Source Options

- **onnxsim (ONNX Simplifier)** — Simplifies ONNX graphs through constant folding, dead-code elimination, and operator fusion [citation:1]. **Used by timmx exports** before deployment.
- **onnx-tensorrt** — Parser that converts ONNX models to TensorRT engines programmatically.
- **torch2trt** — PyTorch to TensorRT converter.
- **tf2onnx** — TensorFlow to ONNX converter.
- **paddle2onnx** — PaddlePaddle to ONNX converter.

**Frameworks for building custom systems**: Combine **ONNX** as the universal intermediate format with **onnxmltools** for traditional ML conversion, **TensorRT** or **OpenVINO** for hardware-specific compilation, **Core ML Tools** for Apple deployment, **TFLite Converter** for mobile, and **Treelite** or **Hummingbird** for tree model acceleration — to build a conversion pipeline tailored to your training framework and deployment targets.

## How to Contribute

1. Fork the repo.
2. Add/edit entries in `README.md` (follow existing format).
3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.
4. Submit PR with a short explanation.

Star the repo if you find it useful!

## Disclaimer

- This is a **community-curated** list — not exhaustive and not an endorsement.
- Model conversion tools differ significantly in format coverage, quantization support, and target hardware. **Runtime conversion cannot fix preprocessing mismatches** — document RGB/BGR order, mean/std normalization, and channel layout before converting [citation:2][citation:8]. **Core ML Tools deprecated Keras and ONNX converters in version 6** — use the unified PyTorch/TensorFlow converter for new projects [citation:3][citation:9]. **TensorRT engines are tied to the specific CUDA, TensorRT, and driver versions** used to build them — rebuild engines when upgrading the serving stack [citation:2]. **Quantization (INT8, FP16) can degrade accuracy** — validate converted model outputs against the original ONNX model before deployment.
- Self-hosted open-source solutions require proper conversion environment isolation (virtual environments for Python tools), validation datasets for accuracy comparison, and version pinning for reproducible artifact generation.

---

**Made for ML engineers deploying models across heterogeneous hardware with format portability.**
Let's make model conversion more open, validation-driven, and hardware-appropriate.
