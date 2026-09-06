---
layout: page
title: xv6 OS Kernel Enhancements & Custom Schedulers
description: Operating System Kernel Modifications Implementing Custom System Calls, Process Accounting, Priority Scheduling, and Multi-Level Queue (MLQ) CPU Schedulers.
importance: 1
category: systems
github: https://github.com/MK2091379/xv6-project
---

## Overview

Monolithic operating system kernels govern execution isolation, hardware abstractions, and fair processor resource sharing across concurrent workloads. The default Round-Robin scheduler in educational Unix-like systems ensures baseline temporal fairness but cannot accommodate heterogeneous workloads demanding strict priority enforcement, real-time guarantees, or multi-class scheduling policies.

This project implements deep kernel-space modifications to **MIT's xv6 operating system** (Unix Version 6 re-implementation) in C and x86 assembly. The enhancements introduce custom system call interfaces, extend the Process Control Block (PCB) with high-resolution execution accounting, and replace the vanilla CPU scheduling mechanism with **Priority-Based Scheduling** and a **Multi-Level Queue (MLQ)** architecture, verified within the QEMU hardware emulator.

---

## Architectural Modifications & Kernel Engineering

The modifications alter low-level kernel infrastructure spanning hardware trap handling, system call vector dispatching, and process life-cycle transitions:

### 1. Trap Handling & Context Switching (`trap.c`, `swtch.S`)
* Intercepts hardware timer clock interrupts to update fine-grained process run-time and wait-time tick counters.
* Enforces scheduler preemption policies, checking queue states at each clock tick to yield or maintain CPU execution rights.

### 2. Process Control Block Augmentation (`proc.h`, `proc.c`)
* Extended `struct proc` to incorporate stateful telemetry: dynamic priority metrics, user-configurable nice values, queue assignments, process creation timestamps, and accumulated execution ticks.
* Refactored process initialization (`allocproc`) and exit sequences (`exit`, `wait`) to maintain invariant metrics across process lifecycles.

### 3. System Call Traversal & User-to-Kernel Transitions (`syscall.c`, `usys.S`, `syscall.h`)
* Added assembly-level entry points and syscall lookup tables to safely route user-space function calls through interrupt gates into privileged kernel space.
* Built diagnostic and control system calls, including `waitx` (extended wait retrieving turnaround and waiting times) and priority alteration primitives.

---

## Advanced CPU Scheduling Engines

### 1. Priority-Based Scheduling
* Implemented custom nice-level adjustments allowing processes to dynamically alter scheduling precedence.
* Replaced the default linear queue iteration with priority-weighted process selection, mitigating starvation while enforcing execution guarantees.

### 2. Multi-Level Queue (MLQ) Scheduler
* Partitioned the scheduling table into distinct prioritized execution queues.
* Segregated computational batch jobs from latency-sensitive interactive tasks, enforcing strict cross-queue priorities while maintaining balanced round-robin scheduling within equivalent priority classes.

---

## Verification & Stress Testing

* **Process Telemetry Validation:** Implemented dedicated test programs (`testwaitx.c`, `testrnps.c`) leveraging `proc_info.h` to measure process turnaround, execution, and wait-time metrics.
* **Kernel Stability & Stress Testing:** Validated concurrency guarantees and memory safety using customized test suites (`testnice.c`, `testspri.c`, `testmlq.c`) alongside the standard xv6 `usertests.c` suite under virtualized **QEMU** execution.

---

## Technical Stack

* **Kernel Languages:** C, x86 Assembly
* **Base Architecture:** MIT xv6 (Unix Version 6 Re-implementation)
* **Virtualization & Emulation:** QEMU
* **Core Domains:** Kernel Programming, Process Control Blocks (PCB), CPU Scheduling, System Call Interfaces, Trap Handlers