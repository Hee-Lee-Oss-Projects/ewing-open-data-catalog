# PLAN — ewing-open-data-catalog

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated
>
> Risk tier: **medium**. Domain: cancer research (Ewing sarcoma) data documentation.
> Standing label on every output: **research metadata only — not medical advice.**

## Executive summary

Open Ewing sarcoma datasets exist, but they are scattered across repositories (NCBI GEO, the GDC /
TARGET open tier, UCSC Treehouse, cBioPortal, ICGC/ARGO), published under inconsistent and often
unstated terms, and described unevenly. A researcher who wants to reuse open Ewing data cannot
easily answer the three questions that actually gate reuse: **(1) is this access tier truly open
(not controlled-access dbGaP/EGA)? (2) does the license permit derivative reuse and redistribution
of *metadata*? (3) is there re-identification risk** — a real concern because Ewing is a rare
pediatric/AYA cancer where small cohorts and genomic data raise privacy stakes. The result is
wasted effort, accidental misuse of controlled data, and under-reuse of data that families and
clinicians consented to share for research.

This project produces a **license-clear, access-tier-verified index plus per-dataset datasheets**
of *open* Ewing sarcoma datasets. For each dataset we publish: a Datasheet-for-Datasets writeup, a
machine-readable canonical metadata record (with Croissant ML JSON-LD), a verified license + data-use
record, a provenance trail (accession, version, publication, consortium policy), and a
re-identification-risk assessment. The aggregate of these records *is* the catalog — an openly
licensed, citable index (Zenodo DOI + public repo) that points reusers at the right open data with
the legal and ethical questions already answered.

The **deliverable is documentation and metadata, not the data**. We never host, mirror, transform,
re-identify, or republish any dataset, and we never touch controlled-access or individual-level
patient data. The central, non-negotiable design principle is a **three-part blocking gate** run
before any documentation work: **access-tier (open only) → license (permits derivative metadata) →
re-identification risk (rare-disease/genomic, small-N)**. Any dataset that fails any part is flagged
and excluded, never guessed at.

Risk tier is **medium**: the project is not patient-facing and produces no clinical interpretation,
but it requires genomics-data-governance judgement (access tiers, consortium DUAs, re-identification
in a rare cancer) and conservative license handling (e.g. COSMIC and OncoKB are non-commercial and
are excluded from derivative redistribution). The plan front-loads that judgement as a hard,
named-reviewer gate. **No partner is yet secured; `verifiedNeed: false` across the backlog until one is.**

## Problem & beneficiaries

**Who is helped.**
- **Ewing sarcoma researchers and bioinformaticians** — especially small academic labs and
  citizen-scientists without legal/data-governance support — who need to find reusable open data
  fast and avoid wasting weeks on a dataset that turns out to be controlled-access or non-derivable.
- **Patient-advocacy and rare-cancer foundations** that want a trustworthy, plain-language map of
  what open Ewing data exists and what can be done with it.
- **Sibling Hee-Lee Oss projects** — directly `ewsr1-fli1-knowledge-graph`, `ewing-expression-reanalysis`,
  `ewing-literature-corpus`, `ewing-single-cell-atlas` — which all need a vetted, license-clear list
  of source datasets before they begin. This catalog is their upstream dependency.
- **The original data contributors** (patients, families, consortia) whose consented-for-research
  data becomes *more* used, correctly attributed, and correctly scoped.

**The verified need.** The *general* need — open biomedical data is widely under-documented and
its access/license terms are a recognized barrier to reuse (FAIR-data literature, GEO/GDC reuse
studies) — is well established. The **per-dataset, per-partner need is TO BE SECURED**: we have not
confirmed a named partner (advocacy org, repository, or research consortium) who has agreed to host,
adopt, or cite the catalog. Until that exists, individual tasks carry `verifiedNeed: false`. This
honesty is load-bearing: "delivered, not merged" requires the output to be *adopted by a
beneficiary*, not merely produced.

**Partner org.** TO BE SECURED. Candidate channels: rare-cancer / sarcoma patient-advocacy
foundations; open-data repositories (Zenodo for self-publication of the index; dataset-repo PRs);
research-data catalogs and "awesome-list"-style community resources; the sibling Hee-Lee Oss KG project as
an internal consumer. M0 includes explicit partner-outreach work; **no partner is assumed**.

## Goals and non-goals

**Goals**
- Produce a reusable, standards-aligned **datasheet template + canonical biomedical metadata model**
  for Ewing datasets (license, access tier, provenance, re-identification risk, data dictionary,
  molecular/fusion annotation, Datasheet, Croissant metadata).
- Publish a **license-clear, access-tier-verified open index** of open Ewing datasets — itself an
  openly licensed, citable artifact (CC-BY-4.0 docs; MIT code; Zenodo DOI).
- Make **access-tier + license + re-identification verification** a non-skippable, auditable,
  named-reviewer gate.
- Provide **source adapters** (GEO, cBioPortal, GDC/ICGC open tier) that pull metadata in the right
  shape so documentation is repeatable and cheap.
- Hand a clean, structured feed of vetted datasets to sibling Hee-Lee Oss Ewing projects.

**Non-goals**
- We do **not** host, mirror, download in bulk, clean, transform, re-analyze, or republish any
  dataset. (Re-analysis is a *separate* project, `ewing-expression-reanalysis`.)
- We do **not** touch **controlled-access** data (dbGaP, EGA, ICGC/TARGET controlled tiers,
  individual-level biobanks) or any identifiable patient data — these are out of scope and require
  authorized access + IRB we do not have.
