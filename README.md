# ⚡ Power BI MCP + Claude — Northwind Traders v2

> **v2 upgrade** of [powerbi-mcp-northwind](https://github.com/usman-analyst/powerbi-mcp-northwind)
> Adds PBIP format + PBIR visual generation + Git-native workflow

![Power BI](https://img.shields.io/badge/Power%20BI-PBIP%20Format-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Claude](https://img.shields.io/badge/Claude-Desktop-cc785c?style=for-the-badge)
![MCP](https://img.shields.io/badge/MCP-Model%20Context%20Protocol-00b4d8?style=for-the-badge)
![PBIR](https://img.shields.io/badge/PBIR-Preview-orange?style=for-the-badge)
![Windows](https://img.shields.io/badge/Windows-Only-0078D6?style=for-the-badge&logo=windows)

---

## 🆚 v1 vs v2 — What's new

| Capability | v1 | v2 |
|---|---|---|
| DAX measures via Claude | YES | YES |
| Date table, time intelligence | YES | YES |
| Model documentation | YES | YES |
| **Create report visuals** | NO | **YES** |
| **Position charts on a page** | NO | **YES** |
| **Git diff shows exact visual changes** | NO | **YES** |
| **AI writes visual.json files** | NO | **YES** |

---

## 🎯 What This Project Adds

v1 gave Claude access to the **semantic model** (DAX, tables, relationships).
v2 gives Claude access to the **report** (pages, visuals, layout) via:

- **PBIP format** — Power BI Project: every file is readable text, tracked by Git
- **PBIR format** — Each visual is a `visual.json` file Claude can generate
- **Filesystem MCP** — Second MCP server lets Claude write files to disk

---

## 🗂 Folder Structure

```
powerbi-mcp-northwindv2/
│
├── README.md
├── CHANGELOG.md                        ← AI session log
├── .gitignore
│
├── setup/
│   └── claude_desktop_config.json      ← TWO MCP servers (modeling + filesystem)
│
├── prompts/
│   ├── prompts_library_v2.md           ← All prompts including PBIR
│   └── pbir_visual_prompts.md          ← Visual-specific quick reference
│
├── outputs/
│   ├── generated_dax_measures.md       ← From v1 (carried over)
│   ├── time_intelligence_dax.md        ← From v1 (carried over)
│   ├── calendar_table_dax.md           ← From v1 (carried over)
│   ├── model_documentation.md          ← From v1 (carried over)
│   └── pbir_visuals/                   ← NEW — generated visual JSON files
│
├── northwind.pbip                      ← Converted from v1 northwind.pbix
├── northwind.Dataset/                  ← All DAX + M code (auto-created on convert)
└── northwind.Report/                   ← All report files (auto-created on convert)
    └── pages/
        ├── Sales Overview/
        │   └── visuals/
        └── Product Analysis/
            └── visuals/
```

---

## 🏗 Architecture (v2)

```
Claude Desktop
      │
      ├── powerbi-modeling MCP ──► northwind.Dataset/  (DAX, measures, relationships)
      │
      └── filesystem MCP       ──► northwind.Report/   (pages, visual.json files)
                                         │
                                         ▼
                                  Power BI Desktop
                                  (auto-reloads on file change)
                                         │
                                         ▼
                                    Git commit
                                  (exact JSON diff)
```

**What leaves your machine:** Table/column names, measure formulas, visual definitions.
**What stays local:** Your actual data rows — never sent externally.

---

## ✅ Prerequisites

- [ ] Power BI Desktop — [Microsoft Store](https://aka.ms/pbidesktopstore)
- [ ] VS Code — [code.visualstudio.com](https://code.visualstudio.com)
- [ ] Claude Desktop — [claude.ai/download](https://claude.ai/download)
- [ ] Node.js — [nodejs.org](https://nodejs.org) ← NEW for filesystem MCP
- [ ] Windows 10/11 — MCP extension is Windows only
- [ ] Completed v1 setup (northwind model built and working)

---

## 🚀 Setup

### Step 1 — Convert northwind.pbix → northwind.pbip

1. Copy `northwind.pbix` from v1 folder to this folder
2. Open it in Power BI Desktop
3. `File → Options → Preview Features` → enable **Power BI Project (.pbip)**
4. `File → Save As` → **Power BI Project (.pbip)** → save to this folder
5. Confirm these folders appeared: `northwind.Dataset/` and `northwind.Report/`

### Step 2 — Configure Claude Desktop

1. Edit `setup/claude_desktop_config.json`
2. Replace `YOUR_USERNAME` with your Windows username
3. Replace `VERSION` in the powerbi-modeling path with your actual extension version
4. Copy the full config into: `Claude Desktop → File → Settings → Developer → Edit Config`
5. Fully restart Claude Desktop

### Step 3 — Verify both MCP servers

`Claude Desktop → File → Settings → Developer`
- `powerbi-modeling` → green ✅
- `filesystem` → green ✅

### Step 4 — Connect and build

```
Connect to northwind in Power BI Desktop
```

Then use prompts from `prompts/prompts_library_v2.md` to build report pages.

---

## 🔐 Security

| Data | Sent to API? |
|------|-------------|
| Column/table names | ✅ Yes |
| Measure DAX formulas | ✅ Yes |
| Visual JSON definitions | ✅ Yes |
| **Actual data rows** | ❌ Never |

---

## ⚠️ Important Warnings

1. **PBIR is Preview** — do not use on production reports
2. **Git commit before every AI session** — `git add . && git commit -m "pre-session backup"`
3. **Verify all AI-generated visuals** — open in Power BI Desktop and test
4. **v1 folder is untouched** — this is a separate fresh repo

---

## 📚 References

- [Power BI Projects (PBIP) — Microsoft Docs](https://learn.microsoft.com/en-us/power-bi/developer/projects/projects-overview)
- [PBIR Schema — Microsoft](https://developer.microsoft.com/json-schemas/fabric/item/report/definition/visualContainer/2.0.0/schema.json)
- [Model Context Protocol — Anthropic](https://modelcontextprotocol.io)
- [v1 repo — powerbi-mcp-northwind](https://github.com/usman-analyst/powerbi-mcp-northwind)

---

*v2 upgrade by usman-analyst. PBIR status: Preview — verify at learn.microsoft.com/power-bi/developer/projects*