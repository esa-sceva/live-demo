# SatcomLLM Local RAG Demo

Two notebooks live in this folder. Both keep **document chunks and the vector database on your machine**. They differ only in where embedding and generation run.

| Notebook | Embeddings + LLM | Chunk / vector storage |
|----------|------------------|------------------------|
| `satcomLLM_demo_local.ipynb` | Local models (sentence-transformers + transformers) | Local (`chunks_cache/`, Qdrant) |
| `satcomLLM_demo_cloud_gpu.ipynb` | Models already hosted on a cloud GPU (OpenAI-compatible APIs) | Local (`chunks_cache/`, Qdrant) |

## Overview

The fully local notebook demonstrates how to build a complete Retrieval-Augmented Generation system using only local resources. Perfect for privacy-sensitive applications, offline environments, or learning RAG fundamentals without API costs.

The cloud GPU notebook is a copy of that demo: chunking and Qdrant stay local, but embedding and generation are HTTP calls to a GPU that already serves both models.

## Prerequisites

**Fully local notebook**
- Python 3.8+
- ~4GB RAM minimum (scales with model size)
- ~3GB disk space (for cached models)
- Runs on **CPU**, **MPS (Apple Silicon)**, or **on-premise GPUs (CUDA)**

**Cloud GPU notebook**
- Python 3.8+
- Network access to a GPU host that already serves the embedding model and the LLM
- No local model download; laptop-class RAM is enough

## Quick Start (fully local)

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

## Quick Start (cloud GPU, local chunks)

Use this when both the embedding model and the LLM are already running on a remote GPU (for example vLLM and/or Text Embeddings Inference).

1. Copy the example env file and set the OpenAI-compatible endpoints:
   ```bash
   cp env.example .env
   # Edit GPU_LLM_URL, GPU_EMBEDDING_URL, and the model names
   ```

2. Open the notebook:
   ```bash
   jupyter notebook satcomLLM_demo_cloud_gpu.ipynb
   ```

3. Place markdown files in the `data/` folder (same as the local demo).

Chunk JSON files and Qdrant still live under `chunks_cache/` and `qdrant_db/`. Model weights stay on the GPU host.

## Notebook Structure

| Part | Description |
|------|-------------|
| **1. Setup & LLM Fundamentals** | Environment setup, model or GPU endpoint configuration |
| **2. RAG Theory** | How retrieval augments generation |
| **3. Vector Database Creation** | Document chunking, embedding, local Qdrant storage |
| **4. RAG Pipeline** | Semantic search + generation |

## Technology Stack

| Component | Fully local notebook | Cloud GPU notebook |
|-----------|----------------------|--------------------|
| Embeddings | all-MiniLM-L6-v2 via sentence-transformers | Hosted embedding model via `/v1/embeddings` |
| Vector DB | Qdrant Local | Qdrant Local |
| LLM | TinyLlama-1.1B via transformers | Hosted LLM via `/v1/chat/completions` |
| Chunking | LangChain (local JSON cache) | LangChain (local JSON cache) |

**Note:** In the fully local notebook you can swap in any HuggingFace / sentence-transformers model that fits your machine. In the cloud GPU notebook, change the model names in `.env` to match whatever is already served on the GPU. Embedding dimension is detected from the hosted model.

## Storage Locations

```
local-demo/
├── env.example        # GPU URLs for the cloud GPU notebook
├── .env               # Your local copy (not committed)
├── data/              # Your markdown documents
├── chunks_cache/      # Cached processed chunks
├── qdrant_db/         # Persistent vector database
└── venv/              # Python virtual environment

~/.cache/huggingface/  # Downloaded models for the fully local notebook only
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

