---
title: "Nutrient: an API that turns PDFs, scans and Office files into structured data"
kind: "booth"
company: "Nutrient"
day: "2026-11-16"
summary: "Nutrient's Data Extraction API parses documents into JSON or Markdown and pulls named fields, with citations, against a schema you supply."
---

# Nutrient: an API that turns PDFs, scans and Office files into structured data

Booth visit: Nutrient · QCon SF 2026 · Mon Nov 16

> Nutrient's Data Extraction API parses documents into JSON or Markdown and pulls named fields, with citations, against a schema you supply.

## Key points

- Their page lists parse, extract, classify and split endpoints, with output that keeps coordinates, confidence scores and page context.
- The industries the page names include mortgages, healthcare and legal.
- The same engine is offered as a cloud API, a self-hosted SDK and a desktop app; with a local model, documents can stay on the machine. The page says cloud AI inference may run in the US.
- A free plan includes 5,000 credits a month; paid tiers are not priced on the page.

Booth, Monday Nov 16. Sources: Nutrient's Data Extraction API pages and docs, read Nov 17, 2026. Figures and claims are the vendor's own; I haven't tested them.

## What it is

Nutrient's Data Extraction API turns PDFs, scans, images and Office files into structured data. It parses documents to layout-aware JSON or Markdown and extracts named fields against a JSON Schema you supply, with a citation for each field.

## How it works

- **Endpoints.** `parse`, `extract`, `classify`, `split`, and forms detection and filling.
- **Modes.** Text, structure, understand and agentic, or auto-routing per page.
- **Output.** JSON with bounds, confidence and reading order, or Markdown for retrieval.

## Docs and getting started

- [Getting started](https://www.nutrient.io/guides/dws-data-extraction/getting-started/)
- [API reference](https://www.nutrient.io/api/reference/data-extraction/public/)
- [Privacy and data handling](https://www.nutrient.io/guides/dws-data-extraction/privacy/)