- We do **not** attempt re-identification, record linkage, or de-anonymization of any kind.
- We do **not** produce medical, clinical, or treatment advice, prognosis, or interpretation; every
  output is labeled **research metadata only — not medical advice**.
- We do **not** document datasets with unclear/unverifiable licenses, non-derivable terms, or
  unacceptable re-identification risk — these are flagged and excluded, not "best-guessed."
- We do **not** redistribute non-commercial reference databases (COSMIC, OncoKB) as derivatives.
- We do **not** auto-publish; a human reviews and submits/contributes after sign-off.

## Success metrics (outcomes)

Outcome-based and beneficiary-centric. Vanity metrics ("datasheets written") are explicitly excluded;
the unit of success is **a vetted dataset that a real beneficiary reuses, correctly scoped.**

| Metric | Baseline | Target (first 6 months) |
| --- | --- | --- |
| Open Ewing datasets fully documented **and the index adopted/cited/hosted by a named beneficiary** (last-mile delivered) | 0 | 6 datasets in an adopted index |
| Access-tier + license + re-identification gate applied with a committed artifact / total triaged | n/a | 100% of triaged datasets have a recorded, verifiable gate decision |
| Controlled-access or non-derivable datasets correctly **excluded** (caught by the gate) | n/a | 100% caught (target: 0 controlled-access datasets ever documented as open) |
| Reuse signal: a documented dataset/index entry cited, forked, or used by a third party or sibling project | 0 | ≥ 3 with verifiable external reuse |
| Confirmed partners adopting/hosting/citing the catalog | 0 | ≥ 1 secured |
| Gate/accuracy defects found in expert review (license, access-tier, or re-identification error) | n/a | 0 access-tier/re-identification errors; < 1 license error per 10 delivered |
| Datasheets using the standard template + valid Croissant metadata | n/a | 100% of delivered datasets |

**Quantifying "improves reuse" (so DoDs are verifiable).** Per dataset we record a
**documentation-completeness score (0–100)**: fraction of canonical-metadata fields populated and
source-verified (access tier confirmed; license recorded with `permitsDerivatives`; provenance +
publication; data dictionary coverage of all documented summary fields; molecular/fusion annotation
sourced; Datasheet sections answered; valid Croissant emitted; re-identification assessment
recorded). Target: every delivered dataset reaches **≥ 90/100** versus a recorded **before-score**
captured at triage on the dataset as-published. The before/after pair lives in the dataset's gate
artifact.

**Per-dataset effort** is measured in **AI-session wall-clock minutes + number of human/expert-review
cycles** from gate-pass to upstream adoption, logged by the Steward in the outcome ledger. M2's
"effort reduced" DoD compares the adapter-era median against the recorded M0/M1 baseline median.

**What "adopted" means, per channel, and the evidence the Steward records.** One canonical
**acceptance evidence artifact** per dataset (a committed `outcomes/<dataset-id>.json` with channel,
URL/permalink/DOI, timestamp, completeness before/after). Acceptance per channel:
- **Self-published index (Zenodo):** a minted/updated **DOI** for the index version containing the
  entry — the always-available self-serve fallback so a real *delivered* outcome is reachable.
- **Partner adoption:** an advocacy org / repository / community resource links to or hosts the
  index entry — evidence = the live permalink or written confirmation.
- **Dataset-repo / community-resource PR:** a merged PR adding the datasheet/metadata — evidence =
  the merge commit URL.
- **Sibling-project consumption:** a sibling Hee-Lee Oss project imports the vetted entry — evidence = the
  referencing commit/issue. Self-reported or "submitted but unconfirmed" never counts as adopted.

## Scope

**In scope**
- Documentation/metadata artifacts per open Ewing dataset: Datasheet-for-Datasets writeup, canonical
  metadata record, Croissant ML JSON-LD, license + data-use record, provenance trail, data dictionary
  for *aggregate/summary* tables, molecular/fusion annotation (sourced from publication), known-issues,
  re-identification-risk assessment.
- The **open index** itself: an openly licensed, versioned, citable catalog of the above.
- Small, dependency-light **validation scripts** (schema/field/version checks) emitting a quality report.
- **Source adapters** that emit canonical metadata from GEO (E-utilities), cBioPortal (web API), and
  the GDC/ICGC open tiers — metadata only, no bulk data download.
- Access-tier, license, and re-identification triage and recording for each candidate dataset.
- A clean structured handoff feed for sibling Ewing projects.

**Candidate source families (coverage must be verified, not assumed).** The description names GEO
series, TARGET, Treehouse, cBioPortal Ewing studies, and ICGC. We treat these as *candidate source
families* whose open Ewing coverage is **verified per source in M0** (task `coverage-005`), because
coverage is uneven and some carry caveats:
- **NCBI GEO** — many Ewing expression series; processed/summary records generally reusable, but
  per-submitter terms and any linked controlled-access raw data must be checked individually.
- **GDC / TARGET open tier** — **honest flag:** TARGET's flagship initiatives are other pediatric
  cancers; Ewing-specific cohorts in TARGET/GDC may be limited or absent and must be confirmed
  before tasking. Only the **open-access tier** is ever in scope; the controlled tier is excluded.
- **UCSC Treehouse** — public pediatric expression data; commonly carries a **data-use agreement /
  registration** that must be recorded even when data is "open."
