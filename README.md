# AI Invoice Extraction Pipeline

An AI-powered invoice extraction and processing pipeline built with n8n, Claude AI, PostgreSQL, and Docker.

This project automatically processes multi-page PDF invoice documents, extracts structured invoice data using LLMs, normalizes the information, persists relational records into PostgreSQL, and safely archives processed documents.

---

# Project Overview

The workflow automates invoice ingestion and structured data extraction from PDF documents received from external providers.

The system:

- Reads PDF files from a monitored ingestion directory
- Extracts text from multi-page PDF invoices
- Splits large documents into individual invoice records
- Uses Claude AI to extract structured invoice data
- Parses and normalizes LLM JSON responses
- Persists invoice headers and invoice line items into PostgreSQL
- Prevents duplicate invoice insertion using business-key upserts
- Prevents duplicate invoice item insertion using relational uniqueness constraints
- Automatically archives successfully processed PDFs

This project was created as part of an AI automation engineering portfolio.

---

# Architecture

```text
PDF Ingestion
    ↓
PDF Text Extraction
    ↓
Invoice Splitting
    ↓
LLM Structured Extraction
    ↓
JSON Normalization
    ↓
PostgreSQL Persistence
    ↓
Processed File Archival

---

# Tech Stack

- n8n
- Docker
- PostgreSQL
- Claude Haiku (Anthropic)
- JavaScript
- WSL2
- GitHub

---

# Workflow Features
## AI-Powered Invoice Extraction

Claude AI extracts structured invoice data including:

- Invoice headers
- Grower information
- Client information
- Air waybill references
- Product line items
- Quantities
- Pricing information

---

# PostgreSQL Relational Persistence

## The workflow stores:

Invoice Headers

- invoice_number
- grower information
- client information
- invoice totals
- raw JSON payloads

Invoice Line Items
- products
- quantities
- pricing
- invoice relationships
- line indexes

---

# Duplicate Protection

### The system uses database-level duplicate prevention:

## Invoice Header Uniqueness

Composite business key:
- grower_ruc
- invoice_number
- air_way_bill

## Invoice Item Uniqueness

Composite relational key:
- invoice_id
- line_index

This enables safe workflow re-execution without duplicate persistence.

---

# File Lifecycle Management

After successful processing:

-PDFs are automatically moved from:
  /files/input-pdfs

to:

  /files/processed

Future failed-processing support will move invalid PDFs to:

  /files/failed

---

# Workflow Steps

1. Read Input PDFs

Reads all PDF files from the Docker-mounted ingestion directory.

2. Extract PDF Text

Uses n8n PDF extraction capabilities to convert PDFs into raw text.

3. Split Invoices into Items

Splits large multi-page documents into individual invoices using recurring document markers.

4. Extract Structured Invoice Data with AI

Claude AI analyzes invoice text blocks and extracts structured JSON data.

5. Parse and Normalize JSON

Converts LLM responses into normalized JSON records.

6. Insert Invoice Headers

Performs duplicate-safe PostgreSQL upserts for invoice header records.

7. Prepare Invoice Items

Transforms nested invoice items into relational database records.

8. Insert Invoice Items

Performs duplicate-safe upserts for invoice line items.

9. Build Processed File List

Aggregates successfully processed source PDF paths.

10. Move Processed PDFs

Archives successfully processed PDFs into the processed directory.

---

# Current Features

- Multi-file PDF ingestion
- Multi-page invoice extraction
- AI-powered structured extraction
- JSON normalization
- PostgreSQL persistence
- Relational invoice modeling
- Duplicate-safe upserts
- Processed-file archival
- Dockerized local environment

# Planned Improvements

- OCR support for scanned PDFs
- Email-triggered invoice ingestion
- Failed-file handling pipeline
- Human review workflow
- Validation and reconciliation rules
- Dashboard and reporting
- Queue-based asynchronous processing
- Cloud deployment

---

# Local Development

Start Services
   docker compose up -d

Stop Services
   docker compose down

---

# Repository Structure
.
├── workflows/
├── screenshots/
├── docker/
├── docs/
└── README.md

---

# Project Status

Active development.

This project is currently evolving into a production-oriented AI document-processing
pipeline focused on automation, reliability, and relational persistence.
