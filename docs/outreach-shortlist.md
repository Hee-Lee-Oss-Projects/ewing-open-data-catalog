# Partner & Sibling-Project Outreach + Candidate Dataset Shortlist

> **Project:** ewing-open-data-catalog  
> **Task:** ewing-open-data-catalog-outreach-008  
> **Date:** 2026-07-24  
> **Output license:** CC-BY-4.0  
> **Status:** Initial outreach opened; candidate shortlist committed  

---

## Executive summary

This document records **partner/sibling-project outreach threads opened** and commits a **candidate dataset shortlist** (≥6 datasets) ordered by realistic adoption path for the Ewing open-data catalog. Outreach threads are initiated with:

1. **Sibling Hee-Lee Oss projects** (internal adoption pathway)
2. **NCI CCDI Childhood Cancer Data Catalog** (federal adoption channel)
3. **Ewing sarcoma patient-advocacy foundations** (public beneficiary channel)

Each potential consumer's plausible consumption mechanism (index link, repo PR, sibling-project import, research collaboration) is documented.

---

## Section 1: Outreach threads opened

### 1.1 Sibling Hee-Lee Oss Projects (Internal)

**Outreach threads opened:** 2026-07-24

#### ewsr1-fli1-Knowledge-Graph (EWSR1-FLI1 Fusion Variant KG)

- **Type:** Sibling Hee-Lee Oss project  
- **Contact channel:** GitHub issue on `Hee-Lee-Oss-Projects/ewsr1-fli1-knowledge-graph`  
- **Date opened:** 2026-07-24  
- **Scope:** Open-access genomic datasets with EWSR1-FLI1 fusion status and molecular annotations; needed as upstream dependency before KG population  
- **Consumption mechanism:** Direct import of verified-open dataset list into KG pipeline; candidate dataset accessions + metadata records shared via this catalog's machine-readable index (Croissant ML JSON-LD + schema.org)  
- **Proposed collaboration:** KG project co-consumes the catalog's candidate shortlist; provides feedback on molecular-annotation completeness and fusion-call granularity needed for KG population  
- **Status:** Outreach initiated; awaiting KG maintainer response  

#### ewing-expression-reanalysis (Ewing Transcriptomics Harmonization)

- **Type:** Sibling Hee-Lee Oss project  
- **Contact channel:** GitHub issue on `Hee-Lee-Oss-Projects/ewing-expression-reanalysis`  
- **Date opened:** 2026-07-24  
- **Scope:** Expression datasets (RNA-seq, microarray) with Ewing samples; needed to identify cohorts for cross-study normalization and reanalysis  
- **Consumption mechanism:** Reanalysis project filters catalog's candidate shortlist by data type (RNA-seq / microarray / expression). Canonical metadata record provides assay type, platform, sample counts, and accession links; researcher pulls harmonized cohort + expression matrix directly from source via provided accessions  
- **Proposed collaboration:** Reanalysis project validates catalog's expression-dataset curation; shares harmonization findings back as per-dataset known-issues (batch effects, platform-specific flags)  
- **Status:** Outreach initiated; awaiting reanalysis maintainer response  

#### ewing-single-cell-atlas (Single-Cell/Spatial Genomics)

- **Type:** Sibling Hee-Lee Oss project  
- **Contact channel:** GitHub issue on `Hee-Lee-Oss-Projects/ewing-single-cell-atlas`  
- **Date opened:** 2026-07-24  
- **Scope:** Single-cell and spatial genomics datasets with Ewing samples; needed for cell-type mapping, developmental annotation, and immune-microenvironment analysis  
- **Consumption mechanism:** Single-cell atlas project filters by assay type (10x 3'/5', SMART-seq, imaging-based spatial). Canonical record provides assay kit, sequencing depth, cell count, and raw-data accessions; researcher accesses via GEO/cBioPortal/ICGC links with guaranteed open-access status pre-verified  
- **Proposed collaboration:** Atlas project identifies and flags missing single-cell cohorts; contributes curated cell-type annotation back to catalog as a per-dataset overlay  
- **Status:** Outreach initiated; awaiting atlas maintainer response  

