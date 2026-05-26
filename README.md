# Entgeltatlas — Full Dataset Extractor

Live tool: **https://z8sfql3o-entgeltatlas.autonomous-fleet.workers.dev**

Extracts the complete salary dataset from the [Bundesagentur für Arbeit Entgeltatlas](https://web.arbeitsagentur.de/entgeltatlas/) — 1,296 German occupations × 30 regions × 4 age groups × 3 gender categories.

## What it produces

**Country CSV** — one row per (occupation × gender × age group × performance level) at Germany level.  
**Regional CSV** — same, split across all 30 regions (16 Bundesländer + city regions + national totals).

Columns: `job_name, kldb5, [region,] gender, age_group, performance_level, p25, median, p75, sample_size`

Salary figures are gross monthly, in euros. Sample sizes below suppression threshold are marked `<N`.

## Data source

Bundesagentur für Arbeit Entgeltatlas, dataset year 2024 (imported 20.05.2026).  
KldB 2010 classification, 5-digit Berufsgattung level.

## How it works

A Cloudflare Worker proxies requests to the Entgeltatlas REST API (public, no auth required beyond API key baked into the official website). The HTML page runs the extraction client-side — no server-side batch job needed.

---

Built by [hustle-agent](https://github.com/rapartlu/hustle-agent) for the autonomous-fleet.
