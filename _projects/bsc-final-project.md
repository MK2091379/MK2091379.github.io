---
layout: page
title: Secure Data Transmission & Information Compression System
description: Research Thesis Implementation Combining Information-Theoretic Lossless Huffman Coding with Symmetric Cryptography (AES & OTP) over Custom TCP Sockets.
importance: 3
category: systems
github: https://github.com/MK2091379/bsc-final-project
---

## Overview

In distributed computing and secure communications, balancing network bandwidth efficiency with end-to-end cryptographic confidentiality is a fundamental design challenge. Naive serialization approaches often introduce redundant packet transmission costs or expand cryptographic surface vulnerabilities.

This research thesis project designs and evaluates an integrated **Secure End-to-End Transmission and Data Compression Architecture**. The pipeline combines information-theoretic lossless data compression (**Huffman Coding**) with symmetric cryptographic primitives (**Advanced Encryption Standard - AES** and information-theoretically secure **One-Time Pad - OTP**) over custom low-level TCP/IP network sockets. The system includes an interactive desktop control interface and an empirical benchmarking engine evaluating computational latency, throughput, and entropy tradeoffs.

---

## Architectural Pipeline

* **Source Encoding & Frequency Analysis:** Statistical frequency extraction across raw input payloads.
* **Lossless Compression (Huffman Tree):** Construction of prefix-free binary trees and compact bit-level serialization to minimize channel bandwidth utilization.
* **Cryptographic Layer:** Application of symmetric ciphers (AES in authenticated block modes or information-theoretically secure One-Time Pad) to compressed bitstreams.
* **Socket Transmission:** Client-server packet transmission and streaming over raw TCP/IP transport sockets.
* **Receiver Daemon & Inversion:** Socket ingestion, key-based payload decryption, prefix-tree decoding, and lossless data recovery.

---

## Core System Modules

### 1. Unified Control Dashboard (`GUI.py`)
* Serves as an interactive desktop control center built with Tkinter.
* Exposes real-time toggles for cipher algorithms (AES vs. OTP), compression tree inspection, bit-packing parameters, and packet transmission monitoring.

### 2. Transmitter Node (`Sending.py`)
* Constructs variable-length prefix codes based on source symbol frequency distributions.
* Serializes variable-length bitstreams and packages binary trees for round-trip inversion.
* Encrypts compressed byte sequences and manages low-level TCP socket buffers for reliable transmission.

### 3. Receiver Daemon (`Receiving.py`)
* Operates as an asynchronous background listener daemon bound to designated TCP ports.
* Ingests network packet frames, verifies payload integrity, and applies inverse cryptographic decryption.
* Traverses reconstructed Huffman tree representations to restore original uncompressed payloads with zero data degradation.

### 4. Empirical Benchmarking & Verification Engine (`AES_vs_OTP.py` & `HuffmanCodingTest.py`)
* **Round-Trip Fidelity:** Automated verification suite proving bit-level serialization consistency and lossless reconstruction across arbitrary payload schemas.
* **Cryptographic Trade-Off Profiling:** Rigorous empirical performance suite measuring encryption/decryption execution latency, memory footprint, and ciphertext entropy profiles between AES and One-Time Pad under variable network loads.

---

## Technical Stack

* **Language & Runtime:** Python 3.8+
* **Information Theory:** Huffman Coding, Prefix-Free Trees, Bit-Level Serialization, Frequency Estimation
* **Cryptographic Primitives:** AES, One-Time Pad (OTP), `pycryptodome`
* **Networking:** Low-level TCP/IP Socket Programming (Client-Server Architecture)
* **Desktop Interface:** Tkinter UI Framework
* **Empirical Analysis:** Latency Profiling, Compression Ratio Analysis, Entropy Benchmarking