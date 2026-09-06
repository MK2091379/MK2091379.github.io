---
layout: page
title: Tile-Based Hardware Accelerator & PE Array
description: Register-Transfer Level (RTL) VHDL Design of a Scalable Parallel Processing Element Array for Compute-Intensive Workloads on FPGAs.
importance: 2
category: systems
github: https://github.com/MK2091379/iust-cad
---

## Overview

High-throughput matrix operations, digital signal processing (DSP), and deep learning workloads are fundamentally constrained by memory bandwidth and the sequential execution limitations of standard Von Neumann architectures. Achieving high-performance compute efficiency requires dedicated, spatial hardware pipelines executing at the Register-Transfer Level (RTL).

This project implements a scalable **Tile-Based Hardware Accelerator and Processing Element (PE) Array** designed entirely in **VHDL** within the **Xilinx Vivado** development suite. Built around modular, interconnected compute units, the architecture enables massive spatial parallelism, structured systolic data routing, and deterministic clock-cycle latency optimized for FPGA logic fabric and DSP slice configurations.

---

## Architectural Decomposition & Hierarchy

The RTL implementation follows a strict hierarchical modular structure designed for clean synthesis and elaboration across distinct abstraction layers:

### 1. Global Definitions & Hardware Package (`Pack.vhd`)
* Establishes system-wide parameterization, defining custom fixed-point data types, bus widths, array structures, and global constants.
* Standardizes universal component declarations across compute blocks to eliminate redundant interface declarations.

### 2. Arithmetic Compute Core (`PE.vhd`)
* Serves as the primary functional Processing Element (PE) responsible for core arithmetic, accumulation, and logical execution.
* Implements localized register stages for input, output, and control signals, mitigating combinational propagation delays.

### 3. Structural Grid Subsystem (`Tile.vhd`)
* Groups and coordinates local clusters of PEs into unified, modular tile blocks.
* Manages structured intra-tile interconnects and intermediate pipelining stages to preserve signal integrity at higher clock frequencies.

### 4. Top-Level Integration Wrapper (`Main.vhd`)
* Instantiates and connects the 2D tile topology across global routing channels.
* Orchestrates clock distribution networks, global synchronous resets, and centralized I/O data buses.

### 5. Dynamic Stimulus & Verification Harness (`main_tb.vhd`)
* Programmatic VHDL testbench generating high-precision clock signals, reset sequences, and dynamic input test vectors.
* Performs behavioral functional verification and monitors output assertions to validate cycle-accurate data propagation.

---

## RTL Verification & Simulation Workflow

The architecture was verified using the Vivado Simulator (`xsim`) toolchain:

* **Design & Synthesis Phase:** Parameter configuration in `Pack.vhd` $\rightarrow$ Core logic description in `PE.vhd` $\rightarrow$ Spatial grouping into `Tile.vhd` $\rightarrow$ Top-level routing in `Main.vhd`.
* **Elaboration & Simulation Phase:** Multi-file VHDL compilation $\rightarrow$ RTL elaboration $\rightarrow$ Automated testbench execution (`main_tb.vhd`) under `xsim` $\rightarrow$ Waveform analysis validating timing closure and zero setup/hold timing violations.

---

## Technical Stack

* **Hardware Description Language:** VHDL (IEEE 1076 standard)
* **EDA & Synthesis Toolchain:** Xilinx Vivado Design Suite (v2020+)
* **Simulation Engine:** Vivado Simulator (`xsim`)
* **Target Hardware:** Field-Programmable Gate Arrays (FPGA)
* **Architecture Domains:** Spatial Computing, Systolic Arrays, RTL Design, Digital Hardware Acceleration