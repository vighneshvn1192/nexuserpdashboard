# ⚡ NEXUS ERP — AI Dashboard Intelligence

Upload any Excel, CSV, or raw text — Claude analyzes it and generates an interactive,
board-ready dashboard with one-click export to Excel, PDF, and PowerPoint. See the **[demo](#)**.

## Quick Start
```bash
git clone https://github.com/your-username/nexus-erp-dashboard.git
cd nexus-erp-dashboard
npm install react react-dom recharts xlsx
npm run dev
```

Get a free API key at [console.anthropic.com](https://console.anthropic.com) and paste it in the app.

> **Shortcut:** Paste `erp-dashboard.jsx` into a Claude.ai artifact — no API key setup needed.

## How It Works
```
Excel / CSV / Raw Text
        ↓
Claude RAG (2-pass) — extracts KPIs, builds charts, writes board narrative
        ↓
Interactive Dashboard (5 tabs) → Export .xlsx / .pdf / .pptx
```

## License

MIT
