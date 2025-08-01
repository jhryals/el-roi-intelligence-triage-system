# EL ROI: AI-Driven Intelligence Triage System

**EL ROI** (Enhanced Language-based Rapid Open-source Intelligence) is an AI-powered triage system designed to support the early phases of the Intelligence Cycle—**Collection**, **Processing & Exploitation**, and **Analysis & Production**.

It ingests live-streaming multilingual OSINT data, processes and enriches it through automated NLP pipelines, and intelligently surfaces thematically relevant insights. Analysts can query the system in natural language, explore communication clusters visually, and export structured intelligence summaries with source traceability.

The purpose of EL ROI is to accelerate insight discovery, reduce cognitive overload, and lay the groundwork for timely, actionable intelligence.

---

## Key Features

### 1. Collection
- Real-time ingestion of multilingual OSINT data (news, blogs, social platforms, etc.)
- Modular architecture designed to support future ingestion of multi-INT sources

### 2. Processing & Exploitation
- Language detection and translation (auto-handling mixed-language inputs)
- Named Entity Recognition (NER) and entity linking
- Text deduplication and normalization
- Source tagging and metadata enrichment

### 3. Analysis & Production
- Semantic clustering of communications
- Thematic classification using AI models (e.g., WMDs, cyber, political unrest)
- Interactive natural language querying
- Source-attributed intelligence output

### 4. Dissemination 
- Export support to CHRONICLE for auto-generated reports (Planned)

---

## System Architecture 

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

## Core Modules

- `data_ingestion/`: Streams multilingual OSINT sources via APIs or webhooks
- `preprocessing/`: Handles cleaning, translation, NER, and deduplication
- `classification/`: Identifies content themes using fine-tuned language models
- `clustering/`: Groups related documents by semantic similarity
- `vector_store/`: FAISS-based vector search engine with PostgreSQL/Elasticsearch metadata
- `nl_interface/`: Natural language query handler with retrieval-based output
- `ui/`: Visual exploration dashboard (Streamlit-based)
- `auth/`: Authentication and authorization services
- `integration/chronicle_exporter/`: Optional output pipe to CHRONICLE

---

## Development Roadmap

### **Phase 1 – Collection & Processing MVP**
- [x] Set up GitHub repo + documentation
- [ ] Ingest multilingual OSINT from RSS/news/social APIs
- [ ] Implement preprocessing:
  - Language detection
  - Translation
  - Named Entity Recognition (NER)
  - Deduplication
- [ ] Prototype clustering and classification using sentence embeddings
- [ ] Integrate vector similarity search with FAISS
- [ ] Implement metadata filtering (PostgreSQL or Elasticsearch)

---

### **Phase 2 – Analyst Interface & Intelligence Exploration**
- [ ] Build Streamlit-based visual dashboard
- [ ] Natural language query integration using RAG pipeline (LangChain/OpenAI)
- [ ] Cluster exploration with interactive graph visualization (Plotly or PyVis)
- [ ] Export intelligence to CHRONICLE format (Markdown, PDF)
- [ ] Analyst feedback capture and relevance scoring
- [ ] Implement secure AuthN/AuthZ (role-based access control)

---

### **Phase 3 – Production Readiness & DevOps**
- [ ] Containerize application with Docker
- [ ] Deploy to cloud platform (GCP or AWS)
- [ ] Set up CI/CD pipelines using GitHub Actions
- [ ] Implement basic logging and monitoring (e.g., Streamlit logs, Prometheus optional)
- [ ] Add basic unit and integration tests for core components
- [ ] Optional: Track ML models and experiments using MLflow or DVC

---

## Tech Stack

### **Languages & Frameworks**
- **Python 3.11**
- **JavaScript** (Streamlit/React UI via Streamlit Components)
- **FastAPI** – backend microservices and API layer
- **Streamlit** – rapid UI prototyping and dashboard
- **Docker** – containerization
- **GitHub Actions** – CI/CD

### **NLP & Machine Learning**
- **spaCy**, **Stanza**, **NLTK** – language preprocessing and NER
- **HuggingFace Transformers** – transformer-based models
- **SentenceTransformers (SBERT)** – document embeddings for clustering & similarity
- **LangChain + OpenAI API** – RAG (retrieval-augmented generation) for natural language interface

### **Data Stores**
- **FAISS** – vector similarity search
- **PostgreSQL** or **Elasticsearch** – metadata indexing and filtering
- **Optional**: **MLflow** – model versioning and experiment tracking

### **Visualization**
- **Plotly**, **PyVis**, **NetworkX** – interactive cluster and entity graphing

### **Deployment**
- **GCP** or **AWS** (planned cloud host)
- **Prometheus/Grafana** (optional monitoring)


---

## Folder Structure 

## 📁 Folder Structure 

- el-roi/
  - auth/
    - login.py
    - roles_config.yaml
  - classification/
    - topic_classifier.py
    - embeddings.py
  - clustering/
    - cluster_engine.py
  - config/
    - pipeline_config.yaml
    - model_params.yaml
    - sources_config.yaml
  - data_ingestion/
    - feeds/
    - scheduler.py
  - deployment/
    - Dockerfile
    - cloud_setup/
    - github_actions/
  - docs/
    - architecture.md
    - api_reference.md
  - feedback/
    - feedback_logger.py
  - integration/
    - chronicle_exporter/
      - exporter.py
  - logging/
    - logger.py
    - log_config.yaml
  - models/
    - embedding_model.py
    - classifier_model.py
    - model_utils.py
  - nl_interface/
    - query_handler.py
    - rag_pipeline.py
  - preprocessing/
    - pipeline.py
    - language_detection.py
    - translation.py
    - ner.py
    - deduplication.py
  - tests/
    - test_preprocessing.py
    - test_vector_store.py
    - test_query_handler.py
  - ui/
    - pages/
    - components/
  - vector_store/
    - faiss_store.py
    - metadata_index.py
  - visualization/
    - entity_graph.py
    - cluster_map.py
  - .env.example
  - .gitignore
  - requirements.txt
  - README.md
  - .secrets/
    - openai_api.key
    - gcp_creds.json


---

## Getting Started (via GitHub GUI)

1. Clone or download this repository from GitHub.
2. Open `.env.example` and fill in required API keys and credentials.
3. Use Streamlit locally to test interface modules (`ui/`).
4. Use the GitHub Projects tab to track development progress.

---

## Usage

This section will be expanded as features are built. Planned capabilities include:

- Start ingestion of multilingual OSINT feeds
- Run automated enrichment (NER, deduplication, etc.)
- Classify and cluster documents by topic
- Search using natural language questions
- Export filtered content to CHRONICLE format
- Visualize results and entity relationships via dashboard

---

## Contributing

Contributions, feedback, and ideas are welcome! Please:

- Fork the repository
- Create a feature branch (`feature-name`)
- Commit your changes
- Submit a Pull Request

For strategic features or integrations, open an issue for discussion.

---

## License

All rights reserved. This project is protected by copyright.

You may not copy, distribute, modify, or use any part of this project without explicit written permission from the author.

---

## Contact

Developed and maintained by **Justin Ryals**  
📫 [LinkedIn](https://linkedin.com/in/justinryals)  
📧 For usage or licensing inquiries, please contact the author directly.


