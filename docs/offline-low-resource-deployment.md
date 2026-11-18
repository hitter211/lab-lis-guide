# Offline and low-resource deployment

> Part of the [LIS / LIMS Selection Guide](../README.md). Last reviewed 2026-11-18.

## Why this document exists

Most LIS buying guides assume reliable connectivity, stable power, a static IP, an on-site IT team and 9-to-5 support in the vendor's time zone. For a large share of laboratories in Southeast Asia, Africa, Latin America and rural areas generally, none of that holds. A system designed only for a well-connected hospital will fail there — not on features, but on assumptions.

---

## 1. Offline-first is a requirement, not a feature

A lab that runs 24/7 needs a **downtime mode** that keeps specimens moving when the server or network does not.

| Element | What must be defined *before* go-live |
|---|---|
| Manual accession numbering | A deterministic rule (e.g. `date-section-sequence`) so downtime specimens never collide with system-generated IDs |
| Manual report form | A printable template with the same fields as the electronic report, marked "issued during system downtime" |
| Result custody | Who records results on paper, where the sheets are kept, and who is authorised to release |
| Back-entry | **Who** re-enters results (normally the original tester), **by when** (a fixed deadline), and how re-entry is marked in the audit trail |
| Reconciliation | A check that every downtime accession has a matching electronic record, and that no result was lost or duplicated |
| Drill | At least one simulated outage per year, with a signed record and an evaluation |

> A downtime procedure that has never been exercised is a document, not a capability. Inspectors ask for the **drill record**, not the policy.

---

## 2. Self-hosting vs cloud

| Constraint | Implication |
|---|---|
| Intermittent connectivity | Local server + local cache; cloud-only SaaS is not viable |
| Data sovereignty / cross-border transfer rules (GDPR and national law) | On-prem or in-country hosting; written data-residency statement |
| Donor / government reporting | Scheduled batch exports that work over low bandwidth, not real-time API calls |
| No static IP / no public DNS | Local network deployment, VPN or store-and-forward sync |
| Limited IT staff | Single-command deployment (e.g. Docker Compose), automated backup, simple restore, clear runbook |
| Unreliable power | UPS for server and switches, graceful shutdown, journaling DB, tested restore from abrupt power loss |

**Ask the vendor:** "What is the minimum viable hardware footprint, and what happens to an in-progress result if power is cut right now?" The answer is more informative than a spec sheet.

---

## 3. Low-bandwidth design

- Avoid chatty, per-keystroke network calls; batch synchronisation windows
- Compress and queue outbound results; retry with idempotency so a duplicate sync does not create a duplicate result
- Keep the local test catalogue, reference ranges and user directory cached
- Serve static assets locally; avoid CDN dependencies for the core UI
- Provide a documented fallback for instruments that write flat files to a shared folder rather than speaking TCP
- Make the audit trail local-first and sync it later — never lose the record because the link was down

---

## 4. Localisation

An English-only interface is a real adoption barrier, and it is not just translation:

| Area | What to confirm |
|---|---|
| UI language | Full translation, including validation messages and error text |
| Report layout | Local regulatory format, facility header, signature blocks, local date/number formats |
| Identifiers | National ID schemes (e.g. IHI/HPI-O/HPI-I in Australia), local patient identifiers |
| Terminology | Local test names alongside LOINC codes; dual coding so both survive |
| Units | Conventional vs SI, and the local convention for decimal separators |
| Character sets | Correct handling of accented and non-Latin names |

---

## 5. Support across time zones

"9–5 US Eastern, email only" is not a support model for a lab in a different hemisphere. Put these in the contract:

- Named implementation owner and a backup
- Response hours **in the lab's local time**, and the escalation path
- Language of support
- Who performs on-site work, and what remote support can actually resolve
- A spare-parts / replacement plan for the server and interface hardware
- Training materials that survive staff turnover (signed sheets, recorded sessions, a runbook in the local language)

---

## 6. Public-health and donor-funded networks

Common in HIV, TB, reference and surveillance laboratory networks:

- Multi-site and cross-site sample referral, with chain of custody across sites
- Indicator exports for **PEPFAR, the Global Fund** and national programmes
- External quality assessment cycles and cross-site exchange (panel testing, blinded samples)
- Stepwise quality frameworks such as **WHO / SLIPTA**, and the evidence they require
- National-scale deployment with a small central IT team — the reason FHIR-native, Docker-based open-source systems have a strong installed base here

> If this is your context, the relevant comparison is not "which LIS has more features" but "which system has been run at national scale with a small team" — see the [Open-source LIS landscape](open-source-lis-landscape.md).

---

## 7. A 10-question pre-purchase checklist

1. Can we issue a report with the server completely offline?
2. What is the manual numbering rule, and who back-enters results by when?
3. What is the minimum hardware footprint, and does it tolerate power cuts?
4. Does the system cache the test catalogue, ranges and user directory locally?
5. Is bulk data export available in a standard format for donor reporting?
6. Is the full UI available in our working language?
7. Are our national identifiers and report formats supported?
8. Who answers a 2 a.m. incident, in what language and within how long?
9. Can we restore from backup without vendor assistance, and when was that last tested?
10. If we lose connectivity for a week, is any audit record lost?

---

*This document generalises from publicly documented requirements (WHO/SLIPTA-style frameworks, Australian Digital Health Agency LIS standards, and MDCG/ISO 15189 information-management expectations). Verify against your own national and programme requirements.*
