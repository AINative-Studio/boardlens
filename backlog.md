# 📋 **BoardLens MVP – Agile Backlog**

| **Epic ID** | **Epic Title** | **Story ID** | **Story Title** | **Description** | **Estimation** |
| --- | --- | --- | --- | --- | --- |
| epic-1 | Company + Meeting Management | 1.1 | Create Company record schema in ZeroDB KV | As a backend developer, I want to define and store company metadata in ZeroDB KV so that each company is uniquely identifiable and queryable. | 1d |
| epic-1 | Company + Meeting Management | 1.2 | Build BoardMeeting data model (KV) and seed sample data | As a backend developer, I want to model board meeting metadata and store it in ZeroDB so we can track meetings across time. | 1d |
| epic-1 | Company + Meeting Management | 1.3 | Implement CLI or REST endpoint for company/meeting management | As a developer, I want to create an interface to interact with company and board meeting records for dev/test usage. | 1d |
| epic-1 | Company + Meeting Management | 1.4 | Build admin UI: company list + meeting timeline | As a user, I want to view companies and their board meeting timelines on a dashboard UI. | 2d |
| epic-2 | Document Upload + Embedding Pipeline | 2.1 | Integrate file upload interface (PDF/PPTX/Docx) | As a user, I want to upload board materials through a UI so they can be embedded and parsed. | 1d |
| epic-2 | Document Upload + Embedding Pipeline | 2.2 | Generate embeddings and store in ZeroDB Vectors | As a backend AI engineer, I want to extract embeddings from board documents and store them for semantic search. | 1d |
| epic-2 | Document Upload + Embedding Pipeline | 2.3 | Persist metadata + document refs in ZeroDB KV | As a backend developer, I want to store metadata about uploaded documents for later lookup and display. | 0.5d |
| epic-2 | Document Upload + Embedding Pipeline | 2.4 | Render uploaded documents with tag filters | As a user, I want to view uploaded documents and filter them by tag or type on the UI. | 1d |
| epic-3 | KPI Extraction + Comparison | 3.1 | Build LLM agent to extract KPIs from deck text | As an AI engineer, I want to extract key performance indicators from board materials using a language model. | 2d |
| epic-3 | KPI Extraction + Comparison | 3.2 | Save KPI_MemoryBlock (forecast) to ZeroDB KV | As a backend developer, I want to persist forecasted KPIs for tracking and comparison. | 1d |
| epic-3 | KPI Extraction + Comparison | 3.3 | Fetch actual KPIs from OpenCap APIs | As a backend engineer, I want to fetch structured performance data from OpenCap to validate forecasts. | 1d |
| epic-3 | KPI Extraction + Comparison | 3.4 | Render forecast vs actual with % delta | As a user, I want to see forecasted vs actual KPIs for each company in a clear visual format. | 1.5d |
| epic-4 | Summary Generation + Memory Storage | 4.1 | Generate board meeting summaries using LLM | As an AI developer, I want to generate natural language summaries of board meetings to aid investor recall. | 1d |
| epic-4 | Summary Generation + Memory Storage | 4.2 | Store meeting summaries in ZeroDB KV + Vectors | As a backend developer, I want to persist summaries in both memory and vector form for later retrieval. | 0.5d |
| epic-4 | Summary Generation + Memory Storage | 4.3 | Build summary recall/search UI (last 3 meetings) | As a user, I want to use AI to recall key highlights across past meetings. | 1d |
| epic-5 | Prompt Engine + Pattern Queries | 5.1 | Integrate ZeroDB Prompt Engine for query support | As a developer, I want to add a prompt-based query interface for semantic questions. | 0.5d |
| epic-5 | Prompt Engine + Pattern Queries | 5.2 | Create reusable prompt templates for investors | As a product owner, I want to define reusable semantic prompts like 'missed targets' or 'burn increase'. | 0.5d |
| epic-5 | Prompt Engine + Pattern Queries | 5.3 | Implement prompt console UI | As a user, I want to enter prompts and view ZeroDB search results in a readable layout. | 1.5d |
| epic-6 | Alerts + Dashboards | 6.1 | Add alert rules for key risk patterns | As a product engineer, I want to define and detect common portfolio performance risks. | 1d |
| epic-6 | Alerts + Dashboards | 6.2 | Display alert flags on portfolio grid | As a user, I want to quickly scan company status using alert indicators. | 1d |
| epic-6 | Alerts + Dashboards | 6.3 | Build health heatmap UI for all companies | As a VC partner, I want to visually assess the portfolio’s health across key metrics. | 1.5d |

---
