# Fresh Market Hub: End-to-End BI Solution

End-to-end business intelligence (BI) solution design for a fictional Australian supermarket retailer. The project includes a weighted vendor evaluation framework, a Microsoft Fabric reference architecture, and demo dashboards built in Power BI and Qlik Sense.

> Developed as an individual capstone assessment for BUSA8031 (Master of Business Analytics), Macquarie University, Session 2, 2026.

---

## The business problem

Fresh Market Hub (FMH) runs stock, sales, staff and customer systems that were acquired or built at different times and were never integrated. Managers have no dashboards, so every question becomes a report request to the Data Department. FMH had started a BI project but needed a clear, evidence-based way to choose between the many vendors on the market.

## What this project delivers

1. **An evaluation framework** that combines five groups of sources into eight weighted criteria.
2. **A reference architecture** that names a specific product for every layer, from source systems to dashboards and custom reports.
3. **A comparison of vendors at every layer:** integration, data warehouse, governance, and four dashboard platforms.
4. **Working demos** in Power BI and Qlik Sense, built on the same measures so the comparison is fair.
5. **Recommendations** with conditions, a fallback option and a phased implementation roadmap.

---

## 1. Evaluation framework

| Source group | Role in the framework |
|---|---|
| Technology, organisation and environment (TOE) framework (Tornatzky & Fleischer, 1990; Puklavec et al., 2018) | Structure: technology, organisation and environment |
| Peer-reviewed BI research (Wixom & Watson, 2001; Işık et al., 2013; DeLone & McLean, 2003; Davis, 1989; Ain et al., 2019) | Most of the criteria content: integration, data quality, ease of use, actual use |
| ISO/IEC 25010:2023 | Completeness check against international software quality characteristics |
| Gartner Magic Quadrant 2026 and Forrester Wave Q2 2025 | Current market evidence, AI trends, vendor viability |
| Data warehousing theory (Sharda et al., 2018) | Back-end requirements |

**Criteria and weights:**

| # | Criterion | Weight |
|---|---|---|
| C1 | Functionality and interactivity | 20% |
| C2 | Ease of use | 15% |
| C3 | Integration | 15% |
| C4 | Governance and security | 15% |
| C5 | AI-assisted analytics | 10% |
| C6 | Scalability and reliability | 10% |
| C7 | Cost | 10% |
| C8 | Vendor viability and support | 5% |

Each option is scored from 1 to 5. As a sensitivity check, the totals are also recalculated with equal weights.

---

## 2. Recommended architecture

| Layer | Recommended | Alternatives compared |
|---|---|---|
| Integration (ETL) | Fabric Data Factory | Qlik Talend Cloud, Informatica IDMC, Fivetran |
| Data warehouse | Fabric Warehouse on OneLake (star schema) | Snowflake, Google BigQuery |
| Semantic layer | Power BI semantic model with row-level security | Within each dashboard platform |
| Dashboards and custom reports | Power BI (dashboards and paginated reports) | Qlik Sense, Tableau, Looker |
| Governance | Microsoft Purview with Entra ID | Collibra |

<!-- Add the architecture diagram: docs/architecture.png -->

## 3. Dashboard platform scores

| Platform | Weighted score | Equal weights |
|---|---|---|
| **Power BI** | **4.50** | 4.50 |
| Qlik Sense | 4.40 | 4.38 |
| Tableau | 4.15 | 4.13 |
| Looker | 3.80 | 3.75 |

Power BI leads on integration, governance and cost, while Qlik Sense was clearly easier to use. Because the margin is only 0.10, the recommendation depends on two conditions:
- FMH already uses Microsoft 365.
- FMH has fewer than about 59 report users, unless a Fabric F64 capacity turns out to be cheaper.

If either condition fails, the fallback is Qlik Cloud Analytics with Qlik Talend Cloud and Snowflake.

---

## 4. Demo dashboards

Both demos use the same core measures and return identical results (revenue $208,287, gross margin 29.8%).

**Power BI** (three pages)
- **Overview:** KPI cards, a monthly combo chart, a category treemap, a state map, and a field-parameter chart that lets users switch dimensions.
- **Store & Product:** a drill-down matrix and an AI decomposition tree.
- **Promotions & Operations:** a scatter plot, a stockout bar chart with conditional colours, and the Key influencers visual.

**Qlik Sense** (two sheets)
- Master measures, alternative dimensions, the associative selection model, a pivot table, a drill-down dimension, and an Insight Advisor analysis.

<!-- Add screenshots to docs/screenshots/ and reference them here, e.g.
![Power BI overview](docs/screenshots/powerbi_overview.png)
-->

---

## Repository structure

```
fresh-market-hub-bi-solution/
├── README.md
├── report/                # Final report (PDF), with personal details removed
├── docs/
│   ├── architecture.png
│   ├── framework.png
│   └── screenshots/       # Power BI and Qlik Sense screenshots
├── powerbi/
│   └── FMH_Power_BI_Demo.pbix
├── qlik/
│   ├── FMH_Qlik_LoadScript.qvs
│   └── FMH_Qlik_Demo.qvf
└── data/
    ├── FMH_Dataset.csv
    └── FMH_StarSchema.xlsx
```

## About the data

`data/FMH_Dataset.csv` is a synthetic retail dataset provided by Macquarie University for the BUSA8031 assessment. It contains 10,000 transaction lines from 2025 across 30 stores in all eight Australian states and territories, with 35 fields covering:

- **Transaction details:** ID, date, time, month, quarter, day of week, weekend flag.
- **Store details:** ID, name, city, state, location type, store size.
- **Product details:** ID, name, category, subcategory.
- **Pricing and promotion:** unit price, unit cost, quantity, discount, promotion type.
- **Financial results:** sales revenue, cost of goods, gross profit, profit margin.
- **Customer:** loyalty tier, age group, payment method, sales channel, fulfilment method, customer rating.
- **Operations and context:** return flag, stockout flag, weather.

`data/FMH_StarSchema.xlsx` holds the same data reshaped into one fact table and seven dimension tables, which the Qlik load script reads.

## How to reproduce the demos

- **Power BI:** open `powerbi/FMH_Power_BI_Demo.pbix` in Power BI Desktop (Windows), or upload it to the Power BI service.
- **Qlik Sense:** in Qlik Cloud, upload `data/FMH_StarSchema.xlsx` to your space, create an app, paste `qlik/FMH_Qlik_LoadScript.qvs` into the Data load editor, update the `lib://` path, and reload. Alternatively, import `qlik/FMH_Qlik_Demo.qvf`.

## Tools

Power BI (web service) · Qlik Cloud Analytics · DAX · Qlik script and set analysis · Microsoft Fabric (architecture design) · APA 7 referencing

## Author

Nhat Thanh Thuy Do, Master of Business Analytics, Macquarie University
