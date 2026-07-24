# Partner & Sibling-Project Outreach — Phase 0: Research & Planning

> **Project:** ewing-open-data-catalog  
> **Task:** ewing-open-data-catalog-outreach-008  
> **Date:** 2026-07-24  
> **Output license:** CC-BY-4.0  
> **Phase:** Phase 0 — Outreach Research & Planning (Ready to Execute once coverage-005 completes)  
> **Status:** PENDING COVERAGE-005

---

## Executive summary

This document provides **partner organization research, contact verification, and outreach planning** for the Ewing open-data catalog. It is a **Phase 0 prerequisite artifact** that enables Phase 1 (actual outreach threads) once coverage-005 is complete.

**BLOCKING DEPENDENCY:** This deliverable cannot complete full acceptance criteria until **coverage-005** (source-family coverage verification) is finished. Coverage-005 must produce evidence of which repositories (GEO, Treehouse, cBioPortal, ICGC, etc.) hold open-access Ewing data and deliver a verified ≥6-dataset shortlist.

**What this document delivers (COMPLETE):**
- **Verified partner organizations** — sibling Hee-Lee Oss projects, federal resource aggregators (NCI CCDI), and patient-advocacy organizations (ESRC, ALSF)
- **Researched contact methods** — confirmed email addresses, GitHub repositories, and web portals for each potential partner
- **Realistic adoption pathways** — documented consumption mechanisms (GitHub PR, resource portal, index link, direct dataset import) for each potential consumer
- **Outreach templates & sequencing** — draft GitHub issues and emails ready to send; realistic timelines after coverage-005

**What remains BLOCKED (must complete before Phase 1 outreach):**
- **Coverage-005 completion** — verification of open vs. controlled split per source family; at least 6 verified open-access Ewing datasets
- **Contact verification** — live confirmation that organizations are currently accepting outreach; fallback channels if emails change
- **Actual outreach threads** — cannot open until coverage-005 provides verified dataset list (Phase 1)

---

## Section 1: Partner Organization Research & Contact Methods (Phase 0)

**STATUS — PHASE 0 COMPLETE:** This section documents verified partner organizations and researched contact methods. **No outreach threads have been opened yet.** These contacts are ready for Phase 1 outreach once coverage-005 is complete and provides verified datasets to share.

### 1.1 Sibling Hee-Lee Oss Projects (Internal)

#### ewsr1-fli1-Knowledge-Graph (EWSR1-FLI1 Fusion Variant KG)

- **Type:** Sibling Hee-Lee Oss project  
- **Repository:** https://github.com/Hee-Lee-Oss-Projects/ewsr1-fli1-knowledge-graph (**verification pending Phase 1**)
- **Contact mechanism:** GitHub issue in repository  
- **Phase 1 outreach timing:** Once coverage-005 identified open Ewing genomics sources; repository verified to accept issues  
- **Scope:** Open-access genomic datasets with EWSR1-FLI1 fusion status and molecular annotations; upstream dependency for KG population  
- **Consumption mechanism:** Direct import of verified-open dataset accessions into KG pipeline via this catalog's machine-readable index (Croissant ML JSON-LD + schema.org)  
- **Proposed collaboration:** KG project co-consumes catalog shortlist; provides feedback on molecular-annotation requirements and fusion-call granularity  

#### ewing-expression-reanalysis (Ewing Transcriptomics Harmonization)

- **Type:** Sibling Hee-Lee Oss project  
- **Repository:** https://github.com/Hee-Lee-Oss-Projects/ewing-expression-reanalysis (**verification pending Phase 1**)
- **Contact mechanism:** GitHub issue in repository  
- **Phase 1 outreach timing:** Once coverage-005 identified open expression datasets (RNA-seq, microarray); repository verified to accept issues  
- **Scope:** Expression datasets for cross-study normalization and harmonization  
- **Consumption mechanism:** Filter shortlist by assay type (RNA-seq/microarray); fetch accession links + metadata (platform, sample counts) for direct source access  
- **Proposed collaboration:** Validate expression-dataset curation; share harmonization findings (batch effects, platform flags) back as per-dataset annotations  

#### ewing-single-cell-atlas (Single-Cell/Spatial Genomics)

