# TASKS — ewing-open-data-catalog

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated
>
> Standing label on every deliverable: **research metadata only — not medical advice.**

## How these tasks map to Elyos

Each task below becomes an Elyos **Task JSON** validated against
`packages/schema/src/schemas.ts`. Field mapping:

- `id` — stable slug ID from the tables (e.g. `ewing-open-data-catalog-template-002`).
- `title` — the table's Title.
- `project` — `ewing-open-data-catalog`.
- `type` — one of `code | research | writing | data | design-spec | maintenance` (per table).
- `lane` — `donated` for all tasks here (no funded escrow). A funded task would add `fundedBudgetUsd`.
- `priority` — `high | medium | low`.
- `domain` — array, e.g. `["cancer-research","ewing-sarcoma","open-data","genomics","open-science"]`.
- `riskTier` — `low | medium | high`. Gate/governance + sensitive-domain tasks are `medium`; the
  project never silently does `high` work (clinical-interpretation tasks are out of scope / escalated).
- `urgent` — boolean; `false` for all current tasks.
- `deliverable` — `pr | dataset | document | translation`. **We never deliver `dataset`** (the data is
  out of scope); code → `pr`, docs/metadata/index → `document`, translations → `translation`.
- `tokenEstimate` — `small | medium | large` (Size column).
- `status` — `open | in-progress | review | delivered | done`; all start `open`.
- `context`, `objective`, `acceptanceCriteria[]`, `resources[]`, `output` — per task.
- `requestor` — **TO BE SECURED** until a partner is confirmed.
- `verifiedNeed` — **`false`** until a named partner/repo/sibling-project agrees to adopt or consume
  the catalog (general need is real; per-task delivery need is unproven).
- `outputLicense` — `CC-BY-4.0` for documentation/metadata/index; `MIT` for code (validators/adapters).

**Reviewer legend:** `Gate` = License+Access+Re-identification reviewer (mandatory, non-skippable);
`Technical` = technical reviewer; `Maintainer` / `Steward` as in PLAN governance.

---

## Milestone M0 — Foundation & cold-start

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ewing-open-data-catalog-reviewer-001 | Name/secure the License+Access+Re-identification reviewer (blocking, non-skippable gate role) | research | small | medium | document | — | Maintainer |
| ewing-open-data-catalog-template-002 | Datasheet template + canonical biomedical metadata model | writing | small | low | document | — | Technical |
| ewing-open-data-catalog-gate-003 | Three-part triage gate: access-tier + license + re-identification (blocking) | design-spec | small | medium | document | — | Gate |
| ewing-open-data-catalog-policy-004 | NC / DUA / share-alike acceptance policy (COSMIC/OncoKB NC, Treehouse/ICGC DUA) | design-spec | small | medium | document | gate-003 | Gate |
| ewing-open-data-catalog-coverage-005 | Source-family coverage verification (open vs controlled Ewing split: GEO/TARGET/Treehouse/cBioPortal/ICGC) | research | medium | medium | document | gate-003 | Gate |
| ewing-open-data-catalog-croissant-006 | Croissant ML metadata generator + spec validator | code | medium | low | pr | template-002 | Technical |
| ewing-open-data-catalog-validator-007 | Reusable metadata validation script + quality report | code | small | low | pr | template-002 | Technical |
| ewing-open-data-catalog-outreach-008 | Partner/sibling-project outreach + candidate dataset shortlist | research | small | low | document | coverage-005 | Maintainer |
| ewing-open-data-catalog-pilot-009 | One GEO Ewing series: datasheet end-to-end + published index entry (Zenodo DOI fallback) | data | medium | medium | document | reviewer-001, template-002, gate-003, policy-004, coverage-005, croissant-006, validator-007, outreach-008 | Gate, Technical |

**Acceptance criteria — key tasks**

