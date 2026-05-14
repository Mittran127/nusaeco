# NusaEco — Procurement Sustainability Co-pilot
 
> AI-powered Scope 3 emissions analysis for procurement teams. Upload your supplier CSV, ask questions in plain English, get instant auditable insights.
 
**🔗 Live tool:** https://mittran127.github.io/nusaeco
 
---
 
## What is NusaEco?
 
NusaEco is a free AI co-pilot built for sustainability analysts and procurement managers who need to understand their Scope 3 supplier emissions — without expensive software or complex data engineering.
 
CSRD (Corporate Sustainability Reporting Directive) now requires large companies to report Scope 3 Category 1 emissions (purchased goods and services) with an audit trail. Most procurement teams are still managing this in Excel, chasing suppliers for data in inconsistent formats and struggling to fill gaps where suppliers haven't reported yet.
 
NusaEco solves the analysis layer — upload your supplier data, ask questions in plain English and get structured insights instantly.
 
---
 
## Features
 
- **Conversational analysis** — ask questions like "which 3 suppliers account for 80% of my Scope 3?" or "give me a CSRD readiness summary" in plain English
- **DEFRA EEIO 2023 gap-filling** — for suppliers with no reported emissions, NusaEco automatically estimates using the UK Government's official supply chain emission factors, citing the exact factor and calculation for auditability
- **Smart column detection** — works with any CSV format, detects common column name variations automatically (spend, annual_spend_gbp, budget etc.)
- **Currency parsing** — handles £, $, € symbols and comma-formatted numbers
- **Data quality scoring** — assesses each supplier's data quality on a 0–100 scale based on GHG Protocol methodology
- **Daily usage limit** — 5 free questions per day per user
- **No data storage** — your CSV is processed in the browser and never stored anywhere
- **CSRD aligned** — built around GHG Protocol Scope 1, 2, and 3 methodology and CSRD Category 1 requirements
---
 
## How to use it
 
**1. Prepare your supplier CSV**
 
Your CSV can use any column names — NusaEco detects them automatically. Recommended columns:
 
| Column | Description | Example |
|--------|-------------|---------|
| supplier_name | Supplier company name | Acme Materials Ltd |
| sector | Industry sector | Manufacturing |
| annual_spend_gbp | Annual spend in £ | 250000 |
| scope1_tco2e | Scope 1 emissions (tCO₂e) | 850 |
| scope2_tco2e | Scope 2 emissions (tCO₂e) | 410 |
| scope3_tco2e | Scope 3 emissions (tCO₂e) | |
| questionnaire_responded | Has supplier responded? | Yes / No |
| data_quality_score | Data quality 0–100 | 65 |
| has_reduction_target | Reduction target? | Yes / No |
| verified | Third-party verified? | Yes / No |
| reporting_year | Data reporting year | 2023 |
 
Missing columns are handled gracefully — NusaEco works with whatever data you have.
 
**2. Upload and analyse**
 
- Visit https://mittran127.github.io/nusaeco
- Upload your CSV using the upload zone
- Ask any question about your supplier emissions data
**3. Try the demo**
 
No supplier data? Download the demo CSV with 20 fictional UK suppliers:
[demo_suppliers.csv](demo_suppliers.csv)
 
---
 
## Example questions to ask
 
- *"Which suppliers account for 80% of my total Scope 3 emissions?"*
- *"Who hasn't responded to the questionnaire and what is our spend at risk?"*
- *"For every supplier with no emissions data, estimate their Scope 3 using DEFRA EEIO factors"*
- *"Give me a CSRD readiness summary across my supplier base"*
- *"Which suppliers have low data quality scores but high annual spend?"*
- *"Draft a follow-up email for suppliers who haven't responded, referencing CSRD requirements"*
- *"Which suppliers are in high-emission intensity sectors with no reduction target?"*
- *"What is my total Scope 3 Category 1 footprint including DEFRA-estimated gaps?"*
---
 
## How DEFRA EEIO estimation works
 
When a supplier hasn't reported emissions data, NusaEco estimates using the **DEFRA EEIO (Environmentally Extended Input-Output) supply chain emission factors** — published annually by DESNZ/DEFRA as part of the UK Government Greenhouse Gas Conversion Factors.
 
