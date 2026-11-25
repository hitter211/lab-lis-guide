# LIS Downtime and Disaster Recovery: The Six Records Every Lab Assessor Asks For

> Part of the [LIS / LIMS Selection Guide](../README.md). Last reviewed 2026-11-25.
> **Disclosure:** This is not an official document. The author provides LIS deployment and source-code licensing services. Regulatory statements summarise the issuing bodies' published frameworks — verify against the current official text (CLIA: [eCFR 42 CFR Part 493](https://www.ecfr.gov/current/title-42/chapter-IV/subchapter-G/part-493); ISO 15189: [ISO](https://www.iso.org/standard/74221.html) or your national accreditation body) before a compliance decision.

---

## Why most labs fail this on inspection day

Ask a lab director "do you have a downtime procedure?" and the answer is almost always yes — there is a document in the quality binder. Ask the three follow-up questions an assessor actually asks, and the room goes quiet:

1. **"Show me the record from your last real failover."** Not a tabletop exercise. An actual outage, with timestamps.
2. **"When the system was down, how did specimens keep moving?"** Which numbering rule? Who authorised paper reports? Who signed them?
3. **"How do you know no result was lost?"** Show me the reconciliation between downtime accessions and back-entered electronic records.

A downtime policy that has never been exercised is a document, not a capability. This holds under CLIA, under CAP accreditation checklists, and under ISO 15189:2022 — all three regimes ultimately ask the same thing: **evidence that continuity was planned, exercised, and reconciled.**

The terminology differs; the artefacts do not. What follows is the artefact list, in a form you can turn into your own SOP pack this week.

---

## The six records (what assessors physically ask to see)

| # | Record | Who completes it | When | What the inspector checks |
|---|---|---|---|---|
| 1 | **Downtime / disaster recovery procedure** | Lab manager drafts, director approves | At establishment, reviewed annually | Approval signature, effective date, version number |
| 2 | **Failover drill record & script** | Drill organiser | Every drill | Attendance, actual outage duration, **evaluation findings with corrective actions** |
| 3 | **System change request form** | Requester + approver | Before every config/template/upgrade/interface change | Change description, risk assessment, approval, **rollback plan** |
| 4 | **System maintenance log** | Lab IT / vendor engineer | Every service visit, backup, patch | Date, scope, performer, **whether a restore was actually verified** |
| 5 | **Outage incident record** | On-duty staff | Every full or partial outage | Start/end time, specimens affected, degradation measures, reconciliation outcome |
| 6 | **Training record** | Trainer | New hires, after every procedure revision | Attendance, content, competency check |

Three fields that are almost always missing and cost real findings:

- **Form 3 needs a rollback plan and a named post-change verifier.** "We changed the report template and it looked fine" is not change control. Un-documented, un-verified, un-backed-up changes are among the most frequently cited deficiencies in information-systems inspections.
- **Form 4 must separate "backup completed" from "restore verified".** A backup that has never been restored is a hypothesis, not a backup. Corrupt or incomplete backup files are regularly discovered on the day they are needed.
- **Form 5 must state specimens affected and the reconciliation outcome** — not just "service restored at 14:30". "Restored" without "reconciled" leaves the data-integrity question open.

---

## The eight questions your procedure must answer

An assessor will not read the whole procedure. They probe. If any of these eight answers is missing, the procedure is incomplete regardless of its page count:

| # | Must answer | Typical deficiency |
|---|---|---|
| 1 | What counts as an outage, and how is it graded? | No distinction between full stop, partial stop, and degradation — so no response timelines exist |
| 2 | Who has authority to declare the downtime procedure active? | "The lab decides" — an assessor will ask *which named role signs* |
| 3 | Who is notified, within what time? | IT is called; clinicians and the vendor are forgotten |
| 4 | How do specimens keep moving during downtime? | **No paper workflow at all — the procedure is unfinished** |
| 5 | How are paper reports issued and by whom? | No "issued during downtime" marking rule |
| 6 | Who re-enters results after recovery, by when, and how is re-entry marked? | "Promptly" with no owner and no deadline |
| 7 | How is reconciliation performed? | No step comparing paper accessions against system records |
| 8 | How often are drills held, and who evaluates them? | Tabletop exercises only; no real failover on record |

Questions 4 and 7 are the dividing line. **Most "downtime procedures" are actually server-restart guides** — they address "the system is sluggish", not "the system is not coming back today and the ER needs 200 results".

---

## A grading scheme that actually works

Grade by **scope × recoverability**, not by vague words like "severity":

| Level | Typical situation | Response (example — set your own) |
|---|---|---|
| **I — full stop** | Database down, server failure, server-room power loss | Immediate degradation; notify clinical areas within 30 minutes |
| **II — partial stop** | One workstation down, one analyser interface lost, printing failed | Switch machines or go manual; restore within 2 hours |
| **III — degraded** | Slow response, intermittent errors, network jitter | Log and report; no stoppage if reporting continues |

