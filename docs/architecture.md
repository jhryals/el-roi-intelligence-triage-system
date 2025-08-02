# EL ROI System Architecture

This document provides a deeper look into the technical architecture and modular design of EL ROI.

---

## Overview

EL ROI is structured around the Intelligence Cycle:  
**Collection → Processing & Exploitation → Analysis & Production → Dissemination**

It transforms raw multilingual OSINT data into structured, actionable intelligence products via automated AI pipelines and human-in-the-loop feedback.

---

## Architecture Diagram

                ┌────────────────────┐
                │  OSINT Data Feeds  │
                └────────┬───────────┘
                         ▼
               ┌──────────────────────┐
               │ Ingestion Pipeline   │
               │ (Streaming/Batch)    │
               └────────┬─────────────┘
                        ▼
          ┌─────────────────────────────┐
          │ Preprocessing & Enrichment  │
          │ - Language Detection        │
          │ - Translation               │
          │ - Entity Extraction         │
          │ - Deduplication             │
          └────────┬────────────────────┘
                   ▼
           ┌────────────────────────────┐
           │ Classification & Clustering│
           └────────┬───────────────────┘
                    ▼
         ┌──────────────────────────────┐
         │ Vector DB + Metadata Store   │
         │ (FAISS + PostgreSQL/Elastic) │
         └────────┬─────────────────────┘
                  ▼
      ┌──────────────────────────────┐
      │ Natural Language Interface   │
      └────────┬────────────┬────────┘
               │            │
   ┌────────────┐   ┌──────────────┐
   │ Analyst     │   │ AuthN/AuthZ │
   │ Feedback    │   └──────────────┘
   └────▲────────┘
        │
        ▼
 ┌────────────────────────────────────┐
 │ Export to CHRONICLE & Visual UI    │
 │ (Exploration, Graphs, Filtering)   │
 └────────────────────────────────────┘

---

## Components

### 1. **Ingestion Pipeline**
- Collects OSINT via RSS, APIs, or streaming sources
- Modular by source type
- Supports future GEOINT/SIGINT/HUMINT inputs

### 2. **Preprocessing & Enrichment**
- Detects language
- Translates content into English
- Extracts entities using NER
- Deduplicates near-identical posts

### 3. **Classification & Clustering**
- Uses ML models to classify themes (e.g., cyber, political unrest)
- Clusters semantically similar posts via SBERT embeddings

### 4. **Vector DB + Metadata Store**
- FAISS used for fast semantic search
- PostgreSQL/Elasticsearch store metadata for filtering and traceability

### 5. **Natural Language Interface**
- Analyst uses plain-English queries to retrieve relevant insights
- Powered by retrieval-augmented generation (RAG)

### 6. **Feedback + Access Control**
- Feedback is captured to fine-tune ranking and tagging
- Role-based AuthN/AuthZ planned for production

### 7. **Export & Visual Interface**
- Reports can be exported in Markdown/PDF
- Analysts interact via a Streamlit dashboard

---

## Notes

- All modules are containerized and designed for easy deployment
- Analyst interaction is prioritized for UX simplicity and rapid triage
