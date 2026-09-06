---
layout: page
title: Knowledge Engineering, Ontologies & Semantic Reasoning Suite
description: Comprehensive Suite Spanning Macroeconomic Ontologies (Neo4j/OWL), Multi-Hop LLM Graph Reasoning (GPT-4.1), and Lexical Semantic Engineering (FarsNet & NetworkX).
importance: 1
category: knowledge-engineering
github: https://github.com/MK2091379/ontology-knowledge-engineering
---

## Overview

Knowledge Representation and Reasoning (KRR) forms the bedrock of symbolic artificial intelligence, bridging unstructured natural language data and deterministic relational logic. Constructing machine-interpretable schemas enables deep multi-hop reasoning, transparent inference path verification, and context grounding that mitigates hallucinations in generative Large Language Models (LLMs).

This project consolidates an advanced **Knowledge Engineering and Semantic Reasoning Suite** spanning three interconnected domains: macroeconomic ontology modeling in **Neo4j** and **W3C OWL/RDF**, empirical evaluation of **LLM graph reasoning (GPT-4.1)** across multi-hop biomedical and scientific taxonomies, and algorithmic traversal of the **FarsNet** Persian lexical semantic database using **NetworkX**.

---

## Core Systems & Modular Breakdown

### 1. Macroeconomic Ontology & Geopolitical Knowledge Graph
* **Domain Modeling:** Captures the complex geopolitical and macroeconomic determinants governing global gold price fluctuations from the outbreak of the Russia-Ukraine conflict onward.
* **Graph Architecture:** Formulates an interconnected graph schema consisting of 48 conceptual/instance nodes and 64 directed relationship edges (e.g., `positivelyCorrelatedWith`, `causedBy`, `sanctionedBy`).
* **Automated Cypher Pipeline:** Implements custom parser scripts (`json_to_cypher.py`) transforming Neo4j Arrows vector exports into transactional, idempotent `MERGE` Cypher queries.
* **Semantic Web Export:** Converts graph stores into standard W3C ontologies (`.owl` / `.rdf`) via `rdflib` (`csv_to_owl.py`), ensuring SPARQL query compliance and formal Description Logic (DL) expressivity.
* **Competency Queries:** Traces multi-variable paths assessing the systemic economic impacts of the 2024 US Presidential Election, crude oil shocks, inflation surges, and regional conflicts.

### 2. Multi-Hop Knowledge Graph Reasoning & LLM Evaluation
* **Evaluation Framework:** Rigorously benchmarks the structural inference capabilities of **GPT-4.1** over structured knowledge graphs across four distinct domains: **CSO** (Computer Science), **FMA** (Human Anatomy), **Pleiades** (Ancient Geography), and **RxNorm** (Pharmacology).
* **Triplet Extraction:** Automates the mining and partitioning of `(Subject, Predicate, Object)` triples into strict taxonomic hierarchies (`is_a`) and non-taxonomic relational properties (`other`).
* **Chain-of-Reasoning Benchmarking:** Evaluates balanced verification questions across multiple reasoning depths:
  * *Single-Hop:* Direct taxonomic subclass verification.
  * *Multi-Hop (Long Chain):* Deep compositional paths spanning 4 to 7 transitive hops.
  * *Non-Taxonomic Relations:* Multi-predicate cross-entity relations.
* **Empirical Prompting Analysis:** Demonstrates that while zero-shot parametric prompting degrades toward random-guess performance (~50%) on deep transitive chains, injecting explicit sub-graph context into prompts elevates retrieval and verification accuracy to ~100%.

### 3. Computational Lexical Semantics on FarsNet
* **Lexical Taxonomy Traversal:** Implements a computational semantic network engine over **FarsNet** (the Persian WordNet lexical ontology), querying hypernymy, hyponymy, meronymy, and domain associative linkages.
* **Graph Traversal & Search:** Utilizes **NetworkX** to construct directed graph representations from structured relational fact triples (`farsnet_facts.tsv`).
* **Automated Inference:** Implements shortest-path algorithms, transitive closure computation, and taxonomic distance metrics to verify lexical semantic entailment.

---

## Key Technical Highlights

* **Graph Database Orchestration:** Native Neo4j administration, Cypher index optimization, and binary dump restoration (`hwii.dump`).
* **Semantic Web Standards:** Construction of serialized RDF/XML and OWL schemas adhering to W3C Semantic Web compliance.
* **Parametric vs. Non-Parametric LLM Profiling:** Systematic benchmarking demonstrating the limitations of internal model weights on long-chain graph deductions without external knowledge augmentation.
* **Network Algorithms:** Graph construction, cycle detection, transitive reduction, and topological pathfinding across dense lexical knowledge bases.

---

## Technical Stack

* **Languages & Core:** Python 3.8+, Pandas, NumPy
* **Graph Databases & Querying:** Neo4j, Cypher Query Language, Arrows.app
* **Semantic Web & Ontologies:** RDFLib, OWL (Web Ontology Language), RDF/XML
* **Graph Analytics:** NetworkX, Matplotlib
* **LLM Benchmarking & Evaluation:** GPT-4.1, Automated Prompt Templating, Jupyter Notebooks
* **Domain Focus:** Knowledge Representation & Reasoning (KRR), Knowledge Graphs, Lexical Semantics, LLM Reasoning