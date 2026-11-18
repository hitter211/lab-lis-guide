# Regulatory map — US, EU/UK, and the ISO 15189 world

> Part of the [LIS / LIMS Selection Guide](../README.md). Last reviewed 2026-11-18.
> **This is a summary for procurement planning, not legal or compliance advice.** Verify every point against the current official text and your own accreditation body.

## 0. The one rule that prevents most mistakes

> **Accreditation and certification attach to laboratories, not to software.**

There is no such thing as an "ISO 15189-certified LIS", a "CLIA-certified LIS", a "CAP-accredited LIS" or a "HIPAA-certified LIS". What exists is:

- obligations on the **laboratory** (or the covered entity), and
- **capabilities and records** the LIS must provide so the laboratory can meet them.

A vendor claiming software certification is describing a regime it does not understand. Treat it as a disqualifier in a technical evaluation.

---

## 1. United States

### 1.1 CLIA — the mandatory floor

| Item | Detail |
|---|---|
| Legal basis | Clinical Laboratory Improvement Amendments of 1988; **42 CFR Part 493** |
| Administered by | **CMS**, with **FDA** and **CDC** in defined roles |
| Applies to | Any US facility testing human specimens for health assessment, diagnosis, prevention or treatment (research excluded) |
| Certificate types | Waiver · Provider-Performed Microscopy (PPM) · Registration · Compliance · Accreditation |
| Complexity tiers | Waived / moderate / high complexity — determine personnel qualifications, QC frequency and test menu |
| Cost | Commonly cited $150–8,000 biennially by certificate type and volume (publicly cited range, verify with CMS) |
| Typical timeline | 60–120 days for a Certificate of Waiver; 120+ days for Compliance / Accreditation |

**What the LIS must track, driven by certificate type:** test menus, personnel qualification records, QC frequencies, proficiency testing, patient test management from collection to reporting, and record retention.

**Why the certificate type is the first question in a demo:** a Certificate of Waiver lab running only cleared simple tests is inspected on a fundamentally different basis from a Certificate of Compliance lab running high-complexity testing. A system configured for one does not automatically satisfy the other.

### 1.2 CAP / COLA / The Joint Commission — deemed status

CMS grants **deeming authority** to approved accrediting organisations. A lab holding current CAP accreditation is generally treated as meeting equivalent CLIA requirements without a separate CMS survey — **but the lab must still hold a valid CLIA certificate and CLIA fees still apply.**

| Body | Shape | Best fit |
|---|---|---|
| **CAP** (Laboratory Accreditation Program) | Peer inspection against ~21 discipline-specific checklists (3,000+ standards cited in published summaries), on-site every two years alternating with an off-year self-inspection | Reference labs, hospital labs, labs wanting the strongest credential |
| **COLA** | CMS-approved, educational/consultative approach, biennial survey | Physician-office labs, small clinical facilities |
| **The Joint Commission** | Hospital-wide accreditation including laboratory | Hospitals already in that system |

**Verify current deemed-status recognition directly with CMS or the accrediting body** — recognised-organisation status can change.

### 1.3 HIPAA / HITECH

Health information in a LIS is Protected Health Information. Obligations include:

- **Privacy Rule**: designated record set, minimum-necessary access, patient rights of access/amendment/accounting, Notice of Privacy Practices
- **Security Rule**: enterprise risk assessment, unique user IDs, role-based access, automatic logoff, audit controls, integrity protections, transmission security, encryption at rest and in transit, contingency planning (backups, disaster recovery, **downtime procedures**)
- **Breach Notification**: reporting to HHS **Office for Civil Rights within 60 days** of discovery; recent CMS guidance also expects parallel CLIA-channel notification for qualifying breaches
- **Business Associate Agreement**: required with any hosted vendor or subprocess handling PHI

> **No software is "HIPAA compliant" on its own.** The covered entity is responsible for the safeguards around whatever it runs. With self-hosted open-source software, you carry the risk analysis, contingency plan, access controls and encryption yourself.

### 1.4 21 CFR Part 11

FDA rules on electronic records and electronic signatures. In practice this means: tamper-evident audit trails, e-signature at result release, version history, and no ability to silently overwrite a released result. Often relevant even outside strict GxP scope because CAP-style inspections look for the same controls.

### 1.5 2025–2026 changes worth knowing