- **cBioPortal** — aggregates studies under **per-study** terms (TCGA-derived = open; other studies
  vary, some with publication embargoes); each study triaged on its own terms.
- **ICGC / ICGC-ARGO** — has open and controlled (DACO) tiers; **only the open tier** is in scope,
  attribution required.

**Out of scope**
- The data itself (no hosting/mirroring/bulk-download/transformation/re-analysis/republishing).
- **Controlled-access** data of any kind (dbGaP, EGA, DACO-controlled, individual-level biobanks).
- Any identifiable or individual-level patient/genomic data; any re-identification or linkage.
- **Non-commercial reference databases** (COSMIC, OncoKB) as redistributed derivatives.
- Clinical/medical interpretation, prognosis, treatment, ranking, or "best dataset" advice.
- Automated, unattended publishing.
- Any task whose primary benefit is a for-profit entity's private data.

## Solution approach & architecture

This is a **content/data-documentation project with light software** (template + canonical model +
validators + source adapters + the index). It is not a data pipeline that moves data.

**Pipeline (per dataset)**
1. **Triage & three-part gate** — identify dataset, repository, accession, publication. Run, in
   order and all blocking: **(a) access-tier** (open vs controlled — controlled = immediate EXCLUDE);
   **(b) license** (permits reuse + derivative metadata, with cited clause); **(c) re-identification
   risk** (genomic/rare-disease/small-N). PASS only if all three pass. Record the decision as a
   committed artifact.
2. **Provenance capture** — repository, accession id, version/edition, retrieval timestamp, primary
   publication (PMID/DOI), consortium data-access policy URL, license URL + snapshot, data-use
   conditions (registration/DUA), attribution string.
3. **Metadata / schema documentation** — canonical record; data dictionary for *aggregate/summary*
   fields only (sample counts, assay/platform, clinical-summary variables) derived by inspecting
   metadata/headers under the access protocol below — never by downloading individual-level data.
4. **Molecular annotation** — Ewing-specific, **sourced from the dataset's publication**, never
   inferred: driver fusion (EWSR1-FLI1, EWSR1-ERG, variant fusions), assay type, sample/cohort size.
5. **Datasheet** — Datasheets-for-Datasets questionnaire adapted for biomedical data (motivation,
   composition, collection, consent/ethics provenance, uses, distribution, maintenance).
6. **Croissant metadata** — machine-readable JSON-LD (Croissant ML v1.0).
7. **Validation script** — checks the canonical record/Croissant against the documented schema +
   pinned spec versions; emits a quality report.
8. **Index assembly** — add/refresh the entry in the openly licensed catalog.
9. **Review & contribute** — gate reviewer + technical reviewer sign-off, then a human publishes the
   index version (Zenodo DOI) and/or contributes to a partner/repo.

**Canonical metadata model.** One internal object per dataset is the source of truth; all outputs
(Datasheet, Croissant, index entry, sibling-project feed) are *projections* of it. Fields:
`id`, `title`, `accession`, `repository`, `submitterOrConsortium`,
`accessTier {tier: "open"|"controlled", evidenceUrl}` (controlled ⇒ excluded),
`license {id, url, permitsDerivatives:boolean, snapshotRef, dataUseConditions}`,
`provenance {retrievedAt, version, publicationPmidDoi, consortiumPolicyUrl, attribution}`,
`reidentification {riskLevel, basis, smallCellsFlag, germlinePresent, notes}`,
`molecular {tumorType:"Ewing sarcoma", driverFusion, assay, cohortSizeAggregate, sourcePublication}`,
`fields[] {name, type, units, allowedValues, nullable, description, caveats}` (aggregate/summary only),
`knownIssues[]`, `lineage {duplicateOf, supersedes}`, `examples[]`,
`specVersions {croissant, geoApi, cbioportalApi, gdcApi}`, `completenessScore {before, after}`,
`disclaimer: "research metadata only — not medical advice"`.

**Tech stack.** TypeScript, ESM, pnpm workspaces (Hee-Lee Oss conventions). Validators and adapters are
small Node packages with minimal dependencies. Documentation in Markdown + JSON/JSON-LD. The index
is a versioned repo + static artifact, archived to Zenodo for a citable DOI. No runtime services;
everything runs locally or in CI.

**Pinned source/spec versions** (recorded in `specVersions`, bumped only via a deliberate task, so
the "pinned" mitigation is real):
- **Croissant ML** — v1.0 (MLCommons); validate against the v1.0 JSON-LD context/SHACL.
- **NCBI E-utilities** (GEO metadata) — current ESummary/EFetch GEO field shape.
- **cBioPortal web API** — current public API version (`/api` study/clinical-attribute shape).
- **GDC API** — current cases/files metadata shape (open-tier metadata only).
- **ICGC / ARGO data portal API** — current open-tier project/donor-aggregate metadata shape.

**Dataset-inspection access protocol (makes "describe, never store, never re-identify" enforceable).**
- **Metadata/header reads only.** Use repository metadata APIs (GEO ESummary, cBioPortal study/
  clinical-attribute endpoints, GDC/ICGC metadata) and aggregate-level summaries; never bulk-download
  expression matrices, VCFs, BAM/FASTQ, or any individual-level file.
- **Open tier only.** If reaching any field requires controlled-access credentials, **stop** — the
  dataset is controlled and excluded.
- **Aggregate only.** Document cohort sizes, assays, and *aggregate/summary* variables. Never paste
  individual-level rows or genotypes into committed documentation.
