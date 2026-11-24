# Why two laboratory information system quotes are never comparable

> Part of the [LIS / LIMS Selection Guide](../README.md). Last reviewed 2026-11-24.
> This note is about **how to compare bids**, not about what a system should cost. For indicative ranges and a fill-in worksheet, see the [total cost of ownership worksheet](tco-worksheet.md). For the scoring instrument, see the [RFP vendor scorecard](rfp-scorecard.md).

---

## 1. The bids arrive in different units, and that is by design

A small private laboratory asks three vendors for a quotation on "a LIS for one lab, two analysers, one hospital interface". Three documents come back:

- Vendor A: a licence figure, a note that analyser drivers are "quoted per instrument after a site survey", and an annual support percentage.
- Vendor B: a bundle that includes four analyser drivers, training for eight users, and a three-year subscription — no perpetual option.
- Vendor C: a low headline number, with a separate price list for modules, and interfaces billed per protocol **and** per direction.

None of these is dishonest. Each is answering a different question. If you compare the headline numbers you will pick the cheapest document, not the cheapest project — and the gap usually reappears during implementation, when the scope is finally pinned down.

The purpose of this guide is to convert three incompatible documents into one comparable structure **before** you negotiate. That is a procurement task, not a technical one, and it takes an afternoon.

---

## 2. Build a scope baseline before you ask anyone for a price

Every normalisation effort fails for the same reason: there is no written scope to normalise against. Write one page containing:

| Baseline item | What to record | Why it changes the price |
|---|---|---|
| Analysers | Brand, model, port present (Y/N), protocol (ASTM / HL7 v2.x / vendor-proprietary), one-way or bidirectional | A proprietary protocol with no published frame spec is a reverse-engineering job, not a configuration task |
| Volume | Samples per day, peak hour, tests per year | Drives sizing, and often pushes you into a different licence tier |
| Integration counterparties | HIS/EMR product and version, regional or national reporting platform, reference lab | Whoever has to change their side controls the schedule |
| Regulatory scope | CLIA only, CAP accredited, ISO 15189, or a national scheme | Determines which validation and record artefacts must be produced and kept |
| Deployment | On-premise, hosted, offline/disconnected, or hybrid | Changes the security and backup work substantially |
| Users and sites | Named users or concurrent, single site or satellite collection points | Licence unit differs by vendor |
| Exit requirement | Must data be exportable in a defined format on termination? | Contracts without this clause are effectively permanent |

Send this baseline with the RFQ and require each vendor to respond **in the same row order**. This single instruction removes most of the ambiguity, and it also reveals which vendors actually read the document.

---

## 3. Five normalisation moves

### 3.1 Normalise the licence unit

Convert every bid to the same unit: cost per year, for the same user count and the same number of sites, over a five-year horizon. A perpetual licence plus 18% annual support and a subscription at a flat monthly rate are not comparable at year one — they diverge sharply by year five. Put both on one line and the difference becomes visible.

### 3.2 Demand an interface schedule, not an interface count

"Includes interfaces" is the single most expensive sentence in a laboratory IT contract. Replace it with a schedule: one row per analyser, with the protocol, the direction, the deliverable (driver, middleware, or manual workaround), and the party responsible for testing on the instrument.

Two instruments of the same model usually share most of the work. Two instruments from different manufacturers share almost none. A count hides this; a schedule does not.

### 3.3 Name the counterparty obligation

For every external interface, write down who changes what:

- Who configures the HL7 v2 message mapping — the LIS vendor, the HIS vendor, or a third party?
- Who pays for the HIS-side change, and what happens if the HIS vendor declines or delays?
- Is there a fallback (flat-file drop, manual upload) if the interface is not ready at go-live?

Most schedule slippage in small-lab projects is not the LIS. It is an unowned dependency on someone else's system.

### 3.4 Price the validation deliverables as line items

This is where accreditation scope silently changes the budget. If your laboratory is CAP accredited or working toward ISO 15189, you will be asked for evidence that the information system was validated before use and after significant change — and that records of that validation are retained.

Ask each vendor to state, in writing, what they provide for:

- A requirements specification you can sign (URS) and a traceable response to it
- Installation and operational qualification evidence (IQ/OQ), or an equivalent documented verification
- Change-control records, including how a post-go-live configuration change is re-verified
- Audit trail specification: what is logged, whether it is immutable, retention period, and how an assessor can review it
- Report-definition control: who can change a report template, and whether the change is versioned