**Method:** Annual spend (£) × sector emission factor (kgCO₂e/£) ÷ 1,000 = estimated tCO₂e
 
**Example:**
> Greenfield Packaging Ltd — no reported data.
> DEFRA estimate: £182,000 × 1.18 kgCO₂e/£ (Fabricated metal products, DESNZ/DEFRA 2023 Annex 13) ÷ 1,000 = **214.8 tCO₂e**
> *GHG Protocol Tier 3 spend-based method — indicative only*
 
This is the GHG Protocol **Tier 3 spend-based method** — valid as an interim estimate where primary activity data is unavailable, and accepted under CSRD for non-material suppliers.
 
**Source:** DESNZ/DEFRA Greenhouse Gas Conversion Factors 2023, Annex 13 — Supply chain (scope 3) emission factors by SIC category.
 
---
 
## Data quality scoring
 
NusaEco scores each supplier's emissions data on a 0–100 scale:
 
| Score | Level | Description |
|-------|-------|-------------|
| 80–100 | High | Activity-based data, third-party verified, GHG Protocol compliant |
| 60–79 | Acceptable | Activity-based data, self-reported, reasonable methodology |
| 40–59 | Estimated | Spend-based or rough estimates |
| 20–39 | Poor | Very limited data, unclear methodology |
| 0–19 | Insufficient | No usable data |
 
---
 
## Regulatory context
 
**CSRD (Corporate Sustainability Reporting Directive)**
Mandatory for large EU companies from FY2024. Requires Scope 3 Category 1 (purchased goods and services) reporting with audit trail. UK companies supplying EU customers are indirectly affected.
 
**GHG Protocol**
The global standard for corporate carbon accounting. NusaEco follows GHG Protocol methodology for Scope 1, 2, and 3 classification, Tier 3 spend-based estimation, and data quality assessment.
 
**SBTi (Science Based Targets initiative)**
Gold standard for supplier reduction targets — targets validated as aligned with 1.5°C pathways. NusaEco flags which suppliers have SBTi commitments.
 
---
 
## Technical architecture
 
```
User browser (GitHub Pages)
        ↓
Cloudflare Worker (rate limiting + API proxy)
        ↓
Anthropic Claude API (claude-sonnet-4-5)
```
 
- **Frontend:** Single HTML file hosted on GitHub Pages
- **Backend:** Cloudflare Worker — API key never exposed to client
- **Rate limiting:** 5 free questions per IP per day via Cloudflare KV
- **Data processing:** All CSV parsing happens client-side in the browser
- **No database:** No user data is stored anywhere
---
 
## Disclaimer
 
NusaEco is a **beta tool for indicative analysis only.**
 
- DEFRA EEIO spend-based estimates are directional (GHG Protocol Tier 3) and must be replaced with supplier-reported activity data before formal CSRD or sustainability report submission
- Results should be verified by a qualified sustainability professional before use in board reports or regulatory filings
- Do not upload data classified as confidential under your organisation's data policy
- CSV data is processed via Anthropic's API and is not stored or used for AI training
---
 
## Built by
 
**Mittran Krishanan** — Process & Sustainability Engineer | Procurement Decarbonisation | CSRD
 
Currently exploring opportunities in UK sustainability and ESG reporting.
 
🔗 LinkedIn: https://www.linkedin.com/in/mittrankrishanan/
🌱 Live tool: https://mittran127.github.io/nusaeco
 
---
 
## Roadmap
 
- [ ] Update to DEFRA EEIO 2025 factors
- [ ] PDF report export
- [ ] Supplier questionnaire tracking
- [ ] Multi-user accounts with data persistence
- [ ] SBTi target validation
- [ ] Multi-language support (French, German for EU CSRD)
---
 
## Feedback
 
This is a work in progress built in public. Feedback, bug reports and feature suggestions are very welcome — open an issue or connect on LinkedIn.
 
If you work in procurement sustainability, ESG reporting or supply chain decarbonisation and find this useful, I'd love to hear how you're using it.