- **template-002 (template + canonical model)**
  - [ ] Canonical metadata model documents every field from PLAN: `id`, `title`, `accession`,
        `repository`, `submitterOrConsortium`, `accessTier{tier,evidenceUrl}`,
        `license{id,url,permitsDerivatives,snapshotRef,dataUseConditions}`,
        `provenance{retrievedAt,version,publicationPmidDoi,consortiumPolicyUrl,attribution}`,
        `reidentification{riskLevel,basis,smallCellsFlag,germlinePresent,notes}`,
        `molecular{tumorType,driverFusion,assay,cohortSizeAggregate,sourcePublication}`, `fields[]`,
        `knownIssues[]`, `lineage{duplicateOf,supersedes}`, `examples[]`, `specVersions`,
        `completenessScore{before,after}`, `disclaimer`.
  - [ ] Markdown datasheet template covers the Datasheets-for-Datasets questionnaire (incl. a
        consent/ethics-provenance section) plus data dictionary, provenance, license/terms record,
        molecular annotation, known-issues, lineage, and worked examples.
  - [ ] Template states the deliverable is documentation/metadata, **not** data; carries the
        "research metadata only — not medical advice" label; documentation output licensed CC-BY-4.0.
  - [ ] At least one filled-in worked example skeleton (synthetic/public metadata only) is included.

- **gate-003 (three-part blocking gate)**
  - [ ] Gate runs in fixed order, all blocking: **(a) access-tier** — PASS only if positively
        confirmed open-access with a cited `evidenceUrl`; controlled-access (dbGaP/EGA/DACO/
        TARGET-controlled/individual biobank) = immediate EXCLUDE; unconfirmable = EXCLUDE.
  - [ ] **(b) license** — PASS only if `permitsDerivatives: true` is set from a cited clause/URL;
        missing/unparseable/NC-reference-DB/embargoed = FLAG/EXCLUDE (no default-allow); defers
        NC/DUA/share-alike cases to `policy-004`.
  - [ ] **(c) re-identification** — applies the methodology: germline-variant-level data EXCLUDED;
        k<5 small-cell flag; geo/linkage checks; aggregate-only confirmed. Any flag = EXCLUDE/FLAG
        unless publisher-documented aggregation meets thresholds; we never re-identify or anonymize.
  - [ ] Inspection during triage follows the access protocol (metadata/header reads, open tier only,
        aggregate only, local/ephemeral, no committed individual-level data; halt on any signal).
  - [ ] Produces a committed, reviewable PASS/FLAG/EXCLUDE artifact per dataset recording which checks
        ran and what fired, plus the completeness before-score.

- **coverage-005 (source-family coverage verification)**
  - [ ] For each named source family (GEO, TARGET/GDC, Treehouse, cBioPortal, ICGC) record whether it
        holds **open-access Ewing** data, with cited evidence and the open vs controlled split.
  - [ ] Explicitly resolves the TARGET question (does an open Ewing cohort exist?); if not, recommends
        dropping TARGET from the source families with rationale recorded.
  - [ ] Output is a committed candidate shortlist (≥ 6 plausibly-open Ewing datasets) ordered by a
        realistic adoption path, each still requiring its own `gate-003` artifact before tasking.

- **croissant-006 (Croissant generator + validator)**
  - [ ] Emits and validates against the **pinned Croissant ML v1.0** context/SHACL (version recorded
        in `specVersions`).
  - [ ] Ships committed golden fixtures (synthetic/public metadata only): valid metadata that must
        pass and malformed cases that must fail, exercised in CI.
  - [ ] Code MIT-licensed; `pnpm build && pnpm test && pnpm lint` green; DCO signed-off.

- **pilot-009 (pilot GEO Ewing series, end-to-end)**
  - [ ] Pilot selected on a realistic delivery path: an informal adoption channel if one exists, else
        the **Zenodo DOI self-serve fallback** so a real *delivered* outcome is reachable.
  - [ ] Dataset passed `gate-003` (open access confirmed; license permits derivative metadata; re-id
        risk acceptable) with the artifact committed.
  - [ ] Complete canonical record + Datasheet + valid Croissant metadata + molecular annotation
        (fusion sourced from the dataset's publication); completeness recorded (before/after, after ≥
        90/100).
  - [ ] Validation script runs clean in CI and emits a quality report; no individual-level data
        committed.
  - [ ] Provenance recorded (accession, version, PMID/DOI, consortium policy URL, attribution;
        license snapshot = committed copy + SHA-256 + Wayback URL); "not medical advice" label present.
  - [ ] Index entry **published with a Zenodo DOI** (and adopted via an informal channel if one
        exists), with the Steward's acceptance evidence artifact (`outcomes/<dataset-id>.json`)
        recorded — or, if no channel materializes, **submitted** with the blocker surfaced.

