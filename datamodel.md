# 🧩 Custom Data Model: BoardLens

Below is a **detailed data model** for **additional fields we need to define ourself**, because they don’t exist directly in OpenCap or ZeroDB as-is — but they work *alongside* those APIs:

---

### 1. `BoardMeeting`

Used to track context around each board meeting for a company.

| Field | Type | Description |
| --- | --- | --- |
| `meeting_id` | UUID | Primary ID |
| `company_id` | UUID | Foreign key to OpenCap Company |
| `date` | Date | Meeting date |
| `document_ids` | List[str] | List of associated doc UUIDs (linked in ZeroDB) |
| `summary_id` | UUID | Reference to parsed summary block (ZeroDB KV ID) |
| `parsed_kpis` | List[Dict] | Forecasted KPIs parsed from deck |
| `tags` | List[str] | Labels like `Q1 2024`, `Budget`, etc. |
| `llm_flagged_risks` | List[str] | Optional risks extracted by LLM |
| `annotation_notes` | Text | Analyst/GP notes (stored via ZeroDB KV or internal) |

---

### 2. `KPI_MemoryBlock`

A bridge structure between parsed board data and OpenCap actuals.

| Field | Type | Description |
| --- | --- | --- |
| `kpi_id` | UUID | ID of the KPI memory |
| `company_id` | UUID | Foreign key |
| `meeting_id` | UUID | Link to board meeting |
| `label` | String | e.g., `MRR`, `Burn`, `Runway` |
| `value` | Float | Forecasted or actual |
| `type` | Enum | `"forecast"` or `"actual"` |
| `source` | String | `"board_deck"` or `"open_cap_api"` |
| `token_context_id` | UUID | For long-context memory traceability |
| `embedding_vector` | Vector | Stored in ZeroDB Vectors API |

---

### 3. `LLM_Summary`

Used for each board meeting or KPI cluster summary.

| Field | Type | Description |
| --- | --- | --- |
| `summary_id` | UUID | Unique ID |
| `company_id` | UUID | Foreign key |
| `meeting_id` | UUID | Optional, if summary is for one meeting |
| `text` | Text | Full AI-generated summary |
| `tone` | Enum | `"green"`, `"yellow"`, `"red"` based on sentiment |
| `memory_vector_id` | UUID | ZeroDB vector ID |
| `created_by_model` | String | Model used: `Claude-3.5`, `GPT-4o`, etc. |

---

### 4. `AlertRuleExecution`

Tracks pattern matches and AI-generated alerts.

| Field | Type | Description |
| --- | --- | --- |
| `alert_id` | UUID | ID of triggered alert |
| `company_id` | UUID | Affected company |
| `rule` | String | Natural language description or prompt |
| `matched_data` | Dict | Snapshot of data that caused the match |
| `date_triggered` | Date | When it happened |
| `severity` | Enum | `"info"`, `"warning"`, `"critical"` |
| `resolved` | Bool | If manually dismissed |

---

### 5. `SemanticPromptLog` (optional for traceability/debugging)

| Field | Type | Description |
| --- | --- | --- |
| `prompt_id` | UUID | Unique query ID |
| `user_id` | UUID | Who ran the prompt |
| `prompt_text` | Text | The input query |
| `results` | List | Retrieved documents or blocks |
| `timestamp` | Datetime | Query time |
| `runtime_ms` | Int | Performance logging |

---

## 🧠 How This Works with OpenCap & ZeroDB

| Data Type | Source System | Role |
| --- | --- | --- |
| Company, Cap Table, Financials | **OpenCap API** | Authoritative structured data |
| Board Decks, Summaries, KPI Memory | **ZeroDB** | AI-native memory + query layer |
| Meeting Metadata, Pattern Rules | **Boardlens App** | Custom logic layer |
| Search + Q&A + Summarization | **ZeroDB Prompt Engine + Claude/GPT** | NLP interface and pattern detection |

---

Since we will be implementing this **entire data model on ZeroDB**, which is API-first and AI-native, the traditional "SQL schema" format is less relevant. Instead, here’s how we should **present the BoardLens data model** for a ZeroDB-native implementation:

---

### 🔹 Format Style: Keyed by API Type

Structure your model around how each part of your data will be stored and queried via **ZeroDB's APIs**:

| Layer | ZeroDB API | Purpose |
| --- | --- | --- |
| Memory Store | `Key/Value API` | Persistent storage for structured fields (e.g., meetings, KPIs) |
| Search Layer | `Vector API` | Embeddings of full docs, summaries, KPI paragraphs |
| Query Layer | `Prompt Engine` | AI-native queries across memory or vector space |

---

## 📘 BoardLens ZeroDB Data Model (Presented by API Layer)

### 1. 🔑 **Key/Value Store**

> Stores structured objects (similar to rows in a database)
> 

### Example: `BoardMeeting`

```json
{
  "kv_namespace": "board_meeting",
  "key": "meeting:company1:2023-Q1",
  "value": {
    "company_id": "company1",
    "meeting_date": "2023-01-15",
    "document_ids": ["doc:deck:123", "doc:okr:456"],
    "tags": ["Q1 2023", "budget", "fundraising"],
    "summary_id": "summary:meeting:company1:q1",
    "annotation_notes": "Founder expects runway through Q3"
  }
}

```

### Example: `KPI_MemoryBlock`

```json
{
  "kv_namespace": "kpi_block",
  "key": "kpi:company1:2023-Q1:MRR:forecast",
  "value": {
    "company_id": "company1",
    "meeting_id": "meeting:company1:2023-Q1",
    "label": "MRR",
    "value": 145000,
    "type": "forecast",
    "source": "board_deck"
  }
}

```

---

### 2. 🧠 **Vector API**

> Stores embeddings for semantic search (e.g., board decks, summaries)
> 

### Example: `LLM_Summary` stored as vector + text

```json
{
  "vector_namespace": "summary_vectors",
  "id": "summary:meeting:company1:q1",
  "text": "In Q1 2023, Company1 missed revenue targets but secured a strategic partnership...",
  "metadata": {
    "company_id": "company1",
    "meeting_id": "meeting:company1:2023-Q1",
    "tone": "yellow"
  },
  "embedding": [0.134, 0.928, 0.501, ...]  // generated by Claude/GPT
}

```

### Example: `Board Deck Section Embedding`

```json
{
  "vector_namespace": "deck_sections",
  "id": "deck:company1:2023-Q1:slide5",
  "text": "Revenue target for Q1 was $150K. Actual: $118K. Burn exceeded budget by 22%.",
  "metadata": {
    "company_id": "company1",
    "slide_number": 5,
    "section": "financials"
  }
}

```

---

### 3. 🔍 **Prompt Engine**

> Used to run queries like:
> 

```json
{
  "prompt": "Which companies missed their runway target more than once?",
  "filter": {
    "namespace": "kpi_block",
    "label": "Runway",
    "type": "forecast"
  }
}

```

Or:

```json
{
  "prompt": "Summarize Company2’s board meetings where CAC exceeded $2,500",
  "filter": {
    "namespace": "summary_vectors",
    "company_id": "company2"
  }
}

```

---

## 🧱 Presentation Output Options

### Option 1: **Developer-Facing Spec (README)**

Organize like:

```markdown
## BoardLens ZeroDB Model

### 🧠 Memory: Key/Value API

- `board_meeting:<company>:<quarter>`
- `kpi_block:<company>:<quarter>:<label>:<type>`

### 🔍 Search: Vector API

- `summary_vectors`
- `deck_sections`

### 🔎 Query: Prompt Engine

- Query summaries and KPI memory blocks by natural language

```

---

### Option 2: **ZeroDB Seed File Format (JSON Lines)**

You can structure seed data like:

```
{"kv_namespace": "board_meeting", "key": "meeting:company1:2023-Q1", "value": {...}}
{"vector_namespace": "summary_vectors", "id": "summary:meeting:company1:q1", "text": "...", "metadata": {...}}
{"kv_namespace": "kpi_block", "key": "kpi:company1:2023-Q1:Burn:actual", "value": {...}}

```

**This data can be uploaded via a CLI, curl, or SDK.**