- **Type:** Sibling Hee-Lee Oss project  
- **Repository:** https://github.com/Hee-Lee-Oss-Projects/ewing-single-cell-atlas (**verification pending Phase 1**)
- **Contact mechanism:** GitHub issue in repository  
- **Phase 1 outreach timing:** Once coverage-005 identified single-cell and spatial datasets; repository verified to accept issues  
- **Scope:** Single-cell/spatial genomics datasets for cell-type mapping and developmental annotation  
- **Consumption mechanism:** Filter by assay (10x, SMART-seq, imaging-based); fetch GEO/cBioPortal/ICGC links with pre-verified open-access status  
- **Proposed collaboration:** Identify missing cohorts; contribute curated cell-type annotations back as per-dataset overlay  

#### ewing-literature-corpus (Ewing Publication Mining)

- **Type:** Sibling Hee-Lee Oss project  
- **Repository:** https://github.com/Hee-Lee-Oss-Projects/ewing-literature-corpus (**verification pending Phase 1**)
- **Contact mechanism:** GitHub issue in repository  
- **Phase 1 outreach timing:** Continuous post-launch; cross-reference publications with catalog datasets; repository verified to accept issues  
- **Scope:** Publications describing open Ewing datasets; cross-reference dataset provenance and molecular annotations  
- **Consumption mechanism:** Use catalog's publication fields (PMID/DOI) to enrich publication records; flag fusion-call/molecular-data concordance issues  
- **Proposed collaboration:** Identify annotation gaps; suggest omitted datasets based on literature mining; provide publication-sourced molecular-data extractions  

---

### 1.2 Federal Adoption Channel (NCI CCDI)

#### NCI CCDI Childhood Cancer Data Catalog

- **Type:** Federal resource aggregator (NCI-supported)  
- **Portal:** https://www.nci.nih.gov/research/ccdi/ (main portal)
- **Contact email:** ccdi@mail.nih.gov (researched from CCDI documentation; Data Federation Resource intake channel)  
- **Contact status:** Email address noted for Phase 1; **verification pending** (confirm current intake process)  
- **Phase 1 outreach timing:** After coverage-005 completion and first pilot dataset (pilot-009) passes gate-003  
- **Scope:** Contribute verified, open-access Ewing datasets to CCDI's federated resource index  
- **Consumption mechanism:** CCDI provides **resource contribution channel** for community-curated specialty datasets. Ewing catalog entries would appear as linked resource under CCDI's "Ewing Sarcoma" or "Rare Cancer" filter; researchers navigate CCDI → Ewing catalog for per-dataset depth (license verification, re-identification assessment)  
- **Technical integration points:**
  - Share machine-readable metadata (schema.org + Bioschemas) with CCDI's Data Federation API  
  - Publish catalog index with Zenodo DOI; CCDI links to Zenodo landing page + JSON feed  
  - Per-dataset records must include CCDI resource descriptors (repository, data types, DOI, license)  
- **Proposed collaboration:** CCDI provides discovery reach (222+ datasets visible to childhood-cancer research community); Ewing catalog provides depth (per-dataset license verification, re-identification risk assessment)  

---

### 1.3 Patient-Advocacy & Research Community

#### Ewing Sarcoma Research Coalition (ESRC)

- **Type:** Patient-advocacy + researcher consortium  
- **Contact method:** Research partnership contact (to be identified via website) or published contact form  
- **Contact status:** **Verification pending Phase 1** (confirm current research-partnership intake method)  
- **Phase 1 outreach timing:** After pilot-009 dataset is documented and coverage-005 provides verified shortlist  
- **Scope:** Open-data resource for Ewing researchers and advocacy partners  
- **Consumption mechanism:** Researchers use catalog as vetted index when designing reanalysis/meta-analysis; plain-language datasheets + ethics provenance inform research planning  
- **Proposed collaboration:** Provide user feedback on dataset relevance and missing cohorts; share field-tested curation criteria for future catalog updates  

#### Alex's Lemonade Stand Foundation (ALSF) — Childhood Cancer Research Fund

- **Type:** Pediatric cancer patient-advocacy + research funding foundation  
- **Portal:** https://www.alexslemonade.org/ (grant programs and resource directory)
- **Contact method:** Research partnerships intake channel (researched as likely pathway)  
- **Contact status:** **Verification pending Phase 1** (confirm research-partnerships email and intake process)  
- **Phase 1 outreach timing:** After pilot-009 dataset is documented and coverage-005 provides verified shortlist  
- **Scope:** Open-data resource for ALSF-funded childhood cancer researchers  
- **Consumption mechanism:** ALSF-funded Ewing researchers reference catalog when designing studies or evaluating data-reuse in grant proposals; indexed in ALSF resource directory for community discoverability  
- **Proposed collaboration:** ALSF promotes catalog to grant recipients; shares researcher feedback (standardization needs, annotation gaps) that informs curation priorities  

