# RFP vendor scorecard (100 points)

> Part of the [LIS / LIMS Selection Guide](../README.md). Last reviewed 2026-11-18.
> Print and bring to the evaluation meeting. Score **evidence**, not the demo.

## Scoring rules

- Score only what you were **shown**. A promise scores 0 until an artefact exists.
- "Supported" without a screenshot, log export or live query = half credit at most.
- Any **disqualifier** (below) ends the evaluation regardless of total.
- Record the vendor's answer in the right-hand column so the score is auditable later.

| Vendor: | | Date: | | Evaluator: | |
|---|---|---|---|---|---|

---

## A. Interoperability evidence — 20 pts

| # | Item | Pts | What to see | Score | Note |
|---|---|---|---|---|---|
| A1 | Exportable local → LOINC mapping table (file you keep) | 5 | | | |
| A2 | Sample ORM/OML and ORU messages, with field mapping document | 4 | | | |
| A3 | FHIR R4 sandbox + capability statement + working Observation / DiagnosticReport | 4 | | | |
| A4 | Written list of **your exact analyser models** with protocol per model | 4 | | | |
| A5 | Bidirectional worklist/result, flat-file fallback, QC/calibration separation | 3 | | | |

## B. Audit trail & records — 20 pts

| # | Item | Pts | What to see | Score | Note |
|---|---|---|---|---|---|
| B1 | Field-level before/after trail, tamper-evident | 5 | | | |
| B2 | Corrected report preserving original value, author, time, reason | 4 | | | |
| B3 | E-signature at release, aligned to 21 CFR Part 11 | 3 | | | |
| B4 | Critical value: detection → notification → read-back → follow-up | 3 | | | |
| B5 | Restore test record + downtime/business-continuity record | 3 | | | |
| B6 | Change control: approval, pre-change backup, verification, sign-off | 2 | | | |

## C. QC & EQA — 12 pts

| # | Item | Pts | What to see | Score | Note |
|---|---|---|---|---|---|
| C1 | Westgard multi-rule evaluation + Levey–Jennings charts | 4 | | | |
| C2 | Out-of-control handling and corrective action workflow | 3 | | | |
| C3 | Block release of out-of-range / QC-failed results before release | 3 | | | |
| C4 | PT / EQA enrolment, deadlines, history, evaluation | 2 | | | |

## D. Regulatory fit — 15 pts

| # | Item | Pts | What to see | Score | Note |
|---|---|---|---|---|---|
| D1 | Written mapping to **your** regime, naming the exact certificate type / accreditation body / country | 5 | | | |
| D2 | Named national profile conformance (e.g. US Core, AUCDI R2, SPIA, My Health Record) | 3 | | | |
| D3 | HIPAA/GDPR controls: role matrix, encryption, audit of exports, BAA/DPA willingness | 3 | | | |
| D4 | IVDR/MDR qualification statement: manages data only, or interprets raw signals? | 2 | | | |
| D5 | Validation documentation (URS → IQ/OQ/PQ) available | 2 | | | |

## E. Deployment & resilience — 10 pts

| # | Item | Pts | What to see | Score | Note |
|---|---|---|---|---|---|
| E1 | On-prem / self-host option with documented minimum footprint | 3 | | | |
| E2 | Offline / downtime mode with manual numbering and back-entry deadline | 3 | | | |
| E3 | Backup strategy + successful restore test evidence | 2 | | | |
| E4 | Multi-site data isolation, if relevant | 2 | | | |

## F. Exit & data ownership — 10 pts

| # | Item | Pts | What to see | Score | Note |
|---|---|---|---|---|---|
| F1 | Contract clause: full structured export including code mappings and audit history | 4 | | | |
| F2 | Documented format and fixed delivery timeframe, no punitive charge | 2 | | | |
| F3 | Source escrow / source-escape clause if vendor stops maintaining | 2 | | | |
| F4 | No per-record or hidden professional-services fee on exit | 2 | | | |

## G. Cost transparency — 8 pts

| # | Item | Pts | What to see | Score | Note |
|---|---|---|---|---|---|
| G1 | Itemised quote: licence, interfaces (how many, unit price for more), validation, training, year-2 maintenance | 4 | | | |
| G2 | Written exclusions list | 2 | | | |
| G3 | TCO projection over 3–5 years, including hosting and staff time | 2 | | | |

## H. Support & local capacity — 5 pts

| # | Item | Pts | What to see | Score | Note |
|---|---|---|---|---|---|
| H1 | Named implementation owner, response hours, language, time zone | 2 | | | |
| H2 | Training material, sign-in sheets, recorded sessions | 1 | | | |
| H3 | Two contactable references at comparable labs | 2 | | | |

---

## Disqualifiers (any one = stop)

- ❌ Claims the software is "ISO 15189 / CLIA / CAP / HIPAA certified"
- ❌ No written data-export / exit clause, or export offered only as PDF
- ❌ No validation documentation for an accredited environment
- ❌ Cloud-only with no BAA / DPA and no answer on data residency
- ❌ Refuses to provide an exportable LOINC mapping table
- ❌ No named reference you can actually contact

---

## Interpretation

| Total | Reading |
|---|---|
| 85–100 | Strong fit; proceed to contract negotiation, focus on exit and interface unit pricing |
| 70–84 | Viable with named gaps; put each gap into the contract as an acceptance item |
| 55–69 | Material risk on records or interoperability; request a remediation plan before shortlisting |
| < 55 | Do not proceed for an accredited / networked deployment |

## Three questions that expose more than the scorecard

1. "Show me a result from last month that was **corrected** — original value, author, time and reason."
2. "Show me the **last restore test** with its recorded outcome."
3. "If we leave in three years, what exactly do we receive, and does it include the **code mappings and audit history**?"

---

*Weighting reflects where accredited and networked LIS deployments most often fail: integration and evidence production, not feature breadth. Adjust weights for your own context, but keep the disqualifiers.*
