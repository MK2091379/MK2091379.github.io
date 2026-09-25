---
layout: page
title: Secure & Scalable DNA Data Storage Pipeline for Archival Big Data
description: B.Sc. Thesis Implementation Integrating Lossless Huffman Compression and Symmetric Cryptography (AES vs. OTP) into Oligonucleotide Mapping Pipelines.
importance: 3
category: systems
github: https://github.com/MK2091379/bsc-final-project
---

## Overview

As global data generation accelerates into the Zettabyte regime, conventional storage media (HDD, NAND Flash, and LTO Tape) face severe physical scaling limits, high energy consumption, and short hardware replacement cycles (5–7 years). **DNA Data Storage (DDS)** offers an ultra-dense archival alternative with a theoretical capacity of ~455 Exabytes per gram, centuries-long retention, and zero idle power dissipation.

While existing simulation frameworks such as **DNACloud** provide foundational mechanisms for translating digital files into nucleotide sequences, they process payloads entirely as plaintext—leaving synthesized biological archives vulnerable to unauthorized sequencing. Furthermore, theoretical DNA cryptography literature predominantly relies on One-Time Pad (OTP) schemes, which require $O(N)$ key storage and fail to scale for Big Data workloads.

This research thesis designs, implements, and benchmarks an end-to-end, format-agnostic **Secure DNA Data Storage Pipeline**. The system integrates lossless entropy reduction (**Huffman Coding**) prior to symmetric encryption (**AES-128**) and maps the resulting ciphertext bitstreams into balanced biological dinucleotide pairs (`AT, GC, CG, TA`).

---

## Technical Walkthrough & Presentation

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 8px; margin: 20px 0; box-shadow: 0 4px 14px rgba(0,0,0,0.15);">
  <iframe 
    src="https://www.youtube.com/embed/FhmGYBCaRQs?rel=0&modestbranding=1" 
    title="Project Technical Walkthrough" 
    frameborder="0" 
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" 
    allowfullscreen
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;">
  </iframe>
</div>

<div style="display: flex; gap: 10px; flex-wrap: wrap; margin-bottom: 25px;">
  <!-- <a href="/assets/pdf/presentation_slides.pdf" target="_blank" style="padding: 8px 16px; background-color: #182B49; color: #ffffff !important; text-decoration: none; border-radius: 5px; font-weight: 500; font-size: 14px;">
    Presentation Slides (PDF)
  </a>
  <a href="/assets/pdf/FinalProject_IUST.pdf" target="_blank" style="padding: 8px 16px; background-color: #007A96; color: #ffffff !important; text-decoration: none; border-radius: 5px; font-weight: 500; font-size: 14px;">
    Full Thesis Document (PDF)
  </a> -->
  <a href="https://github.com/MK2091379/bsc-final-project" target="_blank" style="padding: 8px 16px; border: 1px solid #182B49; color: #182B49 !important; text-decoration: none; border-radius: 5px; font-weight: 500; font-size: 14px;">
    Source Code (GitHub)
  </a>
</div>

---

## End-to-End Architectural Pipeline

1. **Format-Agnostic Binary Ingestion (`file_to_binary`):** Streams arbitrary digital files in 8192-byte chunks into unsigned 8-bit `NumPy` byte buffers while embedding a 2-byte big-endian metadata header to preserve original UTF-8 file extensions during recovery.
2. **Entropy Reduction (`HuffmanCodec`):** Constructs an optimal variable-length prefix tree based on byte frequency distributions. Because chemical DNA synthesis costs scale linearly with sequence length ($\text{Cost} \propto L_{\text{seq}}$), compressing data *before* encryption directly minimizes biological synthesis costs.
3. **Symmetric Cryptographic Layer (`aes_encryption`):** Encrypts the compressed bitstream using **AES-128 in Cipher Feedback (CFB) mode** with a pseudo-random 16-byte Initialization Vector (IV), converting the block cipher into a stream cipher without padding overhead.
4. **Oligonucleotide Mapping (`binary_to_dna`):** Translates encrypted 2-bit pairs into purine-pyrimidine balanced DNA base pairs (`00 -> AT`, `01 -> GC`, `10 -> CG`, `11 -> TA`), outputting synthesized sequence files (`encrypted_dna.txt`).
5. **Decryption & Lossless Reconstruction (`Receiving.py`):** Reverses the nucleotide mapping, extracts the 16-byte IV, decrypts the AES-CFB stream, traverses the serialized Huffman codec (`huff_codec.pkl`), and reconstructs the exact original file format.