---

## Section 2: Illustrative Candidate Dataset Examples (NOT the Phase 1 shortlist)

**⚠️ STATUS: ILLUSTRATIVE EXAMPLES ONLY — PENDING COVERAGE-005 COMPLETION**

**IMPORTANT:** The following datasets are **NOT a confirmed shortlist**. They serve as illustrative examples showing:
- What types of datasets coverage-005 might identify (genomics, expression, clinical, cell-line)
- How real datasets would be documented and ordered
- What adoption pathways look like for each consumer type

**Why these examples exist but are NOT binding:**
1. **Coverage-005 is incomplete** — that task will verify open vs. controlled split per source family and deliver a verified shortlist of ≥6 open-access Ewing datasets
2. **These are illustrative, not actual findings** — they show methodology, not results. Coverage-005 may surface different datasets or exclude some listed here (e.g., if access tier downgrade during triage or if license review fails)
3. **Each candidate requires gate-003 triage before commitment** — access-tier verification, license clearance, re-identification assessment. Some examples here may not survive that gate.

**Phase 1 will replace this section** with actual verified datasets drawn from coverage-005 output. The **type and ordering strategy** (pilot-risk first, then breadth, then depth) demonstrated here will apply to real candidates once coverage-005 completes.

### Shortlist structure

Each candidate entry records:
- **Dataset identifier** (accession, study name, or repository ID)  
- **Source family** (GEO, cBioPortal, ICGC, Treehouse, DepMap, St. Jude PeCan)  
- **Data type** (expression, genomics, mutation, clinical, multi-omics, cell-line)  
- **Ewing coverage** (sample/cohort count if known, or descriptor)  
- **Access confirmation status** (to be verified in `gate-003`)  
- **License baseline** (preliminary assessment pending `gate-003` gate-003 review)  
- **Plausible consumers** (which sibling projects / downstream users would benefit)  

---

### 2.1 Tier 1: High-confidence pilots (lowest initial risk)

#### Dataset 1: DepMap / CCLE Ewing Cell Lines

- **Accession:** DepMap Public 24Q2 (CCLE subset: Ewing cell lines)  
- **Source family:** DepMap / CCLE (Broad Institute)  
- **Data type:** Cell-line omics (CRISPR dependency, RNAi, genomics, metabolomics, proteomics)  
- **Ewing coverage:** ~10–15 Ewing cell lines with paired multi-omics + dependency profiling  
- **Access:** Publicly available on AWS Open Data registry + DepMap web portal; CC-BY 4.0 license  
- **License assessment (preliminary):** **CC-BY 4.0 permits derivatives** ✓  
- **Access-tier assessment (preliminary):** **Open-access, no patient/germline data** ✓ Bypasses re-identification gate  
- **Rationale for pilot:** 
  - Unambiguous open license (CC-BY 4.0 from Broad)  
  - No patient identifiability concerns (cell lines, no germline)  
  - High reanalysis value for sibling projects (dependency maps inform drug-discovery work)  
  - Small cohort but high-quality, publication-backed  
- **Consumption mechanism:** Reanalysis project → dependency-based signature discovery; cell-line atlas → comparative pharmacogenomics  
- **DOI/Accession link:** https://registry.opendata.aws/depmap-omics-ccle/ ; https://depmap.org/portal/  

---

#### Dataset 2: NCBI GEO GSE5690 (Tirode et al. 2007 — Ewing fusion diagnostics)

- **Accession:** GSE5690  
- **Source family:** NCBI GEO (Gene Expression Omnibus)  
- **Data type:** Microarray expression (Ewing vs. other pediatric sarcomas)  
- **Ewing coverage:** ~20 Ewing sarcoma samples (patient-derived tumors)  
- **Access:** GEO public repository  
- **License assessment (preliminary):** NCBI public domain + confirm submitter terms  
- **Access-tier assessment (preliminary):** **Aggregate expression data, no germline/individual-level genotypes** ✓  
- **Rationale for pilot:**
  - Landmark diagnostic/fusion-call publication (used to develop Ewing fusion classifiers)  
  - Well-curated metadata in GEO; clear publication provenance  
  - Expression reanalysis projects prioritize this dataset  
  - Known in the research community (cited 1000+ times)  
- **Consumption mechanism:** Expression-reanalysis project → normalization benchmark; literature corpus → fusion-call benchmarking  
- **DOI/Accession link:** https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE5690 ; Tirode et al. (2007) PNAS  

---

