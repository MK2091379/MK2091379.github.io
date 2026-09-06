---
layout: page
title: OpenUnderstand Static Code Analyzer
description: An open-source, Python-based static code analysis and software metrics extraction framework utilizing ANTLR4 AST parsing for Java.
importance: 1
category: software-engineering
github: https://github.com/MK2091379/iust-compiler-design
---

## Overview

**OpenUnderstand** is a comprehensive, open-source static code analysis and software metrics extraction framework. Designed as a Python-based implementation of the commercial **SciTools Understand API**, this project provides a robust infrastructure to parse, analyze, and extract deep architectural dependencies from Java source code. 

By generating detailed Abstract Syntax Trees (ASTs) via ANTLR4 and systematically traversing them, OpenUnderstand maps complex relationships (e.g., Coupling, Cohesion, Inheritance) and stores the outputs in a structured relational database format (`.oudb`). This enables advanced querying, visualization, and software reverse-engineering.

The development of this compiler-level analysis engine was executed across four rigorous phases, evolving from basic grammatical parsing to a fully benchmarked, cross-project metric engine.

---

## Development Lifecycle & System Architecture

### Phase 1: ANTLR Fundamentals & AST Parsing
The foundational phase established the core parsing infrastructure using the **ANTLR4** parser generator.
* **Custom Grammars:** Developed tailored `.g4` grammars to parse complex data strings (e.g., URL deconstruction, SQL Server connection strings).
* **Java AST Traversal:** Configured `JavaLexer.g4` and `JavaParserLabeled.g4` to generate Python recognizers. Implemented initial AST listeners (`JavaParserLabeledListener`) to extract basic structural metrics, such as method enumerations and class-level attribute counts from raw Java source files.

### Phase 2: Metrics Validation & Database Testing
Focused on the integrity and accuracy of the generated OpenUnderstand Database (`.oudb`), ensuring strict parity with commercial baselines.
* **Entity Population:** Utilized custom traversal scripts to populate relational tables with project entities.
* **API Benchmarking:** Programmed distinct Python calculators to measure software metrics (e.g., `CountDeclClassMethod`, `CountDeclExecutableUnit`, `CountDeclFile`).
* **100% Accuracy Validation:** Directly benchmarked custom database queries against the native SciTools Understand API (`ent.metric()`), achieving exact mathematical parity across all tested packages.

### Phase 3: Cross-Project Benchmarking & Scalability
Scaled the validation framework to ensure the AST traversal and entity resolution algorithms remained robust against diverse, real-world architectural patterns.
* **Complex Codebases:** Benchmarked the engine against structurally complex repositories, including the widely-used `org.json` library and deeply nested legacy codebases.
* **Advanced Entity Filtering:** Deployed dynamic `EntityModel.select()` queries to resolve complex entity relationships, such as mapping static variables to inherited parent classes across multi-file projects.

### Phase 4: The Full Static Code Analysis Engine
The final consolidation of the framework into a production-ready static analysis tool capable of full-scale software reverse engineering.
* **Comprehensive Reference Extraction:** Systematically identifies and extracts core software dependencies spanning `Call/CallBy`, `Define/DefineBy`, `Import/ImportBy`, and `Modify/ModifyBy` graphs.
* **Extensive Testbeds:** Validated against large-scale enterprise Java projects (e.g., Authorize.net, PayPal, and VisaCheckout API gateways) to verify analysis passes under heavy computational loads.

---

## High-Level Engine Architecture

The framework is highly decoupled, categorized into five primary execution domains:
1. **Grammars & Generators (`grammars/`, `gen/`):** Raw ANTLR4 configurations and the auto-generated Python lexers/parsers.
2. **Core Engine (`openunderstand/`):** The central orchestrator managing the parsing lifecycle and AST initialization.
3. **Analysis Passes (`analysis_passes/`):** Modular tree-walkers responsible for extracting specific relational references and dependencies.
4. **Metrics Engine (`metrics/`):** Computational module evaluating codebase health, structural complexity, and object-oriented metrics.
5. **Database Layer (`oudb/`):** The custom ORM mapping in-memory AST representations into persistent `.oudb` relational files.

---

## Technical Stack

* **Language:** Python 3.x
* **Parser Generator:** ANTLR4 (Abstract Syntax Trees)
* **Target Domain:** Java Source Code Analysis & Reverse Engineering
* **Benchmarking Baseline:** SciTools Understand API
* **Documentation:** [OpenUnderstand Official Docs](https://m-zakeri.github.io/OpenUnderstand/)