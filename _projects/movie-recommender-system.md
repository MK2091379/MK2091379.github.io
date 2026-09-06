---
layout: page
title: Intelligent Multi-Tool Movie Recommender System
description: Multi-Modal Recommendation Engine Integrating Collaborative/Content Filtering, Neural Collaborative Filtering (NCF), and LLM Routing Agents.
importance: 5
category: ai-ml
github: https://github.com/MK2091379/movie-recommender-system
---

## Overview

Modern recommendation engines must balance structured statistical personalization with unstructured conversational intent. Classical collaborative or content-based models often struggle with open-domain factual retrieval, while pure Large Language Models (LLMs) hallucinate metadata and cannot efficiently compute collaborative embeddings across millions of user-item interactions.

This project delivers an end-to-end **Intelligent Multi-Tool Movie Recommender System** that integrates classic machine learning, deep neural embeddings, and an LLM orchestration agent. The framework couples two-stage hybrid retrieval (TF-IDF content filtering and SVD matrix factorization), Neural Collaborative Filtering (NCF), and an autonomous routing agent that dispatches user queries to either an analytical SQL database or an algorithmic recommendation engine.

---

## Architectural Decomposition & System Pipeline

* **Autonomous LLM Router Agent:** Evaluates natural language queries via the Groq API (`openai/gpt-oss-120b`). Factual inquiries trigger automated Text-to-SQL generation executed directly against a normalized SQLite relational database (`movies.db`), while personalization requests are routed to the machine learning inference engine.
* **Two-Stage Hybrid Recommendation Pipeline:**
  * *Stage 1 (Candidate Generation):* High-recall retrieval using Content-Based Filtering with TF-IDF vectorization and Cosine Similarity over plot synopses, cast/crew credits, and keyword metadata.
  * *Stage 2 (Candidate Ranking):* High-precision ranking using Singular Value Decomposition (SVD) and Non-Negative Matrix Factorization (NMF) collaborative filtering models to score candidate items based on historical user interaction matrices.
* **Deep Neural Collaborative Filtering (NCF):** A deep learning framework built in TensorFlow/Keras that maps user and item IDs into dense continuous embedding spaces, capturing non-linear latent interactions through stacked multi-layer feedforward layers optimized via Adam.
* **Automated Data Pipeline (ETL):** Normalizes, parses, and cleans multi-table inputs (spanning millions of ratings, movie metadata, and keyword graphs) into an indexed relational schema.
* **Dual User Interfaces:**
  * *Conversational Interface (Streamlit):* Real-time chat application maintaining multi-turn conversational context, LLM thought streaming, and graceful degradation fallback.
  * *Analytical Dashboard (Dash & Bootstrap):* Web-based exploratory UI displaying popularity metrics, personalized candidate rankings, and model evaluation diagnostics.

---

## Core System Modules

### 1. Hybrid ML Recommendation Engine
* Extracts textual representations across plot summaries and tags using $n$-gram TF-IDF matrices.
* Employs matrix factorization algorithms (`scikit-surprise`) to estimate missing entries in user-item rating tensors, resolving cold-start heuristics through hybrid weighting.

### 2. Deep Learning Neural Embeddings (NCF)
* Projects sparse one-hot user and movie identifiers into dense low-dimensional latent vectors.
* Concatenates latent representations and feeds them into fully connected neural layers with non-linear activation functions to discover complex behavioral patterns beyond linear inner products.

### 3. Agentic Routing & SQL Tooling
* Implements prompt-engineered tool routing to parse natural language user questions into syntactically valid SQLite queries.
* Executes schema-aware queries against `movies.db` for deterministic factual questions (e.g., release years, box office earnings, director filmographies).

---

## Technical Stack

* **Languages & Core:** Python 3.8+, Pandas, NumPy, Scikit-Learn
* **Recommendation Algorithms:** Scikit-Surprise (SVD, NMF), TF-IDF Vectorization, Cosine Metric
* **Deep Learning Runtime:** TensorFlow, Keras (Neural Collaborative Filtering)
* **LLM Orchestration & APIs:** Groq API (`openai/gpt-oss-120b`), NLTK, Python-Levenshtein
* **Storage & Relational Schema:** SQLite, Dynamic ETL Pipelines
* **UI & Telemetry:** Streamlit, Dash, Dash Bootstrap Components