# ⚡ NEXUS ERP — AI Dashboard Intelligence

> **Transform unstructured business data into board-ready dashboards in seconds.**  
> Upload any Excel, CSV, or raw text — the RAG-powered AI engine auto-detects structure, extracts KPIs, and generates interactive visualizations with one-click export to Excel, PDF, and PowerPoint.

---

## 📸 Overview

NEXUS ERP is a single-file React MVP that acts as an AI-powered ERP dashboard generator. It ingests raw, unstructured data from any department — Sales, HR, Operations, Finance, Marketing, Supply Chain, IT, or Executive — and uses a multi-pass Claude RAG pipeline to produce professional, interactive dashboards suitable for board-level presentations.

---

## ✨ Features

### 🔍 Data Ingestion
- **Excel upload** (`.xlsx`, `.xls`) — full SheetJS binary parsing with multi-sheet support
- **CSV / TSV / TXT** file upload or drag-and-drop
- **Paste raw data** — unstructured text, mixed formats, copy-pasted spreadsheet rows
- **Auto-structure detection** — no clean headers required; handles truly unstructured layouts

### 🧠 RAG AI Engine (2-Pass Pipeline)
| Pass | What it does |
|------|-------------|
| **Pass 1** | Ingests all sheets, detects department, extracts real KPIs, builds 5 charts with actual data values, identifies insights and recommendations |
| **Pass 2** | Generates a CFO-quality board narrative from the extracted metrics |

### 📊 Interactive Dashboard
- **5 tabs:** Overview · Charts · Insights · Executive · Raw Data
- **KPI cards** with trend indicators and period-over-period change
- **5 chart types:** Area, Bar, Line, Pie, Radar (auto-selected per data type)
- **AI Insights panel** — positive/negative/alert classifications with emoji
- **Strategic Recommendations** grounded in real data patterns
- **Data Quality Score** with completeness reporting

### 📤 One-Click Exports
| Format | Contents |
|--------|----------|
| **Excel (.xlsx)** | 5 sheets: Executive Summary, KPI Dashboard, Chart Data, Insights & Actions, Original Source Data |
| **PDF Report** | Full board-formatted print layout — open in browser, Save as PDF |
| **PowerPoint (.pptx)** | 6 professional slides: Title, KPI Grid, Chart Tables, Insights, Recommendations, Executive Summary |

### 🏢 8 Department Profiles
Sales · HR & People · Operations · Finance · Marketing · Supply Chain · IT & Tech · Executive

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Framework | React 18 (single `.jsx` file) |
| Charts | Recharts (Area, Bar, Line, Pie, Radar) |
| Excel Parsing | SheetJS (`xlsx`) |
| Excel Export | SheetJS (`xlsx`) |
| PPT Export | PptxGenJS 3.12 (loaded from CDN) |
| PDF Export | Browser Print API (styled HTML window) |
| AI / RAG | Anthropic Claude (`claude-sonnet-4-20250514`) |
| Styling | Inline CSS + Google Fonts (Plus Jakarta Sans, IBM Plex Mono) |

---

## 🚀 Getting Started