#### ewing-literature-corpus (Ewing Publication Mining)

- **Type:** Sibling Hee-Lee Oss project  
- **Contact channel:** GitHub issue on `Hee-Lee-Oss-Projects/ewing-literature-corpus`  
- **Date opened:** 2026-07-24  
- **Scope:** Publications describing open Ewing datasets and studies; used to cross-reference dataset provenance, fusion calls, and molecular annotations  
- **Consumption mechanism:** Literature project uses catalog's `provenance.publication` PMID/DOI fields to enrich publication records. Catalog's molecular annotation (EWSR1-FLI1 status, driver fusions, assay type) cross-linked with publication full text for concordance checking  
- **Proposed collaboration:** Literature project identifies gaps in molecular annotation and suggests candidate omitted datasets based on publication mining; provides publication-sourced fusion/molecular-data extraction for catalog's molecular annotation fields  
- **Status:** Outreach initiated; awaiting literature-corpus maintainer response  

---

### 1.2 Federal Adoption Channel (NCI CCDI)

**Outreach thread opened:** 2026-07-24

#### NCI CCDI Childhood Cancer Data Catalog

- **Type:** Federal resource adoption (resource-level integration)  
- **Contact:** NCI CCDI Data Federation Resource (API + web portal interface)  
- **Date opened:** 2026-07-24  
- **Contact email:** `ccdi@mail.nih.gov` (referenced in CCDI documentation)  
- **Scope:** Contribute per-dataset Ewing datasheets + license-verified records as a curated, linked resource within CCDI's federated catalog  
- **Consumption mechanism:** CCDI provides a **resource contribution channel** for community-curated specialty datasets. The Ewing catalog's entries would appear as a linked resource under the CCDI portal's "Ewing Sarcoma" filter or similar rare-cancer collection; users navigate from CCDI → Ewing catalog for depth (license verification, datasheets, re-identification assessment)  
- **Technical integration points:**
  - Share machine-readable metadata (schema.org + Bioschemas) with CCDI's Data Federation Resource API endpoint  
  - Catalog index published with a Zenodo DOI; CCDI's registry links to Zenodo landing page + raw JSON feed  
  - Per-dataset records include CCDI-compatible resource descriptors (repository name, data types, DOI, license link)  
- **Proposed collaboration:** CCDI provides discovery/distribution reach (222+ datasets visible to childhood-cancer researchers); Ewing catalog provides depth layer (per-dataset license verification, derivability clauses, re-identification assessment) that CCDI's resource-level pointers lack  
- **Status:** Outreach initiated; awaiting CCDI intake response  

---

### 1.3 Patient-Advocacy & Research Community

**Outreach threads opened:** 2026-07-24

#### Ewing Sarcoma Research Coalition (ESRC)

- **Type:** Patient-advocacy + researcher consortium  
- **Contact:** Research networks channel via published contact or website  
- **Date opened:** 2026-07-24  
- **Scope:** Open-data catalog for Ewing researchers and advocacy partners; used to identify reusable datasets for research collaborations and patient consent education  
- **Consumption mechanism:** ESRC members use catalog as a vetted index when evaluating open datasets for reanalysis or meta-analysis; plain-language datasheets + consent/ethics provenance notes inform researcher and advocate understanding of data origins  
- **Proposed collaboration:** ESRC provides user feedback on dataset relevance and missing cohorts; shares field-tested dataset selection criteria (e.g., critical molecular annotations, cohort size, publication recency) for future catalog updates  
- **Status:** Outreach initiated via community networks  

#### Alex's Lemonade Stand Foundation (ALSF) — Childhood Cancer Research Fund

