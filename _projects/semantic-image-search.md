---
layout: page
title: Semantic Image Search & Recommender Engine
description: End-to-End Visual Product Retrieval Engine Pairing OpenAI CLIP Representation Learning with Qdrant Vector DB, FastAPI, and React.
importance: 4
category: ai-ml
github: https://github.com/MK2091379/semantic-image-search
---

## Overview

Traditional e-commerce search platforms often rely on keyword matching and hand-curated catalog metadata, failing to interpret complex visual attributes such as textures, geometric silhouettes, and subtle design cues. Consequently, users searching for specialized merchandise lack intuitive ways to discover products without exact lexical descriptions.

This project delivers an end-to-end **Semantic Visual Search and Recommendation Engine** designed to retrieve and recommend commercial products directly from user-uploaded imagery. By leveraging representation learning via OpenAI's **CLIP** model and indexing high-dimensional representations into the **Qdrant** vector database, the platform executes sub-second approximate nearest neighbor (ANN) searches over 12,000 product images, serving real-time recommendations through a decoupled FastAPI backend and React frontend.

---

## System Architecture & Pipeline

* **Data Engineering & Preprocessing:** Ingestion and normalization pipelines built with OpenCV and Pillow (PIL) that standardize resolution scales, adjust aspect ratios, and format raw inputs for neural embedding extraction.
* **Representation Learning (OpenAI CLIP):** Employs the visual transformer backbone of CLIP to map unstructured pixel arrays into a dense 512-dimensional semantic latent space, capturing fine-grained structural and contextual product characteristics.
* **Vector Indexing & Similarity Search (Qdrant):** Stores high-dimensional vector embeddings paired with JSON-serialized product payloads. Query vectors execute K-Nearest Neighbors (KNN) searches using cosine distance metrics to deliver millisecond-latency nearest-neighbor retrieval.
* **High-Throughput API Gateway (FastAPI):** Asynchronous RESTful service orchestrating indexing tasks, request payload sanitization, vector search dispatches, and real-time system health checks.
* **Interactive Frontend (React 18):** Modern web dashboard supporting direct drag-and-drop file uploads, browser camera capture, dynamic similarity ranking views, and interactive product inspection.

---

## Operational Workflows

### 1. Offline & Batch Indexing Pipeline
* Product images and associated metadata (titles, descriptions, merchant links, categories) are ingested from the dataset.
* Images undergo normalization transforms before passing through the CLIP image encoder.
* The extracted 512-dimensional floating-point vectors are written to Qdrant alongside relational metadata payloads.

### 2. Real-Time Search & Retrieval Pipeline
* The user supplies an arbitrary query image via file upload or integrated camera feed.
* The API layer transforms the image buffer and computes its query embedding using CLIP.
* Qdrant performs a KNN vector search against the pre-indexed collection, ranking candidates by cosine proximity.
* The API formats and returns ordered product cards with associated metadata payloads to the React interface.

---

## Dataset & Practical Validation

* **Corpus Scale:** Evaluated over an indexed corpus of approximately 12,000 commercial product images and associated metadata extracted from the *Pindo* e-commerce marketplace.
* **Semantic Vector Clustering:** The latent space naturally clusters conceptually and morphologically related products without requiring explicit category supervision or manual label tagging.
* **Retrieval Quality:** Empirical queries across varied product classes (such as modern chandeliers, mechanical watches, and gaming peripherals) return structurally and contextually cohesive recommendations with consistent sub-second latency.

---

## Technical Stack

* **Representation Learning:** OpenAI CLIP (Contrastive Language-Image Pre-Training)
* **Vector Database:** Qdrant (HNSW / Cosine Similarity Indexing)
* **Backend Services:** Python 3.9+, FastAPI, Uvicorn
* **Frontend Application:** React 18, HTML5 Canvas / WebRTC Camera Integration
* **Image Processing:** OpenCV, Pillow (PIL), NumPy
* **Domain Focus:** Visual Information Retrieval, Metric Learning, Vector Search Architectures