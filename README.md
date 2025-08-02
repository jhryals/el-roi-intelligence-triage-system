# EL ROI: AI-Driven Intelligence Triage System

**EL ROI** (Enhanced Language-based Rapid Open-source Intelligence) is an AI-powered system that accelerates the triage of vast multilingual OSINT streams by operationalizing the early phases of the Intelligence Cycle: **Collection**, **Processing & Exploitation**, and **Analysis & Production**.

It ingests, enriches, and semantically clusters high-volume communications, enabling analysts to query insights in natural language, explore visual patterns, and export intelligence reports with full source traceability. EL ROI reduces cognitive overload and increases the speed at which actionable intelligence can be surfaced, analyzed, and disseminated.

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
- Export support to CHRONICLE for auto-generated reports (Markdown, PDF)
- Analyst dashboard available via a secure **Streamlit-based web interface**

---

### User Interaction
- Analysts access the system through a secure browser-based interface
- Natural language queries return interactive results within the web app
- Results can be filtered, visualized, and exported to CHRONICLE (an AI-powered reporting module for structured summary generation), which can then be transformed into standard intelligence reporting formats.

> ℹ️ While Streamlit supports rapid prototyping, future UI enhancements may include migration to a full-stack web framework (e.g., React + FastAPI) for scalability and finer control.

---

## System Architecture

```text
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
```

---

## Core Modules

- `data_ingestion/`: Streams multilingual OSINT sources via APIs or webhooks
- `preprocessing/`: Handles cleaning, translation, NER, and deduplication
- `classification/`: Identifies content themes using fine-tuned language models
- `clustering/`: Groups related documents by semantic similarity
- `vector_store/`: FAISS-based vector search engine with PostgreSQL/Elasticsearch metadata
- `nl_interface/`: Natural language query handler with retrieval-based output
- `ui/`: Visual exploration dashboard (Streamlit-based web app)
- `auth/`: Authentication and authorization services
- `integration/chronicle_exporter/`: Optional output pipe to CHRONICLE
- `visualization/`: Entity and cluster graph exploration
- `feedback/`: Analyst feedback logger and relevance scorer
- `logging/`: Operational log management and error tracking

---

## Folder Structure

- `el-roi/`
  - `auth/` – Authentication and role-based access control
  - `classification/` – Thematic classification using AI models
  - `clustering/` – Semantic clustering of documents
  - `config/` – Pipeline and model configuration files
  - `data_ingestion/` – OSINT ingestion via APIs, feeds, and schedulers
  - `deployment/` – Dockerfiles, CI/CD configs, and cloud deployment
  - `docs/` – System architecture and technical documentation
  - `feedback/` – Analyst feedback logging and scoring
  - `integration/`
    - `chronicle_exporter/` – Export logic to CHRONICLE report format
  - `logging/` – Log formatting and management
  - `models/` – ML model wrappers, utilities, and checkpoints
  - `nl_interface/` – Natural language query handling (RAG pipeline)
  - `preprocessing/` – NLP tasks: NER, translation, deduplication
  - `tests/` – Unit and integration test cases
  - `ui/` – Streamlit-based analyst dashboard
  - `vector_store/` – FAISS + metadata DB logic
  - `visualization/` – Cluster and entity graph visualization
  - `.env.example` – Environment variable template
  - `.gitignore` – Git exclusions
  - `requirements.txt` – Python dependencies
  - `README.md` – Project overview and documentation
  - `.secrets/` – Git-ignored local API keys and credentials

---

## Development Roadmap

### Phase 1 – Collection & Processing MVP
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

### Phase 2 – Analyst Interface & Intelligence Exploration
- [ ] Build Streamlit-based visual dashboard (browser-accessible)
- [ ] Natural language query integration using RAG pipeline (LangChain/OpenAI)
- [ ] Cluster exploration with interactive graph visualization (Plotly or PyVis)
- [ ] Export intelligence to CHRONICLE format (Markdown, PDF)
- [ ] Analyst feedback capture and relevance scoring
- [ ] Implement secure AuthN/AuthZ (role-based access control)

### Phase 3 – Production Readiness & DevOps
- [ ] Containerize application with Docker
- [ ] Deploy to cloud platform (GCP or AWS)
- [ ] Set up CI/CD pipelines using GitHub Actions
- [ ] Implement basic logging and monitoring (e.g., Streamlit logs, Prometheus optional)
- [ ] Add basic unit and integration tests for core components
- [ ] Optional: Track ML models and experiments using MLflow or DVC

---

## Tech Stack

### Languages & Frameworks
- **Python 3.11**
- **JavaScript** (Streamlit/React UI via Streamlit Components)
- **FastAPI** – backend microservices and API layer
- **Streamlit** – browser-based web app dashboard
- **Docker** – containerization
- **GitHub Actions** – CI/CD

### NLP & Machine Learning
- **spaCy**, **Stanza**, **NLTK** – language preprocessing and NER
- **HuggingFace Transformers** – transformer-based models
- **SentenceTransformers (SBERT)** – document embeddings for clustering & similarity
- **LangChain + OpenAI API** – RAG (retrieval-augmented generation)

### Data Stores
- **FAISS** – vector similarity search
- **PostgreSQL** or **Elasticsearch** – metadata indexing and filtering
- **Optional**: **MLflow** – model versioning and experiment tracking

### Visualization
- **Plotly**, **PyVis**, **NetworkX** – interactive cluster and entity graphing

### Deployment
- **GCP** or **AWS** (planned cloud host)
- **Prometheus/Grafana** (optional monitoring)

---

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/el-roi-intelligence-triage-system.git
cd el-roi-intelligence-triage-system
```

### 2. Configure Environment

Copy `.env.example` to `.env` and fill in your API keys (e.g., OpenAI, GCP):

```bash
cp .env.example .env
```

### 3. Run Modules

#### Start Streamlit Analyst Dashboard (Web App)

```bash
streamlit run ui/pages/dashboard.py
```

#### Run Ingestion Pipeline (CLI)

```bash
python data_ingestion/scheduler.py
```

---

## Usage Examples

- Start ingestion of multilingual OSINT feeds
- Run automated enrichment (NER, translation, deduplication)
- Classify and cluster documents by topic
- Search using natural language questions
- Visualize entity relationships and cluster maps
- Export source-attributed summaries to CHRONICLE format

---

## Contributing

We welcome contributions and ideas:

1. Fork the repository  
2. Create a feature branch (`feature/your-feature`)  
3. Commit your changes  
4. Submit a Pull Request  

For strategic suggestions or integrations, open an issue first.

---

## License

**All rights reserved.**  
You may not copy, distribute, modify, or use any part of this project without explicit written permission from the author.

---

## Contact

Developed and maintained by **Justin Ryals**  
📫 [LinkedIn](https://www.linkedin.com/in/justin-ryals-a61627371/)  
📧 For usage or licensing inquiries, please contact the author directly.
