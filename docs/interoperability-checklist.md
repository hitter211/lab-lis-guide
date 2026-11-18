# Interoperability checklist — LOINC, HL7 v2, FHIR R4, ASTM

> Part of the [LIS / LIMS Selection Guide](../README.md). Last reviewed 2026-11-18.
> Print this and use it in the demo. Ask the vendor to show the artefact, not describe it.

## Why this document exists

Most LIS implementations fail on integration, not on missing features. Every analyser model has its own protocol; some output flat files to a shared folder, others use proprietary serial protocols; calibration data, QC results and patient results may arrive in different message types. And field-level mapping between LIS and EHR is where errors hide: test codes, specimen source codes, result units and abnormal-flag definitions must match on both sides.

---

## A. Terminology — LOINC

**LOINC** (Logical Observation Identifiers Names and Codes) is the international standard for identifying health observations, measurements and documents, maintained by **Regenstrief Institute**. As of the current release there are **112,405 codes** (LOINC v2.83). A LOINC code represents the *question*; the answer may be a numeric value with units, a SNOMED CT coded qualitative result, or an ICD-coded diagnosis.

A Fully-Specified Name has six parts, separated by colons:

`Component : Property : Timing : System : Scale : Method`

Example — `806-0`, manual white-cell count in CSF:

| Part | Value |
|---|---|
| Component | Leukocytes |
| Property | NCnc (Number Concentration) |
| Timing | Pt (Point in Time) |
| System | CSF |
| Scale | Qn (Quantitative) |
| Method | Manual count |

| # | Check | Pass condition | Vendor answer |
|---|---|---|---|
| A1 | **Exportable mapping table** | A file (CSV/XLSX) mapping every local test code → LOINC code + Long Common Name + unit. You keep it, version it. | |
| A2 | **Dual coding** | HL7 v2 and FHIR messages can carry both local and LOINC identifiers | |
| A3 | Coverage of your top 50 tests | Mapped, with units and reference ranges aligned | |
| A4 | Mapping ownership on change | Documented process when a new test is added; you can edit the mapping | |
| A5 | Qualitative results | SNOMED CT (or agreed code system) for coded results | |
| A6 | Version tracking | Which LOINC release the mapping was built against (v2.83 or later) | |

> **Disqualifier:** "We handle the codes for you" with nothing exportable. If you cannot take the mapping with you, you cannot leave.

---

## B. Transport — HL7 v2.x

HL7 v2 remains the most common transport for lab orders/results in US clinical settings.

| Message | Direction | Carries |
|---|---|---|
| **ORM / OML** | EHR → LIS / lab | Patient, ordering provider, requested test, specimen requirements, order details |
| **ORU** | LIS → EHR | Result values, units, reference ranges, abnormal indicators, specimen info, status, timestamps |
| **ACK / query** | Both | Acknowledgement and reconciliation |

| # | Check | Pass condition | Vendor answer |
|---|---|---|---|
| B1 | Conformance statement | Exact HL7 v2 version named (e.g. v2.4.1 ORM minimum in some national profiles) | |
| B2 | Sample messages | Real ORU / ORM samples you can inspect, not a screenshot | |
| B3 | Field mapping document | PID / OBR / OBX segment mapping, including test code, specimen source, units, abnormal flags | |
| B4 | Abnormal flag alignment | Both sides agree on H / L / HH / LL / A semantics | |
| B5 | Corrected & amended results | Original result preserved, clear version history, no silent overwrite | |
| B6 | Duplicate / unmatched handling | Rejected, cancelled, delayed, unmatched results routed to manual reconciliation, never auto-filed | |
| B7 | Structured vs narrative | Numeric values stored as structured data with units, not free text | |
| B8 | Critical values | Immediate alert to the responsible clinician, with documented contact and read-back | |

---

## C. API layer — FHIR R4