- **Electronic-only CLIA notifications**: CMS transitioned CLIA correspondence, fee coupons and certificates to electronic delivery, with full enforcement from **1 March 2026**. Labs must maintain a monitored compliance mailbox and keep LIS report templates current; outdated templates and unmonitored notices are a recurring inspection finding.
- **Cytogenetics reporting**: updated ISCN nomenclature and clearer interpretive narratives are being pushed by CAP/CMS; LIS report templates need to support structured nomenclature.
- **LDT rule**: the FDA's 2024 rule to regulate laboratory-developed tests as devices was **rescinded 19 September 2025** after a district-court vacatur (March 2025). **CLIA remains the operative federal framework.** A vendor selling "FDA-ready" as a substitute for CLIA work is misrepresenting the landscape.

---

## 2. European Union and United Kingdom

### 2.1 ISO 15189 via national accreditation bodies

**ISO 15189:2022** is the international standard for medical laboratories — quality and competence, covering pre-examination, examination and post-examination processes. The 2022 (fourth) edition adopted the ISO harmonised structure, introduced risk-based thinking, strengthened patient safety, and **strengthened requirements for information management and laboratory information systems**.

- **UK**: **UKAS** is the sole national accreditation body; ISO 15189 accreditation is a requirement for NHS pathology laboratories.
- Accreditation is **scope-specific**: the published scope lists the examinations covered. Always check the accrediting body's **public register** rather than a certificate PDF, and confirm status/dates — scopes can lapse, be suspended, or be narrower than marketing implies.

### 2.2 GDPR

Health data is a special category of personal data. For a LIS: lawful basis, data minimisation, access/erasure rights, DPIA where required, processor agreements, and **data-residency / international-transfer controls**. Cloud-only SaaS with servers outside the EEA needs a documented transfer mechanism.

### 2.3 IVDR / MDR — an important qualification boundary

Under **MDCG** qualification guidance, software falls into three groups:

| Group | Example | Regulatory status |
|---|---|---|
| **IVD under IVDR 2017/746** | Software that interprets raw measurement data to produce a diagnostic finding — e.g. ELISA optical-density analysis, blot-pattern interpretation, a smartphone app deriving a glucose value from a test-strip photo | IVD, risk class A/B/C/D, CE marking |
| **Medical device under MDR** | Software analysing medical images, or measurements not from in-vitro tests, that supports medical decisions | MDR device |
| **Neither** | **A LIS that only manages data or organises laboratory processes**; software that merely stores, forwards or presents results; simple statistics and charts | Not an IVD, not a device |

> This is a genuinely useful procurement question: **ask the vendor where its product sits on that line.** A LIS that only manages data generally needs neither IVDR nor MDR conformity assessment — but if it auto-interprets raw analyser signals, the answer changes. Confirm with regulatory counsel for your specific configuration.

### 2.4 National / European digital-health layers

- **EHDS** (European Health Data Space): LOINC v2.83 added microbiology concepts supporting the EHDS microbiology model, requested by the HL7 Europe Lab Semantic WG.
- **Australia** (a useful example of a national profile beyond the EU): the Australian Digital Health Agency's LIS standard requires **LOINC**, **SNOMED CT-AU**, **SPIA** (Standardised Pathology Informatics in Australia), **FHIR** document authoring/consumption, **HL7 v2.4.1 ORM** minimum, **IHI / HPI-O / HPI-I** identifiers, **AUCDI Release 2**, **My Health Record** pathology upload with patient-level consent, **Essential 8** cyber controls, and compliance with the **Privacy Act 1988 (Cth)** plus state/territory privacy legislation. DICOM applies where histology imaging is stored.
- Lesson: **"FHIR compliant" is not a country-specific answer.** Ask for written confirmation against the exact national profile you operate under.

---

## 3. The ISO 15189 world (70+ countries)

ISO 15189 is adopted by accreditation bodies in more than 70 countries and is built on ISO/IEC 17025 and ISO 9001 principles, tailored to medical laboratories. Accreditation bodies operate under **ISO/IEC 17011** and peer evaluation via the **ILAC MRA**. Since **1 January 2026**, **Global ACI** has replaced ILAC and IAF, merging the ILAC MRA and IAF MLA into a single arrangement; existing accreditations and legacy marks remain recognised through the transition.

### 3.1 Why it is commercially decisive outside the US

In many markets accreditation is not optional in practice — it is tied to licensing or reimbursement:

