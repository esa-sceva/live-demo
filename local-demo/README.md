# SatcomLLM Local RAG Demo

A fully local RAG pipeline that runs entirely on your machine — no external APIs required.

## Overview

This notebook demonstrates how to build a complete Retrieval-Augmented Generation system using only local resources. Perfect for privacy-sensitive applications, offline environments, or learning RAG fundamentals without API costs.

## Prerequisites

- Python 3.8+
- ~4GB RAM minimum (scales with model size)
- ~3GB disk space (for cached models)

### Supported Hardware

Runs on **CPU**, **MPS (Apple Silicon)**, or **on-premise GPUs (CUDA)**. The notebook automatically detects and uses the best available option.

## Quick Start

1. **Open the notebook:**
   ```bash
   jupyter notebook satcomLLM_demo_local.ipynb
   ```

2. **Run the setup cell** — it will automatically:
   - Create a virtual environment (`./venv/`)
   - Install all dependencies
   - Download models on first run

3. **Add your documents:**
   - Place markdown files in the `data/` folder

That's it — no API keys needed!

## Notebook Structure

| Part | Description |
|------|-------------|
| **1. Setup & LLM Fundamentals** | Environment setup, local model configuration, tokenization basics |
| **2. RAG Theory** | How retrieval augments generation |
| **3. Vector Database Creation** | Document chunking, embedding, Qdrant storage |
| **4. RAG Pipeline** | Semantic search + local LLM generation |

## Technology Stack

| Component | Default | Customizable |
|-----------|---------|--------------|
| Embeddings | all-MiniLM-L6-v2 (384-dim, ~80MB) | Any sentence-transformers model |
| Vector DB | Qdrant Local | In-memory or persistent |
| LLM | TinyLlama-1.1B (~2.2GB) | Any HuggingFace model |
| Chunking | LangChain | Configurable chunk size/overlap |

**Note:** You can swap in any compatible model. Larger models (e.g., Llama-7B, Mistral) provide better quality but require more RAM/VRAM. Embedding dimension affects vector DB size.

## Storage Locations

```
local-demo/
├── data/              # Your markdown documents
├── chunks_cache/      # Cached processed chunks
├── qdrant_db/         # Persistent vector database
└── venv/              # Python virtual environment

~/.cache/huggingface/  # Downloaded models (automatic)
```

## Key Features

- **Fully offline** after initial model download
- **Flexible hardware** — runs on CPU, MPS, or on-prem GPUs
- **Customizable models** — use any embedding or LLM model that fits your resources
- **Chunk caching** — skip re-processing on subsequent runs
- **Persistent storage** — vector DB survives restarts

## Performance Considerations

| Resource | Impact |
|----------|--------|
| **RAM/VRAM** | Determines max model size you can load |
| **Embedding model** | Larger models → better retrieval, more memory |
| **Embedding dimension** | Higher dims → larger vector DB, better accuracy |
| **LLM size** | Larger models → better generation, slower inference |

Start with the defaults (TinyLlama + MiniLM) and scale up based on your hardware.

## Time Required

~10 minutes for full demo (longer on first run due to model downloads).

## Contact

For questions or issues, contact the SatcomLLM team at [ESA SCEVA](https://github.com/esa-sceva).

