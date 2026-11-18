# Open-source LIS landscape (2026)

> Part of the [LIS / LIMS Selection Guide](../README.md). Last reviewed 2026-11-18.
> **We have a commercial interest** (we sell deployment, source licensing and white-label services), so this page is deliberately plain about where open source is the better choice. Verify every project's current release, licence and activity against its own repository before committing.

## The short version

**Open source is the right call when** you have real in-house engineering/IT capacity, a light or absent formal validation burden, and a workflow shape the project was actually built for. It is usually the wrong call when you would have to buy most of that capacity from a contractor anyway — the labour does not get cheaper because the licence is free.

---

## Active clinical LIS projects

### OpenELIS Global

| | |
|---|---|
| **Licence** | MPL-2.0 (file-level copyleft) |
| **Maintainer** | DIGI-UW / University of Washington International Training and Education Center for Health (I-TECH) |
| **Stack** | Java, Docker; **FHIR R4 native** |
| **Interfaces** | ASTM, HL7, CSV for analysers |
| **Scope** | Clinical, public-health and environmental surveillance labs; pathology/cytology workflows; QC; EQA; specimen disposal; workload dashboard |
| **Installed base** | 1,000+ labs in 25+ countries, from single hospital labs to national reference labs (**project/vendor-published figure, not independently verified**) |
| **Latest release** | 3.3.0 (20 October 2026); 3.2.3.0 baseline noted in the release history |
| **Accreditation alignment** | States support for ISO and SLIPTA-style requirements (vendor/project claim — verify) |
| **Strengths** | FHIR-native, analyser integration, proven at national scale, no licence fee, Docker install |
| **Honest limitations** | Built for laboratory **networks** and public-health programmes, not a single small private lab; running it at scale needs IT staff and planning; a general private clinical lab should weigh the fit before investing engineering time |

> **This is the project you will be compared against.** Do not pretend otherwise. The honest differentiation for a commercial/white-label offering is: small-lab ergonomics, local language and report layout, specific analyser drivers, named support with response hours, and country-specific conformance work — **not** feature breadth, where a national-scale open-source project will win.

### C4G BLIS

| | |
|---|---|
| **Shape** | Basic clinical laboratory information system aimed at resource-limited settings |
| **Status** | Publishing releases again as of 2026 (per a third-party 2026 index) |
| **Best fit** | Very small labs, low-resource deployments wanting something simpler than OpenELIS |
| **Check first** | Current maintenance cadence, licence, and whether it covers your reporting/QC needs |

### GNU Health — Occhiolino module

| | |
|---|---|
| **Shape** | Laboratory module inside the wider GNU Health hospital/public-health system |
| **Best fit** | Organisations already deploying GNU Health |
| **Check first** | Whether you are willing to adopt the full GNU Health stack |

### Vibe Tox (Vibe Toxicology LIS)

| | |
|---|---|
| **Licence** | GPL-3.0-only |
| **Shape** | Desktop application (Windows/macOS/Linux), single machine, **offline**, covering orders → reports, QC, review/release, billing handoff, audit, encrypted backup |
| **Best fit** | Small US clinical toxicology labs wanting a single-computer system |
| **Status (as of 5 Nov 2026)** | In development, built with substantial AI assistance, tested on **synthetic data only, not clinically validated** |
| **Interfaces** | ASTM serial/TCP instrument connectivity; **no inbound order interface or EHR integration** |

---

## Analytical / research LIMS (not clinical reporting systems)

| Project | Licence | Stack | Best fit | Caveat |
|---|---|---|---|---|
| **SENAITE** | GPLv2 (senaite.core) | Python / Plone, modular, REST API | General analytical, research and testing labs; ISO/IEC 17025-oriented | **`senaite.health`, the healthcare extension, was archived in January 2024.** Latest core release 2.6.0 (April 2025) as of Oct 2026; commits continue. Verify clinical capability before assuming it. |
| **Bika LIMS / Ingwe** | GPL | Plone → Ingwe (Bika 4) is Docker-based on the SENAITE core | Water, food, cannabis, environmental testing | Active development has largely moved to the SENAITE fork; not clinical-reporting-first |
| **eLabFTW** | AGPLv3 | ELN | Research electronic lab notebook | **Not a clinical LIS** |
| **OpenSpecimen** | BSD-3 | Biobanking | Biobank / biospecimen management | **Not a clinical LIS** |
| **Baobab LIMS** | GPL-3.0 | Biobanking | — | No release since 2018 (per 2026 index) |
| **OpenLIMS** | GPLv3 | PHP/MySQL | Generic | Effectively archived; no updates since mid-2010s |
| **LabKey Server** | Apache-2.0 | Research data | Biomedical research | Research, not diagnostic reporting |
| **LabWare / STARLIMS / LabVantage / Thermo SampleManager** | Commercial | Enterprise LIMS | Large industrial / pharma / multi-discipline labs | Commercial, not open source; listed here to make the category boundary clear |

---

## Licence obligations — this matters if you redistribute

| Licence | Obligation in plain terms |
|---|---|
| **MPL-2.0** | File-level copyleft: modified MPL files must stay MPL and be made available; you may combine with proprietary files in the same project |
| **GPLv2 / GPL-3.0** | Distributed derivative works must be released under the same licence with source; internal-only use does not trigger distribution |
| **AGPLv3** | Additionally triggers on **network use** — a modified AGPL system offered as a service must offer its source to remote users |
| **BSD-3 / Apache-2.0** | Permissive; attribution and notice retention; generally allows closed-source commercial products |
| **GPL-3.0-only** | No "or later" upgrade flexibility |

> "Open source" does **not** automatically mean "you can close it, rebrand it and sell it". If white-label or closed-source redistribution is your plan, read the licence of every dependency, not just the top-level project. This is exactly why a commercial dual-licence or an explicit source-licence agreement exists.

---

## Verification checklist before you commit engineering time

1. **Is the project still active?** Commit frequency, release cadence, number of independent contributors, more than one organisation depending on it.
2. **Which standards, at which version, with what conformance evidence?** "FHIR R4 native" should be testable in a sandbox.
3. **Can your team operate it?** Operational complexity is the most commonly underestimated cost, and the one that decides whether the deployment survives.
4. **What is the community's health?** A single maintainer is a bus-factor risk.
5. **What is the exit?** Is data extractable in a standard format, and what would migration cost?
6. **What is the 10-year TCO**, including hosting, support, upgrades and the staff to run it?
7. **Does it fit your workflow shape?** A public-health-network system forced into a single private lab — or a research LIMS forced into diagnostic reporting — is the most common category error.

> Question 3 disqualifies more candidates in practice than question 2.

---

## Where a commercial / white-label offering legitimately fits

Not "better features". These four:

1. **Small-lab ergonomics** — a single-site private or hospital lab does not need a national-network system, and needs far less setup.
2. **Localisation** — interface language, report layout, date/number formats, national identifiers and report templates.
3. **Named support** — a person, response hours, a language, a contractual SLA. A community forum is not a support model for an accredited lab.
4. **Country-specific conformance work** — the exact national profile, done and documented, rather than a generic "standards-compliant" claim.

If those four are not worth paying for, an open-source project is genuinely the better answer — and we will say so.

---

*Sources: project repositories and release pages (OpenELIS Global, SENAITE, Bika/Ingwe, eLabFTW, OpenSpecimen, C4G BLIS, GNU Health), third-party 2026 open-source LIMS indexes and cost guides, Regenstrief/HL7 standards documentation. **All installed-base, release and capability claims above are third-party or vendor/project-published and are not independently verified.** Check each project's own repository before relying on this table.*
