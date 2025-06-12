# 📆 Sprint Plan: **BoardLens MVP – Sprint 1 (14 Days)**

### 🎯 Sprint Goal

Deliver a working MVP that allows uploading board decks, parsing KPIs, storing summaries + data in ZeroDB, and visualizing portfolio company performance via OpenCap actuals + memory recall.

---

## 🔁 Sprint Cadence

- **Sprint Length**: 14 days
- **Daily Standup**: 15 mins
- **Demo + Retrospective**: End of Day 14
- **XP Practices**: TDD, Pair Programming (with AI agent), Continuous Integration

---

## 🧩 Sprint Breakdown: Epics → Stories

### **🧠 EPIC 1: Company + Meeting Management**

Build structured entities to manage companies and board meetings in ZeroDB.

| Story | Description | Owner | Est |
| --- | --- | --- | --- |
| #1.1 | Create `Company` record schema in ZeroDB KV | Backend | 1d |
| #1.2 | Build `BoardMeeting` data model (KV) and seed sample data | Backend | 1d |
| #1.3 | Implement REST endpoint or CLI to add/view companies + meetings | Backend | 1d |
| #1.4 | Build admin UI: company list + meeting timeline | Frontend | 2d |

---

### **📥 EPIC 2: Document Upload + Embedding Pipeline**

Enable uploading and vectorizing board materials.

| Story | Description | Owner | Est |
| --- | --- | --- | --- |
| #2.1 | Integrate file upload interface (PDF/PPTX/Docx) | Frontend | 1d |
| #2.2 | Generate embeddings via Claude or GPT + store in ZeroDB Vectors | Backend | 1d |
| #2.3 | Persist metadata + document references in ZeroDB KV | Backend | 0.5d |
| #2.4 | Render documents w/ tag filters on dashboard | Frontend | 1d |

---

### **📊 EPIC 3: KPI Extraction + Comparison**

Parse goals from board decks and compare with OpenCap actuals.

| Story | Description | Owner | Est |
| --- | --- | --- | --- |
| #3.1 | Build LLM agent to extract KPIs from text/PDF | Backend (AI) | 2d |
| #3.2 | Save `KPI_MemoryBlock` (forecast) to ZeroDB KV | Backend | 1d |
| #3.3 | Fetch actual KPIs from OpenCap (`/financial-reports/`, `/metrics/`) | Backend | 1d |
| #3.4 | Match and render forecast vs actual with % delta | Frontend | 1.5d |

---

### **🧠 EPIC 4: Summary Generation + Memory Storage**

Generate long-form meeting summaries and allow LLM recall.

| Story | Description | Owner | Est |
| --- | --- | --- | --- |
| #4.1 | Prompt Claude/GPT to summarize each board meeting | Backend (AI) | 1d |
| #4.2 | Store summary in ZeroDB Vector + KV | Backend | 0.5d |
| #4.3 | Add "Summarize last 3 meetings" NLP search field | Frontend | 1d |

---

### **🔍 EPIC 5: Prompt Engine + Pattern Queries**

Enable investors to ask semantic questions about patterns.

| Story | Description | Owner | Est |
| --- | --- | --- | --- |
| #5.1 | Integrate ZeroDB Prompt Engine | Backend | 0.5d |
| #5.2 | Create pre-defined prompt templates ("Find all companies that...") | Backend | 0.5d |
| #5.3 | UI for running prompts + displaying results | Frontend | 1.5d |

---

### **🚥 EPIC 6: Alerts + Dashboards**

Visual indicators and alerts based on trends/patterns.

| Story | Description | Owner | Est |
| --- | --- | --- | --- |
| #6.1 | Add alert rules (burn spike, missed targets) | Backend | 1d |
| #6.2 | Show alert icons on company tiles | Frontend | 1d |
| #6.3 | Build health heatmap for portfolio view | Frontend | 1.5d |

---

## 🧪 Test Plan (TDD/BDD Stories)

- Write tests for:
    - ✅ KPI parsing accuracy (unit tests)
    - ✅ Summary generator consistency
    - ✅ Prompt query resolution correctness
    - ✅ Vector search returns expected blocks
- Snapshot tests on:
    - Visual output of dashboard delta views

---

## 🧰 Dev Environment

- **Backend**: FastAPI, Python, Supabase (mocked OpenCap), ZeroDB SDK
- **Frontend**: React + Tailwind + shadcn/ui
- **AI Services**: LangChain + Claude/GPT-4o
- **Testing**: Pytest, React Testing Library
- **CI/CD**: GitHub Actions + Railway/Vercel

---

## 🧠 Velocity Assumptions

- **Total Developer Days Available**: ~20–22
- **Buffer (Bugs + Polish)**: 2 days
- **Target Stories to Ship**: ~25–30
- **Confidence**: MVP ready for demo within sprint ✅

---
