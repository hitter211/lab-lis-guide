# Buying a LIS for a Small or Community Laboratory: Spec Before You Shop

> Part of the [LIS / LIMS Selection Guide](../README.md). Last reviewed 2026-11-27.
> Written for laboratories running 20–150 samples a day with one to three analysers and a handful of staff — the size where most purchasing advice quietly stops being useful. This note is about **what to specify and how to buy**, not about price levels; for indicative ranges and a fill-in worksheet, see the [total cost of ownership worksheet](tco-worksheet.md).

---

## 1. The problem with "small lab" advice

Most LIS guidance is written for a 600-bed hospital: multi-site, 40 analysers, a dedicated IT department, an integration engine. A community laboratory reads it and concludes it needs a smaller version of that system. It usually does not. It needs a **narrower** system, and narrowing is a specification exercise, not a discount negotiation.

The failure mode is consistent across markets. A lab buys an entry-level product that covers result entry and report printing, then discovers during an inspection — or during its first accreditation cycle — that quality control records, result review history and audit trails were "available in the enterprise edition". The upgrade costs more than the difference would have cost at the start, and the migration is done under time pressure.

So the first question is not "what is the cheapest LIS". It is: **which records must this laboratory be able to produce on demand, and can the candidate system produce them?**

## 2. What a small laboratory actually needs

| Capability | Needed at 20–150 samples/day? | Why |
|---|---|---|
| Analyser connectivity (ASTM E1394 or HL7 v2) | Yes | Manual transcription is the main source of wrong results at low volume, because there is no second reader |
| Levey-Jennings QC with Westgard rules | Yes | required by any accreditation or licensing regime you are likely to face |
| Proficiency testing (EQA/PT) record keeping | Yes | the record, not the result, is what gets inspected |
| Critical value notification log | Yes | time-stamped, who was called, who took the call |
| Result review / electronic signature with role separation | Yes | distinguishes "entered" from "released" |
| Audit trail on result edits | Yes | the single most commonly under-specified item |
| Delta checks | Usually | valuable at low volume, cheap to configure |
| Microbiology susceptibility, blood bank modules | Rarely | buy as an add-on later if the service grows |
| Multi-site consolidation, reference-lab send-out portal | Not initially | adds configuration cost with no early benefit |
| Line-level interfacing to an automation track | No | not applicable |

The asymmetry is worth stating plainly: **functionality can be deferred; record-keeping cannot.** A deferred module is an invoice later. A missing audit trail is a finding at inspection, and findings are more expensive than invoices.

## 3. The regulatory lines that actually drive the specification

Requirements differ by jurisdiction, but three families show up almost everywhere and each one changes what you must buy.

**CLIA (United States).** CLIA is the floor, and it is mostly about records: test records, QC records, PT results, personnel records. The record-retention rule (42 CFR 493.1105) sets a two-year baseline for most records, with longer periods for certain specialties. In practice this means the LIS must retain and reproduce historical results and QC **without** relying on exports someone remembered to make. Ask vendors to show you a two-year-old QC chart, not a screenshot of last week's.

**CAP accreditation.** CAP adds checklist requirements around result review, critical value reporting, and computer-system validation. The practical consequence for a small lab is that the LIS needs documented validation at installation and after significant changes — and that documentation is a deliverable you should require in the contract, not something to assemble afterwards.

**ISO 15189.** ISO 15189:2022 has a dedicated laboratory information management requirement, covering validation of the system, protection and integrity of data, and continuity during downtime. Labs in 70+ countries are accredited against it, and in several markets it is effectively mandatory for reimbursement. Even where it is voluntary, the downtime requirement is the one that surprises small labs: you need a documented manual fallback, and the LIS has to support reconciliation when it comes back.

If you are unsure which regime applies, start from the [regulatory map](regulatory-map.md) and the [inspector evidence checklist](inspector-evidence-checklist.md) rather than from a vendor's compliance brochure.

## 4. Interfaces: where "small" stops being cheap

Two interfaces dominate the budget, and neither scales down as much as buyers expect.

**Analyser drivers.** Cost is per model, not per laboratory. Two identical analysers share a driver; two different models do not. Bidirectional communication (LIS sends sample IDs, analyser returns results) requires configuration on the analyser side and is often gated by the analyser vendor. At small volume, unidirectional is usually enough — but if you plan to add a second analyser of a different brand next year, price that driver now. It is cheaper to buy it in the initial scope.

**EHR / HIE integration.** In the US this is typically an HL7 v2 ORU^R01 feed to the EHR plus an order feed inbound; increasingly a FHIR R4 API for patient access and public-health reporting. Outside the US it may be an national or regional HIE profile. The cost driver is never the standard — it is **who has to change their system**. If the EHR vendor charges for the interface and the laboratory pays, that needs to be written down before signature.

> Interface scope in detail: [Interoperability checklist — LOINC, HL7 v2, FHIR R4, ASTM](interoperability-checklist.md).

## 5. Four procurement routes, and what each one really costs

