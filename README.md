# SatcomLLM RAG Demo

Interactive Jupyter notebooks demonstrating how to build Retrieval-Augmented Generation (RAG) systems for satellite communications domain knowledge using the [llama3-satcom model](https://huggingface.co/esa-sceva).

## Repository Structure

This repository contains two complete RAG implementations, each designed for different use cases:

### 📦 `local-demo/` - Fully Local RAG System

A **completely offline** RAG pipeline that runs entirely on your local machine. Perfect for:
- Privacy-sensitive applications
- Offline environments
- Learning RAG fundamentals without API costs
- Customization and experimentation

**Technology Stack:**
- Local embeddings: `sentence-transformers` (all-MiniLM-L6-v2)
- Local vector DB: Qdrant (in-memory or file-based)
- Local LLM: TinyLlama or similar small models
- **No API keys required** - everything runs locally

### ☁️ `on-cloud-demo/` - Cloud-Based RAG System

A **production-ready** RAG pipeline using cloud services. Ideal for:
- High-performance inference
- Scalable deployments
- Production applications
- Access to larger, more powerful models

**Technology Stack:**
- Cloud embeddings: DeepInfra API (Qwen3-Embedding-4B)
- Cloud vector DB: Qdrant Cloud
- Cloud LLM: RunPod vLLM with SatcomLLM
- **Requires API keys** - see `on-cloud-demo/README.md` for setup

## Quick Start

Choose the demo that fits your needs:
- **Want to run offline?** → Start with `local-demo/`
- **Need production performance?** → Use `on-cloud-demo/`

Each folder contains detailed instructions in its respective README and notebook.

## Contact

For questions or issues, contact the SatcomLLM team at [ESA SCEVA](https://github.com/esa-sceva).

