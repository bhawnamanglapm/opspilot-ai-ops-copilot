# OpsPilot — AI Operations Copilot

*⭐⭐⭐⭐⭐ Built · try the live demo*

> Exported from the portfolio page on 2026-10-19. The live page is the canonical version: https://bhawnamanglapm.github.io/travel-tech-more.html#case-ai-ops-copilot

- Confidence-based auto-approval, live threshold slider
- 6-stage pipeline: ingest → classify → parse → rules → review → case
- PII redaction + fraud/value guardrails
- Full audit log, every decision explained

**Tools used:** HTML/CSS/JS — self-contained interactive prototype, no framework or backend.

### Why This Exists

Every other AI project on this site is either a data-analysis dashboard (SQL, Amplitude, Power BI) or a customer-facing conversational copilot (the Travel Support AI Copilot). Neither one demonstrates the specific shape of AI product I actually shipped-adjacent work in at Bajaj Finance: an internal operations tool that triages a high-volume inbound queue, extracts structured data from unstructured text, and decides — with a human safety net — what can be auto-processed versus what a person has to look at. That's a real, common enterprise-AI pattern, and it wasn't represented here until now.

### The Scenario

**"Meridian Financial"** is a fictional NBFC (no real company, named or implied). Its partner-operations inbox receives a constant stream of emails: partners disputing a payout amount, resubmitting a rejected KYC document, or escalating an unresolved claim. Today that's a person reading every email, deciding what it is, pulling out the relevant details, and deciding what to do — the exact kind of repetitive, rule-governed decision that AI operations tooling is built for, and the same category of problem PCMS solved for payout *calculation* at Bajaj Finance, applied here to payout *correspondence* instead.

### My Approach

Built the full pipeline as a working prototype rather than a static mockup: an **LLM Classifier** stage that categorizes each email (Payout Dispute / KYC Resubmission / Claim Escalation / Irrelevant), a **Parser** stage that extracts structured fields, and a **Business Rules Engine** that decides auto-approval based on two independent signals: classifier confidence against a configurable threshold, *and* three hard guardrails that override confidence entirely (a payout above ₹2,00,000, a partner ID with an active fraud flag, or a duplicate claim reference number). The confidence threshold slider on the live demo is fully functional — dragging it re-runs the routing logic against all 14 sample cases in real time, the same lever an ops lead would actually pull in production to trade off automation coverage against review volume.

### Key Design Decisions

- **Confidence alone isn't the approval gate — confidence AND guardrails are.** A classifier can be 97% confident about a case that's still too risky to auto-approve (a large payout, a flagged partner). Modeling these as two separate, independently-overridable checks — not one blended score — is the difference between a demo that looks safe and a system that actually is.
- **PII gets redacted before it reaches any surface a human doesn't strictly need it on** — logs, dashboards, this demo included. The full unmasked value only ever exists inside the secure case record itself, not in anything an ops analyst scans while triaging a queue.
- **Every routing decision is explained, not just logged.** The audit log doesn't just say "approved" or "reviewed" — it states the exact reason (which threshold was cleared, or which specific guardrail fired), because an ops lead auditing a month of automated decisions needs to trust the "why," not just the "what."

### Recommendations

What I'd push for next if this were a real system, not a portfolio prototype:

- **Track guardrail-override rate as its own metric, separate from auto-approval rate.** A rising share of high-confidence cases getting caught by guardrails is an early signal worth watching on its own — it might mean fraud patterns are shifting, not just that guardrails are "working."
- **Route human review decisions back into a feedback loop.** Every case a human overturns or confirms is a labeled example; without feeding that back into the classifier, the system never gets better at exactly the cases it's currently worst at.
- **Set the threshold per category, not globally.** A 90% bar might be too conservative for well-formed KYC resubmissions and too loose for payout disputes — a single global slider is the simplest version of this control, not the final one.

### Where the Real Risk Sits

Same discipline as every other AI project here: the risk isn't the classifier being wrong sometimes — it's a wrong decision being *irreversible* and *unexplained*. The guardrails exist specifically to catch the cases where being wrong is expensive (a large payout, a flagged partner), and the audit log exists so a wrong auto-approval is never a mystery when someone has to unwind it. A system that's merely accurate isn't good enough here; it has to be accurate *and* legible.
  [  [image: OpsPilot dashboard: a 6-stage architecture pipeline (Email Ingestion through Automated Case Creation), KPI tiles (14 processed, 7 auto-approved, 7 to review, 88% avg confidence), a live confidence-threshold slider, a 14-row case queue with category badges and status pills, PII redaction and fraud-guardrail panels, and a full audit log]  ](https://bhawnamanglapm.github.io/projects/ai-ops-copilot/dashboard.html)

Click the screenshot to open the live, interactive demo — drag the confidence threshold and click any row to expand its routing reason (also available in dark mode).

### Quick recall

| Section | Summary |
|---|---|
| **Problem** | A partner-operations inbox gets a constant stream of emails (payout disputes, KYC resubmissions, claim escalations) that a person reads, categorizes, and extracts data from one at a time — the same repetitive, rule-governed decision pattern AI operations tooling exists for, and a real shape of AI product not yet represented elsewhere on this site. |
| **Research steps** | Built the full 6-stage pipeline (ingest → classify → parse → rules → review → case) as a working prototype rather than a static mockup → deliberately modeled approval as two independent, non-blendable checks (confidence threshold AND hard guardrails) instead of one combined score → redacted PII before it reaches any surface a human doesn't strictly need it on → made every routing decision state its specific reason, not just its outcome, since an ops lead auditing a month of decisions needs the "why." |
| **Solution** | OpsPilot — a confidence-gated triage pipeline with a live, functional threshold slider, 3 hard guardrails that override confidence entirely (large payout, flagged partner, duplicate claim), and a full audit log explaining every auto-approval or review routing. |
| **Conclusion** | The real risk was never the classifier being wrong sometimes — it's a wrong decision being irreversible and unexplained. A system here has to be accurate and legible; accuracy alone isn't enough when someone eventually has to unwind a bad auto-approval. |

### Which feature is used at which step

| Feature | Used at |
|---|---|
| **LLM Classifier** | Stage 2 — categorizes each inbound email (Payout Dispute / KYC Resubmission / Claim Escalation / Irrelevant) |
| **Parser** | Stage 3 — extracts structured fields from the classified email |
| **Confidence threshold slider** | Stage 4 (Business Rules Engine) — the lever an ops lead would actually pull to trade off automation coverage against review volume |
| **3 hard guardrails** | Stage 4, alongside confidence — override auto-approval regardless of confidence score on a large payout, a flagged partner, or a duplicate claim reference |
| **PII redaction** | Before anything reaches a dashboard, log, or this demo — the unmasked value only exists in the secure case record |
| **Audit log** | Stage 6 (case creation) — states the exact reason behind every routing decision for later review |

Link[live demo →](https://bhawnamanglapm.github.io/projects/ai-ops-copilot/dashboard.html) Image[dark-mode screenshot →](https://bhawnamanglapm.github.io/projects/ai-ops-copilot/screenshots/dashboard-dark.png)