**Route 1 — Inherited from a health system or network.** The laboratory joins a platform already operated by a parent organisation. Licence cost approaches zero; the cost is paid in scheduling and in scope. The community site typically receives a subset configured for the parent's workflow, and local requests queue behind enterprise priorities. Acceptable when the site is genuinely a spoke; frustrating when it is the only laboratory in a private clinic.

**Route 2 — Bundled by a local integrator.** A regional reseller supplies software, interfaces, deployment and support as one contract. This is the most common route in most markets and often the best one for a small lab, because the value is the person who answers the phone. The risk is lock-in: the software may be licensed by a third party, so switching integrators means rebuilding interfaces and re-exporting data.

**Route 3 — Open source, self-hosted.** Licence cost is zero; operations cost is not. A credible 2026 third-party estimate puts a self-hosted open-source LIS at roughly $27,800–69,800 in year one and $17,500–34,000 ongoing, dominated by staff time for hosting, patching, backups, interface building and security work (third-party published estimate, **not independently verified**). For a lab with in-house IT this can be excellent value. For a lab with one biomedical scientist and no server room, it is a second job.

**Route 4 — Subscription / SaaS.** Low entry cost, no server, predictable monthly line. Three clauses decide whether it is a good deal: what happens offline, who owns the data, and what the exit looks like. Ask for the export format in writing, and ask whether the export is included in the subscription or billed as a professional service.

## 6. Contract clauses worth more than the discount

1. **Data export**: complete, documented, machine-readable, at no additional charge, on request and at termination.
2. **Interface ceiling**: how many analyser drivers are included, the unit price beyond that, and whether proprietary protocols are priced differently.
3. **Change-of-scope rate**: the per-day rate for configuration work after go-live, fixed for at least three years.
4. **Support escalation**: response time by severity, and what "critical" means (a laboratory that cannot release results).
5. **Maintenance basis**: percentage of what, and a cap on annual increases.
6. **Validation documentation**: who produces the IQ/OQ/PQ or equivalent, and is it in scope.
7. **Price protection on renewal**: renewal pricing stated in numbers, not "then-current list price".

## 7. A short specification you can send to vendors

Send the same one page to every candidate and ask for a line-by-line response:

- Daily and peak sample volume, test menu, analyser list with model and protocol, current interface status
- Required records: QC, PT/EQA, critical values, audit trail, result review, retention period
- Regulatory regime you are subject to, and whether accreditation is planned within 24 months
- Interfaces in scope: analyser drivers (count and models), EHR orders and results, public-health reporting
- Deployment model: on-premise, hosted, or hybrid; downtime procedure expected of the LIS
- Training: days included, on-site or remote, and who is trained
- Response: included drivers, implementation days, maintenance basis, export terms

The responses will still not be directly comparable — that is what the [quote normalisation procedure](lis-quote-comparison.md) is for — but they will be comparable enough to eliminate two or three candidates in an afternoon.

## 8. Frequently asked questions

**Is a $500/month SaaS LIS enough for a community laboratory?**
Sometimes. It is enough when you have one or two analysers, standard test menus, and stable connectivity. It is not enough when you need CAP-grade validation documentation, a downtime procedure you can defend at inspection, or an interface to an EHR that the vendor has never integrated with.

**Can we run on the HIS module instead?**
A hospital information system's laboratory module typically covers order entry, result capture and report printing. It rarely covers analyser connectivity, Westgard QC, PT records or audit trails. If any of those are inspected in your jurisdiction — and in most they are — the module is a stopgap, not a system.

**Do we need bidirectional analyser communication?**
At 20–150 samples/day, usually not. Bidirectional matters when sample-ID assignment and rerun workflow become a bottleneck, or when you add an analyser that requires host query. Price it, but do not assume you need it on day one.

**How long does implementation take for a single-site laboratory?**
Typically four to twelve weeks for a single site with two or three analysers, of which the analyser drivers and validation documentation are the long poles. Any quote promising two weeks is either excluding validation or has done this exact configuration before.

**What is the most common mistake small labs make?**
Buying on the licence figure and discovering the interface, validation and audit-trail costs afterwards. The second most common is choosing a system with no export and finding out at the point of switching.

---

## Related reading

- [Total cost of ownership worksheet (USD)](tco-worksheet.md) — the line items to fill in before you talk to anyone
- [Why two LIS quotes are never comparable](lis-quote-comparison.md) — normalise bids before negotiating
- [RFP vendor scorecard (100 points)](rfp-scorecard.md) — turn this specification into scores
- [Inspector evidence checklist](inspector-evidence-checklist.md) — what an assessor will actually ask to see
- [Offline and low-resource deployment](offline-low-resource-deployment.md) — when connectivity cannot be assumed

---

**Disclosure**: the author provides LIS deployment and source-code licensing services. Cost figures cited above are third-party published estimates or indicative ranges, not quotations, and are marked accordingly. Regulatory statements are summaries only — verify against the published CLIA, CAP and ISO 15189 requirements that apply to your laboratory.
