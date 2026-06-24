# AMD FidelityFX SDK 2.0.0 — FSR 4.0.2 Source (MIT)

This is the **AMD FidelityFX SDK 2.0.0**, containing the **FSR 4.0.2 ML-Upscaler** source code. It was published by AMD on [GPUOpen](https://gpuopen.com/) under the **MIT License**.

## What This Is

The FidelityFX SDK is AMD's collection of optimized rendering techniques for DirectX 12 and Vulkan applications. This version (2.0.0) includes:

| Technique | Version | Description |
|-----------|---------|-------------|
| **Super Resolution (ML-Upscaler)** | **4.0.2** | Machine learning-based upscaling — the primary focus of this archive |
| Super Resolution (Temporal) | 2.3.4 | Temporal multi-frame accumulation upscaler |
| Super Resolution (Upscaler) | 3.1.5 | FSR 3 temporal upscaler |
| Frame Interpolation | 3.1.5 | Frame generation from motion vectors |
| RCAS, SPD, and more | various | Supporting sharpening, downscaling, and utility effects |

## Why This Repository Exists

This source was used as a **structural reference** for the [FSR 4.1.0 Reverse Engineering project](https://github.com/rolaandjayz/fsr-4.1.0-re). The 4.0.2 source provided:

- The neural network architecture (encoder → bottleneck → decoder)
- The complete tensor schema (78 tensors with exact shapes and offsets)
- The FP8 weight quantization format
- The provider-layer dispatch contract that 4.1.0 inherits
- The HLSL shader source for all model variants

FSR 4.0.2 and 4.1.0 share the same model version (`fsr4_model_v07`). Understanding 4.0.2 was essential to understanding 4.1.0.

## License

**MIT License** — Copyright © 2025 Advanced Micro Devices, Inc.

This is AMD's original license, as published on GPUOpen. The full text is in [LICENSE](LICENSE).

> AMD has published every version of FSR from 1.0 through 4.0.2 under the MIT license — the most permissive open-source license in common use. This includes full shader source code, integration code, and build systems.

## Key Paths

- **FSR 4 upscaler source**: `Kits/FidelityFX/upscalers/fsr4/`
- **FSR 4 shaders**: `Kits/FidelityFX/upscalers/fsr4/internal/shaders/`
- **ML2Code runtime**: `Kits/FidelityFX/upscalers/fsr4/dx12/ml2code_runtime/`
- **Provider (DX12)**: `Kits/FidelityFX/upscalers/fsr4/dx12/ffx_provider_fsr4_dx12.cpp`
- **SDK license**: `docs/license.md`

## Model Variants

The FSR 4 source includes both INT8 and FP8 quantized variants:

- `fsr4_model_v07_i8_*` — INT8 quantized (quality, balanced, performance, ultraperf, native, drs)
- `fsr4_model_v07_fp8_no_scale_*` — FP8 quantized without per-tensor scale (quality, balanced, performance, ultraperf, native, drs)

Each variant includes:
- `pre.hlsl` — Encoder/input shader
- `passes_*.hlsl` — Body compute shaders (parameterized by spatial scale)
- `post.hlsl` — Decoder/output shader
- `initializers.bin` — Weight initializer data

## Disclaimer

This repository is an archival copy of AMD's published, MIT-licensed source code. No modifications have been made to AMD's original files. All copyright and attribution belongs to Advanced Micro Devices, Inc.

The [FSR 4.1.0 RE project](https://github.com/rolaandjayz/fsr-4.1.0-re) is a separate repository containing original reverse engineering analysis work.
