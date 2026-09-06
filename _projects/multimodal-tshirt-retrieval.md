---
layout: page
title: Multimodal T-Shirt Retrieval System
description: Zero-Shot Multimodal IR Engine Combining CLIP Zero-Shot Visual Search, BLIP Image Captioning, and ChromaDB Dense Retrieval with Cross-Encoder Reranking.
importance: 6
category: ai-ml
github: https://github.com/MK2091379/multimodal-tshirt-retrieval
---

## Overview

Text-to-image e-commerce search requires handling both low-level visual patterns (e.g., cut, color palette, graphic prints) and nuanced high-level semantic descriptions (e.g., vintage aesthetic, typography nuances). Relying solely on raw visual matching often misses explicit semantic queries, while standard text-keyword indexing fails on unstructured product images lacking manual metadata.

This project implements an end-to-end **Multimodal Information Retrieval (IR) System** tailored for apparel search across 1,993 product images. The framework deploys pre-trained Vision-Language Models (VLMs) and dense vector search in a zero-fine-tuning setup, benchmarking direct zero-shot visual latent space alignment against automated generative image captioning paired with bi-encoder retrieval and cross-encoder neural reranking.

---

## Retrieval Architecture & Pipeline

* **Task 1 — Zero-Shot Visual Search (CLIP):** Projects arbitrary natural language text queries and catalog images into a shared multimodal metric space using `openai/clip-vit-base-patch32`. Candidate retrieval is executed via cosine similarity between normalized text and image embedding vectors.
* **Task 2 — Automated Visual Captioning (BLIP):** Synthesizes rich descriptive textual annotations for each catalog image using `Salesforce/blip-image-captioning-base`, automatically transcribing garment colorways, collar structures, graphic motifs, and typography.
* **Task 3 — Dense Semantic Retrieval & Reranking:**
  * *Dense Vector Indexing:* Encodes BLIP-generated descriptions via `BAAI/bge-small-en-v1.5` and indexes them into a high-performance **ChromaDB** vector database.
  * *First-Stage Bi-Encoder Retrieval:* Performs fast nearest-neighbor vector search over dense index representations to yield high-recall candidates.
  * *Second-Stage Cross-Encoder Reranking:* Reranks the top candidates via `BAAI/bge-reranker-base`, performing full cross-attention across query-caption pairs to capture fine-grained linguistic and visual semantics.

---

## Architectural Highlights & Engineering Decisions

### 1. Model Selection & Rationale
* **Zero-Shot Alignment:** `clip-vit-base-patch32` establishes baseline visual similarity directly from pixels without domain-specific re-training.
* **VRAM-Optimized Generative Captioning:** `blip-image-captioning-base` delivers concise apparel descriptions with a compact memory footprint, avoiding out-of-memory (OOM) exceptions on resource-constrained consumer GPUs (such as NVIDIA T4 / P100 accelerators).
* **Two-Tier Dense Retrieval:** Coupling `bge-small-en-v1.5` (top-ranked on MTEB benchmarks) for fast vector candidate extraction with `bge-reranker-base` eliminates the representational bottleneck inherent to pure dual-encoder dot products.

### 2. Accelerator Memory Management
* Incorporates deterministic GPU memory cleanup routines (`gc.collect()` paired with `torch.cuda.empty_cache()`) across sequential evaluation stages.
* Accommodates mixed execution pipelines across Hugging Face Transformers, Sentence-Transformers, and ChromaDB vector stores within unified Jupyter execution environments.

---

## Dataset & Comparative Telemetry

* **Evaluation Corpus:** 1,993 commercial T-shirt product images sourced from the Kaggle Applied Data Mining benchmark.
* **Comparative Diagnostics:** Generates side-by-side Top-$N$ visual comparative matrices contrasting direct CLIP visual projections with the captioning-plus-reranking retrieval pipeline, isolating semantic divergence between direct visual similarity and caption-derived relevance.

---

## Technical Stack

* **Language & Runtime:** Python 3.12, PyTorch, CUDA
* **Vision-Language Models:** Hugging Face Transformers (`CLIP`, `BLIP`)
* **Vector Storage & Semantic Indexing:** ChromaDB, Sentence-Transformers
* **Dense Embedding & Reranking:** BAAI BGE (`bge-small-en-v1.5`, `bge-reranker-base`)
* **Image Processing & Data Handling:** Pillow, NumPy, Pandas
* **Domain Focus:** Multimodal Information Retrieval, Vision-Language Modeling, Dense Vector Search