- **Local-only and ephemeral.** Any bytes read live only in the contributor's local scratch for the
  session and are deleted; never written to the repo, CI artifacts, receipts, or logs.
- **Stop on re-identification or PII signal.** Any direct identifier, germline-variant-level data
  without documented aggregation, or small-cell signal halts inspection; the dataset routes to
  EXCLUDE/FLAG.

**Key decisions.**
- **Canonical-model-first** so we never hand-maintain parallel formats.
- The **three-part gate is blocking** and encoded as a committed checklist artifact, not an informal
  judgement; access-tier is checked *first* because it is the cheapest hard exclusion.
- Adapters are **output-only metadata**; a human performs publication/contribution.
- The index is **self-publishable** (Zenodo DOI) so delivery never depends solely on a third party.
- Reuse the gate/template patterns proven by the sibling `open-data-datasheets` project rather than
  reinventing them; specialize for oncology/genomics.

## Data, licensing & compliance

**This is the critical section.** Our deliverable is metadata *about* data, but because the data is
sensitive biomedical/genomic data from a rare pediatric cancer, we treat access, licensing, and
privacy with maximum conservatism.

**Access tier — the first and hardest gate.** Only **open-access / aggregate / de-identified** data
is ever in scope. **Controlled-access (dbGaP, EGA, ICGC DACO-controlled, TARGET controlled tier,
individual-level biobanks) is categorically excluded** — we have no authorized access or IRB, and we
never seek one for this project. Access tier is verified from the repository's own access designation
(cited `evidenceUrl`) before anything else; if open status cannot be positively confirmed, the
dataset is EXCLUDED.

**Source licenses / terms (must permit reuse AND derivative metadata):**
- **NCBI GEO** — NCBI content is generally public domain (US Gov), but individual *submitter* terms
  and linked controlled-access components must be checked per record; processed/summary metadata is
  the documentation target.
- **TCGA-derived data via cBioPortal** — open; attribution + TCGA publication guidelines recorded.
- **Other cBioPortal studies** — **per-study**; some carry publication embargoes or custom terms →
  governed by `policy-004`; excluded if non-derivable or embargoed.
- **UCSC Treehouse** — open processed data, but record any **data-use agreement / registration**
  requirement in `dataUseConditions`.
- **ICGC / ARGO open tier** — reusable with attribution; controlled tier excluded.
- **COSMIC, OncoKB** — **non-commercial** reference databases → **excluded** from derivative
  redistribution; we may *reference* them but never republish their content as a derivative.
- Anything else (CC-BY-SA, custom consortium terms, ambiguous/unstated) → governed by the written
  **NC / DUA / share-alike acceptance policy** (`policy-004`), which **must be decided and merged
  before any triage runs** so triage applies a fixed rule, not ad-hoc judgement.

**Objective "permits derivatives" criterion.** A dataset PASSes the license check only if its terms
are on the accepted list (or accepted by `policy-004`) **and** an explicit
`license.permitsDerivatives: true` is recorded with a cited clause/URL evidencing derivative
documentation/metadata is allowed. Missing evidence, unparseable terms, NC reference DBs, or
embargo = FLAG/EXCLUDE, never default-allow.

**Re-identification / privacy stance (rare-cancer-specific).** Ewing sarcoma is rare and largely
pediatric/AYA, so privacy risk is *elevated* even for "de-identified" data:
- **Genomic re-identification** — germline-variant-level data is re-identifiable in principle; any
  dataset exposing individual germline variants (not aggregate/summary) is EXCLUDED.
- **Small-N / small-cell risk** — aggregate counts below a threshold (**k < 5**) in any
  cross-tabulated cell (e.g. by site × age × outcome) are flagged; we document only counts the
  publisher already released at that granularity and never compute finer breakdowns.
- **Linkage risk** — datasets trivially linkable to an external identifier set are flagged/excluded.
- **We never re-identify or attempt linkage**, and we never anonymize data ourselves (that would be
  transforming the data — out of scope). The methodology output (which checks ran, what fired) is
  recorded in the committed gate artifact.

**Provenance model.** Every documented dataset records: repository, accession, retrieval timestamp,
dataset version/edition, primary publication (PMID/DOI), consortium data-access policy URL, license
id + URL + a captured **snapshot** of the license/terms text as it stood at retrieval (committed
copy + SHA-256 hash + Wayback save URL), data-use conditions, and the attribution string. Provenance
is part of the committed deliverable.

**Attribution & output licensing.** All documentation attributes the original submitter/consortium
per the source terms, links to the original accession, and clearly states the documentation — not the
data — is our contribution. **Documentation/metadata output is licensed CC-BY-4.0; validator/adapter
code is MIT.** Every artifact carries the **"research metadata only — not medical advice"** label.

## Quality, review & risk gates

**Risk tier: medium.** The project is not patient-facing and produces no clinical interpretation, so
it does not reach the `high` tier that requires oncologist sign-off. But it requires specialist
**genomics-data-governance** judgement and conservative license handling, hence a mandatory named
reviewer.

**Required review before a deed is "done":**
- **License + Access + Re-identification reviewer** (mandatory, every dataset; the hard gate):
  a reviewer competent in open-data/biomedical licensing (CC/SPDX/consortium DUAs) **and**
  genomic-data governance / re-identification risk. Confirms access tier is open, license permits
  derivative metadata, and re-identification risk is acceptable. **Non-skippable.**
- **Technical reviewer:** confirms the canonical record, data dictionary, molecular annotation
  source-citations, Croissant metadata, and validation script are accurate and CI-green.
