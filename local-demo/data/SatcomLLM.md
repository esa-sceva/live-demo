# SatcomLLM

SatcomLLM is an ongoing ESA ARTES 4.0 Future Preparation activity (activity code 1A.128, status date 24 October 2025). It assesses how open-source large language models can be adapted to the satellite communications sector. The public project page is [SatcomLLM on the ESA CSC archive](https://resilience.esa.int/archives/projects/satcomllm).

The project builds the SatCom Expert Virtual Assistant (SCEVA). SCEVA is a demonstrator that combines instruction fine-tuning with retrieval-augmented generation (RAG) so answers can be grounded in documents for technical and operational satcom tasks.

## Objectives

SatcomLLM identifies satcom applications where an LLM can help, including engineering support, mission documentation, and anomaly analysis, and prioritises those use cases with ESA and industry experts. It builds a curated domain corpus and evaluation benchmarks, then develops and assesses SCEVA and its RAG-enabled variants. Models, datasets, and software are released under open licenses where possible, in support of European digital sovereignty and the ARTES programme.

## Benefits

General-purpose assistants such as ChatGPT or Gemini are not adapted to satcom workflows and raise confidentiality, licensing, and reliability concerns. SCEVA is fine-tuned on curated satcom data and can cite a document store, which supports tasks such as link-budget evaluation, engineering analysis, mission documentation, and regulatory checks. It can run in a controlled environment on the cloud, on local servers, or on an edge platform.

## Features

SCEVA is built on an open-source LLM adapted to satellite communications. The project describes SatcomLLM as an approximately 70B-parameter model fine-tuned on a curated satcom dataset of about 160,000 documents. Users reach it through an API and a web interface for question answering, technical summarisation, and knowledge exploration. Expert users can fine-tune further on proprietary data.

SCEVA-RAG links answers to a document store that users can fill with their own material. SCEVA-RAG-ARTES is a variant pre-populated with ARTES 4.0 documentation.

## System architecture

The system uses two instruction fine-tuning tracks of Llama models, 8B and 70B. Training has two steps: first, hundreds of thousands of satcom question-answer pairs that teach terminology and workflows; second, a smaller reviewed set focused on reasoning and multi-step problem solving. A data pipeline ingests, cleans, deduplicates, labels, and formats examples. RAG is available at inference time so answers can cite trusted documents. Evaluation uses automatic metrics and expert review on tasks such as link budgets, protocol choices, and mission planning.

## Plan and current status

The plan starts with use-case identification with ESA, RINA, and other stakeholders, then benchmarks open-source LLMs on satcom tasks, fine-tunes SatcomLLM, and integrates it into SCEVA with RAG variants. Milestones are MS1 (use cases and benchmarks), MS2 (model adaptation and prototype), and a final review that demonstrates SCEVA and SCEVA-RAG.

The activity is in an iterative training phase: models are retrained with different hyperparameters, with improved data curation and evaluation on each pass. A vector database of over 100,000 satellite-communication documents supports retrieval. The frontend and backend are being finalised for internal testing by the ESA technical officer.

## Companies

Pi School (Italy) and RINA Consulting (Italy) carry out the activity for the European Space Agency.
