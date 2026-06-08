# Project 3: Excel to AI Auto-Report Agent

## Quick Start (MVP Skeleton Included)

```bash
# cd "/Volumes/new/vibe code/work finding/new work/03-excel-ai-auto-report-agent"
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
cp -n .env.local.example .env.local
python main.py --input data/input/sample_sales.csv --no-email
```

If OpenAI key is not configured, the pipeline uses a fallback local summary.

## Current Folder Structure

```
03-excel-ai-auto-report-agent/
├── agent/
│   ├── config.py
│   ├── io_loader.py
│   ├── validate.py
│   ├── metrics.py
│   ├── summarizer.py
│   ├── report_writer.py
│   ├── email_sender.py
│   └── pipeline.py
├── data/
│   ├── input/sample_sales.csv
│   └── output/
├── scheduler/
│   ├── run_daily.sh
│   └── cron.example
├── docs/RUNBOOK.md
├── .env.example
├── requirements.txt
└── main.py
```

## 1) Goal

Build an automation agent that converts daily Excel reports into cleaned analytics, LLM summaries, and scheduled email outputs.

Core business value:
- save daily reporting time
- reduce manual spreadsheet errors
- provide consistent decision-ready summaries

## 2) Target Clients

- operations teams
- finance assistants
- ecommerce store owners
- Fiverr and Upwork buyers with repetitive reporting tasks

## 3) Architecture

Excel files
-> Python loader (Pandas)
-> validation and transformation
-> metric computation (SQL or Pandas)
-> GPT summary generation
-> report output (Excel or PDF)
-> email sender
-> scheduler (cron or Airflow)

Optional extension:
- PostgreSQL for history tracking
- FastAPI endpoint for trigger and status

## 4) Technical Stack

- Python
- Pandas
- SQL (optional with PostgreSQL)
- OpenAI API
- Airflow optional
- FastAPI optional for service mode

## 5) Data and Governance Design

- ODS: uploaded spreadsheet snapshots
- DWD: standardized tables by template
- DWS: daily and weekly KPI aggregates
- ADS: executive summary dataset and email-ready payload

Governance controls:
- data dictionary for each template column
- Great Expectations checks for nulls, duplicates, outliers
- lineage for source file to final KPI and narrative

## 6) Security and Compliance

- masking of personal fields in report output
- role-based report access
- optional encrypted archival storage
- run logs for traceability

## 7) AI Agent Features

- trend summary in business language
- anomaly explanation for KPI spikes or drops
- auto-generated next-step recommendations
- optional NL2SQL interface over stored metrics

## 8) Delivery Milestones

- Milestone 1 (Week 1): template parser and validation
- Milestone 2 (Week 2): KPI engine and report generator
- Milestone 3 (Week 3): GPT summary and email workflow
- Milestone 4 (Week 4): scheduler and deployment handoff

## 9) Marketplace Packages

Basic:
- one Excel template
- daily summary email
- 1 KPI dashboard table

Standard:
- multiple templates
- anomaly detection
- weekly and monthly summaries

Premium:
- API trigger mode
- role-based delivery
- deployment in client cloud environment

## 10) MVP Acceptance Criteria

- one-click pipeline from Excel upload to sent email
- report includes KPI table and AI summary
- invalid rows are captured in a validation log
- schedule runs reliably for 5 consecutive test days

## 11) Implemented in This Skeleton

- CSV and Excel ingestion with required column validation
- Data cleanup and invalid-row separation
- KPI computation by summary, region, and month
- AI summary generation with OpenAI and fallback mode
- Output artifacts (CSV, TXT, JSON)
- SMTP email sending (optional)
- Cron-friendly scheduler script