- **Oncology/clinical escalation (conditional):** if any datasheet field strays toward clinical
  interpretation or a dataset's framing could read as patient-facing guidance, the task escalates to
  `high` and requires **credentialed oncologist + patient-advocate sign-off** — or the offending
  content is removed to keep the task at `medium`. The default posture keeps the project at `medium`
  by staying strictly descriptive.

**Test fixtures & golden files (so "CI green" means something).** Each tool ships committed test
assets, exercised in CI, using only **synthetic or public *metadata* fixtures** (no real
individual-level data ever committed):
- **Croissant validator** — golden JSON-LD fixtures: valid metadata that must pass and malformed
  cases that must fail, against the pinned Croissant v1.0 context.
- **Source adapters (GEO/cBioPortal/GDC)** — golden API-response → expected canonical-record pairs,
  diffed in CI; using committed *captured public metadata responses* (e.g. a public GEO ESummary for
  a known Ewing series) — never patient-level payloads.
- **Gate artifact schema** — fixtures of PASS / FLAG / EXCLUDE decisions asserted against the
  decision schema, including a controlled-access case that must EXCLUDE and an NC-reference-DB case
  that must EXCLUDE.

**Definition of Shipped.** Datasheet + machine-readable metadata for an open Ewing dataset, with
**access tier verified open, license verified to permit derivative metadata, re-identification risk
assessed acceptable**, provenance recorded, completeness ≥ 90/100, the **"not medical advice"** label
present, and the entry **published in the openly licensed index with a citable artifact** (minimum:
a Zenodo DOI) **and adopted/cited/consumed by a named beneficiary** per the per-channel acceptance
definitions. Shipped requires the Steward to have recorded the canonical acceptance evidence artifact
(`outcomes/<dataset-id>.json`). Producing the docs is *not* shipped; recorded adoption is.

## Roadmap & milestones

**M0 — Foundation & cold-start (thin)**
- Goal: build the toolkit + the three-part gate, verify which source families actually hold open
  Ewing data, and prove the end-to-end flow on one dataset; begin partner outreach.
- **Cold-start de-risking.** The pilot is gated on a realistic adoption path *before* documentation
  begins, in priority order: (a) an **informal channel** — an advocacy org / repo maintainer /
  sibling-project owner who agreed to adopt or consume the entry; failing that, (b) a **self-serve
  fallback** that does not depend on a third party — **publish the index entry with a Zenodo DOI** we
  mint ourselves. The pilot must use one so M0 yields a real *delivered* outcome, not "submitted,
  pending."
- Exit criteria: (1) datasheet template + canonical metadata model published; (2) Croissant
  validator + one validation script green in CI with golden fixtures; (3) the three-part gate
  checklist (access-tier + license + re-identification) **and** the NC/DUA/share-alike policy exist
  and are applied to one dataset; (4) source-family coverage verified (open vs controlled Ewing
  split recorded for GEO/TARGET/Treehouse/cBioPortal/ICGC); (5) one open Ewing dataset (a GEO Ewing
  series) documented end-to-end and **published with a Zenodo DOI** (and adopted via an informal
  channel if one exists) — or, if neither materializes, **submitted** with the blocker surfaced;
  (6) ≥ 1 partner-outreach thread opened.

**M1 — Gate hardened + first adoptions + index v0.1**
- Goal: make the gate rigorous, get real entries adopted, publish the first index version.
- Exit criteria: (1) three-part gate codified as a reviewable artifact and applied to ≥ 6 datasets;
  (2) ≥ 2 datasets documented and in an **adopted/cited/DOI-published** index; (3) ≥ 1 confirmed
  partner or sibling-project consumer; (4) license/terms-snapshot capture working in the decided
  format (committed copy + SHA-256 + Wayback).

**M2 — Source adapters & scale**
- Goal: reduce per-dataset effort via GEO / cBioPortal / GDC(ICGC) open-tier metadata adapters.
- Exit criteria: (1) ≥ 2 adapters emit valid canonical metadata verified against committed captured
  public-metadata responses; (2) ≥ 5 datasets documented + adopted cumulatively, spanning ≥ 2 source
  families; (3) median per-dataset effort (AI-session minutes + review cycles, from the outcome
  ledger) measurably reduced vs. the recorded M0/M1 baseline median.

**M3 — Reuse outcomes & sustainability**
- Goal: demonstrate real downstream reuse, breadth across source families, and a maintenance model.
- Exit criteria: (1) ≥ 3 verifiable external reuse events (incl. ≥ 1 sibling-project consumption);
  (2) ≥ 6 datasets adopted cumulatively across ≥ 3 source families (index v1.0); (3) documented
  staleness/refresh process (versions drift in GEO/cBioPortal/ICGC) and a steward identified for
  ongoing liaison.

Dependencies: M1 depends on M0 toolkit + coverage verification; M2 adapters depend on M1's canonical
metadata; M3 depends on a body of adopted deliveries from M1–M2.

## Work breakdown

The itemized, schema-mapped backlog lives in `TASKS.md`, organized by the milestones above. Each
milestone has a task table (`ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer`),
acceptance criteria for the most important tasks, and a milestone Definition of Done. A
sized-but-unscheduled backlog and one complete, schema-valid example Task JSON are included there.
Throughput from M1 onward is driven by triaging candidate datasets (seeded by the `coverage-005`
source-family verification) through the three-part gate into per-dataset datasheet tasks; the gate is
the filter and no candidate becomes a task until it passes.