**M0 Definition of Done:** gate reviewer named (blocking role filled before pilot review); template +
canonical model + three-part gate + NC/DUA/share-alike policy published (policy merged before any
triage); source-family coverage verified (open vs controlled Ewing split recorded; TARGET resolved);
Croissant generator + one validation script green in CI with golden fixtures; one GEO Ewing series
documented end-to-end and **published with a Zenodo DOI** (evidence artifact recorded) — or submitted
with the blocker surfaced; ≥ 1 partner-outreach thread opened.

---

## Milestone M1 — Gate hardened + first adoptions + index v0.1

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ewing-open-data-catalog-snapshot-010 | License/data-use-terms snapshot capture in provenance flow | code | small | low | pr | template-002, gate-003 | Technical |
| ewing-open-data-catalog-triage-011 | Triage 6 candidate Ewing datasets through the three-part gate | research | medium | medium | document | gate-003, policy-004, coverage-005 | Gate |
| ewing-open-data-catalog-doc-012 | Datasheet for adopted dataset #2 (cBioPortal Ewing study) | data | medium | medium | document | pilot-009, triage-011 | Gate, Technical |
| ewing-open-data-catalog-doc-013 | Datasheet for adopted dataset #3 (ICGC open-tier Ewing project) | data | medium | medium | document | pilot-009, triage-011 | Gate, Technical |
| ewing-open-data-catalog-partner-014 | Secure first confirmed partner / sibling-project consumer | research | small | low | document | outreach-008 | Steward |

**Acceptance criteria — key tasks**

- **snapshot-010 (license/terms snapshot capture)**
  - [ ] Implements the **decided** format: committed local copy of the license/terms page + SHA-256
        hash + Wayback save URL; `license.snapshotRef` records committed path, hash, Wayback timestamp;
        also captures `dataUseConditions` text where a DUA/registration applies. Bare URL insufficient.
  - [ ] Code MIT-licensed; tests + CI green; no credentials embedded.

- **triage-011 (triage 6 candidates)**
  - [ ] Six datasets evaluated with a committed `gate-003` artifact each (access-tier + license + re-id;
        PASS/FLAG/EXCLUDE + rationale), applying `policy-004`.
  - [ ] Each PASS records access-tier evidence, license id/URL/snapshot, `permitsDerivatives: true`
        with cited clause, and the re-identification assessment.
  - [ ] Any controlled-access, NC reference DB, embargoed, germline-level, or small-N-risky dataset is
        EXCLUDED/FLAGGED with the concern surfaced (not guessed).

