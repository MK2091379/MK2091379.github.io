---
layout: page
permalink: /cv/
title: CV
nav: true
nav_order: 5
description: Curriculum Vitae of Seyyed Moein Kazemi.
toc:
  sidebar: left
---

<div class="text-center my-4">
  <a href="{{ '/assets/pdf/MoeinCV.pdf' | relative_url }}" class="btn btn-primary" target="_blank" rel="noopener noreferrer">
    <i class="fa-solid fa-file-pdf"></i> Download CV (PDF)
  </a>
</div>

## Research Interests
Deep Learning &middot; Deep Reinforcement Learning &middot; Medical AI &middot; Efficient Deep Learning &middot; Time Series Forecasting

---

## Education

**Shahid Beheshti University** | Tehran, Iran  
*Master's Degree, Data Science* | *Sep 2024 – Sep 2026*  
* **Thesis:** Designing a Dynamic Forecasting and Risk Management Framework in Stock Trading: A Probabilistic Deep Learning Approach *(Supervisor: [Dr. Ehsan Bahrami Samani](https://scholar.google.com/citations?user=P4blMhIAAAAJ&hl=en))*

**Iran University of Science and Technology** | Tehran, Iran  
*Bachelor's Degree, Computer Engineering* | *Sep 2019 – Nov 2023*  
* **Thesis:** Storing Big Data on DNA: Design and Implementation of a Secure Pipeline Using Cryptographic Protocols *(Supervisor: [Dr. Marzieh Malekimajd](https://scholar.google.com/citations?user=UxkvKfsAAAAJ&hl=en))*

---

## Publications & Preprints

1. **Kazemi, S. M.**, Azarpour, A., Riahi Madvar, M. CRNN-KAN: A Lightweight Hybrid Framework for Robust Phonocardiogram Classification. *Informatics in Medicine Unlocked*. Status: Under Review.
2. **Kazemi, S. M.**, Heydari, P. RL-WavKAN: An Ultra-Lightweight Reinforcement-Learned Wavelet Kolmogorov–Arnold Network for Phonocardiogram Classification. Status: Manuscript in Preparation.
3. Azarpour, A, **Kazemi, S. M.** SW-KAN: Kolmogorov–Arnold Networks with Stieltjes–Wigert q-Orthogonal Polynomials. *Neurocomputing*. Status: Under Review.
4. Riahi Madvar, M., **Kazemi, S. M.**, Yousefi, S. Scalable unsupervised outlier detection in high-dimensional big data via collision-based subspace selection and deep reinforcement learning. *Applied Soft Computing*. Status: Under Review.
5. **Kazemi, S. M.**, Bahrami Samani, E. Probabilistic Joint Forecasting of Bivariate Time Series with LSTM via Dynamic Student-$t$ Likelihood. *Annals of Data Science*. Status: Under Review. 
6. **Kazemi, S. M.**, Ghanbary, S., Riahi-Madvar, M. Discovering Actionable Marketing Insights: Rare Association Rule Mining for Customer Behavior Analysis. *2025 10th International Congress on Fuzzy and Intelligent Systems (CFIS)*. DOI: 10.1109/CFIS68949.2025.11652160.

---

## Research Experience

### Research Assistant
**Shahid Beheshti University, Tehran, Iran** | *Supervisor: Dr. Mahboobeh Riahi-Madvar* | *Apr 2025 – Sep 2026*

* **Lightweight Hybrid Deep Learning for Medical Time Series (CRNN-KAN)** *(Jan 2026 – Sep 2026)*
  * Proposed a novel, parameter-efficient CRNN-KAN architecture for robust phonocardiogram (PCG) classification.
  * Integrated a CNN-BiLSTM backbone for spatiotemporal feature extraction with an EfficientKAN classification head, utilizing SiLU and sinusoidal basis functions.
  * Achieved competitive AUC scores across three clinical datasets (PhysioNet, CirCor, PASCAL) while reducing trainable parameters to 1.31M (a 100x reduction vs. VGG16).
  * Validated the physiological interpretability of the learned acoustic representations using Score-CAM visualizations.

* **Scalable Outlier Detection in Big Data (mCRMR-GPPO)** *(Apr 2025 – Dec 2025)*
  * Developed a distributed, unsupervised anomaly detection framework for high-dimensional big data, deployed on Apache Spark using the MapReduce programming model.
  * Formulated a novel subspace selection criterion (mCRMR) leveraging Locality-Sensitive Hashing (LSH) and collision-based redundancy to isolate informative features.
  * Designed a hierarchical Gated Proximal Policy Optimization (GPPO) architecture, filtering normal instances efficiently and dedicating deep neural network processing strictly to complex anomaly patterns.
  * Demonstrated near-linear computational scalability across cluster nodes and achieved near-perfect AUC ($\approx$99%) on synthetic and real-world high-dimensional datasets.

* **Rare Association Rule Mining for Bank Marketing** *(Jul 2025 – Sep 2025)*
  * Designed an interpretable data mining pipeline to replace black-box marketing models, extracting actionable "flip rules" to explain customer behavior shifts.
  * Implemented an adaptive dynamic minimum-support mechanism and MinHash LSH to mitigate the rule explosion problem and efficiently discover rare, high-impact patterns.
  * Identified precise decision boundaries that successfully improved targeted marketing campaign conversion rates from 11.7% to 64.7% (a 5.53x lift).

### Research Assistant
**Shahid Beheshti University, Tehran, Iran** | *Supervisor: Dr. Ehsan Bahrami Samani* | *Oct 2025 – Dec 2025*

* **Probabilistic Joint Forecasting of Bivariate Time Series**
  * Engineered a Bivariate Probabilistic LSTM framework to jointly forecast returns, volatility, and dynamic cross-asset correlations for commodity markets (Gold and Brent Crude Oil).
  * Parameterized a dynamic Student-$t$ likelihood optimized via Negative Log-Likelihood (NLL) to explicitly model heavy-tailed distributions and extreme financial shocks.
  * Produced well-calibrated 95% predictive intervals and outperformed SOTA baselines (Transformer, TCN, N-BEATS) in accuracy and tail risk quantification.

### Independent Researcher
**Collaborative Research, Tehran, Iran** | *Jan 2026 – Present*

* **1D Reinforcement-Learned Wavelet KAN (RL-WavKAN)** *(Jan 2026 – Present)*
  * Developed an ultra-lightweight 1D Wavelet Kolmogorov-Arnold Network for direct raw audio classification, bypassing computationally heavy 2D spectrogram transformations.
  * Formulated a custom Proximal Policy Optimization (PPO) agent to dynamically optimize the scale and translation of continuous wavelet basis functions during training.
  * Reduced the computational footprint to 145K parameters and $\sim$0.0003 GFLOPs, achieving an inference latency of 0.036 ms/sample for real-time cardiovascular screening.

* **Stieltjes-Wigert $q$-Orthogonal Polynomials in KANs (SW-KAN)** *(Jan 2026 – Sep 2026)*
  * Developed the SW-KAN architecture, replacing standard B-spline activations with Stieltjes-Wigert $q$-orthogonal polynomials to improve parameter efficiency and gradient stability.
  * Resolved the domain mismatch problem by introducing a smooth exponential-of-tanh domain mapping from $\mathbb{R}$ to the semi-infinite support $(0, \infty)$.
  * Leveraged a numerically stable three-term recurrence for $\mathcal{O}(N)$ evaluation, outperforming 18 baseline polynomial KAN variants on image classification and 2D function approximation tasks.

### Undergraduate Research Assistant
**Iran University of Science and Technology, Tehran, Iran** | *Supervisor: Dr. Marzieh Malekimajd* | *Sep 2022 – Sep 2023*

* **Secure Big Data Storage on DNA**
  * Investigated DNA as an ultra-high-density, long-term storage medium for Big Data, addressing capacity and longevity limitations in conventional storage architectures.
  * Developed a complete data-to-DNA simulation pipeline in Python, successfully integrating file-to-binary conversion, Huffman coding for lossless data compression, and DNA sequence mapping.
  * Enhanced the standard DNACloud software framework by introducing a robust cryptographic security layer to protect synthesized genetic data.
  * Implemented and benchmarked AES and OTP encryption algorithms, evaluating computational efficiency and execution time across variable data payload sizes (up to 10 million characters).

---

## Teaching & Academic Experience

* **Teaching Assistant:** Machine Learning, Multivariate Analysis *(Instructor: [Dr. Sakineh Dehghan](https://scholar.google.com/citations?user=qLfJiRAAAAAJ&hl=en))*
* **Teaching Assistant:** Machine Learning, Advanced Machine Learning, Pattern Recognition *(Instructor: [Dr. Ahmad Ali Abin](https://scholar.google.com/citations?user=BrxRchIAAAAJ&hl=en))*
* **Head TA & TA:** Advanced Data Mining (Head TA), Machine Learning *(Instructor: [Dr. Mahboobeh Riahi-Madvar](https://scholar.google.com/citations?user=t0Ct8QoAAAAJ&hl=en))*
* **Teaching Assistant:** Big Data *(Instructor: [Dr. Hamed Malek](https://scholar.google.com/citations?user=_IIio8oAAAAJ&hl=en))*
* **Teaching Assistant:** Deep Learning *(Instructor: [Dr. Zeinab Hajimohammadi](https://scholar.google.com/citations?user=6Is4zNIAAAAJ&hl=en))*

---

## Selected Technical Projects

* **Multimodal Vision-Language Medical Report Generator (CXR-Report-Generator):** Developed an end-to-end encoder-decoder pipeline combining Vision Transformer (ViT) and GPT-2 to automatically generate clinical reports from Chest X-ray images via cross-attention mechanisms. *Tools: PyTorch, Hugging Face Transformers, Python, OpenCV.* [[GitHub](https://github.com/MK2091379/cxr-report-generator)]

* **FracAtlas Bone Fracture CAD Pipeline:** Built a multi-task computer-aided diagnosis system utilizing DenseNet-121 for global classification and ResNet34-UNet for precise semantic segmentation, integrated with Meta's SAM for zero-shot boundary delineation. *Tools: PyTorch, Segmentation Models, OpenCV, Python, Segment Anything (SAM).* [[GitHub](https://github.com/MK2091379/fracatlas-bone-fracture-detection)]

* **DeepRC: Immune Repertoire Classification:** Implemented a deep Multiple Instance Learning (MIL) framework using 1D CNN and LSTM sequence encoders paired with attention pooling to predict disease status from high-throughput immunosequencing data. *Tools: PyTorch, SciPy, Scikit-Learn, H5py, Python.* [[GitHub](https://github.com/MK2091379/deep-rc)]

* **Multimodal Semantic Image Search & Recommender:** Architected an end-to-end visual search engine leveraging OpenAI CLIP for deep semantic feature extraction and Qdrant vector database for high-performance K-NN retrieval, backed by FastAPI and React. *Tools: FastAPI, React.js, Qdrant, CLIP, PyTorch, Python.* [[GitHub](https://github.com/MK2091379/semantic-image-search)]

* **xv6 OS Kernel Enhancements:** Modified MIT's xv6 operating system kernel by implementing custom system calls, dynamic process accounting, and advanced Multi-Level Queue (MLQ) CPU scheduling architectures. *Tools: C, x86 Assembly, QEMU, Linux.* [[GitHub](https://github.com/MK2091379/xv6-project)]

* **Knowledge Engineering & Semantic Reasoning Suite:** Developed macroeconomic ontologies in Neo4j/OWL and rigorously benchmarked GPT-4.1 multi-hop reasoning capabilities over structured biomedical and scientific knowledge graphs. *Tools: Neo4j, Cypher, RDFLib, NetworkX, GPT-4.1, Python.* [[GitHub](https://github.com/MK2091379/ontology-knowledge-engineering)]

* **OpenUnderstand Static Code Analyzer:** Engineered an open-source, Python-based static code analysis framework utilizing ANTLR4 AST parsing for Java to extract complex software metrics and reverse-engineer architectural dependencies. *Tools: Python, ANTLR4, Abstract Syntax Trees (AST).* [[GitHub](https://github.com/MK2091379/iust-compiler-design)]

* **Intelligent Multi-Tool Movie Recommender:** Built a hybrid recommendation engine integrating TF-IDF content filtering, Deep Neural Collaborative Filtering (NCF), and an autonomous LLM routing agent for natural language text-to-SQL factual retrieval. *Tools: TensorFlow, Keras, Scikit-Surprise, Groq API, SQLite, Streamlit.* [[GitHub](https://github.com/MK2091379/movie-recommender-system)]

---

## Technical Skills

* **Programming Languages:** Python, C/C++, SQL, R, MATLAB, Bash.
* **AI & Deep Learning Libraries:** PyTorch (Geometric, Torchaudio, Torchvision), TensorFlow, Hugging Face, XGBoost, Scikit-Learn, OpenCV, CUDA.
* **Architectures & Paradigms:** Sequence Models (KAN, LSTM, TCN), Foundation Models (ViT, CLIP, SAM), Deep RL (PPO, DQN, Contextual Bandits), Probabilistic Modeling, LLM Agents & RAG.
* **Data Engineering & MLOps:** PySpark, Vector DBs (Qdrant, ChromaDB), Relational DBs (PostgreSQL), Docker, FastAPI, Linux.
* **Developer Tools:** Git, LaTeX, GNU Make.

---

## Selected Coursework

* **Machine Learning & AI:** Machine Learning (19.75/20), Deep Learning (19.5/20), Advanced Data Mining (19.25/20), Multi-Agent Systems [Focus: RL & LLMs] (19/20), Artificial Neural Networks (18.5/20)
* **Mathematics & Foundations:** Differential Equations (19/20), Multivariate Statistical Analysis (18.5/20), Engineering Probability & Statistics (17/20)
* **Data Systems & Analytics:** Big Data Analytics (17.25/20)

---

## Honors & Awards

* **Top 1.5% Nationwide:** Ranked in the top 1.5% among ~15,000 participants in the Iranian Nationwide M.Sc. Entrance Exam

* **Top 0.6% Nationwide:** Ranked in the top 0.6% among >160,000 participants in the Iranian Nationwide B.Sc. Entrance Exam