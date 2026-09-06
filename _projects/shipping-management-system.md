---
layout: page
title: Maritime Shipping & Logistics Management System
description: Modular Backend and Containerized Platform for Cargo Forwarding, Consignment Lifecycle Tracking, and Vessel Logistics.
importance: 3
category: software-engineering
github: https://github.com/MK2091379/shipping-management-system
---

## Overview

Global freight forwarding and maritime logistics demand scalable, highly dependable transaction backends capable of tracking multi-modal cargo lifecycles, monitoring vessel schedules, and enforcing strict compliance auditing. Managing cargo movement requires robust relational modeling, role-based operational permissions, sub-second query filtering across high-volume manifests, and containerized deployment infrastructure.

This project implements an enterprise-ready **Maritime Shipping and Cargo Logistics Management Backend** built in Python. The platform coordinates end-to-end consignment tracking, vessel route mapping, automated database schema synchronizations, and role-based access control, fully containerized via **Docker** and **Docker Compose** for reproducible production deployments.

---

## System Architecture & Modular Subsystems

The backend decomposes logistics operations into decoupled modules governing data persistence, authentication, operational search, and administrative governance:

### 1. Application Entrypoint & Orchestration (`main.py`)
* Coordinates API routing pipelines, middleware chains (CORS, request logging, error handlers), and runtime server execution.
* Directs inbound requests across operational, administrative, and query subsystems.

### 2. Identity, Governance & Authentication (`auth.py`)
* Enforces role-based access control (RBAC) separating field operators, vessel dispatchers, cargo auditors, and system administrators.
* Utilizes cryptographic JSON Web Tokens (JWT) and salted hash verification to secure state-modifying operational endpoints.

### 3. Search & Manifest Query Engine (`search.py`)
* Optimized query processing pipeline executing high-performance lookups across shipments, international container identifiers, vessel registries, and transit routes.
* Implements multi-attribute filtering, date-range partition queries, and pagination to handle enterprise-scale cargo datasets with minimal query latency.

### 4. Administrative Control & Monitoring (`admin.py`)
* Dedicated administrative interface and privileged endpoints managing operational overrides, client provisioning, and system health monitoring.
* Tracks shipment event logs and generates audit trails across critical consignment status transitions.

### 5. Dual Database Architecture & ORM Persistence (`database.py`, `database_local.py`, `migration.py`)
* **Production Persistence:** Connects to robust PostgreSQL instances via SQLAlchemy ORM and Psycopg2 adapters, utilizing connection pooling for high-concurrency throughput.
* **Development Isolation:** Features an independent SQLite configuration (`database_local.py`) enabling rapid local testing, prototyping, and offline development.
* **Schema Evolution:** Dedicated migration scripts (`migration.py`) manage database instantiation, relational integrity constraints, and automated schema synchronization.

---

## Key Technical Implementations

* **Data Validation & Type Safety:** Strict request/response payload validation and environment variable serialization using Pydantic and Python-dotenv, preventing malformed manifest injections.
* **Containerized Orchestration:** Standardized `Dockerfile` and multi-container `docker-compose.yml` configurations orchestrating the application server, PostgreSQL database, and persistent data volumes with zero host configuration drift.
* **Exploratory Analytics & Telemetry:** Interactive Jupyter testing environments (`test.ipynb`) facilitating end-to-end scenario validation, query profiling, and cargo throughput analysis.

---

## Technical Stack

* **Languages & Core:** Python 3.9+, Pydantic, Python-dotenv
* **API Framework:** FastAPI / Flask
* **Database & Persistence:** PostgreSQL, SQLite, SQLAlchemy, Psycopg2
* **Authentication & Security:** JWT (JSON Web Tokens), Cryptography, RBAC
* **DevOps & Containerization:** Docker, Docker Compose
* **Testing & Analytics:** Jupyter Notebook, SQL Dumps
* **Domain Focus:** Supply Chain Management, Maritime Logistics, Enterprise Fleet Tracking