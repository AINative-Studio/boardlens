## 🖥️ **Frontend Product Requirements Document (PRD)**
Product Name: BoardLens
Platform: Web (Desktop + Tablet)
Tech Stack: React + Tailwind + shadcn/ui + Zustand or Redux for state
Data Sources: ZeroDB APIs (Vectors, KV, Prompt Engine), OpenCap APIs

--- ## 🧭 1. Navigation Structure ### Top Nav (Persistent)
Logo + Title
Search Prompt Field (AI/ZeroDB prompt engine)
Profile Dropdown (Settings, Log out)
### Side Navigation (Collapsible)
📊 Dashboard
🏢 Companies
🗓 Meetings
📁 Documents
📈 KPI Comparisons
🔍 AI Explorer
⚠️ Alerts
--- ## 🧱 2. Key Screens & Components --- ### 📊 A. Portfolio Dashboard
Goal: Overview of portfolio health, quick insights.

Components:

Portfolio Health Heatmap (company x metric matrix, colored R/Y/G)
Recent Alerts (AI-detected from ZeroDB)
Top Movers (best/worst forecast-to-actual deltas)
Board Timeline (last 3 meetings for each company)
--- ### 🏢 B. Company Profile View
Goal: Deep dive into each portfolio company

Route: /companies/:companyId

Sections:

Header: Name, Stage, Industry, OpenCap ID
KPI Trend Cards: MRR, Burn, Runway, GM, etc.
Cap Table Snapshot (fetched from OpenCap)
Meeting History (linked to /meetings/:meetingId)
Alert Log
--- ### 🗓 C. Meeting Viewer
Route: /meetings/:meetingId

Components:

Title bar: Meeting name, date, tags
Document preview (inline PDF viewer)
Summary Block (Claude/GPT summary)
KPI Delta Table (Forecast vs Actual)
Upload Notes / Comments (stored in ZeroDB KV)
Timeline Navigator (scroll through meetings)
--- ### 📁 D. Document Upload & Management
Route: /documents

Features:

Drag-and-drop upload (PDF, PPTX, DOCX)
Assign metadata: company, meeting, type, tags
AI Parsing Status + Summary preview
Document Table View: filterable by type, date, tags
--- ### 📈 E. KPI Comparison Table
Route: /kpis

Table Columns:

Company | Metric | Meeting | Forecast | Actual | % Delta | Source | Tags Features:
Filter by KPI type (MRR, Burn, etc.)
Filter by date range or company
Export to CSV/PDF
--- ### 🔍 F. AI Prompt Console
Route: /explorer

Function: Natural language querying via ZeroDB Prompt Engine

Example Prompts:

“Which companies have missed revenue targets twice?”
“Summarize all meetings for Company2 in 2024”
“Show meetings where burn increased but headcount shrank”
Components:

Prompt input bar
Result viewer (table + memory block highlights)
Save prompt to Favorites
--- ### ⚠️ G. Alerts Feed
Route: /alerts

Goal: Show auto-detected performance anomalies

Alert Types:

🔴 Missed KPIs (forecast-to-actual delta > threshold)
🟡 Runway shrinkage
🟢 Outperformance
🧠 LLM-generated red flag (summary sentiment = red)
Features:

Filter by company, severity
Dismiss / Resolve actions
Inline links to source meetings or KPIs
--- ## 🧩 3. UI Components (Modular)
CompanyCard
MeetingCard
KPITrendChart
KPIDeltaTable
PromptSearchBar
AlertBadge
DocumentUploader
SummaryBlock
TimelineScroller
--- ## 🧪 4. Testing Requirements
Unit: Component tests for inputs, dropdowns, tables
Integration: Form submission (upload, tag), document parsing preview
Snapshot: Summary blocks, heatmaps, prompt responses
--- ## 🧰 5. Dev Tools & Libraries
UI: [shadcn/ui](https://ui.shadcn.com)
Styling: Tailwind CSS
State: Zustand or Redux Toolkit
Querying: TanStack Query (for OpenCap, ZeroDB)
PDF Viewer: react-pdf
Charting: recharts or react-vis
Auth: Supabase Auth (or OpenCap-compatible JWT)
--- ## ✅ 6. MVP Must-Haves | Screen | Critical Components | | -------------------- | ------------------------------- | | Dashboard | Health heatmap, recent alerts | | Company Profile | KPI cards, meeting list | | Meeting Viewer | PDF + summary, KPI table | | KPI Comparison Table | Forecast vs actual view | | Document Upload | Upload + AI summary preview | | AI Prompt Console | Prompt input + semantic results | --- ## 🔜 Future Enhancements
Collaboration: Inline notes & comments
Voice search (prompt)
Email export: Auto-generate IC/LP-ready reports
AI-generated "Board Prep Packs"
