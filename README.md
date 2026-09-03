# WebLLM economic-data extraction demo

A small, browser-only comparison of two local LLM runtimes for extracting structured economic data from policy documents. No server or API key is required: the selected model downloads to the browser on first use and runs with WebGPU.

## Demos

- [`index.html`](index.html) uses [WebLLM](https://github.com/mlc-ai/web-llm) with `Llama-3.2-1B-Instruct-q4f16_1-MLC`. It requests schema-constrained JSON, falls back to plain generation when needed, and flags a few obvious field mistakes.
- [`transformer.htm`](transformer.htm) uses [Transformers.js](https://github.com/huggingface/transformers.js) with `onnx-community/Qwen2.5-0.5B-Instruct` as a comparison. It checks whether the response parses as JSON, but does not use constrained decoding.
- [`web.js`](web.js) is a minimal WebLLM API example for running from a JavaScript toolchain.

## Run

Serve the directory over localhost; do not open the HTML files with `file://`.

```sh
python3 -m http.server
```

Open the local URL printed by the command, then use `index.html` or `transformer.htm`. On first use, wait for the model download before extraction begins.

## Requirements

- A current browser with WebGPU enabled (Chrome or Safari work best).
- Enough disk space and memory for the downloaded model; the default WebLLM model is approximately 1 GB.
- Internet access on first use for the model files and browser-loaded packages.

## Notes

The sample document is editable. Paste another central-bank minute or similar text, run extraction, and treat the output as a model result to review—not authoritative economic data.

To try another WebLLM model, change `MODEL_ID` near the top of `index.html`. The page contains the existing `gemma3-1b` experiment and its required configuration override.

This is the demonstration for the article [WebLLM vs Transformers.js: which in-browser LLM engine should you ship?](https://truongphan.com/2026/09/02/webllm-vs-transformersjs/) by [Truong Phan](https://truongphan.com/)