---

## The drill script: write it as a timeline

A drill record written as prose proves nothing. A timeline with timestamps, names and counts is the artefact assessors accept:

| Time | Action | Record |
|---|---|---|
| T+0 | Login fails; restart attempt fails; graded Level I and reported | Discovery time, grading rationale |
| T+8 | Clinical areas, IT and vendor all notified | Notification targets and times |
| T+15 | Backup numbering rule activated; paper accessioning begins | First manual accession number |
| T+60 | Paper reports issued — dual signature, marked "issued during system downtime" | Report count |
| T+95 | Recovery verified item by item: login, query, print, analyser link | Recovery criteria ticked |
| T+180 | One-by-one reconciliation: manual numbers ↔ system records; no losses, no duplicates | Reconciliation conclusion and any discrepancy handling |

Two practical rules:

1. **Do one real failover per year** — in a test environment or off-peak window. Inspectors ask "how long was your last *actual* outage?"; labs with only tabletop records cannot answer, and the gap is visible.
2. **Every drill must end with an evaluation**, and its corrective actions must be visibly closed in the next drill record. An improvement list nobody follows is worse than no list — it documents that you knew and did not act.

---

## What the LIS itself must support

A perfect procedure fails if the software cannot execute it. Put these four into any RFP or upgrade requirement:

1. **Configurable manual numbering** that cannot collide with system-generated numbers (e.g. an independent `date-section-sequence` segment reserved for downtime).
2. **Back-entered results marked as such**, with the original testing time preserved — not silently stamped with the re-entry timestamp.
3. **Tamper-evident audit logs** that survive degradation, so manual actions taken during downtime can be appended and traced afterwards.
4. **Restore that is actually testable** — ideally one-command recovery into a standby environment. Without it, nobody dares run a real failover drill, and the drill record stays permanently theoretical.

The audit-trail and evidence items above map directly onto the artefacts listed in the [inspector evidence checklist](inspector-evidence-checklist.md).

---

## A note on connectivity: downtime is not always the server's fault

For labs in low-resource settings — and for any cloud-hosted deployment — the more common failure is **the network, not the server**. A cloud-only LIS converts "server down" risk into "link down" risk, and the downtime procedure must cover it explicitly: is there a local cache? Can staff open orders offline? How does data sync after recovery, and how do paper accessions merge without creating duplicates? See [Offline & low-resource deployment](offline-low-resource-deployment.md) for the offline-first design questions to ask before signing.

---

## Common questions

**How often should the downtime procedure be revised?**
A common pattern is annual review, plus an immediate revision after a vendor change, a major version upgrade, an organisational change, or any Level I incident. Follow your own quality-system document and the current text of your accreditation standard — do not copy another lab's cycle.

**Do we really need a live failover drill, or are tabletop exercises enough?**
At least one live switchover per year is the defensible position (test environment or off-peak is fine); tabletop exercises supplement. With tabletop records only, expect the assessor to probe actual outage duration and whether the paper workflow has ever really run.

**We have no dedicated IT person. Who owns this?**
Name a part-time information officer (usually a technologist who knows the system), and contract the vendor's support terms in writing: response time, on-site time, and a named backup contact. A procedure listing a single phone number is a procedure that fails the day that person is on holiday.

**Are paper reports issued during downtime legally valid?**
Yes, when the safeguards exist: tester and reviewer signatures, issue time, a "issued during system downtime" mark, paper originals retained per your retention policy, and back-entry plus reconciliation after recovery. Remove any one of these and the report becomes indefensible in a retrospective review.

**Does any of this apply if we are ISO 15189 accredited rather than CLIA/CAP?**
The artefacts are the same. ISO 15189:2022 tightened information-management and record-control requirements; CLIA's quality-system framework and CAP's accreditation checklists converge on the same evidence — exercised continuity procedures, change control, backup with verified restore, and reconciliation. Only the checklist item numbers differ; verify the current numbering with your accrediting body rather than relying on any secondary summary, including this one.

---

## Related reading

- [Inspector evidence checklist](inspector-evidence-checklist.md) — the full artefact list assessors ask to see in the room
- [Offline & low-resource deployment](offline-low-resource-deployment.md) — designing the downtime mode before go-live, not after the first outage
- [Regulatory map — US, EU/UK, ISO 15189 world](regulatory-map.md) — where continuity and record requirements sit in each regime
- [Total cost of ownership worksheet](tco-worksheet.md) — DR capability is a contract line, not free after-sales goodwill

---

**Disclosure:** The author provides LIS deployment and source-code licensing services. The form fields and drill timeline above come from implementation and inspection-support experience and are industry practice, not the official requirements of any accreditation body. Checklist item numbers and review frequencies should be verified against the current official text of your applicable regime and your own quality-system documents.
