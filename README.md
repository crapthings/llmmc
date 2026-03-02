# LLM Memory Calculator

A single-file React app that estimates LLM memory usage (VRAM/RAM) by model size, quantization format, and runtime overhead.

## Features

- Model size input with common presets (`1.5B` to `671B`)
- Memory estimates for:
  - Precision: `FP32`, `FP16 / BF16`
  - Quantized: `INT8`, `GPTQ / AWQ 4-bit`
  - GGUF: `Q8_0`, `Q6_K`, `Q5_K_M`, `Q5_K_S`, `Q4_K_M`, `Q4_K_S`, `Q3_K_M`, `Q2_K`
- Overhead control (`0%` to `200%`)
- GPU fit panel using a `Q4_K_M` reference estimate
- Visual comparison bars and formatted memory totals

## Formula

```text
Memory (GB) = Params * 1e9 * BitsPerParam / 8 / (1024^3)
Total (GB)  = Memory * (1 + OverheadPercent / 100)
```

## Run Locally

No build step required.

1. Open `index.html` directly in a browser, or
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
