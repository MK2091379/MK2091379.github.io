---
layout: page
title: DeepRC Immune Repertoire Classification
description: Deep Multiple Instance Learning (MIL) Architecture for High-Throughput TCR/BCR Sequencing and Immunodiagnostic Prediction.
importance: 3
category: ai-ml
github: https://github.com/MK2091379/deep-rc
---

## Overview

Modern immunosequencing technologies produce massive repertoires consisting of millions of distinct T-cell receptor (TCR) and B-cell receptor (BCR) sequences per individual. Associating these variable-sized collections of immune receptors with clinical phenotypes (e.g., infectious disease status or autoimmune conditions) presents a complex **Multiple Instance Learning (MIL)** challenge: disease-associated antigen-binding motifs are often sparse, subtle, and buried within huge background repertoires of non-reactive sequences.

**DeepRC (Deep Repertoire Classification)** implements a deep Multiple Instance Learning neural framework designed to classify large-scale immune repertoire datasets. The framework treats each immune repertoire as an unordered, variable-sized bag of CDR3 amino acid sequences, employing sequence encoders paired with attention-based pooling mechanisms to extract sub-sequence motifs and aggregate sequence-level representations into robust patient-level diagnostic predictions (such as Cytomegalovirus [CMV] status).

---

## Architectural Pipeline

* **Sequence Representation & Tokenization:** Parsing variable-length CDR3 amino acid chains and mapping them into continuous embedding spaces.
* **Sequence Feature Extraction:** Parallelized 1D Convolutional Neural Networks (CNN) or Long Short-Term Memory (LSTM) recurrent networks capturing local biochemical motifs and amino acid contextual dependencies.
* **Attention-Based Pooling:** Single-head and multi-head attention mechanisms assigning dynamic relevance scores to individual sequences within a repertoire bag, naturally identifying disease-associated sequence signatures.
* **Phenotype Classification Head:** Fully connected layers aggregating attention-weighted repertoire vectors to produce single-task or multi-task clinical predictions.

---

## Core System Architecture

### 1. Model Implementations (`architectures.py`)
* **1D CNN Sequence Encoders:** Parameter-efficient convolution kernels tailored for identifying localized sub-sequence motifs independently of sequence position.
* **LSTM Encoders:** Recurrent sequence processing models capturing non-local contextual dependencies across long CDR3 loops.
* **Attention Modules:** Trainable attention pooling mechanisms that compute normalized attention weights across bags containing up to hundreds of thousands of sequences.

### 2. Training Engine & Task Routing (`training.py` & `task_definitions.py`)
* Flexible optimization loops supporting binary cross-entropy (BCE) and multi-task loss landscapes with learning rate scheduling and early stopping.
* Mini-batch repertoire sampling designed to manage high-throughput sequencing bags efficiently without memory exhaustion.

### 3. High-Throughput Ingestion & Caching (`dataset_readers.py` & `dataset_converters.py`)
* Optimized I/O pipelines parsing tabular TSV/CSV repertoire profiles and clinical metadata.
* Preprocessing utilities utilizing **HDF5 (`h5py`)** and memory-mapped binary representations to enable high-throughput batching on high-performance accelerators.

### 4. Benchmark Reproduction Suites (`examples/`)
* **Real-World Cohort Benchmarking (`cmv.py`):** High-throughput immunosequencing prediction evaluating binary CMV infection status.
* **Synthetic & Controlled Motif Insertion (`cmv_with_implanted_signals.py` & `simulated.py`):** Controlled signal-to-noise evaluations assessing model sensitivity across varying motif frequencies and synthetic noise baselines.
* **Generative Repertoires (`lstm_generated.py`):** Model evaluation over synthetic repertoires produced via generative sequence language models.

---

## Technical Stack

* **Deep Learning Framework:** PyTorch, Torchvision
* **Data Serialization & High-Throughput I/O:** HDF5 (`h5py`), Pandas, NumPy
* **Scientific Computing & Signal Analysis:** SciPy, Scikit-Learn
* **Evaluation Metrics:** ROC-AUC, Balanced Accuracy, Precision-Recall AUC
* **Domain Focus:** Computational Immunology, Multiple Instance Learning (MIL), Bio-NLP