### Prerequisites
- Node.js 18+
- An Anthropic API key — get one at [console.anthropic.com](https://console.anthropic.com)

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/your-username/nexus-erp-dashboard.git
cd nexus-erp-dashboard

# 2. Install dependencies
npm install

# 3. Add your API key
# The app calls the Anthropic API directly from the browser.
# Set your key in your environment or proxy setup (see Configuration below).

# 4. Start the development server
npm run dev
```

### Dependencies

```bash
npm install react react-dom recharts xlsx
```

For a Vite scaffold:

```bash
npm create vite@latest nexus-erp -- --template react
cd nexus-erp
npm install recharts xlsx
# Replace src/App.jsx with erp-dashboard.jsx
npm run dev
```

---

## ⚙️ Configuration

### API Key Setup

The app calls `https://api.anthropic.com/v1/messages` directly. In production, **never expose your API key in client-side code**. Use one of these approaches:

**Option A — Local dev proxy (recommended for development)**
```js
// vite.config.js
export default {
  server: {
    proxy: {
      '/api': {
        target: 'https://api.anthropic.com',
        changeOrigin: true,
        rewrite: (path) => path.replace(/^\/api/, ''),
        headers: { 'x-api-key': process.env.ANTHROPIC_API_KEY }
      }
    }
  }
}
```

**Option B — Environment variable via backend**  
Deploy a minimal Express/Next.js API route that forwards requests with the key server-side.

**Option C — Claude.ai Artifacts (zero-config)**  
Paste `erp-dashboard.jsx` directly into a Claude.ai artifact — the API key is handled automatically.

---

## 📁 Project Structure

```
nexus-erp-dashboard/
├── erp-dashboard.jsx     # Full application — single self-contained file
├── README.md
└── package.json
```

The entire application is intentionally a **single JSX file** for portability. It can be split into components as needed for production.

---

## 🗺️ How It Works

```
User Input (Excel / CSV / Raw Text)
        │
        ▼
┌─────────────────────────────┐
│   SheetJS Parser            │  Reads binary Excel, multi-sheet,
│   (all formats)             │  unstructured layouts
└────────────┬────────────────┘
             │  Raw row data + sheet names
             ▼
┌─────────────────────────────┐
│   RAG Pass 1 — Claude       │  Detects dept, extracts KPIs,
│   Data Analysis             │  builds chart data, finds insights
└────────────┬────────────────┘
             │  Structured JSON dashboard
             ▼
┌─────────────────────────────┐
│   RAG Pass 2 — Claude       │  Generates CFO board narrative
│   Narrative Generation      │  from extracted metrics
└────────────┬────────────────┘
             │
             ▼
┌─────────────────────────────┐
│   Interactive Dashboard     │  Overview / Charts / Insights /
│   (Recharts + React)        │  Executive / Raw Data tabs
└────────────┬────────────────┘
             │
             ▼
     Export: .xlsx / .pdf / .pptx
```

---

## 📋 Usage Guide

### 1. Upload Data
Drag and drop any `.xlsx`, `.xls`, `.csv`, or `.txt` file onto the drop zone — or click to browse. Multi-sheet Excel workbooks are fully supported.

### 2. Paste Raw Data
You can also paste CSV rows, unstructured numbers, or even describe your data in plain English:
```
Q1 sales $2.3M, Q2 $2.8M (+22%), top product Widget A at 40% revenue share,
headcount 142, pipeline $8.4M, churn rate 4.2%...
```

### 3. Select Department *(optional)*
Helps the AI focus its analysis. Leave blank for auto-detection.

### 4. Generate
Click **⚡ Generate AI Dashboard** — the RAG pipeline runs in ~10–15 seconds.

### 5. Explore
Navigate across tabs. Hover charts for detailed tooltips.

### 6. Export
- **Excel** — downloads immediately as `.xlsx`
- **PDF** — opens a print-ready window; use browser's "Save as PDF"
- **PowerPoint** — downloads as `.pptx` (allow pop-ups if prompted)

---

## 🧪 Sample Datasets

Four built-in sample datasets are included for instant testing:

| Sample | Department | Rows | Columns |
|--------|-----------|------|---------|
| Sales Q-Data | Sales | 12 months | Revenue, Target, Units, Returns, Region |
| HR Analytics | HR & People | 8 employees | Salary, Performance, Tenure, Satisfaction, Turnover Risk |
| Operations KPIs | Operations | 8 weeks | Efficiency, Downtime, Output, Defect Rate, OEE |
| Finance P&L | Finance | 6 quarters | Revenue, COGS, Gross Profit, EBITDA, Net Income, Cash Flow |

---

## 🔒 Security Notes

- API calls are made client-side in the current MVP — suitable for local use and Claude.ai Artifacts
- For production deployment, route all Anthropic API calls through a backend proxy
- No data is stored server-side; all processing is in-memory per session
- Excel files and text are sent directly to the Anthropic API for analysis

---

## 🗺️ Roadmap

- [ ] Backend API proxy for secure key management
- [ ] Multi-file upload and cross-file synthesis
- [ ] Persistent dashboard storage (save & reload sessions)
- [ ] Custom KPI targets and threshold alerts
- [ ] Google Sheets and live database connectors
- [ ] Scheduled report generation and email delivery
- [ ] White-label theming per organization
- [ ] Role-based access (Executive, Manager, Analyst views)
- [ ] Natural language Q&A on uploaded data

---

## 🤝 Contributing

Contributions are welcome. Please open an issue first to discuss what you'd like to change.

```bash
# Fork the repo, create a branch, make your changes
git checkout -b feature/your-feature-name
git commit -m "Add: your feature description"
git push origin feature/your-feature-name
# Open a Pull Request
```

---

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.

---

## 🙏 Acknowledgements

- [Anthropic Claude](https://anthropic.com) — RAG AI engine
- [Recharts](https://recharts.org) — chart visualizations
- [SheetJS](https://sheetjs.com) — Excel parsing and export
- [PptxGenJS](https://gitbrent.github.io/PptxGenJS/) — PowerPoint generation
- [Google Fonts](https://fonts.google.com) — Plus Jakarta Sans, IBM Plex Mono

---

<div align="center">
  <strong>Built with ⚡ NEXUS ERP · AI Dashboard Intelligence</strong><br/>
  <sub>Powered by Claude RAG · Multi-department analytics · Board-ready output</sub>
</div>
