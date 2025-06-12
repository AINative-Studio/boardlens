**Project Title**: BoardLens

**Tagline**: AI-native performance intelligence for venture portfolios

**Version**: 0.1

**Infra Stack**: AI Native ZeroDB + OpenCap + LLMs (Claude/GPT-4o)

---

### 🧠 Executive Summary

**BoardLens** enables VC firms to monitor portfolio company performance by parsing and embedding board materials, comparing declared goals to actuals from [OpenCap](http://api.opencapstack.com) APIs, and surfacing trends using natural language queries. Powered by [**ZeroDB**](https://zerodb.ainative.studio), it gains fast memory recall, multimodal document indexing, and real-time KPI pattern discovery using vector + key-value infrastructure purpose-built for AI-native apps.

---

### 🧰 Infra Architecture Update

| Layer | Tool / API | Purpose |
| --- | --- | --- |
| Vector Store | `ZeroDB Vectors API` | Embed and retrieve board decks, summaries, KPIs |
| Memory Store | `ZeroDB Key-Value API` | Store parsed outputs, metadata, timestamps |
| Query Engine | `ZeroDB Prompt Engine` | Natural language interface to performance memory |
| LLM Layer | GPT-4o / Claude via LangChain | Semantic parsing, summary generation |
| Structured Data | `OpenCap APIs` | Financial metrics, cap table info, documents |

---

### 🔑 Feature Enhancements via Verified ZeroDB Capabilities

### 1. 📥 AI-Native Board Document Ingestion

- Upload PDF/PPTX → ZeroDB handles:
    - Embedding (`Vectors API`)
    - Parsed summaries and KPIs (`Key-Value API`)
- All documents stored with:
    - `company_id`, `meeting_date`, `doc_type`, `openCap_linked`

### 2. 🧠 KPI & Goal Memory Engine

- LLM extracts:
    - Revenue targets, Burn projections, Hiring plans
- Stored as:
    - `memory block` in Key-Value API
    - `semantic vector` for recall/querying

### 3. 🔍 AI Pattern Search with Prompt Engine

- Example:
    
    > “Which companies increased burn without revenue growth since Q3 2023?”
    > 
- Powered by: `ZeroDB Prompt Engine` → semantic search + filtered KPI snapshots

### 4. 📈 Goal vs Actual Tracking

- Pull actuals from:
    - `GET /financial-reports/`
    - `GET /metrics/history/`
    - `GET /share-classes/`
- Compare against ZeroDB memories:
    - Memory: `“Q4 2024: Target burn $400K, Target ARR $1.5M”`
    - Actual: `Burn $510K, ARR $1.1M → alert`

### 5. 🔁 Long-Term Memory for Board History

- Timeline of parsed meeting summaries
- AI recall:
    
    > “What goals has [Company X] missed more than twice?”
    > 
    > 
    > → Uses key-value + vector query history
    > 

---

### 🖥 Dashboard Modules (ZeroDB-Powered)

- **Board Timeline**: Board summaries rendered with linked KPI memories
- **Pattern Feed**: AI outputs alerts across companies (burn spikes, layoffs, dilution)
- **Prompt Console**: NLP search across memory (Claude/GPT over ZeroDB)
- **Portfolio Heatmap**: Color-coded tracker of red/yellow/green company health

---

### 📦 ZeroDB API Usage

| Capability | Method/Flow |
| --- | --- |
| Embed Board Deck | `POST /vector` w/ board file and tags |
| Store KPI Memory | `POST /kv` structured memory: company + date |
| Search KPI Drift | `POST /prompt` query: “companies with flat NRR” |
| Recall Last 3 Board Meetings | `GET /kv?tags=company_id` |
| Summarization Block Storage | `POST /kv` with parsed LLM output and metadata |

---

### 📅 MVP Build Scope (ZeroDB)

**Day 1**

- Document uploader (with tag UI)
- Vector + KV integration with ZeroDB
- LLM-based board summary + KPI extractor

**Day 2**

- Prompt search across summaries
- OpenCap API sync (actual vs projected)
- Dashboard: memory timeline + alerts

---