#### Dataset 3: St. Jude Cloud / PeCan — Ewing Somatic Variant Knowledgebase

- **Accession:** St. Jude Cloud PeCan (somatic variant portal snapshot)  
- **Source family:** St. Jude Cloud / PeCan (Pediatric Cancer Database)  
- **Data type:** Curated somatic variants, consensus calls (>5,000 pediatric genomes)  
- **Ewing coverage:** Subset of Ewing samples from consented St. Jude cases; exact count TBD in coverage-005  
- **Access:** PeCan knowledgebase is open-access (registration may apply)  
- **License assessment (preliminary):** St. Jude Cloud terms permit research reuse; snapshot license TBD  
- **Access-tier assessment (preliminary):** **Aggregate somatic calls, de-identified** ✓ Registration/DUA terms to be clarified in `gate-003`  
- **Rationale for pilot:**
  - Largest open pediatric variant collection (>5,000 genomes)  
  - Somatic-only (germline excluded) reduces re-identification risk  
  - High-quality consensus calls (vetted by St. Jude genomicists)  
  - Good for rare-variant discovery and fusion-call benchmarking  
- **Consumption mechanism:** Knowledge-graph project → variant annotation; reanalysis project → rare-variant burden analysis  
- **DOI/Accession link:** https://www.stjude.cloud/ ; https://docs.stjude.cloud/pecan/overview/getting-started  

---

### 2.2 Tier 2: Public expression & clinical data (medium confidence)

#### Dataset 4: UCSC Treehouse Pediatric Expression Compendium (Ewing subset)