| Country | Body / instrument | Commercial consequence |
|---|---|---|
| **Australia** | NATA / RCPA | NATA accreditation to ISO 15189 is a prerequisite for Approved Pathology Laboratory status and Medicare benefits |
| **New Zealand** | IANZ | Accreditation based solely on ISO 15189, required by the Health and Disability Services (Safety) Act 2001 for public and private diagnostic labs |
| **United Kingdom** | UKAS | Required for NHS pathology laboratories |
| **India** | NABL (QCI) | ISO 15189 accreditation incentivised or mandated for PM-JAY "Gold/Silver" certification and government reimbursement |
| **Vietnam** | Ministry of Health, Circular 24/2017/TT-BYT | Quality roadmap; Level 4 and Level 5 (highest tiers) specifically require ISO 15189, with central/provincial hospitals mandated to comply to maintain licences and funding |
| **Singapore** | SAC-SINGLAS or CAP, under the Healthcare Services Act 2020 | Recognised pathways to demonstrate technical competence for licensing |
| **Philippines** | PhilHealth Circular 2021-0001 | International accreditation such as ISO 15189 enables "Center of Excellence" status, affecting contracting and premium reimbursement tiers |
| **Malaysia** | SAMM / FOMEMA | MS ISO 15189 accreditation required to become a FOMEMA panel laboratory for foreign-worker medical examinations |
| **United States** | A2LA, CAP | Both operate ISO 15189-based programmes; CAP offers one alongside its own checklist programme |

> Country-specific mandates above are summarised from published articles and secondary sources. **Verify locally with the accreditation body before relying on them** — scopes, circulars and reimbursement rules change.

### 3.2 Public-health and donor-funded networks

For HIV, TB, reference and surveillance laboratories in low- and middle-income countries, expect:

- **WHO / SLIPTA** stepwise quality improvement frameworks
- Donor reporting (PEPFAR, Global Fund, national programmes) with indicator exports
- Multi-site and cross-site exchange, external quality assessment cycles
- This is the segment where **OpenELIS Global** has its strongest installed base (project claims 1,000+ labs across 25+ countries — vendor/project-published, not independently verified).

### 3.3 ISO/IEC 17025 — when it is the wrong standard

ISO 17025 governs testing and calibration laboratories generally. It is the right frame for industrial, environmental, food and materials labs — and the reason a LIMS is often the wrong tool for a clinical lab. If a vendor answers a clinical-accreditation question with ISO 17025 language, check which market the product was actually built for.

---

## 4. What this means for a LIS purchase — a consolidated checklist

| Regime | Must-have LIS capability |
|---|---|
| CLIA | Certificate-type-driven test menus, personnel qualification records, QC frequency tracking, PT records, retention config, critical-value documentation |
| CAP | Field-level audit trail, 21 CFR Part 11 e-signature, Westgard QC + L-J charts, PT tracking, competency logs, version-controlled SOPs |
| HIPAA | Role-based access, unique IDs, auto-logoff, audit controls, encryption, BAA, breach-response documentation, downtime plan |
| ISO 15189 | Full process traceability, corrected-report original value, QC out-of-control handling, EQA records, risk-based information management, backup / restore testing |
| GDPR | DPIA support, data minimisation, erasure/access workflows, residency and transfer controls, processor agreements |
| IVDR/MDR | Written qualification statement: does the product only manage data, or does it interpret raw signals? |
| National profiles | Named conformance (e.g. AUCDI R2, SPIA, My Health Record, IHI), not a generic "FHIR compliant" claim |

## 5. Verification discipline

1. Ask for the **accreditation body's public register entry**, not a certificate PDF.
2. Check the **published scope** contains the examinations you need.
3. Check **status and dates** — suspended, withdrawn and expired accreditations are a real procurement risk.
4. Ask how the vendor sources reagents and consumables feeding accredited examinations — the supply chain must be traceable too.
5. Record every compliance statement in the contract as a **capability the system provides**, never as a certification the software holds.

---

*Sources: CMS / FDA / CDC (CLIA, 21 CFR Part 11), HHS OCR (HIPAA), College of American Pathologists, ISO 15189:2022 and ISO/IEC 17011, ILAC / Global ACI, UKAS, NATA, IANZ, NABL, SAC, PhilHealth, FOMEMA, Vietnam MoH Circular 24/2017/TT-BYT, EU MDCG qualification guidance, IVDR 2017/746, GDPR, Australian Digital Health Agency. Secondary sources used for country mandates and 2025–26 regulatory dates — verify against the official text.*