| Resource | Represents |
|---|---|
| **ServiceRequest** | A laboratory order |
| **Observation** | An individual result / measurement (value, unit, reference range, abnormal flag, observation date/time) |
| **DiagnosticReport** | A grouped report referencing its Observations; **US Core** profile requires status, a LAB category code, a test code (preferably LOINC), patient reference, effective time and issued time |
| **Patient / Practitioner / Specimen** | Supporting references |

| # | Check | Pass condition | Vendor answer |
|---|---|---|---|
| C1 | Sandbox | A working test endpoint with credentials | |
| C2 | Capability statement | Published, listing actually implemented resources | |
| C3 | DiagnosticReport + Observation | Demonstrated end-to-end, not just a "FHIR-ready" slide | |
| C4 | US Core / national profile | Named conformance where applicable | |
| C5 | Terminology binding | Observation.code carries LOINC; qualitative values carry SNOMED CT where applicable | |
| C6 | Reference ranges & flags | Present on Observation, age/sex configurable | |
| C7 | API versioning & rate limits | Documented, with a deprecation policy | |
| C8 | Bulk export | Full data extract in a standard format for migration / exit | |

---

## D. Instruments — ASTM and everything else

| # | Check | Pass condition | Vendor answer |
|---|---|---|---|
| D1 | **Your exact analyser models** | Written list of make + model already integrated, with protocol per model | |
| D2 | ASTM E1381 / E1394 | Lower-layer framing and record format supported over serial and TCP/IP | |
| D3 | HL7 v2 from analysers | Where the instrument emits HL7 rather than ASTM | |
| D4 | **Bidirectional** | Worklist sent out, results received back — not one-way | |
| D5 | Flat-file fallback | Shared-folder / CSV import for older instruments | |
| D6 | Middleware boundary | Clear statement of what the middleware does vs the LIS (protocol translation, auto-verification, QC evaluation) | |
| D7 | QC & calibration messages | Handled separately from patient results | |
| D8 | Downtime / repeat testing | Manual result entry with an audit record and a back-entry deadline | |
| D9 | Per-interface price | Unit price for additional analysers written into the contract | |

---

## E. Master data & reconciliation

| # | Check | Pass condition |
|---|---|---|
| E1 | Test catalogue sync | LIS, EHR, billing and middleware stay aligned; a change process exists |
| E2 | Patient master index | Matching rule documented; duplicate detection |
| E3 | Provider directory | Ordering provider resolvable on both sides |
| E4 | Reference range tables | By age / sex / population; versioned |
| E5 | Order status tracking | Rejections, cancellations, delays, never-returned results visible |
| E6 | Audit of interface events | Interface logs queryable for inspections |

---

## F. National / regional add-ons (examples)

| Country / region | Additional requirements to confirm |
|---|---|
| **Australia** | AUCDI Release 2, SPIA, SNOMED CT-AU, LOINC, FHIR document authoring/consumption, HL7 v2.4.1 ORM minimum, IHI / HPI-O / HPI-I identifiers, My Health Record pathology upload with patient consent, DICOM for histology imaging, Essential 8, Privacy Act 1988 (Cth) + state privacy laws |
| **United States** | US Core DiagnosticReport profile, CPT/HCPCS for billing, ABN / medical-necessity triggers, HIPAA BAA |
| **EU / EEA** | GDPR transfer controls, EHDS-aligned microbiology terminology, national identifier schemes |
| **Public-health / donor networks** | Indicator exports for PEPFAR / Global Fund / national programmes, cross-site EQA exchange |

---

## G. The exit test (ask before signing)

1. If we terminate in three years, what exactly do we receive, in what format, and within how many days?
2. Does the export include **LOINC mappings, reference ranges, audit history and corrected-report history** — or only current results?
3. Is there a **source escrow** or source-escape clause if the vendor stops maintaining the product?
4. Is there any per-record or professional-services charge for the export?

> A vendor confident about interoperability will answer these in writing. One that hesitates is telling you where the lock-in is.

---

*Sources: Regenstrief Institute (LOINC), HL7 International (v2.x, FHIR R4, US Core), ASTM E1381/E1394, Australian Digital Health Agency LIS standard. Verify current versions against the official specifications.*
