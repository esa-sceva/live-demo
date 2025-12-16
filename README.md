# SatcomLLM RAG Demo

Interactive Jupyter notebooks showcasing how to perform inference and build Retrieval-Augmented Generation (RAG) systems for satellite communications, using the [llama3-satcom model](https://huggingface.co/esa-sceva).

## Repository Structure

This repository contains two complete inference+RAG implementations, each designed for different use cases:

### 📦 `local-demo/` - Fully Local RAG System

A **completely local** RAG pipeline that runs entirely on your local machine. Perfect for:
- Privacy-sensitive applications
- Offline environments (once the model is downloaded locally)
- Learning RAG fundamentals without API costs
- Customization and experimentation
- Leveraging on-premise GPUs (or MPS Apple Silicon) for accelerated inference (if available)

**Technology Stack:**
- Local embeddings: `sentence-transformers` (all-MiniLM-L6-v2)
- Local vector DB: Qdrant (in-memory or file-based)
- Local LLM: TinyLlama or similar small models
- GPU acceleration: Supports CUDA (NVIDIA), MPS (Apple Silicon), and CPU
- **No API keys required**: everything runs locally

### ☁️ `on-cloud-demo/` - Cloud-Based RAG System

A **production-ready** RAG pipeline using cloud services. Ideal for:
- High-performance inference
- Scalable deployments
- Access to larger, more powerful models (for embedding and inference)

**Technology Stack:**
- Cloud embeddings: DeepInfra API (Qwen3-Embedding-4B)
- Cloud vector DB: Qdrant Cloud
- Cloud LLM: RunPod vLLM with SatcomLLM
- **Requires API keys**: see `on-cloud-demo/README.md` for setup

## Quick Start

Choose the demo that fits your needs:
- **Want to run the model and RAG pipeline locally or on on-prem GPUs?** Start with `local-demo/`
- **Need better performances?** Use `on-cloud-demo/`

Each folder contains detailed instructions in its respective README and notebook.

## Contact

For questions or issues, contact the SatcomLLM team at [ESA SCEVA](https://github.com/esa-sceva).