Vendors who have never supported an accredited laboratory will answer these with "we can provide a document". That answer is a risk indicator, not a deliverable. See the [inspector evidence checklist](inspector-evidence-checklist.md) for the artefacts assessors actually ask to see, and the [regulatory map](regulatory-map.md) for how CLIA, CAP, and ISO 15189 differ in what they require.

### 3.5 Fix the support definitions

"24/7 support" means nothing without a response-time table, and "response" is not "resolution". Require:

- Severity definitions with examples (result release blocked = severity 1)
- Response and workaround targets per severity
- Named escalation contact, not a ticket queue
- Whether the annual fee is capped, and what the renewal basis is in year four
- What happens to the fee if you add an analyser or a site mid-term

---

## 4. Integration: say "FHIR R4" only if you can scope it

International tenders increasingly ask for FHIR. That is reasonable — but "FHIR support" without a resource list and a use-case list is not a specification.

If FHIR is in scope, pin it down:

| Question | Why it matters |
|---|---|
| Which FHIR version — R4, R4B, R5? | Resource and search-parameter differences are not cosmetic |
| Which resources, which direction? | Typical laboratory scope: `ServiceRequest` in, `Specimen` and `DiagnosticReport` out, with `Observation` for results and `Patient`/`Practitioner`/`Organization` as references |
| Synchronous REST, or asynchronous messaging? | Determines whether a failed message blocks the workflow |
| Which terminologies — LOINC, SNOMED CT, local codes? | Mapping is the actual work, not the transport |
| Who maintains the mapping when a test is added? | Usually unpriced, and it is a recurring cost |

In most laboratories today, the working interface is still HL7 v2.x or ASTM over a serial or TCP connection, with FHIR at the boundary to a national platform or a modern EMR. The [interoperability checklist](interoperability-checklist.md) covers the acceptance tests for all three, including the failure paths that vendors tend to leave out.

---

## 5. Structure the money so that risk is visible

A comparable bid also has a comparable payment structure. Ask every vendor to map payments to acceptance events, and reject "30% on signature, 70% on go-live" if it means you carry all the interface risk.

A defensible structure for a small laboratory:

1. Signature — mobilisation only
2. Scope baseline signed off — including the analyser schedule
3. Each analyser verified against a defined acceptance test
4. HIS/EMR interface accepted end-to-end, including a rejected-message path
5. Validation evidence delivered and accepted (if in accreditation scope)
6. Go-live plus a defined hypercare period
7. Retention against the exit clause, released when the data export is verified

Retention is not hostility. It is the only mechanism that keeps an exit clause meaningful.

---

## 6. The exit clause is part of the price

Ask for a sample export, not a promise. Specifically:

- Format: CSV, SQL dump, or a documented API?
- Scope: results, audit trail, QC records, images, report PDFs?
- Fidelity: are reference ranges, units, and flags preserved per result, or flattened into text?
- Cost: is the export chargeable, and at what rate?
- Timing: how many days after request?

A laboratory that cannot leave has no negotiating position at renewal. This is the one line item where paying more now is usually correct.

---

## 7. A one-page normalisation table

Use this as the cover sheet of your comparison. If a cell is empty, that vendor has not answered the question — do not fill it in for them.

| Row | Vendor A | Vendor B | Vendor C |
|---|---|---|---|
| Five-year total, same scope | | | |
| Analysers covered (count / models) | | | |
| Proprietary protocols (count) | | | |
| Bidirectional interfaces (count) | | | |
| HIS/EMR change owner | | | |
| Validation evidence provided | | | |
| Audit trail: immutable? retention? | | | |
| Report template control by customer? | | | |
| Support: severity table attached? | | | |
| Renewal basis and cap | | | |
| Data export format and cost | | | |
| Retention held against exit | | | |

When the table is complete, the decision is usually obvious — and it is rarely the lowest headline number.

---

## 8. What this guide does not do

It does not tell you what your project will cost. Cost depends on your analyser estate, your integration counterparties, your accreditation scope, and your deployment model, and any single figure published without those inputs is a marketing number. The [TCO worksheet](tco-worksheet.md) gives indicative ranges with their sources marked, including which figures are vendor-published and therefore unverified.

It also does not promise that a system will make you compliant. Software can support the records an assessor asks for; it cannot substitute for your own validation, training, and review. Wording matters here: a product "supports ISO 15189 information-management requirements" — it is not "ISO 15189 certified", and any vendor claiming the latter is worth a second look.

---

*Disclosure: the author provides LIS deployment and source-code licensing services. This note describes procurement practice from project experience and should be read as an industry observation, not a quotation. No prices are stated here because no independently verifiable dataset supports a specific figure.*