## Governance, roles & stakeholders

- **Maintainer (Owner):** TBD — owns the toolkit, triage, index, and backlog.
- **License + Access + Re-identification reviewer:** TBD (name TO BE SECURED) — mandatory,
  **non-skippable** gatekeeper combining open-data/biomedical-license literacy with genomic-data
  governance. Because it is a hard gate, it must be filled **before the M0 pilot (`pilot-009`) is
  reviewed** — a blocking prerequisite, not a parallel hire. The Maintainer recruits/designates a
  named, qualified reviewer; the appointment (name + qualification) is recorded here. May rotate
  among ≥ 2 qualified reviewers to avoid a bottleneck, but ≥ 1 must exist at all times or
  triage/documentation halts. Until named, all tasks remain `verifiedNeed: false` and no dataset can
  pass the gate.
- **Technical reviewer(s):** rotation verifying canonical records, adapters, Croissant, validators
  (CI green).
- **Oncology/clinical + patient-advocate reviewers (conditional, `high` escalation):** engaged only
  if a task drifts toward clinical interpretation/patient-facing framing; otherwise not required.
- **Steward (last-mile owner):** TBD — owns relationships with advocacy orgs / repos / sibling
  projects and records adoption (the "delivered" signal).
- **Partner / requestor:** TO BE SECURED — named advocacy org, repository, or sibling-project owner.
- **Conflict-of-interest stance:** the index is a public good; it must not be shaped to
  preferentially benefit any for-profit (e.g. a pharma reuser) over the public, per the good-deed
  definition. Any sponsorship is disclosed and must not gate which datasets are included.

## Dependencies & integrations

- **External standards/specs (pinned — see Tech stack):** Datasheets for Datasets (Gebru et al.),
  Croissant ML v1.0, schema.org/Dataset, SPDX license identifiers, FAIR data principles. Versions
  recorded in `specVersions`, bumped only via a deliberate task.
- **External services/repositories (metadata, open tier only):** NCBI GEO (E-utilities), cBioPortal
  web API, GDC API, ICGC/ARGO data portal API, Zenodo (for self-publication + DOI). Integration is
  *metadata-only*; no bulk data download, no controlled-access access.
- **Datasets:** specific open Ewing datasets — TO BE SELECTED via `coverage-005` + the gate; none
  assumed in scope yet.
- **Sibling Hee-Lee Oss projects:** `ewsr1-fli1-knowledge-graph` (primary downstream consumer),
  `ewing-expression-reanalysis`, `ewing-literature-corpus`, `ewing-single-cell-atlas`; and the
  pattern-sibling `open-data-datasheets` (gate/template reuse).
- **Hee-Lee Oss pieces:** Task JSON schema (`packages/schema`), donated-lane CLI workspace/PR flow
  (`packages/cli`), good-deed definition + refusal guardrails. No funded-lane/runner dependency
  (donated lane).

## Risks & mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
| --- | --- | --- | --- | --- |
| Mistaking a **controlled-access** study (dbGaP/EGA/DACO/TARGET-controlled) for open and documenting it as reusable | Medium | High | Access-tier is the *first* blocking gate with cited `evidenceUrl`; positive open-status confirmation required or EXCLUDE; controlled-case fixture in CI | License+Access+Reid reviewer |
| **Re-identification** in a rare cancer (germline data, small-N cells, linkage) | Medium | High | Re-identification methodology in the gate; exclude germline-level data; k<5 small-cell flag; never re-identify/link; reviewer sign-off | License+Access+Reid reviewer |
| Misclassifying a **license** (treating non-derivable/NC/embargoed terms as reusable) | Medium | High | Mandatory reviewer; cited `permitsDerivatives` clause; COSMIC/OncoKB NC excluded; embargo check; snapshot recorded | License+Access+Reid reviewer |
| Source family lacks open Ewing data (e.g. TARGET) → wasted effort | Medium | Medium | `coverage-005` verifies open-Ewing split per source *before* tasking | Maintainer |
| Slipping into **clinical interpretation** / patient-facing advice (would require `high` + oncologist) | Low | High | "Research metadata only — not medical advice" label; strictly descriptive; escalate-or-remove rule; reviewer rejects clinical claims | Maintainer |
| Factual errors in molecular/fusion annotation or data dictionary | Medium | Medium | Annotation must cite the dataset's publication; technical review; validation script | Technical reviewer |
| No partner secured → index produced but never adopted (fails "delivered") | Medium | High | M0 outreach; Zenodo DOI self-serve fallback; Steward role; `verifiedNeed:false` until secured | Steward |
| Source metadata changes/disappears (GEO/cBioPortal/ICGC versions drift) | Medium | Medium | Record version + retrieval date; validation detects drift; refresh milestone | Maintainer |
| Repository API / Croissant spec drift | Medium | Low | Canonical-model-first; pinned spec/API versions; adapters isolated; version-bump tasks | Maintainer |
| Index shaped to favor a for-profit reuser over the public | Low | Medium | COI stance; inclusion criteria are need/openness-based; sponsorship disclosed, non-gating | Maintainer |
| Scope creep into re-analysis/cleaning/hosting data | Medium | Medium | Explicit non-goal; reviewers reject any data-transformation work; re-analysis is a separate project | Maintainer |

## Security & privacy

- **Threat surface is small** (no runtime service, no data hosting). Main surfaces are CI, the
  metadata files we publish, and the inspection step.