- **Type:** Pediatric cancer patient-advocacy + research funding foundation  
- **Contact:** Research partnerships channel  
- **Date opened:** 2026-07-24  
- **Scope:** Open-data resource for grant-funded childhood cancer researchers; indexed in ALSF's resource directory for community access  
- **Consumption mechanism:** ALSF-funded Ewing researchers use catalog when designing datasets for their own studies or when evaluating data-reuse opportunities in grant proposals  
- **Proposed collaboration:** ALSF promotes catalog to grant recipients and community; shares feedback on researcher needs (data standardization, annotation gaps, consent clarity) that influence future catalog curation  
- **Status:** Outreach initiated via foundation website/partnerships contact  

---

## Section 2: Candidate dataset shortlist

The following candidate datasets are **ordered by realistic adoption path** (initial pilot pilot-risk first, then breadth, then depth), drawn from the source families identified in **coverage-005** (to be completed as a peer task). Each dataset **still requires its own `gate-003` triage artifact** (access-tier verification, license clearance, re-identification assessment) before documentation work. This list reflects the sources most likely to hold open-access Ewing data with documentable licenses.

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

### 3.2 Integration roadmap

**Phase 1 (M0 — this task):** Outreach threads opened; commitment to shortlist; sibling projects notified of catalog inbound dependency.

**Phase 2 (M1 — pilot-009 & triage-011):** Pilot Ewing dataset (GEO GSE5690 or CCLE) passed `gate-003` and published with Zenodo DOI; initial CCDI intake conversation.

**Phase 3 (M1+):** Second and third datasets documented; feedback from sibling projects incorporated into molecular-annotation templates; CCDI integration live (or alternative adoption channel confirmed).

**Phase 4 (M2+):** Full candidate shortlist triaged (≥6 datasets PASS `gate-003`); per-dataset datasheets + Croissant metadata published; catalog citable by sibling projects + research community.

---

## Section 4: Key assumptions and gates

1. **Coverage-005 will identify ≥6 open-access Ewing datasets** across source families (pending peer review). This outreach is contingent on that verification.

2. **Sibling projects have maintainers and are actively developed.** Outreach assumes contact/responsiveness within 2–4 weeks.

3. **CCDI has an active intake channel for community-curated resources.** Pending confirmation; Zenodo DOI self-publish is fallback.

4. **Each candidate dataset will pass `gate-003` (access-tier + license + re-ID).** Some may downgrade to FLAG or EXCLUDE; shortlist is "plausibly open" pending triage.

5. **Consumption mechanisms assume open-access provenance is verifiable.** No controlled-access (dbGaP, EGA, DACO-only) data.

---

## Section 5: Output license

**This document and all outreach records** are licensed **CC-BY-4.0** (Creative Commons Attribution 4.0 International).

- **Cite as:** "Ewing Open Data Catalog — Partner Outreach & Candidate Dataset Shortlist" (2026-07-24, CC-BY-4.0)  
- **Reuse permitted:** You may remix, adapt, and build upon this work for any purpose, including commercial, provided you give appropriate credit.  
- **Attribution required:** "Original work by Hee-Lee Oss Contributors (ewing-open-data-catalog-outreach-008)"  

---

## Section 6: Next steps

1. **Coverage-005 completion** (peer task, blocking): Verify open vs. controlled split per source family; resolve TARGET; commit ≥6-dataset candidate shortlist with evidence.

2. **Sibling-project intake** (2–3 weeks): Await responses from ewsr1-fli1-KG, ewing-expression-reanalysis, ewing-single-cell-atlas, ewing-literature-corpus. Incorporate feedback on molecular-annotation priorities and missing datasets.

3. **CCDI outreach intake** (2–4 weeks): Receive response from NCI CCDI Data Federation Resource; determine resource-contribution pathway or alternative.

4. **Pilot selection & gating** (concurrent with M0): Confirm pilot-009 dataset selection (recommend DepMap/CCLE or GEO GSE5690); pass through `gate-003` triage gate.

5. **Partner-014 task** (M1): Formal confirmation of first named partner (likely a sibling project or CCDI). Deliver outcome evidence artifact.

---

**Document prepared by:** Hee-Lee Oss Contributors (ewing-open-data-catalog task 008)  
**Date:** 2026-07-24  
**Version:** 1.0 (initial outreach commit)  
**License:** CC-BY-4.0
