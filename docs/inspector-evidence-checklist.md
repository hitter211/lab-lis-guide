# Inspector evidence checklist — what must be produced in the room

> Part of the [LIS / LIMS Selection Guide](../README.md). Last reviewed 2026-11-18.
> Built around what CAP-style inspections and ISO 15189 assessments repeatedly ask to see. Print it, and use it to run your own pre-inspection dry run.

## How to use this

For each item, do not ask "does your system support this?" — ask **"show me the record from last month."** A capability that exists in configuration but produces no record is a finding, not a feature.

---

## 1. Six records inspectors ask for on nearly every visit

| # | Record | What to open in the LIS | Common finding |
|---|---|---|---|
| 1 | **Tamper-evident audit trail** | A result that was edited: who changed it, the before and after value, when, at single-field level | Only a "last modified by" field; no before-value |
| 2 | **Electronic signatures** | A released report with the signer, timestamp and meaning of signature (review / release) | Shared logins; password-only with no documented e-signature path |
| 3 | **Internal QC** | Westgard multi-rule evaluation, Levey–Jennings chart, an out-of-control event and its corrective action | QC stored as images or spreadsheets outside the system; out-of-range results released without a block |
| 4 | **Proficiency testing / EQA** | PT sample flagging, submission deadline, result history, evaluation and any corrective action | PT tracked in email, not in the system |
| 5 | **Personnel competency** | Qualification and training records with expiry alerts; documented competency assessment | Paper files with no expiry tracking |
| 6 | **SOP / document control** | Version-controlled procedures with approval workflow and current-version indication | Shared drive with `SOP_final_v3.docx` |

---

## 2. Result and report integrity

| # | Evidence item | What an assessor checks |
|---|---|---|
| 2.1 | **Corrected / amended report** | Original value preserved; author, time and reason recorded; recipient notified; no silent overwrite |
| 2.2 | **Critical (panic) value** | Detection, time of notification, recipient, read-back confirmation, follow-up documentation |
| 2.3 | **Reference ranges** | Age/sex/population specific, versioned, visible on the report with abnormal flags |
| 2.4 | **Delta checks** | Comparison against prior results configured; a flagged implausible change and how it was resolved |
| 2.5 | **Auto-verification rules** | The rules themselves are documented and clinically validated, with an audit of what was auto-released |
| 2.6 | **Result traceability** | Result bound to method, instrument, reagent lot, calibration and operator |
| 2.7 | **Report format** | Only final, authenticated reports released; preliminary / corrected clearly distinguished |

---

## 3. Specimen chain of custody

| # | Evidence item | What an assessor checks |
|---|---|---|
| 3.1 | Accessioning | Barcode, timestamp, operator, unique specimen ID |
| 3.2 | State changes | Received → aliquoted → tested → stored → disposed, each with time and operator |
| 3.3 | Split specimens / aliquots | Parent-child relationship traceable |
| 3.4 | Rejection / recollection | Reason, decision, notification and outcome recorded |
| 3.5 | Pre-examination controls | Collection time, transport conditions, acceptance criteria |
| 3.6 | Post-examination | Storage location, retention and disposal records |

---

## 4. Information management (ISO 15189:2022 emphasis)

The 2022 edition strengthened requirements around information management and LIS. Expect questions on:

| # | Evidence item | What an assessor checks |
|---|---|---|
| 4.1 | **Backup** | Documented strategy (what, how often, where, retention), and the actual execution log |
| 4.2 | **Restore testing** | A completed restore test with a recorded result — a backup that has never been restored is not evidence |
| 4.3 | **Downtime / business continuity** | A documented downtime procedure, and the record of the last real or simulated outage: manual report numbering, who back-entered results, and by when |
| 4.4 | **Change control** | A software change with impact assessment, approval, pre-change backup confirmation, verification plan, sign-off and post-change monitoring |
| 4.5 | **Access control** | Role matrix, unique user IDs, periodic permission review, prompt removal of leavers |
| 4.6 | **Security / privacy** | Encryption in transit and at rest, audit of access and export events, incident response record, BAA/DPA where applicable |
| 4.7 | **Data integrity on interfaces** | Evidence that inbound results are validated and matched before filing; handling of unmatched/duplicate results |
| 4.8 | **Retention** | Retention rules matching the applicable federal/state/national requirement, with configurable periods |
| 4.9 | **System validation** | URS → IQ/OQ/PQ (or equivalent) documentation for the configured system, not just the vendor's generic certificate |

> **4.2 and 4.3 are the two most common gaps.** Almost every lab has a backup; far fewer can show a successful restore test or a downtime scenario with a completed record.

---

## 5. US-specific additions

| # | Item | Why |
|---|---|---|
| 5.1 | CLIA certificate type reflected in configuration | Determines test menus, QC frequency and personnel records |
| 5.2 | Personnel qualification records | CLIA sets qualifications for testing and supervisory roles |
| 5.3 | PT enrolment and performance for all accredited examinations | Mandatory input to the CAP two-year cycle |
| 5.4 | 21 CFR Part 11 e-signature controls | Expected alongside the audit trail |
| 5.5 | Report templates current with nomenclature updates (e.g. ISCN cytogenetics) | Outdated LIS templates are a recurring CMS/CAP citation category |
| 5.6 | Breach response documentation | OCR reporting within 60 days; CLIA-channel parallel notification where applicable |
| 5.7 | HIPAA risk assessment and contingency plan | Security Rule administrative safeguards |

---

## 6. A 30-minute self-check

1. Pick **one result from last month that was corrected**. Can you show the original value and the reason in under two minutes?
2. Pick **one QC out-of-control event**. Can you show the Westgard rule, the L-J chart and the corrective action?
3. Show the **last restore test** with its recorded outcome.
4. Show the **last downtime drill** — or, if there was none, explain why the procedure has never been exercised.
5. Show the **last software change**: approval, pre-change backup, verification and sign-off.
6. Show one **critical value**: detection → notification → read-back → follow-up.
7. Show the **current permission review** and one removed leaver.
8. Export the **LOINC mapping table** and one full ORU message.

> If any of these takes more than a few minutes, that is the gap an assessor will find. It is almost never a missing feature — it is a missing record.

---

## 7. What the software cannot do for you

Accreditation assesses the **laboratory's quality system in operation**. A LIS provides the capability to create records; it cannot create the discipline of filling them in. Internal audits, management review, corrective action follow-through, and participation in EQA remain the laboratory's responsibility.

**A vendor that says "buy our system and you will pass" is describing neither accreditation nor software accurately.**

---

*Sources: College of American Pathologists Laboratory Accreditation Program, CLIA (42 CFR Part 493) and CMS inspection guidance, ISO 15189:2022 (information management, record control, pre-/post-examination processes), 21 CFR Part 11, HIPAA Security Rule. Verify against your own accreditation body's current checklist.*