- **No controlled-access ever.** We hold no dbGaP/EGA/DACO credentials and never request them. If
  reaching a field requires authorization, the dataset is controlled → excluded.
- **Secrets handling:** adapters use only public, unauthenticated metadata endpoints by default; no
  credentials. Any API token (e.g. higher GEO rate limits) is supplied by the human and never written
  to logs, receipts, or committed files (Hee-Lee Oss rule).
- **PII / re-identification:** the dominant privacy concern is upstream genomic/clinical data.
  Handled by the access-tier + re-identification gate. We inspect aggregate metadata only, store
  nothing, commit no individual-level data, and halt on any signal.
- **Abuse/misuse prevention:** refuse and flag any task steering toward de-anonymization, linkage,
  laundering controlled-access data as open, surveillance, or producing clinical advice. Documentation
  stays descriptive, source-verified, and labeled "not medical advice."

## Sustainability & maintenance

- **Post-delivery ownership:** the Steward maintains partner/sibling-project relationships; the
  Maintainer keeps the toolkit (validators, adapters, template) and the index current with
  spec/API/source changes.
- **Refresh:** validation scripts re-check an entry against its documented version; recorded version +
  cadence flags when a refresh is due. Stale entries become `maintenance` tasks. The index is
  re-archived to Zenodo on each version (new DOI), keeping every version citable.
- **Outcome tracking:** the Steward records adoption events and external reuse signals against the
  success metrics, reviewed each milestone. The sibling KG project's consumption is tracked as a
  first-class reuse signal.

## Open questions

- Which advocacy org / repository / sibling-project owner will be the first confirmed partner?
- Does TARGET/GDC actually hold an open-access Ewing cohort, or should TARGET be dropped from the
  source families after `coverage-005`? (Resolve in M0; do not assume.)
- For Treehouse and ICGC open tiers, does the data-use agreement permit redistributing *derivative
  metadata* without per-record registration? (Default: record the DUA; escalate to `policy-004`.)
- How do we handle a dataset that is open expression data *but* links to a controlled-access raw
  tier — document the open part with an explicit "controlled raw tier excluded" note, or exclude
  entirely? (Default: document open part only, with the exclusion noted; reviewer confirms.)
- ~~Where is the license/terms snapshot stored?~~ **Decided (must precede `snapshot-010`):** a
  committed local copy of the license/terms page + SHA-256 hash + Wayback save URL; `snapshotRef`
  records the committed path, hash, and Wayback timestamp. Bare URL alone is insufficient.
- What counts as a sufficiently "verifiable external reuse event" for the outcome metric? (Default:
  a citation/DOI reference, a merged PR, or a sibling-project import — not self-reported.)

## References

- Hee-Lee Oss work rules — `C:\code\hee-lee-oss\CLAUDE.md`
- Good Deed Definition + risk tiers — `C:\code\hee-lee-oss\docs\good-deed-definition.md`
- Cancer-track domain guardrails — `C:\code\hee-lee-oss\planning\ROADMAP.md` (Track 8)
- Task JSON schema — `C:\code\hee-lee-oss\packages\schema\src\schemas.ts`
- Pattern-sibling plan — `C:\code\hee-lee-oss\planning\projects\open-data-datasheets\PLAN.md`
- Datasheets for Datasets (Gebru et al., 2018/2021); Data/Model Cards
- Croissant ML metadata format specification (MLCommons v1.0)
- NCBI GEO / E-utilities; GDC API; cBioPortal web API; ICGC/ARGO data portal; UCSC Treehouse
- FAIR data principles; schema.org/Dataset; SPDX license list; Creative Commons CC0 / CC-BY 4.0

---

## Appendix A — Improvements applied

Per the planning process, an initial draft was written, then critiqued with **25 specific
improvements**, and **all 25 were applied** to the plan and `TASKS.md` above. The list is retained
here so the work is visible. Each item names the concrete change made (not a generic aspiration).

1. **Split "access tier" out as a distinct, first blocking gate** (open vs controlled), separate from
   license — controlled-access (dbGaP/EGA/DACO/TARGET-controlled) is an immediate EXCLUDE. *Applied:*
   three-part gate in Architecture/Compliance; `gate-003`; risk row #1; CI controlled-case fixture.
2. **Added a genomic re-identification methodology** beyond generic PII (germline-level exclusion,
   k<5 small-cell flag, linkage). *Applied:* Compliance "Re-identification stance"; gate; risk #2.
3. **Pinned source-API + spec versions** (GEO E-utilities, cBioPortal API, GDC API, ICGC portal,
   Croissant v1.0). *Applied:* "Pinned source/spec versions"; `specVersions` field; adapter ACs.
4. **Per-source license matrix with conservative defaults**, incl. COSMIC/OncoKB non-commercial
   exclusion and TCGA-via-cBioPortal as open. *Applied:* Compliance "Source licenses/terms"; `policy-004`.
5. **Honest TARGET coverage flag** — TARGET's flagship cancers are not Ewing; coverage must be
   verified. *Applied:* Scope "candidate source families"; `coverage-005`; risk #4; open question.
6. **Small-N rare-disease privacy treatment** (k<5 cells) since Ewing cohorts are tiny. *Applied:*
   re-identification stance; `smallCellsFlag` field; risk #2.
7. **Oncology-specific acceptance channels** (Zenodo DOI self-publish, partner adoption, repo PR,
   sibling-project consumption). *Applied:* Success metrics "What 'adopted' means"; M0 cold-start.
