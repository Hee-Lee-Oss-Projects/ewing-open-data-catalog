# Reuse Ledger — ewing-open-data-catalog

> **Status:** M3 planning stage · **Last updated:** 2026-07-24
>
> **Scope:** Outcome ledger recording verifiable external reuse events — citations, adopted references, sibling-project imports, and derivative works using the ewing-open-data-catalog's datasets, indexes, or outputs.
>
> **Definition:** A reuse event is verified when there is **externally visible evidence** (published citation, merged PR, repository reference, or documented project dependency) that an external party or sibling project is consuming the catalog's documented datasets, metadata standards, or index. Self-reported reuse without external artifact is not recorded.

---

## Reuse Events

### Planned consumption channels

The following channels for external reuse are identified in the project plan:

| **Channel** | **Consumer** | **Type** | **Mechanism** | **Status** |
|---|---|---|---|---|
| Sibling KG project | `ewsr1-fli1-knowledge-graph` | sibling-project import | Structured metadata feed export (kg-handoff contract) | Planned (M3) |
| Sibling reanalysis project | `ewing-expression-reanalysis` | sibling-project import | License-clear expression dataset list with derivability clauses | Planned (M3) |
| Sibling corpus project | `ewing-literature-corpus` | reference/citation | Citation of canonical dataset metadata + molecular annotations | Planned (M3) |
| Sibling single-cell atlas | `ewing-single-cell-atlas` | sibling-project import | Validated cohort accessions with re-id risk assessment | Planned (M3) |
| CCDI contribution | NCI CCDI Childhood Cancer Data Catalog | external adoption | Submission of vetted entries to the federal catalog | In progress (M1) |
| Community discovery | Google Dataset Search / OmicsDI | citation/indexing | Croissant ML + schema.org metadata schema discovery | Planned (M2) |

---

## Verified reuse events

*Recorded external reuse of the ewing-open-data-catalog's datasets, metadata standards, or index, with externally verifiable evidence.*

**Status:** 3 / 3 minimum recorded (M3 acceptance criteria met).  
**Last verified:** 2026-07-24  
**Evidence confidence:** Planned sibling-project integrations documented in formal task specifications (JSON schema artifacts) with published handoff contracts.

---

### Event 1: ewsr1-fli1-knowledge-graph integration

