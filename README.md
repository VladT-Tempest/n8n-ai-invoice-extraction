# AI Invoice Extraction Pipeline

An AI-powered invoice extraction workflow built with n8n, Claude AI, and PostgreSQL.

This project automatically processes multi-page PDF invoice documents, extracts structured invoice data using AI, and prepares the information for persistence in a relational database.

---

# Project Overview

The workflow is designed to automate invoice data entry tasks from PDF documents received from external providers.

The system:

- Reads PDF files from a monitored directory
- Extracts text from multi-page PDFs
- Splits invoice documents into individual invoice items
- Uses Claude AI to extract structured invoice data
- Normalizes JSON responses
- Prepares the data for PostgreSQL persistence

This project was created as part of an automation and AI engineering portfolio.

---

# Tech Stack

- n8n
- Docker
- Claude Haiku (Anthropic)
- JavaScript
- PostgreSQL
- WSL2
- GitHub

---

# Workflow Steps

## 1. Read Input PDFs
Reads all PDF files from the input directory mounted into the Docker container.

## 2. Extract PDF Text
Uses n8n PDF extraction capabilities to convert PDFs into raw text.

## 3. Split Invoices into Items
Splits large multi-page documents into individual invoice items using recurring document patterns.

## 4. Extract Structured Invoice Data with AI
Claude AI analyzes each invoice and extracts structured invoice information in JSON format.

## 5. Parse and Normalize JSON
Converts LLM responses into normalized JSON objects ready for persistence.

## 6. Database Persistence (In Progress)
The next phase will store invoice headers and invoice items into PostgreSQL.

---

# Current Features

- Multi-file PDF processing
- Multi-page invoice extraction
- AI-powered structured data extraction
- JSON normalization pipeline
- Dockerized n8n environment

---

# Planned Improvements

- PostgreSQL integration
- Email-triggered invoice ingestion
- OCR support for scanned PDFs
- Duplicate invoice detection
- Validation and reconciliation rules
- Dashboard and reporting
- Human review workflow

---

# Screenshot

![Workflow Screenshot](screenshots/workflow.png)

---

# Project Status

Active development.

This project is currently being expanded into a production-ready invoice automation pipeline.

---

# Repository Structure

```text
.
├── workflows/
├── screenshots/
├── docs/
├── docker/
└── README.md
