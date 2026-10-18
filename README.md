# OpsPilot: AI operations copilot prototype

**Interactive prototype (HTML/CSS/JS).**

## In one minute

A prototype of an internal operations tool for a fictional NBFC ('Meridian Financial'). It triages a partner-operations inbox through a six-stage pipeline (ingest, classify, parse, rules, review, case). Auto-approval needs both classifier confidence above a threshold and no guardrail hit (payout above Rs 2,00,000, active fraud flag, or duplicate claim reference). A slider re-runs the routing against 14 sample cases.

## Links

- Portfolio case study: https://bhawnamanglapm.github.io/travel-tech-more.html#case-ai-ops-copilot
- Live prototype: https://bhawnamanglapm.github.io/projects/ai-ops-copilot/dashboard.html

## What is in this repo

| File | What it is |
|---|---|
| dashboard.html | Self-contained interactive prototype |
| screenshots/ | Light and dark screenshots |
| CASE_STUDY.md | The write-up, exported from the portfolio page |

## What is real, modeled or not verified

| Topic | Status |
|---|---|
| Scripted prototype | A search of dashboard.html found no network requests. The 14 sample cases and their 'classifier' results are fixed data in the page, not output from a live model. |
| Fictional company | Meridian Financial is invented. No real company data was used. |

## Provenance and credit

- Product owner, built with AI (Claude).
- Copied on 2026-10-19 from the `projects/ai-ops-copilot` folder of [bhawnamanglapm.github.io](https://github.com/bhawnamanglapm/bhawnamanglapm.github.io). The portfolio repo's commit history is not carried over, and the portfolio copy is unchanged.
- The portfolio repo is MIT-licensed. No separate licence file has been added here; that is the owner's decision.