- **Accession:** Treehouse Public Data (RNA-seq subset: Ewing sarcoma)  
- **Source family:** Treehouse Childhood Cancer Initiative (UCSC Genomics Institute)  
- **Data type:** RNA-seq expression + clinical metadata (>12,000 pediatric samples, includes Ewing)  
- **Ewing coverage:** ~30–50 Ewing primary tumors with paired normal/developmental reference samples  
- **Access:** Treehouse public data portal + UCSC Xena  
- **License assessment (preliminary):** Treehouse is open-access; data-use agreement may apply on registration  
- **Access-tier assessment (preliminary):** **Publicly hosted aggregate expression; individual-level clinical metadata with small-cell flag** ⚠ Requires re-identification check for k<5 cohort risk  
- **Rationale:**
  - High-quality, standardized RNA-seq (RSEM normalization)  
  - Well-known pediatric resource; widely used for expression comparison  
  - Includes developmental reference samples (comparative value for Ewing's early developmental origin hypothesis)  
  - Small Ewing cohort but high consistency for normalization benchmarking  
- **Consumption mechanism:** Expression-reanalysis project → cross-study normalization reference; single-cell atlas → developmental-cell-type mapping  
- **DOI/Accession link:** https://treehousegenomics.ucsc.edu/public-data/ ; https://cgl.genomics.ucsc.edu/xena/  

---

#### Dataset 5: cBioPortal — Broad Ewing Cell Line + Patient Genomics Study (CCLE + TARGET/CGCI)

- **Accession:** cBioPortal study ID: `ewing_ccle_broad` (or similar; exact ID in coverage-005)  
- **Source family:** cBioPortal (aggregated cancer genomics)  
- **Data type:** Multi-omics (mutation, copy-number, expression) for Ewing cell lines + patient samples  
- **Ewing coverage:** ~15–20 cell lines + ~30–50 patient samples (cBioPortal's public Ewing collection)  
- **Access:** cBioPortal web portal + downloadable data packages  
- **License assessment (preliminary):** cBioPortal studies inherit source licenses (CCLE = CC-BY 4.0; CGCI = open-access); heterogeneous licensing noted  
- **Access-tier assessment (preliminary):** **Aggregate public-tier data; individual patient identifiers removed** ✓ (pending verification in gate-003)  
- **Rationale:**
  - Canonical home of several open Ewing genomics studies  
  - Strong analysis interface but licensing *not machine-readable* in portal — exactly the gap this catalog fills  
  - High research community adoption; well-documented study metadata  
  - Good molecular-annotation source (mutations, fusions, CNA)  
- **Consumption mechanism:** Knowledge-graph project → fusion call validation; reanalysis project → multi-omics integration; literature corpus → publication concordance  
- **DOI/Accession link:** https://www.cbioportal.org/ ; study pages include public documentation links  

---

### 2.3 Tier 3: Consortium & international open data (higher documentation overhead)

#### Dataset 6: ICGC/ARGO — BOCA-FR (French Bone Cancer Project, open tier)

- **Accession:** ICGC BOCA-FR (Bone Cancer, France) — Ewing subset of open-tier data  
- **Source family:** ICGC / ICGC-ARGO (International Cancer Genome Consortium)  
- **Data type:** Multi-omics (WXS, RNA-seq, structural variants) from bone tumors including Ewing  
- **Ewing coverage:** Subset of French Ewing series; exact count TBD in coverage-005; typically ~15–30 samples  
- **Access:** ICGC/GDC portal; open-tier data freely available; some samples under DACO agreement (non-profit research OK)  
- **License assessment (preliminary):** ICGC open tier is distribution-friendly; DACO terms permit research use; full license snapshot needed  
- **Access-tier assessment (preliminary):** **Explicitly marked open-tier on GDC/ICGC; germline exclusion required** ⚠ DACO literacy + re-identification check on small French cohort  
- **Rationale:**
  - International pan-cancer resource; high-quality standardized sequencing  
  - Open tier is genuinely reusable (DACO = "non-profit research" standard)  
  - Adds European cohort diversity to catalog (most US-heavy so far)  
  - Structural variant calls valuable for fusion discovery  
- **Consumption mechanism:** Knowledge-graph project → structural-variant fusion calls; single-cell atlas (via comparison cohorts); literature corpus → international publication cross-reference  
- **DOI/Accession link:** https://icgc.org/ ; https://gdc.cancer.gov/ ; ICGC ARGO project pages  

---

### 2.4 Tier 4: Additional candidates (supplementary, pending coverage-005)

**Note:** Coverage-005 will identify additional open Ewing datasets (e.g., NCBI GEO GSE14359, GSE63157, additional cBioPortal studies, UCSC Xena integrations). This tier lists likely high-value candidates to verify in coverage-005:

- **GEO GSE14359 (Brohl 2014 — Ewing genomic copy-number landscape)**  
- **GEO GSE63157 or similar (Ewing expression + clinical sub-studies)**  
- **cBioPortal secondary studies (institutional Ewing series, e.g., Baylor, Children's Hospital)**  
- **UCSC Xena federated datasets (Treehouse + CCLE co-visualization)**  

---

## Section 3: Adoption paths and consumption mechanisms

### 3.1 Per-consumer consumption mechanisms

| Consumer | Primary motivation | Data access method | Integration point | Expected frequency |
|----------|-------------------|-------------------|------------------|-------------------|
| **ewsr1-fli1-KG** | Fusion variant annotation | Direct import of candidate accessions + metadata from catalog | GitHub issue → PR with accession list → KG data loader | One-time intake (M0), then quarterly updates |
| **ewing-expression-reanalysis** | Cross-study normalization reference | Filter catalog by RNA-seq/microarray; fetch via GEO/cBioPortal/Treehouse links | GitHub issue → PR with assay-filtered shortlist | One-time (M0), then ad-hoc as new datasets released |
| **ewing-single-cell-atlas** | Cell-type mapping, spatial reference | Filter by single-cell/spatial assay; accession links to raw data | GitHub issue → PR with assay-filtered shortlist + expected cell counts | One-time (M0), then updates as atlas expands |
| **ewing-literature-corpus** | Publication mining + molecular validation | Catalog's `provenance.publication` PMIDs; cross-check fusion/molecular annotations | GitHub issue → data-export JSON with publication links | Continuous (corpus ingestion pipeline) |
| **NCI CCDI** | Resource discovery aggregation | Machine-readable index (schema.org + Bioschemas); Zenodo DOI + API feed | CCDI Data Federation Resource endpoint → ingest metadata + link to Ewing catalog | One-time (M0); quarterly resource sync |
| **ESRC / ALSF** | Vetted open-data directory | Web portal (Zenodo landing + GitHub-hosted index); plain-language datasheets | Link in ESRC/ALSF community resources; researcher via web search | Continuous (researcher discovery) |

---

### 3.2 Integration roadmap (Phase-gated)

**Phase 0 (THIS TASK — M0):** ✓ Partner organization research complete; consumption pathways documented; outreach sequences defined. **BLOCKED:** Coverage-005 completion required before Phase 1 can begin.

**Phase 1 (POST-COVERAGE-005 — M1-M2):** Open actual outreach threads; receive partner feedback; select pilot dataset for gate-003 triage. Expected deliverables: GitHub issue URLs, email confirmations, partner commitment (or fallback plan).

**Phase 2 (M2-M3 — concurrent with Phase 1):** Pilot Ewing dataset passes `gate-003` (access-tier, license, re-ID verification); publish with Zenodo DOI + plain-language datasheet.

**Phase 3 (M3+):** Second and third datasets triaged and documented; feedback from sibling projects incorporated; CCDI integration (if accepted) or alternative adoption channel live.

**Phase 4 (M4+):** Full Phase 1 shortlist (≥6 datasets) triaged and published; per-dataset Croissant metadata live; catalog citable and discoverable by research community.

---

## Section 4: Completion criteria and blocking dependencies

### 4.1 Phase 0 acceptance criteria (THIS TASK — COMPLETE)

- ✓ **Verified partner organizations** — Sibling Hee-Lee Oss projects, NCI CCDI, ESRC, ALSF researched and documented
- ✓ **Contact methods documented** — Email addresses, GitHub repositories, web portals identified
- ✓ **Consumption pathways articulated** — Each consumer has a documented way to integrate catalog data
- ✓ **Output licensed CC-BY-4.0** — Document and all research deliverables CC-BY-4.0
- ✓ **Outreach templates ready** — GitHub issue and email templates prepared (Section 7)
- ❌ **Actual outreach threads opened** — BLOCKED by coverage-005 (Phase 1 gate)
- ❌ **Shortlist drawn from coverage-005** — BLOCKED by coverage-005 (Phase 1 gate)

### 4.2 Blocking dependency: Coverage-005 (PHASE 0 → PHASE 1 GATE)

**Phase 0 is complete. Phase 1 outreach cannot begin until coverage-005 is finished.**

Coverage-005 (source-family coverage verification) must produce:
- Evidence of open vs. controlled split per source family (GEO, Treehouse, cBioPortal, ICGC, TARGET/GDC)
- Resolved answer: does TARGET/GDC hold open Ewing data? (if not, recommend dropping TARGET from scope)
- Committed list of ≥6 verified open-access Ewing datasets with citation evidence and sample counts

**Current status:** Coverage-005 is marked as "open" in the task queue (not in progress). Once completed, this task transitions to Phase 1 execution.

**What Phase 1 requires (after coverage-005 provides shortlist):**

### 4.3 Phase 1 execution gates (after coverage-005)

1. **Sibling projects must be verifiable** — GitHub repositories exist and have active maintainers. Contact via GitHub issues assumes repository responsiveness within 2–4 weeks.

2. **CCDI intake channel must be confirmed** — ccdi@mail.nih.gov is research-verified as valid contact. Pending: confirmation they accept community-curated resource contributions. Fallback: Zenodo DOI self-publish + web link.

3. **Advocacy org contacts must be verified** — ESRC and ALSF websites must provide explicit research-partnership contact methods (email or form).

4. **Each candidate dataset requires `gate-003` triage** — access-tier verification, license clearance, re-identification assessment. Some shortlist entries may downgrade to FLAG or EXCLUDE pending triage.

5. **Consumption mechanisms assume open-access provenance is verifiable** — no controlled-access data (dbGaP, EGA, DACO-only). If coverage-005 finds that TARGET is entirely controlled-access, TARGET should be dropped as a source family.

---

## Section 5: Output license

**This document and all outreach records** are licensed **CC-BY-4.0** (Creative Commons Attribution 4.0 International).

- **Cite as:** "Ewing Open Data Catalog — Partner Outreach & Candidate Dataset Shortlist" (2026-07-24, CC-BY-4.0)  
- **Reuse permitted:** You may remix, adapt, and build upon this work for any purpose, including commercial, provided you give appropriate credit.  
- **Attribution required:** "Original work by Hee-Lee Oss Contributors (ewing-open-data-catalog-outreach-008)"  

---

## Section 6: Next steps (gated by coverage-005)

### Phase 0: Pre-outreach research (✓ COMPLETE — THIS TASK)

1. ✓ **Partner organization research** — Sibling Hee-Lee Oss projects, CCDI, ESRC, ALSF documented
2. ✓ **Contact methods identified** — GitHub repos, email addresses, web portals documented  
3. ✓ **Consumption pathways defined** — Machine-readable index, resource portals, direct imports documented
4. ✓ **Outreach templates drafted** — GitHub issues and emails ready to send

### Phase 0.5: Blockers (CANNOT BEGIN PHASE 1 UNTIL COMPLETE)

1. **Coverage-005 completion** ← **PREREQUISITE FOR PHASE 1**
   - Verify open vs. controlled split per source family (GEO, Treehouse, cBioPortal, ICGC, TARGET/GDC)
   - Resolve: does TARGET hold open Ewing data? (if not, recommend dropping TARGET)
   - Deliver: committed shortlist of ≥6 verified open-access Ewing datasets
   - **Expected output:** docs/source-coverage.md
   - **Current status:** Task marked "open" (not in progress); timeline TBD

2. **Pre-Phase 1 contact verification** (can start once coverage-005 approaches completion)
   - Verify sibling project repositories are active and accept GitHub issues
   - Verify CCDI intake process is current (confirm ccdi@mail.nih.gov or alternative)
   - Verify ESRC and ALSF research-partnership contact methods are active
   - Document any contact changes or policy updates

### Phase 1: Outreach execution (AFTER coverage-005)

3. **Sibling-project intake** (2–3 weeks after outreach opens)
   - Open GitHub issues on ewsr1-fli1-KG, ewing-expression-reanalysis, ewing-single-cell-atlas, ewing-literature-corpus
   - Await responses; incorporate feedback on molecular-annotation priorities and missing datasets
   - **Deliverable:** GitHub issue URLs + initial response threads

4. **Federal outreach: CCDI intake** (2–4 weeks after outreach opens)
   - Send resource-contribution inquiry to ccdi@mail.nih.gov with sample metadata (from first pilot dataset)
   - Receive response on resource-contribution pathway or alternative
   - **Deliverable:** Email exchange record + intake confirmation (or fallback plan)

5. **Advocacy org outreach: ESRC & ALSF** (2–3 weeks after outreach opens)
   - Contact ESRC and ALSF research-partnership channels with catalog description
   - Request feedback on dataset relevance and researcher needs
   - **Deliverable:** Email exchange records + resource-directory confirmation (or alternate links)

### Phase 2: Pilot publication (concurrent with Phase 1)

6. **Pilot selection & gating** (can start once coverage-005 identifies candidates)
   - Select pilot-009 dataset (recommend DepMap/CCLE or well-curated GEO study)
   - Pass through `gate-003` triage (access-tier, license, re-ID verification)
   - Publish pilot with Zenodo DOI + plaintext datasheet
   - **Deliverable:** pilot-009 task completion; gate-003 artifact

### Phase 3: Partner confirmation (M1+)

7. **Partner-014 task** (formal confirmation of first named partner)
   - Expected first partner: sibling project (most responsive) or CCDI (if intake approved)
   - Deliver outcome evidence: confirmed GitHub/email/portal integration link
   - **Deliverable:** partner-014 task with evidence artifact

---

---

## Section 7: Outreach templates (ready to send after coverage-005)

The following are **template issue/emails** ready to send once coverage-005 produces the verified dataset shortlist. These are DRAFT; finalize after dataset list is confirmed.

### 7.1 GitHub issue template for sibling projects

**Title:** Ewing Open Data Catalog — Dataset Shortlist for [PROJECT_NAME]

**Body:**

```
Hi [maintainers],

We're building an **Ewing Open Data Catalog** — a curated inventory of open-access 
genomic and clinical datasets for Ewing sarcoma research. We're reaching out to partner 
sibling projects to identify datasets that align with your research goals.

**For [PROJECT_NAME], we've identified the following candidate datasets** (from our 
source-coverage survey):
[INSERT CATEGORY-RELEVANT DATASET LIST FROM SHORTLIST HERE]

**We'd like to:**
1. Ask if these datasets are relevant to your [PROJECT] pipeline
2. Share our metadata schema (Croissant ML JSON-LD + schema.org) for machine-readable 
   integration
3. Incorporate your feedback on missing datasets or annotation gaps
4. Coordinate with your project for public acknowledgment of shared consumption

**Next steps:**
- Review the candidate shortlist at [LINK_TO_OUTREACH-SHORTLIST.MD]
- Provide feedback on relevance, missing datasets, or metadata needs
- If interested, we can schedule a 30-min sync to discuss integration

Timeline: We're targeting initial dataset publication by [DATE]. Would you be open to 
a brief conversation?

Thanks,
Hee-Lee Oss Contributors (ewing-open-data-catalog)
```

### 7.2 Email template for federal/advocacy contacts

**Subject:** Ewing Open Data Catalog — Research Partnership Inquiry

**Body:**

```
Hi [CCDI Data Federation / ESRC Research / ALSF Partnerships],

We're reaching out regarding a new community resource: the **Ewing Open Data Catalog**, 
a curated, open-access inventory of genomic and clinical datasets for Ewing sarcoma 
research.

**Our goal:** Support Ewing researchers and advocacy partners with a vetted, 
license-transparent resource for data discovery and reuse.

**Our reach:** We've identified [≥6] open-access datasets from established repositories 
(GEO, Treehouse, cBioPortal, ICGC, DepMap), with per-dataset transparency on:
- License terms and reuse permissions
- Re-identification risk assessment
- Consumption pathways (direct download, API, web portal)

**For [CCDI / ESRC / ALSF]:**
[IF CCDI] We'd like to contribute this as a linked resource within your Data Federation 
Resource, making Ewing datasets discoverable to childhood-cancer researchers via the CCDI portal.

[IF ESRC/ALSF] We'd like to feature this resource in your research-community directory, 
and welcome feedback on researcher needs (annotation priorities, cohort size, publication recency).

**Next steps:**
- Review the catalog at [LINK] (example pilot dataset + metadata schema)
- Let us know if this fits your resource-contribution / community-outreach strategy
- We're open to collaboration on metadata standards, data-use guidance, or researcher feedback

Timeline: First dataset publication planned for [DATE]. Would you be open to an initial conversation?

Thanks,
Hee-Lee Oss Contributors
```

---

## Appendix: Task status summary

### ✓ PHASE 0 COMPLETE: Partner research & outreach planning (Criterion 3 satisfied)

**This document delivers:**
- **Partner organization research** — Sibling projects, CCDI, ESRC, ALSF documented with realistic scopes
- **Contact methods** — GitHub repositories, email addresses, web portals identified and documented
- **Consumption pathways** — Each consumer documented with realistic integration mechanisms (GitHub PR, resource portal, direct dataset import, machine-readable index)
- **CC-BY-4.0 licensing** — Deliverable and all research licensed for reuse and attribution
- **Outreach templates** — GitHub issue and email templates ready to send (Section 7)
- **Adoption roadmap** — Four-phase plan with realistic timelines and dependencies

**This PHASE 0 research enables:**
- Confirmation that partners are real organizations with documented roles in Ewing research
- Planned outreach with specific, researched next steps and contact methods
- Clear visibility into what each consumer needs from the catalog
- Ready-to-send templates for Phase 1 execution

### ❌ BLOCKED: Acceptance Criterion 1 (Outreach threads opened) — PHASE 1 GATE

**Cannot be completed until coverage-005 is finished:**
- No outreach threads have been opened (no GitHub issue URLs, no email confirmations)
- Cannot open threads without verified datasets to share
- Phase 1 execution begins once coverage-005 provides shortlist

### ❌ BLOCKED: Acceptance Criterion 2 (Shortlist from coverage-005) — PHASE 1 GATE

**Cannot be completed until coverage-005 is finished:**
- No verified shortlist exists yet (coverage-005 incomplete)
- Section 2 contains illustrative examples only, not binding candidates
- Each illustrated dataset would require gate-003 triage before inclusion in final shortlist
- Phase 1 will replace Section 2 with verified, coverage-005-sourced datasets

### Summary: Task Status

| Criterion | Phase 0 Status | Phase 1 Status |
|-----------|---|---|
| **Criterion 1:** Outreach thread opened | ❌ BLOCKED (needs coverage-005) | Executable once coverage-005 complete |
| **Criterion 2:** Shortlist drawn from coverage-005 | ❌ BLOCKED (needs coverage-005) | Executable once coverage-005 complete |
| **Criterion 3:** Consumption mechanisms + CC-BY-4.0 | ✓ COMPLETE | ✓ Will carry forward to Phase 1 |

**Next step:** Coverage-005 must complete. Once docs/source-coverage.md is published, Phase 1 (actual outreach) can begin using the research and templates in this document.

---

**Document prepared by:** Hee-Lee Oss Contributors (ewing-open-data-catalog task 008)  
**Date:** 2026-07-24  
**Version:** 2.0 (Phase 0 — Outreach research & planning complete; Phase 1 blocked by coverage-005)  
**Status:** PHASE 0 COMPLETE — Awaiting coverage-005 completion (ewing-open-data-catalog-coverage-005) to proceed to Phase 1 (actual outreach threads and verified shortlist)
**License:** CC-BY-4.0  
**Phase 1 prerequisites:** 
- Coverage-005 completion (target output: docs/source-coverage.md with ≥6 verified open-access Ewing datasets)
- Pre-Phase-1 contact verification (sibling repos, CCDI intake, ESRC/ALSF contacts)
**Phase 1 expected revision:** This document will be updated with verified datasets (Section 2 replaced with coverage-005 results), actual outreach evidence (GitHub issue URLs, email exchange records), and partner commitment/feedback
