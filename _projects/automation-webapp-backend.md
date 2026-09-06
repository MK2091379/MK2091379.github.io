---
layout: page
title: Enterprise Resource Management & Office Automation Backend
description: Scalable, Multi-App Django REST API with Role-Based Access Control, OpenAPI Documentation, and Corporate ERP Subsystems.
importance: 2
category: software-engineering
github: https://github.com/MK2091379/automation-webapp-backend
---

## Overview

Modern enterprise environments require robust, highly modular service layers to orchestrate operational workflows—spanning personnel management, fiscal auditing, logistical dispatch, and resource tracking. Distributed corporate services must guarantee strict Role-Based Access Control (RBAC), fine-grained record-level permissions, auditability, and scalable schema discovery.

This project delivers an enterprise-grade **Office Automation & Enterprise Resource Planning (ERP) Backend System** implemented in Python using **Django** and **Django REST Framework (DRF)**. Designed around domain-driven architectural paradigms, the platform integrates 14 specialized sub-applications under a unified global middleware, standardizing token authentication, dynamic pagination, relational schemas, and interactive OpenAPI documentation.

---

## Architecture & Subsystem Decomposition

The platform decouples business domains into discrete applications operating over an optimized relational database schema (compatible with SQLite and PostgreSQL):

### 1. Identity, Governance & Core Logic
* **`automation/`:** System routing nerve center; configures production ASGI/WSGI entry points, global exception handlers, customized dynamic pagination filters (`pagination.py`), and universal RBAC access policies (`permissions.py`).
* **`Register/`:** User lifecycle and security module implementing customized abstract user models, cryptographic token authentication, and multi-tier employee demographic metadata.

### 2. Human Capital & Financial Infrastructure
* **`HRdesk/`:** Enterprise personnel portal handling departmental onboarding, organizational hierarchies, and intra-office correspondence.
* **`Salary/`:** Automated payroll compensation engine calculating variable wage matrices, statutory deductions, shift-based hours, and disbursement ledger pipelines.
* **`TimeAndDateTracker/`:** High-precision attendance verification system capturing check-in/out timestamps, delay tracking, shift intervals, and work-hour analytics.
* **`FinReport/`:** Fiscal ledger consolidation application producing aggregated expense summaries, budgetary disclosures, and departmental financial telemetry.

### 3. Corporate Logistics & Facility Management
* **`CompanyAssets/`:** Asset lifecycle and inventory tracking subsystem managing equipment assignments, serial custody, and asset depreciation.
* **`dormitory/`:** Corporate housing and living quarters management tracking real estate blocks, occupancy ratios, and resident allocation states.
* **`Transportation/`:** Corporate transit and vehicle fleet dispatch engine supporting transit validation and geospatial route mapping via Leaflet.js and Django Location Field.
* **`Food/` & `FoodImage/`:** Dining and commissary subsystem organizing meal scheduling, dynamic menu pricing, dietary profiles, and high-resolution media storage.

### 4. Workflow Orchestration & Collaboration
* **`ServiceCounter/`:** Internal ticketing portal handling formalized IT and administrative service tickets, manager reviews, and deterministic status progression.
* **`ToDoList/` & `Notepad/`:** Departmental productivity suite managing asynchronous task queues, priority weighting, rich text technical memos, and document attachments.
* **`BulletinBoard/`:** Broadcast messaging engine facilitating company-wide administrative announcements and event publication feeds.

---

## Key Technical Implementations

* **Role-Based Access Control (RBAC):** Custom permission classes overriding default DRF handlers to enforce principle-of-least-privilege access across endpoints based on user groups and operational roles.
* **Interactive OpenAPI/Swagger Specifications:** Native automated schema generation utilizing `drf-yasg`, exposing interactive OpenAPI 2.0/3.0 UI explorers via Swagger and ReDoc.
* **Performance Telemetry:** Integrated Django Debug Toolbar hooks for query profiling, N+1 query identification, and SQL transaction optimization prior to WSGI/Gunicorn production deployment.

---

## Technical Stack

* **Core Framework:** Python, Django, Django REST Framework (DRF)
* **Database & ORM:** SQLite / PostgreSQL, Django ORM
* **Authentication & Security:** Token-Based Authentication, Custom RBAC Engine
* **API Documentation:** OpenAPI Specification, `drf-yasg`, Swagger UI, ReDoc
* **Geospatial & Mapping:** Leaflet.js, Django Location Field
* **Deployment & Monitoring:** WSGI / ASGI (Gunicorn Ready), Django Debug Toolbar