- **doc-012 / doc-013 (datasets #2 and #3)** *(shared pattern)*
  - [ ] Source passed `gate-003` with committed artifact; molecular/fusion annotation sourced from the
        dataset's publication (PMID/DOI), never inferred.
  - [ ] Complete canonical record + Datasheet + valid Croissant; completeness ≥ 90/100 (before/after
        recorded); "not medical advice" label present; no individual-level data committed.
  - [ ] Entry added to index v0.1 and **adopted/cited/DOI-published**, with the Steward's acceptance
        evidence artifact recorded — or submitted with the blocker surfaced.

- **partner-014 (first confirmed partner)**
  - [ ] A named advocacy org / repository / sibling-project owner confirms they will adopt, host,
        cite, or consume the catalog.
  - [ ] Adoption/consumption mechanism documented (index link / repo PR / sibling-project import).
  - [ ] Tasks for that partner updated to `verifiedNeed: true` with `requestor` set.

**M1 Definition of Done:** three-part gate applied to ≥ 6 datasets with committed artifacts; ≥ 2
datasets documented and in an **adopted/cited/DOI-published** index (v0.1); ≥ 1 confirmed
partner/consumer; license/terms-snapshot capture working in the decided format.

---

## Milestone M2 — Source adapters & scale

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ewing-open-data-catalog-geo-015 | GEO / NCBI E-utilities metadata adapter | code | medium | low | pr | croissant-006 | Technical |
| ewing-open-data-catalog-cbioportal-016 | cBioPortal web-API metadata adapter | code | medium | low | pr | croissant-006 | Technical |
| ewing-open-data-catalog-gdc-017 | GDC / ICGC open-tier metadata adapter | code | medium | medium | pr | croissant-006 | Technical, Gate |
| ewing-open-data-catalog-scale-018 | Datasheets for datasets #4–#6 via adapters | data | large | medium | document | geo-015, cbioportal-016, partner-014 | Gate, Technical |

**Acceptance criteria — key tasks**

- **geo-015 (GEO adapter)** *(pattern also applies to cbioportal-016 and gdc-017)*
  - [ ] Transforms the source's **public metadata** response into a valid canonical record for the
        **pinned API version** (recorded in `specVersions`): geo-015 → E-utilities ESummary/EFetch;
        cbioportal-016 → cBioPortal `/api` study/clinical-attribute; gdc-017 → GDC/ICGC open-tier
        cases/files metadata.
  - [ ] Ships committed golden **captured public-metadata response → expected canonical record**
        fixtures, diffed in CI; output validated against the canonical-model schema.
  - [ ] **Open tier only:** the adapter never requests authenticated/controlled-access endpoints; for
        gdc-017 the Gate reviewer confirms the open-tier scoping (hence `riskTier: medium`).
  - [ ] Code MIT-licensed; unit tests + CI green; no credentials embedded; no individual-level data
        in fixtures.

- **scale-018 (datasets #4–#6)**
  - [ ] All three datasets pass `gate-003` with committed artifacts.
  - [ ] Canonical records emitted via the relevant adapter; entries adopted/DOI-published, spanning
        ≥ 2 source families, with acceptance evidence artifacts recorded.
  - [ ] Per-dataset effort recorded in the outcome ledger (AI-session minutes + review cycles) to show
        reduction vs. the recorded M0/M1 baseline median.

**M2 Definition of Done:** ≥ 2 source adapters emitting valid canonical metadata (golden
captured-response fixtures, pinned API versions); ≥ 5 datasets documented + adopted cumulatively
across ≥ 2 source families; measurable median per-dataset effort reduction vs. the M0/M1 baseline.

---

## Milestone M3 — Reuse outcomes & sustainability

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ewing-open-data-catalog-reuse-019 | Track and verify external reuse events (incl. sibling-project consumption) | research | small | low | document | doc-012, doc-013, scale-018 | Steward |
| ewing-open-data-catalog-refresh-020 | Staleness/refresh process + source version-drift detection | maintenance | small | low | document | validator-007 | Maintainer |
| ewing-open-data-catalog-landscape-021 | Broaden coverage across ≥ 3 source families → index v1.0 | data | large | medium | document | scale-018, refresh-020 | Gate, Technical |

**Acceptance criteria — key tasks**

- **reuse-019 (reuse tracking)**
  - [ ] ≥ 3 verifiable external reuse events recorded in the outcome ledger (citation/DOI reference,
        merged PR, or sibling-project import — incl. ≥ 1 sibling-project consumption).
  - [ ] Each event links to externally verifiable evidence (no self-reported reuse).

- **refresh-020 (staleness/refresh)**
  - [ ] Documented process to detect when a documented dataset has drifted from its recorded version
        (GEO/cBioPortal/ICGC updates); validation script flags drift; stale entries become
        `maintenance` tasks.
  - [ ] Index re-archived to Zenodo on each version (new DOI), keeping prior versions citable.

**M3 Definition of Done:** ≥ 3 verifiable reuse events (≥ 1 sibling-project); ≥ 6 datasets adopted
cumulatively across ≥ 3 source families (index v1.0); maintenance/refresh process documented and a
steward identified for ongoing liaison.

---

## Backlog / future

| ID | Title | Type | Size | Risk | Deliverable | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| ewing-open-data-catalog-dedup-022 | Duplicate/lineage detection across reposts & re-curations | code | medium | low | pr | Populates `lineage{duplicateOf,supersedes}`; avoids double-counting cohorts |
| ewing-open-data-catalog-i18n-023 | Translate a delivered datasheet summary (domain reviewer) | translation | small | medium | translation | Widens reuse; needs bilingual domain reviewer; keep "not medical advice" label |
| ewing-open-data-catalog-dash-024 | Outcome dashboard for adopted entries + reuse events | code | medium | low | pr | Reads the outcome ledger; supports success-metric tracking |
| ewing-open-data-catalog-kg-handoff-025 | Structured handoff feed to ewsr1-fli1-knowledge-graph | design-spec | small | low | document | Vetted-dataset feed for the sibling KG project; defines the export contract |

---

## Example task JSON

```json
{
  "id": "ewing-open-data-catalog-reviewer-001",
  "title": "Name/secure the License+Access+Re-identification reviewer (blocking gate role)",
  "project": "ewing-open-data-catalog",
  "type": "research",
  "lane": "donated",
  "priority": "high",
  "domain": ["cancer-research", "ewing-sarcoma", "open-data", "genomics", "data-governance"],
  "riskTier": "medium",
  "urgent": false,
  "deliverable": "document",
  "tokenEstimate": "small",
  "status": "open",
  "context": "This catalog documents only OPEN-ACCESS, aggregate, de-identified Ewing sarcoma datasets; controlled-access (dbGaP/EGA/DACO) and individual-level data are out of scope. Because Ewing is a rare pediatric/AYA cancer, license interpretation, access-tier verification, and genomic re-identification risk require specialist judgement. The three-part gate (access-tier + license + re-identification) is a non-skippable blocking step, so a named, qualified reviewer must exist before any dataset is documented. No partner is yet secured, so verifiedNeed is false and requestor is TO BE SECURED.",
  "objective": "Recruit/designate and record a named reviewer competent in both open-data/biomedical licensing (CC/SPDX/consortium DUAs) and genomic-data governance / re-identification risk, who will sign off the blocking gate before the M0 pilot is reviewed.",
  "acceptanceCriteria": [
    "A named reviewer (with stated qualification in open-data/biomedical licensing AND genomic-data governance / re-identification) is recorded in PLAN.md Governance.",
    "The reviewer's scope and authority are documented: confirms access tier is open, license permits derivative metadata (permitsDerivatives clause cited), and re-identification risk is acceptable; can EXCLUDE/FLAG any dataset.",
    "At least one named, qualified reviewer exists at all times; a rotation of >= 2 is preferred to avoid a single-person bottleneck; if none exists, triage and documentation halt.",
    "The role is confirmed filled before the M0 pilot task (ewing-open-data-catalog-pilot-009) is reviewed; until filled, all tasks remain verifiedNeed:false and no dataset can pass the gate.",
    "Conflict-of-interest stance recorded: the reviewer must not be steered to shape inclusion toward any for-profit beneficiary."
  ],
  "resources": [
    "C:\\code\\elyos\\planning\\projects\\ewing-open-data-catalog\\PLAN.md",
    "C:\\code\\elyos\\docs\\good-deed-definition.md",
    "C:\\code\\elyos\\planning\\ROADMAP.md",
    "Datasheets for Datasets (Gebru et al.)",
    "SPDX license list; Creative Commons CC0 / CC-BY 4.0"
  ],
  "output": "A short governance document naming the License+Access+Re-identification reviewer(s), their qualifications, scope/authority, rotation plan, and COI stance, recorded in PLAN.md Governance and committed to the project repo.",
  "requestor": "TO BE SECURED",
  "verifiedNeed": false,
  "outputLicense": "CC-BY-4.0"
}
```

---

## Backlog rollup

- **Scheduled tasks: 18** across 4 milestones (M0: 9, M1: 5, M2: 4, M3: 3).
- **Backlog (sized, unscheduled): 4** (dedup, i18n, dashboard, KG handoff) → **22 total**.
- Every per-dataset documentation task is blocked on its own committed `gate-003` artifact (access-tier
  → license → re-identification) before work proceeds; listing a candidate never pre-approves it.
- No task delivers `dataset`: code → `pr`; documentation/metadata/index → `document`; translation →
  `translation`. `verifiedNeed: false` and `requestor: "TO BE SECURED"` until a partner is confirmed.