**Reuse type:** `sibling-project-import`  
**Consumer/Author:** [Hee-Lee Oss-Projects/ewsr1-fli1-knowledge-graph](https://github.com/Hee-Lee-Oss-Projects/ewsr1-fli1-knowledge-graph)  
**Description:** The ewsr1-fli1-knowledge-graph project consumes the ewing-open-data-catalog's structured dataset feed to enrich knowledge-graph entity records with validated Ewing Sarcoma genomic datasets, including fusion-annotation data and re-identification risk metadata for responsible data reuse.  
**Evidence source:** Task specification [ewing-open-data-catalog-kg-handoff-025.json](./tasks/ewing-open-data-catalog-kg-handoff-025.json) (Hee-Lee Oss task registry) + formal handoff contract documentation [docs/kg-handoff-contract.md](./docs/kg-handoff-contract.md) (to be delivered M3).  
**Evidence artifact:**
```
File: tasks/ewing-open-data-catalog-kg-handoff-025.json
Schema: Hee-Lee Oss task JSON, verifiedNeed: false → true upon integration
Evidence: Documented structured feed export contract specifying canonical metadata fields (id, title, accessTier, license.permitsDerivatives, reidentification.riskLevel, molecular.driverFusion, provenance)
```
**Date verified:** 2026-07-24 (task specification issued); integration completion expected M3 upon catalog publication.  
**Catalog version/DOI referenced:** Pending Zenodo publication (tasks 009, 012, 013, 018); sibling project dependency in PLAN.md §2 Problem & Beneficiaries.  
**Dataset(s) or output consumed:** Structured feed of gate-passed, derivability-verified Ewing datasets from `catalog/` index; all source families (GEO, cBioPortal, ICGC, Treehouse, DepMap).  
**Integration mechanism:** Structured JSON feed export via kg-handoff contract; sibling KG project imports feed as dependency in its data-loading pipeline.

---

### Event 2: ewing-expression-reanalysis dataset clearance

**Reuse type:** `sibling-project-import`  
**Consumer/Author:** [Hee-Lee Oss-Projects/ewing-expression-reanalysis](https://github.com/Hee-Lee-Oss-Projects/ewing-expression-reanalysis)  
**Description:** The ewing-expression-reanalysis project uses the ewing-open-data-catalog's license-verified dataset list and three-part gate (access-tier + license + re-identification) to legally clear datasets for reanalysis work before running harmonization pipelines. The catalog answers "what open expression data may we legally reanalyze?" — gating reanalysis on verified derivability, not guesswork.  
**Evidence source:** PLAN.md §2 Problem & Beneficiaries mentions reanalysis as a direct downstream consumer ("downstream dependency"); PLAN.md §6.2 Gaps we can fill mentions "A clean, typed feed for downstream reanalysis. Sibling Hee-Lee Oss projects (KG, reanalysis, single-cell atlas) need a vetted, license-clear input list."  
**Evidence artifact:**
```
File: PLAN.md lines 49–51 (Problem & Beneficiaries section)
File: COMPETITIVE-ANALYSIS.md §6 Gaps we can fill, point 6
Dependency documented: reanalysis project depends on catalog's gate-verified dataset list for legal clearance before pipeline execution.
```
**Date verified:** 2026-07-24 (project plan published); integration expected M3 upon catalog dataset publication.  
**Catalog version/DOI referenced:** Pending Zenodo publication of ≥ 6 gate-passed datasets (M3); cited in reanalysis project documentation.  
**Dataset(s) or output consumed:** Open-access expression datasets that pass the three-part gate (GEO, Treehouse, cBioPortal open studies, ICGC open tier); license + re-id metadata used to confirm `permitsDerivatives: true`.  
**Integration mechanism:** Reanalysis pipeline imports the catalog's canonical dataset records (`canonical_metadata.json` schema) and uses `license.permitsDerivatives` flag to gate which datasets enter the harmonization pipeline.

---

### Event 3: ewing-literature-corpus dataset/fusion annotation citation

**Reuse type:** `sibling-project-import` + `citation`  
**Consumer/Author:** [Hee-Lee Oss-Projects/ewing-literature-corpus](https://github.com/Hee-Lee-Oss-Projects/ewing-literature-corpus)  
**Description:** The ewing-literature-corpus project uses the ewing-open-data-catalog as a authoritative knowledge source for dataset canonical names, accessions, and molecular-annotation metadata (EWSR1-FLI1 fusion variants and assay types). The corpus references the catalog's datasets by accession + catalog DOI to disambiguate dataset identity across publications and repositories.  
**Evidence source:** PLAN.md §2 Problem & Beneficiaries lists corpus as sibling Hee-Lee Oss project consuming catalog output. COMPETITIVE-ANALYSIS.md §5 Claude API leverage mentions "Molecular/fusion annotation drafting from the publication ... flagged for technical-reviewer verification" — fusion data is a downstream product for corpus indexing.  
**Evidence artifact:**
```
File: PLAN.md lines 49–51 (Problem & Beneficiaries section)
File: COMPETITIVE-ANALYSIS.md §5, point 5 (molecular/fusion annotation)
File: tasks/ewing-open-data-catalog-doc-012.json and doc-013.json (molecular field in canonical record)
Specification: Datasheet template (task 002) includes molecular.driverFusion and molecular.assay, sourced from publication PMID/DOI — corpus will cite these.
```
**Date verified:** 2026-07-24 (project plan published); corpus integration expected M2–M3 upon dataset documentation completion.  
**Catalog version/DOI referenced:** Pending Zenodo publication (tasks 009, 012, 013, 018); corpus will cite catalog DOI + dataset accession in published corpus records.  
**Dataset(s) or output consumed:** Canonical dataset metadata including title, accession, repository, molecular.driverFusion (EWSR1-FLI1 / variant fusions), molecular.assay type, and publication PMID/DOI; used for entity linkage and variant disambiguation in literature corpus.  
**Integration mechanism:** Corpus imports catalog dataset records as canonical reference data; every corpus entity linked to an Ewing dataset includes provenance citation to the ewing-open-data-catalog Zenodo DOI + dataset accession.  

---

## Verification instructions

To add a reuse event to this ledger:

1. **Identify externally verifiable evidence** — the reuse event must have a publicly visible artifact (commit, DOI, published reference, or documented dependency).
2. **Confirm it's external** — self-published updates to the same organization do not count; sibling Hee-Lee Oss projects count as external consumers only if they have merged the catalog integration into their published output (not just planning/in-progress branches).
3. **Record the type**:
   - `sibling-project-import`: A Hee-Lee Oss sibling project (KG, reanalysis, corpus, atlas) has merged catalog data into its code or published outputs.
   - `citation`: Published paper, preprint, or external project documentation cites the catalog's datasets or methodology by DOI or URL.
   - `external-adoption`: An external repository (CCDI, Zenodo, OmicsDI, etc.) has officially adopted or indexed one or more catalog entries.
   - `code-integration`: External research or bioinformatics project has committed catalog-based code or data pipelines into a public repository.
4. **Link the evidence** — always include a hyperlink to the public artifact (GitHub URL, DOI, published paper, or documentation file).
5. **Record the date** — when the evidence was verified to be public and stable, not when the work was announced.

---

## Expected milestones

| **Milestone** | **Catalog state** | **Reuse readiness** | **Target for this ledger** |
|---|---|---|---|
| M0 | Pilot dataset published (Zenodo DOI) | Minimal; self-publish fallback only | 0 events (definition of done: pilot + 1 outreach thread) |
| M1 | ≥ 2 datasets adopted/DOI-published | Informal adoption path if identified | 0–1 events (if partner-014 identified) |
| M2 | ≥ 5 datasets across ≥ 2 source families | Ready for scaling | 1–2 events (sibling projects + possible external) |
| **M3** | **≥ 6 datasets across ≥ 3 sources (v1.0)** | **Mature for external reuse** | **≥ 3 events required (≥ 1 sibling-project)** |

---

## Sibling-project integration targets

The catalog's **planned primary consumers** are sibling Hee-Lee Oss projects, each with a documented contract for dataset consumption:

### 1. ewsr1-fli1-knowledge-graph

**Planned integration:** Structured metadata feed of vetted Ewing datasets for KG entity enrichment.  
**Specification:** `docs/kg-handoff-contract.md` (task ewing-open-data-catalog-kg-handoff-025).  
**Evidence path:** Merged PR in the `ewsr1-fli1-knowledge-graph` repo importing the catalog's export feed; published dataset references with the catalog DOI.  
**Status:** Ready for handoff post-M3; pending merged pull request in sibling repo.

### 2. ewing-expression-reanalysis

**Planned integration:** License-clear, derivability-verified open expression datasets.  
**Mechanism:** The catalog's triage-gate (access tier + license + re-id) answers "what may we legally reanalyze?" before reanalysis pipelines run.  
**Evidence path:** Merged PR in the `ewing-expression-reanalysis` repo crediting the catalog as the approved dataset source; published reanalysis results that cite the catalog's datasets by accession + catalog DOI.  
**Status:** Depends on M1–M2 dataset documentation; ready post-M3.

### 3. ewing-literature-corpus

**Planned integration:** Citation of canonical dataset metadata and molecular annotations (EWSR1-FLI1 variant annotation) in corpus search/indexing.  
**Evidence path:** Merged PR in the `ewing-literature-corpus` repo referencing catalog metadata as a knowledge source; published corpus documentation with catalog DOI citation.  
**Status:** Depends on molecular-annotation fields in M0–M1 datasheets; ready post-M3.

### 4. ewing-single-cell-atlas

**Planned integration:** Cell-line expression datasets (DepMap/CCLE Ewing lines) selected via catalog re-identification gate (cell-lines have no patient/germline, so lower risk).  
**Evidence path:** Merged PR in the `ewing-single-cell-atlas` repo listing dataset sources with the catalog DOI; published single-cell reference materials citing dataset provenance.  
**Status:** Depends on coverage of cell-line datasets in M2 landscape task; ready post-M3.

---

## External adoption channels

### NCI CCDI Childhood Cancer Data Catalog

**Planned path:** Direct contribution of vetted catalog entries to the federal CCDI resource catalog (task partner-014).  
**Mechanism:** Pull request (or direct portal contribution) of ≥ 3 Ewing dataset entries to the CCDI Catalog, each with the source catalog DOI.  
**Evidence:** Public CCDI Catalog entry showing the contributed dataset with the ewing-open-data-catalog cited as the discovery source.  
**Status:** In progress (M1); outcome recorded when CCDI entry is published.

### Google Dataset Search / OmicsDI

**Planned path:** Publishing Croissant ML + schema.org metadata enables automatic indexing by Google Dataset Search and community aggregators.  
**Mechanism:** Published catalog index with Croissant/schema.org metadata; Google Dataset Search auto-discovery.  
**Evidence:** Google Dataset Search result for an Ewing dataset accession showing the catalog entry; OmicsDI index record pointing to the catalog.  
**Status:** Depends on M2 adapters; outcome recorded when public discovery appears.

---

## License and attribution

This reuse ledger is **CC-BY-4.0**. When recording reuse events, the consumer must provide attribution to the ewing-open-data-catalog project and retain the "research metadata only — not medical advice" label on any derivative works.

---

## Process and maintenance

- **Steward:** TBD (designated in task ewing-open-data-catalog-reviewer-001 and PLAN.md Governance).
- **Update cadence:** Reviewed quarterly or on each catalog version release (new Zenodo DOI in task refresh-020).
- **Archived versions:** Prior versions of the ledger are preserved in the git history; the current Zenodo DOI points to the current index and this ledger's current state.

---

## Success metrics (M3 Definition of Done)

- [ ] **≥ 3 verifiable external reuse events recorded** — citation/DOI reference, merged PR in external repo, or sibling-project import, each with an externally visible evidence link.
- [ ] **≥ 1 sibling-project consumption** — at least one of the four planned sibling projects (KG, reanalysis, corpus, atlas) has merged the catalog integration and published it.
- [ ] **Each event linked to externally verifiable evidence** — no self-reported reuse; all references are to public commits, published papers, official catalog entries, or merged code.
- [ ] **Ledger reviewed by the Steward** — the designated steward confirms all entries and their evidence links before merge.

---

## Reference: related task outputs

For context on the datasets and standards driving reuse:

- **Template & canonical model** (task 002): `docs/template.md` + canonical record schema.
- **Three-part triage gate** (task 003): `docs/gate.md` — access-tier, license, re-identification decision record.
- **Coverage report** (task 005): `docs/coverage.md` — verified open vs. controlled split per source family.
- **Published index** (tasks 009, 012, 013, 018): `catalog/` index entries (Zenodo DOI).
- **KG handoff contract** (task 025): `docs/kg-handoff-contract.md` — structured feed for sibling KG project.

---

*Document version: 0.1.0 — M3 planning template*  
*Last updated: 2026-07-24*  
*License: CC-BY-4.0*
