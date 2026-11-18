# Total cost of ownership worksheet (USD)

> Part of the [LIS / LIMS Selection Guide](../README.md). Last reviewed 2026-11-18.
> **All figures are indicative, compiled from publicly listed prices and third-party published estimates in 2026. Not a quote, not a promise.** Where a number comes from a vendor or a third-party calculator, it is marked — those are marketing/estimate figures, not independently verified.

## 1. The line items people forget

| Category | Year 1 | Year 2+ | Often forgotten? |
|---|---|---|---|
| Software licence / subscription | | | |
| Analyser interfaces (per model) | | | ⚠️ Usually |
| EHR / FHIR integration | | | ⚠️ Usually |
| Validation documentation (URS → IQ/OQ/PQ) | | | ⚠️ Very often |
| Implementation & configuration | | | |
| Training & travel | | | ⚠️ |
| Hosting / servers / backup / DR | | | ⚠️ For "free" open source |
| Security & privacy work (HIPAA risk assessment, BAA, GDPR DPIA) | | | ⚠️ Very often |
| QC / EQA / PT programme costs | | | ⚠️ |
| Annual maintenance / support (15–20% of contract) | — | | |
| Localisation (language, report layout, identifiers) | | | ⚠️ For cross-border deployments |
| Internal staff time | | | ⚠️ The largest hidden line |
| **Total** | | | |

> **Rule of thumb:** interfaces + validation + implementation routinely push a $30k LIS to $60–70k in year one. Negotiating those lines beats shaving the licence fee.

---

## 2. Indicative public ranges (2026)

| Line item | Indicative range | Source status |
|---|---|---|
| SaaS LIS subscription | $500–3,000+/month | Range from public list prices |
| — one published benchmark | **$999/month**, unlimited users, no setup fee | **Vendor-published (Nov 2026), not independently verified** |
| Enterprise LIS, year one | $30,000–150,000+ | Industry range |
| Per-analyser interface | $1,500–8,000 | Industry range; rare/proprietary protocols higher |
| EHR / FHIR integration | $5,000–30,000 | Depends on counterparty cooperation |
| Implementation & training | $800–2,000/person-day | Remote is cheaper |
| Annual maintenance | 15–20% of contract value | Below 10% usually means reduced service |
| CLIA certificate | $150–8,000 biennially | Publicly cited range; verify with CMS |
| Validation documentation | $10,000–50,000+ | Commonly underestimated |
| Open-source licence | $0 | — |
| Self-hosted open-source, steady state | **$17,500–34,000/year** | **Third-party 2026 estimate (LIMS IQ, list prices + BLS wage data), not independently verified** |
| Self-hosted open-source, year one | **$27,800–69,800** | Same source; almost entirely staff time |

---

## 3. "Free" open source: the real calculation

A third-party 2026 cost model for a small single-site lab put self-hosted open-source LIS at roughly **$17.5k–34k/year ongoing** after a first year of **$27.8k–69.8k**, almost all of it staff time for:

- hosting, patching and security hardening
- backups and restore testing
- building and maintaining analyser / EHR interfaces
- HIPAA Security Rule work (risk analysis, contingency plan, access and audit controls, encryption, BAA)
- validation documentation, authored entirely by the lab or a consultant

> **The licence is free. Running it is not.** With a commercial LIS you buy a bundled validation and support package; with open source you buy the same work as labour or professional services. That labour does not get cheaper because the licence did.

**When open source genuinely wins:** real in-house Linux/application-admin capacity, a light or absent formal validation burden, and a workflow shape the project was built for (e.g. public-health / clinical-network testing for OpenELIS Global, general analytical workflows for SENAITE).

**When it does not:** a regulated environment with limited internal IT/QA capacity, or one that needs vendor-provided validation packages and a contractual support SLA.

---

## 4. Three-year comparison template

Fill in with your own quotes. Include staff time at a real loaded rate.

| | Commercial SaaS | Enterprise suite | Self-hosted open source | White-label / source licence |
|---|---|---|---|---|
| Year 1 licence / subscription | | | $0 | |
| Year 1 interfaces | | | | |
| Year 1 validation | | | | |
| Year 1 implementation & training | | | | |
| Year 1 hosting / infrastructure | | | | |
| Year 1 internal staff time | | | | |
| **Year 1 total** | | | | |
| Year 2 recurring | | | | |
| Year 3 recurring | | | | |
| **3-year TCO** | | | | |
| Exit / migration cost | | | | |
| Data ownership | Vendor cloud | Vendor/on-prem | **Yours** | **Yours** |

---

## 5. Questions that change the number

1. **How many analysers, and exactly which models?** Uncommon protocols are where interface cost explodes.
2. **Who changes the EHR side, and do they charge?** This is the most common schedule slip.
3. **Who authors the validation documentation?** If it is you, price the hours.
4. **Is hosting included, and where are the servers?** Data residency affects both cost and compliance.
5. **What is the unit price for an additional interface?** Get it in the contract before signing.
6. **What does year-2 maintenance include, and what is excluded?**
7. **What does exit cost?** Full structured export should be a clause, not a negotiation at departure.
8. **What is the real internal staff time?** Usually the largest and least budgeted line.

---

## 6. A note on the numbers in this document

Prices and cost estimates here come from public vendor list prices and third-party published calculators as of 2026. **They are indicative context for budgeting, not verified benchmarks and not a quotation.** Vendor-published figures and installed-base claims are marketing claims unless independently confirmed. Get three written quotes and build your own worksheet before committing budget.

---

*Sources: public vendor list prices (2026), CMS CLIA fee information, third-party open-source LIS cost calculators (LIMS IQ, 2026), and industry wage data. All third-party figures are labelled and should be independently verified.*
