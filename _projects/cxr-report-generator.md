---
layout: page
title: CXR Medical Report Generator
description: Automated Multimodal Vision-Language Pipeline for Clinical Report Generation from Chest X-Rays.
importance: 1
category: ai-ml
related_publications: false
github: https://github.com/MK2091379/cxr-report-generator
---

## Overview

Automated radiology report generation represents a critical frontier in **Medical AI**, bridging high-resolution computer vision and clinical Natural Language Processing (NLP). Radiologists spend considerable time writing narrative descriptions for standard radiographs; automating the extraction of radiographic findings and diagnostic impressions can accelerate emergency triage and reduce diagnostic fatigue.

This project delivers an end-to-end multimodal sequence-to-sequence deep learning framework (**CXR-Report-Generator**) designed to ingest raw chest X-ray (CXR) scans and automatically synthesize clinically coherent, structured radiology reports (*Findings* and *Impressions*).

---

## Architectural Design

The pipeline builds upon a custom formulation of the `VisionEncoderDecoderModel` architecture, utilizing dense cross-attention mechanisms to map spatial radiographic feature representations into a high-dimensional language space.

### System Pipeline
* **Input Processing:** Ingestion of raw Chest X-Ray (CXR) scans standardized to a resolution of 224x224 pixels.
* **Encoder Stage (ViT):** Application of patch projection and self-attention via a Vision Transformer to extract contextual visual hidden states (visual embeddings).
* **Multimodal Alignment:** Utilization of cross-attention mechanisms to align the extracted visual embeddings directly with the language generation space.
* **Decoder Stage (GPT-2):** Auto-regressive generation of the synthesized narrative report (Findings & Impressions) using a causal language model.

### 1. Visual Feature Encoding (Vision Transformer)
* **Backbone:** `google/vit-base-patch16-224-in21k`
* Standard radiographs are preprocessed, normalized, and resized to 224x224 pixels.
* The image is tokenized into non-overlapping 16x16 patches. A trainable linear projection maps each flattened patch into 768-dimensional visual tokens with 1D learnable position embeddings.
* Stacked multi-head self-attention blocks capture long-range contextual spatial relationships across bilateral lung fields, cardiac silhouettes, and pleural spaces without the local receptive field limitations of traditional CNNs.

### 2. Auto-regressive Language Decoding (GPT-2)
* **Backbone:** Generative Pre-trained Transformer 2 (`gpt2`)
* The decoder functions as a causal language model conditioned directly on the encoder's visual hidden states.
* Cross-attention layers were explicitly constructed and fine-tuned to map spatial visual tokens to the target medical vocabulary distribution, guiding sequential token-by-token clinical narrative generation.

---

## Technical Highlights & Engineering Considerations

* **Robust Model Binding:** To bypass known configuration routing bugs and `is_decoder` attribute mismatches inside standard Hugging Face wrappers (such as `from_encoder_decoder_pretrained`), the ViT encoder and GPT-2 decoder were instantiated independently, custom-configured, and explicitly bound via `VisionEncoderDecoderModel`.
* **Hardware-Aware Training:** Optimized for distributed and cloud accelerators via `Seq2SeqTrainer`. Incorporates mixed-precision policies (FP16) with fallbacks for architectures lacking specialized Tensor Cores to prevent CUDA accelerator initialization failures (`cudaErrorNoKernelImageForDevice`).

---

## Dataset & Preprocessing

The model was trained and validated on the benchmark **Indiana University Chest X-ray (Open-I)** dataset:
* **Payload:** 7,470 clinical radiographs paired with 3,851 structured diagnostic patient reports.
* **Pipeline Integration:**
  * Cleaned, filtered, and aggregated disparate views (Frontal/PA and Lateral projections).
  * Merged target fields (`findings` and `impressions`) into coherent diagnostic summaries.
  * Applied on-the-fly image transformations and dynamic tokenization padding/truncation for efficient batch collation.

---

## Evaluation Metrics

Model performance is automatically evaluated at every epoch using standard Natural Language Generation (NLG) criteria:
* **BLEU (Bilingual Evaluation Understudy):** Quantifies exact n-gram precision against ground-truth radiologist reports.
* **ROUGE-L:** Computes the Longest Common Subsequence (LCS) to assess sentence-level fluency, structural recall, and grammatical preservation.

---

## Technology Stack

* **Frameworks:** PyTorch, Hugging Face (`transformers`, `evaluate`)
* **Computer Vision:** OpenCV, PIL, Torchvision
* **Evaluation & NLP:** SacreBLEU, ROUGE-Score
* **Data Engineering:** NumPy, Pandas, Scikit-Learn