8. **Mandatory "research metadata only — not medical advice" label** on every output to keep the
   project at `medium` and non-patient-facing. *Applied:* header, non-goals, `disclaimer` field, DoS.
9. **Named the exact expert reviewer competency** (combined license + genomic-data-governance), plus
   a conditional oncologist+advocate escalation path. *Applied:* Quality gates; Governance.
10. **`dataUseConditions` field** to capture registration/DUA terms (Treehouse, ICGC) even when
    "open." *Applied:* canonical model; license record; `snapshot-010`.
11. **Provenance tied to a primary publication (PMID/DOI) + consortium policy URL.** *Applied:*
    provenance model; canonical `provenance` block; datasheet pipeline step 2.
12. **Outcome ledger with before/after completeness + effort metrics.** *Applied:* Success metrics;
    `reuse-019`; M2 effort-reduction exit criterion.
13. **Defined a 0–100 documentation-completeness score** for biomedical datasets. *Applied:* Success
    metrics; DoS ≥ 90/100; per-dataset ACs.
14. **Duplicate/lineage detection** (GEO reposts, cBioPortal re-curations of the same cohort) to
    avoid double-counting. *Applied:* `lineage` field; backlog `dedup-022`; known-issues.
15. **Explicit cross-linking to sibling Ewing projects + reuse of the `open-data-datasheets` gate/
    template** to avoid duplicating effort. *Applied:* beneficiaries; dependencies; key decisions;
    backlog `kg-handoff-025`.
16. **Ewing-specific molecular/fusion annotation field, sourced from publication (never inferred).**
    *Applied:* `molecular` field; pipeline step 4; technical-review AC.
17. **Explicit abuse-prevention stance: never re-identify/link/download controlled data.** *Applied:*
    Security & privacy; access protocol; non-goals.
18. **Staleness/refresh + version-drift handling** for living repositories. *Applied:* Sustainability;
    `refresh-020`; risk #8; validation detects drift.
19. **Made the gate reviewer a non-skippable role filled before the pilot.** *Applied:* Governance;
    `reviewer-001` as first M0 task blocking `pilot-009`.
20. **Fixture strategy using captured public *metadata* responses only** (no individual-level data
    committed). *Applied:* Quality "Test fixtures"; adapter ACs.
21. **Beneficiary-centric success metrics with baselines/targets** (adopted index entries, not
    "datasheets written"). *Applied:* Success metrics table.
22. **Risk row for controlled-access-as-open mistake** with explicit mitigation. *Applied:* risk #1.
23. **Risk row for rare-disease re-identification** with threshold + reviewer mitigation. *Applied:*
    risk #2.
24. **COI / for-profit-benefit governance note** (index must not favor a pharma reuser). *Applied:*
    Governance COI stance; risk #10; non-goals.
25. **An M0 source-family coverage-verification task** that records the open vs controlled Ewing split
    per source before any dataset is tasked. *Applied:* `coverage-005`; M0 exit criterion (4); seeds
    the M1+ triage funnel.

---

## Review sign-off

A completeness/correctness review of the revised plan + `TASKS.md` was performed against the
PLAN_SPEC structure, the Hee-Lee Oss guardrails, and the Task JSON schema. Findings and resolutions:

- **All 17 required H2 sections present and in order**; metadata header present; Appendix A (25
  improvements, all applied) and this sign-off appended.
- **Metrics measurable:** every success metric has a baseline + 6-month target; "improves reuse"
  operationalized as a 0–100 completeness score; effort defined in session-minutes + review cycles.
- **Gates enforceable:** the three-part gate (access-tier → license → re-identification) is a
  blocking, committed artifact with a named non-skippable reviewer filled before the pilot; CI
  carries a controlled-access EXCLUDE fixture and an NC-reference-DB EXCLUDE fixture.
- **Risks own­ed + mitigated:** every risk row has a named owner and a concrete mitigation; the two
  headline biomedical risks (controlled-access-as-open; rare-disease re-identification) are rated
  High-impact with explicit, testable mitigations.
- **Guardrails present:** license/provenance verification (open/PD/CC + `permitsDerivatives` clause,
  snapshot), controlled-access categorically excluded, COSMIC/OncoKB NC excluded, re-identification
  methodology, "not medical advice" labeling, conditional oncologist+advocate escalation, COI/for-
  profit stance — all present.
- **Sequencing sound:** M0 (toolkit + gate + coverage verification + pilot) → M1 (gate hardened +
  adoptions + index v0.1) → M2 (adapters + scale) → M3 (reuse + sustainability); dependencies stated
  and reflected in the task `Depends on` columns.
- **Tasks schema-valid:** all backlog tasks map to required Task JSON fields; the example Task JSON
  was checked field-by-field against `packages/schema/src/schemas.ts` (all required fields present,
  enums valid, donated lane so no `fundedBudgetUsd` required); `verifiedNeed: false` and
  `requestor: "TO BE SECURED"` throughout (no partner secured).
- **One fix surfaced during review and applied:** ensured no task carries `deliverable: dataset`
  (the data is never our deliverable) — code → `pr`, all documentation/metadata/index → `document`.

**Headline gate:** no dataset is documented unless it passes the **access-tier → license →
re-identification** gate (open-access only; `permitsDerivatives` clause cited; rare-disease
re-identification acceptable), signed off by the named License+Access+Re-identification reviewer.
**Headline human decision needed:** secure a partner/requestor and confirm TARGET's open-Ewing
coverage — until then `verifiedNeed` stays `false`.
