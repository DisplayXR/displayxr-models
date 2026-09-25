# DisplayXR conversion models

Content-addressed ONNX model blobs used by the DisplayXR Browser's **Convert to 3D** feature (real-time 2D→3D lifting of videos and images for glasses-free 3D displays) and by the `@displayxr/inline3d` web SDK's `lift()` API.

Every file is published once, under its SHA-256, as an asset of the permanent [`blobs`](https://github.com/DisplayXR/displayxr-models/releases/tag/blobs) release: `https://github.com/DisplayXR/displayxr-models/releases/download/blobs/<sha256>.onnx`. Blobs are immutable; a new model version is a new blob plus a manifest bump. The manifest (`models.json`, schema 1) is the source of truth for names, roles, hashes and sizes, and is mirrored byte-for-byte in the SDK and the browser installer.

## Models

| name | what | upstream | licence | size | sha256 | in installer |
|---|---|---|---|---|---|---|
| `vda-small-stream-518x294` | Video-Depth-Anything-Small (streaming, w16 = fp16 weights/fp32 compute), 518×294 | [ByteDance](https://github.com/DepthAnything/Video-Depth-Anything) | Apache-2.0 | 58 MB | `71e3ae9e96606afe905eb2f4bab71700e7b9a5b6167bf9d145851720b452a949` | yes |
| `vda-small-stream-364x210` | Video-Depth-Anything-Small (streaming, w16), 364×210 | [ByteDance](https://github.com/DepthAnything/Video-Depth-Anything) | Apache-2.0 | 58 MB | `2bcf27020b45bd25f3ed4e28b3fc328c33af934661c0ee2be73a427a30d4f184` | yes |
| `da2-small` | Depth-Anything-V2-Small, fp16, dynamic shape | [HKU / TikTok](https://github.com/DepthAnything/Depth-Anything-V2) | Apache-2.0 | 50 MB | `2df6223f206b5164e21f664ace61dabeb9bb6a49b8b5a3e00510b4807d0f5b04` | yes |
| `moge3-vitl-770x434` | MoGe-3 ViT-L backbone (no SSR refiner), fp16, 770×434 | [Microsoft](https://github.com/microsoft/MoGe) | MIT | 715 MB | `46d6b8c0c800c160b83414a6beb49194a7be1a7e6774f4538603abea488c8b9f` | yes |
| `moge3-vitl-1022x574` | MoGe-3 ViT-L backbone (no SSR refiner), fp16, 1022×574 | [Microsoft](https://github.com/microsoft/MoGe) | MIT | 757 MB | `7db5c5273208dd04119bc4273907f9f653f383586cc5028ebd87417f8d8721a5` | yes |
| `da3mono-large-770x434` | Depth Anything 3 Mono-Large, fp16, 770×434 | [ByteDance Seed](https://github.com/ByteDance-Seed/Depth-Anything-3) | Apache-2.0 | 669 MB | `c8cb2d8254d3515e5bac0e9747bd2477fab06649ebebd064e797a230d55585de` | on demand |
| `da3mono-large-1022x574` | Depth Anything 3 Mono-Large, fp16, 1022×574 | [ByteDance Seed](https://github.com/ByteDance-Seed/Depth-Anything-3) | Apache-2.0 | 672 MB | `459676dadee0cd76d24b7723aca1a8113880f8d5afcc7410d9a085e75d554507` | on demand |
| `light-inpaint-v1-1024x576` | iw3 light_inpaint_v1 (disocclusion inpainting), fp16, 1024×576 | [nagadomi](https://github.com/nagadomi/nunif) | MIT | 7 MB | `2af8952a4da6e8fde91da120329656ef885e16e159faa25b821902688658ad36` | yes |
| `light-inpaint-v1-512x288` | iw3 light_inpaint_v1, fp16, 512×288 | [nagadomi](https://github.com/nagadomi/nunif) | MIT | 5 MB | `c1cd5b9ac2a37840efa135641f4f7e5824ee8f6b067472c0f5037d9b2e8be011` | yes |

Total: 2.99 GB (installer set ≈ 1.65 GB).

## Licences

These files are ONNX conversions of the upstream authors' released weights; each blob carries its upstream licence (Apache-2.0 or MIT), reproduced in [`LICENSES/`](LICENSES/). Only permissively licensed models are published here — models under non-commercial or research-only terms are deliberately excluded. Conversion notes: DINOv2 position embeddings are baked for the fixed input resolution; the streaming Video-Depth-Anything export carries its 42-slot temporal cache as explicit inputs/outputs; MoGe-3 is exported without its CUDA-only sparse refiner (`refine_steps=0`); "w16" means fp16 weights with fp32 compute (pure fp16 compute is numerically unsafe on WebGPU for the streaming model).

The conversion scripts and the SDK that consumes these blobs live in the [`displayxr-web`](https://github.com/DisplayXR/displayxr-web) repository.
