# Changelog — AI Session Log
**Project:** powerbi-mcp-northwind v2
**Dataset:** Northwind Traders (Kaggle — jeetahirwar/northwind-traders)

All AI-assisted changes are logged here.
Format: date · branch · what changed

---

## [Unreleased — v2 setup in progress]

### Setup tasks remaining
- [ ] Convert northwind.pbix → northwind.pbip
- [ ] Add filesystem MCP to claude_desktop_config.json
- [ ] Verify northwind.Dataset/ folder created after conversion
- [ ] Verify northwind.Report/ folder created after conversion
- [ ] First PBIR session — Sales Overview page visuals
- [ ] First PBIR session — Product Analysis page visuals
- [ ] Push v2 repo to GitHub as powerbi-mcp-northwindv2

---

## v1.0.0 — Completed (in powerbi-mcp-northwind)
**Repo:** github.com/usman-analyst/powerbi-mcp-northwind

### What was built in v1
- MCP connection established (Power BI Modeling MCP Server via VS Code)
- DimDate table created with fiscal year, sort columns, IsWeekend flag
- Base measures: Total Revenue, Total Orders, AOV, Units Sold, Freight, Discount %
- Customer measures: Total Customers, Avg Orders/Customer, Avg Revenue/Customer
- Product measures: Products Sold, Active/Discontinued, Avg Unit Price
- Employee measures: Total Employees, Revenue/Employee, Orders/Employee
- Time intelligence: MTD, QTD, YTD, PY, MoM%, YoY%, Rolling 3M, Rolling 12M
- Calculated columns: FreightBand, DeliveryStatus, LineTotalBand, PriceTier
- Column descriptions added to all 7 tables
- Full model documentation generated
- northwind.pbix uploaded to GitHub

### What v1 could NOT do (gaps fixed in v2)
- Could not create report pages or visuals
- Could not position charts on a page
- Could not write any report files
- No Git tracking of report changes