# LLM Memory Calculator

A single-file React app that estimates LLM memory usage (VRAM/RAM) by model size, quantization format, and runtime overhead.

## Online Demo

https://crapthings.github.io/llmmc/

## Features

- Model size input with common presets (`1.5B` to `671B`)
- Memory estimates for:
  - Precision: `FP32`, `FP16 / BF16`
  - Quantized: `INT8`, `GPTQ / AWQ 4-bit`
  - GGUF: `Q8_0`, `Q6_K`, `Q5_K_M`, `Q5_K_S`, `Q4_K_M`, `Q4_K_S`, `Q3_K_M`, `Q2_K`
- Overhead control (`0%` to `200%`)
- GPU fit panel using a `Q4_K_M` reference estimate
- Desktop RTX 50-series presets, including both RTX 5060 Ti memory variants
- Recent RTX PRO and Ada professional GPUs, plus PRO 6000 MIG partitions
- Data center presets for H100/H200 variants, B200/B300, L4/L40/L40S, and AMD MI300X (memory per GPU)
- Visual comparison bars and formatted memory totals

## Formula

```text
Memory (GB) = Params * 1e9 * BitsPerParam / 8 / (1024^3)
Total (GB)  = Memory * (1 + OverheadPercent / 100)
```

## Run Locally

No build step required.

1. Double-click `index.html` (or open it directly in a browser), or
2. Serve with a local static server for best results:

```bash
python3 -m http.server 8080
```

Then visit `http://localhost:8080`.

## Tech Stack

- React 18 (UMD via CDN)
- Babel Standalone (in-browser JSX transform)
- Tailwind CSS CDN
- Inline SVG icon components

## Notes

- Estimates are directional. Actual usage depends on runtime, context length, batch size, KV cache behavior, and framework implementation.
- SEO metadata is included in `index.html` (`description`, Open Graph, Twitter, robots, and JSON-LD).

## GPU Memory Sources

- [NVIDIA GeForce comparison](https://www.nvidia.com/en-eu/geforce/graphics-cards/compare/): RTX 5050 / 5060 (8 GB), 5060 Ti (8 / 16 GB), 5070 (12 GB), 5070 Ti / 5080 (16 GB), and 5090 (32 GB). Desktop specifications only.
- [NVIDIA HGX reference architecture](https://docs.nvidia.com/enterprise-reference-architectures/hgx-ai-factory-h100-h200-b200/latest/components.html): H100 (80 GB), H200 (141 GB), and B200 (180 GB per GPU).
- [NVIDIA enterprise reference architectures](https://developer.nvidia.com/blog/powering-ai-factories-with-nvidia-enterprise-reference-architectures/): HGX B300 (270 GB per GPU).

- User-provided cloud catalog screenshots: RTX PRO 6000 / 6000 WK (96 GB), PRO 4500 / 4500 SE (32 GB), PRO 4000 (24 GB), RTX 4000 Ada (20 GB), RTX 2000 Ada (16 GB), H100 NVL (94 GB), H100 SXM / PCIe (80 GB), H200 SXM (141 GB), L40 / L40S (48 GB), L4 (24 GB), and AMD MI300X (192 GB).
- Cloud catalog capacities are preserved explicitly for B300 (288 GB) and H200 NVL (143 GB), labeled `(Cloud)` in the UI. These are provider-listed capacities, not universal specifications for every deployment. The separate B300 HGX entry retains 270 GB.
- PRO 6000 MIG entries (48 / 24 GB) represent individual partitions, not full GPUs.

All full-GPU entries use memory per GPU, not total server or rack memory. GPU fit compares memory capacity only; runtime and quantization support depend on the software stack. The cloud catalog's availability, prices, and environment-specific compatibility labels are not part of the calculator.
