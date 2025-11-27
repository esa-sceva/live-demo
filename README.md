# SatcomLLM RAG Demo

An interactive Jupyter notebook demonstrating how to build a ready-to-use Retrieval-Augmented Generation (RAG) system for satellite communications domain knowledge, on top of a [llama3-satcom model](https://huggingface.co/esa-sceva).

## Overview

This notebook teaches you to build a complete RAG pipeline that combines semantic search with large language models. The system retrieves relevant context from a vector database and generates grounded, source-attributed responses using a cloud-hosted LLM.

## Prerequisites

- Python 3.8 or higher
- API keys for:
  - **DeepInfra** (embeddings) - [Sign up](https://deepinfra.com)
  - **RunPod** (LLM inference) - [Sign up](https://runpod.io)
  - **Qdrant Cloud** (vector database) - [Sign up](https://qdrant.tech)

## Setup

1. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

2. **Configure API keys:**
   ```bash
   cp env.example .env
   # Edit .env and add your API keys
   ```

3. **Prepare documents:**
   - Create a `data` folder in the notebook directory
   - Add your markdown (.md) files to the `data` folder

## Notebook Structure

The demo is organized into 4 main parts:

- **Setup and LLM Fundamentals**: install dependencies, configure API keys, and understand core concepts like tokenization and prompting. You'll test the connection to the RunPod vLLM endpoint to ensure everything works before building the RAG system.

- **Theory around RAG**: understand the principles of Retrieval-Augmented Generation (RAG), including how retrieval complements generative models by providing up-to-date and domain-specific context.

- **Embedding Vector Database Creation**: load and chunk markdown documents, generate embeddings using DeepInfra, create a Qdrant vector database collection, and populate it with embedded document chunks. This builds the knowledge base that powers semantic search.

- **Retrieval and RAG Pipeline**: implement semantic search to find relevant documents, build the complete RAG pipeline that combines retrieval with generation, and test the system with real questions. You'll see how retrieved context improves answer quality and enables source attribution.
## Technology Stack

| Component | Technology | Purpose |
|-----------|------------|---------|
| Embeddings | DeepInfra (Qwen3-4B) | Text → 2560-dim vectors |
| Vector DB | Qdrant Cloud | Semantic similarity search |
| LLM | RunPod vLLM | Fast inference with SatcomLLM |
| Chunking | LangChain | Header-based splitting |




## Time Required

Approximately 10 minutes to complete the full demo.


## Contact

For questions or issues, please contact the SatcomLLM team at [ESA SCEVA](https://github.com/esa-sceva).