---

## Core System Modules

### 1. Interactive Desktop Control Center (`GUI.py`)
* Built with `Tkinter` to provide an interactive desktop interface for end-to-end file-to-DNA encryption and DNA-to-file recovery.
* Integrates native OS file dialogs (`filedialog`) to process arbitrary file formats seamlessly.

### 2. DNA Encoder & Cryptographic Pipeline (`Sending.py`)
* Streams input files in 8192-byte chunks and prepends a 2-byte big-endian header preserving the original UTF-8 file extension.
* Compresses binary payloads via `HuffmanCodec` (`dahuffman`), serializes the prefix tree (`huff_codec.pkl`), encrypts the stream using **AES-128-CFB**, and maps bit-pairs to DNA dinucleotides (`encrypted_dna.txt`).

### 3. DNA Decoder & File Reconstruction Engine (`Receiving.py`)
* Ingests synthesized oligonucleotide sequence files (`encrypted_dna.txt`) and translates biological base pairs (`AT, GC, CG, TA`) back into binary ciphertext.
* Extracts the 16-byte Initialization Vector (IV), performs inverse AES-CFB decryption, decodes the bitstream via the serialized Huffman tree, and restores the lossless original file (`result.<ext>`).

### 4. Empirical Benchmarking Suites (`AES_vs_OTP.py` & `HuffmanCodingTest.py`)
* **Compression Complexity Profiling (`HuffmanCodingTest.py`):** Implements a custom from-scratch Huffman coding tree using min-heap priority queues (`heapq`) to measure encoding and decoding latency across scaling payload lengths.
* **Cryptographic Scalability Engine (`AES_vs_OTP.py`):** Evaluates round-trip encryption and decryption execution latency between **AES-128** (`MODE_CBC` with PKCS7 padding) and **One-Time Pad (OTP)** (`os.urandom` XOR) across variable payload scales.

---

## Empirical Benchmarking & Key Findings

* **Huffman Compression Latency Profiling (`HuffmanCodingTest.py`):** Evaluated encoding and decoding execution times across randomized payloads ranging from $10^1$ to $10^{10}$ characters, identifying tree construction and serialization (`pickle`) trade-offs for monolithic in-memory files.
* **Cryptographic Scalability (`AES_vs_OTP.py`):** Conducted macro stress profiling comparing **AES-128** against **One-Time Pad (OTP)** across the full scaling spectrum from $10^1$ to $10^{10}$ characters:
  * **Micro Scale ($10^1\text{--}10^4$ chars):** Sub-millisecond execution latency for both methods, with negligible initial context and IV setup overhead for AES.
  * **Mid Scale ($10^4\text{--}10^6$ chars):** Linear expansion in OTP memory footprint due to $O(N)$ key allocation requirements.
  * **Big Data Domain ($10^7\text{--}10^{10}$ chars):** OTP suffers catastrophic RAM exhaustion and severe latency surges (4–15 seconds) caused by large-array memory operations, whereas AES maintains a strictly deterministic, flat, sub-second execution profile ($< 0.2$ seconds).
* **Biochemical & Distributed Scaling Analysis:** Investigated wet-lab constraints—including homopolymer run dropouts, GC-content equilibrium (45%–55%), and ~1% biological indel/substitution error rates—highlighting the necessity of outer Error-Correcting Codes (Reed-Solomon / Fountain Codes) and distributed chunking frameworks (PySpark / MapReduce) for terabyte-scale deployment.

---

## Technical Stack

* **Language & Runtime:** Python 3.8+
* **Data Processing & Serialization:** `NumPy` (`uint8` buffer streams), `pickle`
* **Information Theory & Compression:** `dahuffman` (Prefix-Free Codec), custom `heapq` binary tree implementation
* **Cryptographic Primitives:** `PyCryptodome` (`AES-128` in `MODE_CFB` & `MODE_CBC`, CSPRNG `get_random_bytes`), `os.urandom` OTP engine
* **Biological Computing:** 2-Bit Dinucleotide Dictionary Mapping (`AT, GC, CG, TA`), `DNACloud` Architecture Analysis
* **Desktop Interface & Benchmarking:** `Tkinter` GUI Framework, `Matplotlib`, `lorem`