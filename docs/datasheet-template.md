# Datasheet Template: Ewing Open Data Catalog

**Research Documentation — Not Medical Advice**

**License:** CC-BY-4.0  
**Template Version:** 1.0  
**Last Updated:** 2026-07-24

---

## How to Use This Template

This template implements the **Datasheets for Datasets** framework (Gebru et al., 2019) adapted for biomedical research data in the Ewing Open Data Catalog. It provides a structured format to document:

- **What** the dataset contains and who created it
- **Why** it was created and how it was collected
- **How** to access it and use it legally
- **What** limitations and known issues users should know
- **Whether** it's suitable for their research questions

**Important Disclaimers:**
- This is a *documentation template*, not the data itself. It describes metadata standards and is **research documentation only — not medical advice**.
- Datasets in this catalog are for research and educational use. Any clinical applications require independent expert validation, institutional review, and appropriate regulatory approval.
- Use this template to create datasheets for any biomedical or open science dataset. The datasheet is licensed CC-BY-4.0; the data's license is specified separately within.

---

## Instructions for Dataset Submitters

1. **Identify your dataset** — Locate the dataset you're documenting (GEO series, cBioPortal study, institutional repository, Zenodo record, published data supplement, etc.)
2. **Gather source documentation** — Have access to: original publications, repository records, Methods section, data README, ethical review approvals
3. **Complete all sections** — Fill in Sections A–J below. If a section truly doesn't apply, write "N/A — [brief reason]"
4. **Include worked examples** — Provide at least one filled-in example showing typical metadata values (see Section K)
5. **Review for accuracy** — Double-check facts against source publications and repository records
6. **Submit to catalog** — Submit the completed datasheet (as Markdown) to the Ewing catalog via GitHub PR

---

## Section A: Motivation and Purpose

### A.1 — Why was this dataset created or curated?

Describe the scientific question, research goal, or clinical context that motivated the creation or inclusion of this dataset in the Ewing Open Data Catalog.

**For original datasets:**
- What research question does it address?
- What clinical or biological problem does it illuminate?
- What gap in available data does it fill?

**For re-published/curated datasets:**
- What was the original study's purpose?
- Why is this dataset included in the Ewing catalog specifically?
- Does it represent a new aggregation or analysis?

**Example:**
> This dataset contains RNA-seq profiles from five Ewing sarcoma cell lines with EWSR1-FLI1 fusion, collected to identify fusion-specific transcriptional signatures and potential therapeutic targets. The study was performed at Baylor College of Medicine's Center for Pediatric Cancer. These cell lines are included in the Ewing catalog as foundational reference transcriptomes for fusion-driven Ewing sarcomaand as benchmark data for algorithm development.

**Your response:**
```
[Provide motivation and curation rationale here]
```

---

### A.2 — Who collected/created the data, and when?

Specify the individuals, institutions, and timeframe involved in data generation.

- Names and institutional affiliations of investigators
- Date range of data collection
- Date of data analysis/processing completion
- Date of submission to public repository (if applicable)

**Example:**
> Dr. Jane Smith and colleagues at Baylor College of Medicine's Center for Pediatric Cancer. Cell culture and RNA extraction occurred from January 2023 to August 2024. RNA-seq was performed in-house on an Illumina NovaSeq platform. Bioinformatic analysis and quality control were completed by October 2024. Data submitted to GEO in November 2024 (accession GSE234567).

**Your response:**
```
[Provide collection timeframe and team information here]
```

---

### A.3 — Is this dataset part of a larger study or consortium?

Name any parent studies, research consortia, or collaborative projects.

**Examples:**
- TARGET-Ewing (National Cancer Institute)
- Kids First Data Resource Center (National Institutes of Health)
- Treehouse Pediatric Cancer Initiative (UC Santa Cruz)
- Children's Oncology Group (COG) Studies
- ICGC Ewing Sarcoma Project

Include relevant consortium publications, data release policies, or embargo periods.

**Example:**
> This dataset is part of the Kids First Data Resource Center (Kids First DRC) initiative funded by the NIH Office of the Director and the National Cancer Institute. Consortium data release policy requires that researchers be credited in publications. See https://kidsfirstdrc.org/policies for full terms.

**Your response:**
```
[Provide consortium/study affiliation information here]
```

---

### A.4 — What are related or predecessor datasets?

Document lineage, versioning, and complementary data.

- **Newer versions** — If this is a new release, which version(s) does it supersede?
- **Related cohorts** — Are there companion datasets (same study, different assays)?
- **Derived datasets** — Does this combine or extend other published data?
- **Public datasets** — If mirrored in GEO, cBioPortal, or Zenodo, note the primary repository

**Example:**
> - **Parent study:** `ewing-bcm-2024-ewing-patient-rnaseq` (patient-derived tumor samples; same lab, complementary data)
> - **Related dataset:** `ewing-chop-2023-fusion-proteomics` (same five cell lines; proteomics data)
> - **Supercedes:** `ewing-bcm-2023-cell-lines-v1` (older version; use v2.0 or later for new analyses)
> - **Primary repository:** GEO GSE234567 (this is the authoritative copy; all updates posted there first)

**Your response:**
```
[Provide lineage and related dataset information here]
```

---

## Section B: Composition and Data Structure

### B.1 — What do the rows/instances represent?

Describe the unit of observation in the dataset.

- Each row is a **[what?]** — sample, patient, tumor, cell line, experiment, etc.
- How are rows organized? (by patient? by timepoint? by assay?)
- What makes a row unique?

**Example:**
> Each row represents one RNA-seq library from an Ewing sarcoma cell line. Five cell lines (A673, TC-71, EW8, TC-32, RH1) were cultured and sequenced in biological triplicate (15 libraries total). Each library is uniquely identified by sample_id (e.g., EWING-A673-01).

**Your response:**
```
[Describe the unit of observation here]
```

---

### B.2 — How many instances/rows are there?

Provide total counts and breakdowns if applicable.

**Example:**
> - **Total libraries:** 15 (5 cell lines × 3 biological replicates)
> - **Total reads:** ~675M raw reads (45M per library average)
> - **Aligned reads:** ~630M (93% alignment rate)

**Your response:**
```
[Provide instance/row counts here]
```

---

### B.3 — Data Dictionary: What are all the columns/variables?

Create a table documenting every column in the dataset:

| Column Name | Data Type | Description | Required? | Example | Units |
|---|---|---|---|---|---|
| `sample_id` | string | Unique identifier | Yes | EWING-A673-01 | N/A |
| `cell_line` | string | Ewing cell line name | Yes | A673 | N/A |
| `replicate` | integer | Biological replicate | Yes | 1 | count |
| `rna_extraction_date` | date | When RNA was extracted | Yes | 2024-01-15 | YYYY-MM-DD |
| `library_kit` | string | RNA-seq library prep kit | Yes | NEXTflex | N/A |
| `sequencer` | string | Sequencing platform | Yes | Illumina NovaSeq 6000 | N/A |
| `raw_reads` | integer | Number of raw sequencing reads | No | 45,000,000 | count |
| `aligned_reads` | integer | Reads aligned to GRCh38 | No | 42,000,000 | count |
| `fusion_confirmed` | boolean | EWSR1-FLI1 confirmed by qPCR | Yes | true | Yes/No |
| `quality_flag` | enum | QC status | Yes | PASS | PASS, REVIEW, FAIL |
| `notes` | string | Free-text comments | No | Slight adapter contamination | N/A |

**Your response:**
```
[Provide data dictionary table here]
```

---

### B.4 — Are there natural splits or subsets of the data?

Describe how the data can be partitioned (e.g., for machine learning train/test split, temporal splits, subgroup analyses).

**Example:**
> No pre-defined splits. For machine learning applications, we recommend:
> - **Stratified by cell line:** Train on 4 lines, hold out 1 line as validation (avoids within-cell-line overfitting)
> - **By assay quality:** Separate high-quality (quality_flag = PASS) from review-level samples for conservative analyses

**Your response:**
```
[Describe natural splits or suggested partitioning here]
```

---

### B.5 — Are there known data quality issues or gaps?

Document any problems, incompleteness, or anomalies users should know about.

| Issue | Affected Samples | Severity | Recommended Action | Resolved? |
|---|---|---|---|---|
| RNA integrity below ideal | EWING-TC-32-02 | Low | Flag in analyses; consider excluding from QC-strict subsets | No |
| Adapter contamination | EWING-TC-32-02, EWING-RH1-03 | Low | Trim adapters before alignment | Yes (v2.1) |
| Missing quality data | 3 samples | Low | Contact submitter for RIN values | Partial |

**Example:**
> - **Sample EWING-TC-32-02:** RNA integrity number (RIN) = 7.1 (below ideal 8.0); included but should be flagged in downstream analyses
> - **Samples EWING-RH1-01 and EWING-RH1-03:** ~5% adapter contamination in raw FASTQ; pre-trimming required
> - **Overall:** No missing values in core columns; all libraries successfully sequenced

**Your response:**
```
[Describe known issues, missing values, and quality concerns here]
```

---

## Section C: Collection and Preprocessing

### C.1 — How was the data acquired? (Methods for each data type)

Provide detailed methods for data collection and generation. Include:
- **Sample source** — Where did samples come from? (cell lines, patients, tissues)
- **Collection protocol** — How were samples collected, preserved, or cultured?
- **Extraction/preparation** — RNA extraction, protein preparation, etc.
- **Measurement technology** — Sequencing platform, microarray, assay kit, etc.
- **Analysis pipeline** — Alignment, normalization, quality control steps

**Example (RNA-seq):**
> **Cell culture:** Five Ewing sarcoma cell lines (A673, TC-71, EW8, TC-32, RH1) maintained in RPMI 1640 + 10% FBS at 37°C, 5% CO₂. Cultures tested negative for mycoplasma (Lonza MycoAlert) and maintained at passages 8–15.
>
> **RNA extraction:** Total RNA from ~1×10^7 cells using TRIzol (Invitrogen). Quality assessed by Agilent Bioanalyzer; RIN ≥7.5 required.
>
> **Library prep & sequencing:** NEXTflex RNA-seq kit; 1 μg total RNA per sample. Illumina NovaSeq 6000; 2×150 bp paired-end; targeting 45M reads/library.
>
> **Bioinformatics pipeline:**
> - Adapter trimming: Trim Galore (cutadapt defaults)
> - Alignment: STAR v2.7.10a to GRCh38
> - Quantification: featureCounts v2.0.1 (Subread)
> - Normalization: edgeR v3.38.0 (CPM; log2(CPM + 1))
> - Quality control: Removal of genes with CPM < 1 across all samples

**Your response:**
```
[Provide detailed methods here]
```

---

### C.2 — Over what time period was data collected?

Specify the timeline for sample collection, processing, and analysis.

**Example:**
> Sample collection: January 2023 – August 2024  
> RNA extraction and library prep: January 2024 – August 2024  
> Sequencing: August 2024 – September 2024  
> Bioinformatic processing and QC: September 2024 – October 2024  
> Repository submission: November 2024

**Your response:**
```
[Provide collection and processing timeline here]
```

---

### C.3 — Were any preprocessing or normalization steps applied?

Document all computational transformations, including software versions.

**Example:**
> **Raw to aligned:**
> 1. Quality control (FastQC)
> 2. Adapter trimming (Trim Galore v0.6.10)
> 3. Alignment to GRCh38 (STAR v2.7.10a)
> 4. Alignment QC (samtools v1.15, Picard Tools v2.27)
>
> **Aligned to counts:**
> 1. Quantification with featureCounts v2.0.1 (Subread)
> 2. Count matrix assembly (R v4.2.0)
>
> **Normalization for downstream:**
> 1. Counts per million (CPM)
> 2. Log2 transformation: log2(CPM + 1)
> 3. Filtering: Remove genes with CPM < 1 in all samples (reduces noise)

All software versions and parameters documented in lab GitHub: [link]

**Your response:**
```
[Describe preprocessing and normalization steps here]
```

---

### C.4 — Were ethical review or informed consent procedures followed?

Describe IRB approvals, consent models, and ethical compliance.

**For cell line data:**
> This study uses established commercial cell lines (ATCC, DSMZ) that are widely available research materials. No human subjects research approval required. Cell line authentication performed by STR profiling (IDEXX Laboratories).

**For patient-derived data:**
> IRB approval: [Institution IRB #XXXX-XXXX]  
> Informed consent: Broad research consent (allows secondary research)  
> Restrictions: No consent for commercial use; contact PI before clinical translation  
> De-identification: Coded patient IDs; no PHI; meets HIPAA Safe Harbor

**Your response:**
```
[Describe ethical review and consent procedures here]
```

---

## Section D: Provenance and Attribution

### D.1 — What is the original source of each data instance?

Explain how each sample, record, or observation came into being.

**For original datasets:**
> Samples were derived from five commercially available Ewing sarcoma cell lines:
> - A673 (ATCC CRL-1598)
> - TC-71 (ATCC CRL-1983)
> - EW8 (ATCC CRL-2141)
> - TC-32 (DSMZ ACC-379)
> - RH1 (ATCC CRL-7684)

**For curated/aggregated datasets:**
> This dataset aggregates RNA-seq from three public repositories:
> - GEO (47 samples from GSE12345)
> - cBioPortal (23 samples from TARGET-Ewing)
> - Zenodo (15 samples from institutional submission)

**Your response:**
```
[Describe the source and provenance of data here]
```

---

### D.2 — Has this dataset been used in prior publications or studies?

Cite any publications where this exact data or subsets were analyzed.

**Example:**
> This is newly generated data. However, related transcriptomic studies in the same cell lines:
> - Smith et al. (2023). "Fusion-specific signatures in Ewing sarcoma." *Cancer Res.* PMID:35678901
> - Johnson et al. (in press). "EWSR1-FLI1 dependency profiling." Preprint: https://doi.org/...

**Your response:**
```
[List prior publications using this data here]
```

---

### D.3 — Are there known limitations on reproducibility?

Describe factors affecting whether analyses can be reproduced.

**Example:**
> 1. **Cell line drift:** Commercial lines accumulate mutations over passages. Data represent passages 8–15; re-authentication recommended for extended culture.
> 2. **Single platform:** Sequenced on one instrument type (Illumina NovaSeq). Batch effects from other platforms (PacBio, 10x) should be evaluated before meta-analysis.
> 3. **Manual processing:** RNA extraction and library prep are manual; residual technical variation across replicates expected.
> 4. **No code release:** Bioinformatic scripts available upon request (not published yet).

**Your response:**
```
[Describe reproducibility limitations here]
```

---

## Section E: Uses and Licensing

### E.1 — What is this dataset intended for?

Describe primary and secondary use cases.

**Example:**
> **Primary use:** Identify EWSR1-FLI1 fusion-specific transcriptional signatures as targets for therapeutic development in Ewing sarcoma.
>
> **Secondary uses:**
> - Benchmark for Ewing sarcoma RNA-seq analysis pipelines
> - Algorithm validation (fusion detection, copy-number analysis)
> - Educational examples for genomics courses
> - Cross-study cohort comparisons

**Your response:**
```
[Describe intended uses here]
```

---

### E.2 — What are the access restrictions and license terms?

Specify how the dataset can be used, modified, and redistributed.

| Aspect | Details |
|---|---|
| **License** | CC0-1.0 (Public Domain Dedication) |
| **License URL** | https://creativecommons.org/publicdomain/zero/1.0/ |
| **Permits derivatives** | Yes |
| **Permits commercial use** | Yes |
| **Requires attribution** | No (appreciated, but not required) |
| **Access tier** | Public (no authentication) |
| **Data use restrictions** | None |
| **Consent restrictions** | N/A (cell lines) |
| **Publication policy** | None |

**Example (for restricted data):**
> License: CC-BY-4.0  
> Access: Controlled (requires approved data access request)  
> Permits derivatives: Yes, but with attribution  
> Permits commercial: No  
> Consent restrictions: Broad research use only; no clinical translation without PI approval  
> Publication policy: 12-month embargo from data release

**Your response:**
```
[Specify license and access restrictions here]
```

---

### E.3 — Is this dataset suitable for [machine learning / clinical decision support / regulatory submissions]?

Explicitly assess suitability for different use contexts.

**Machine learning:**
> Yes, suitable for:
> - Fusion detection algorithm training (balanced positive examples)
> - Transfer learning from larger single-cell RNA-seq datasets
> - Batch-effect modeling across platforms
>
> Limitations: Small sample size (n=5 lines); cell line-specific biases may not generalize to primary tumors

**Clinical decision support:**
> No. This is cell line data, not patient-derived. Cannot be used to support clinical claims. Any clinical application requires validation in patient cohorts with appropriate ethical oversight.

**Regulatory submissions (FDA, EMA):**
> Not recommended as primary evidence. Cell line data can support exploratory science but not clinical efficacy or safety claims. Would require preclinical/clinical bridging studies.

**Your response:**
```
[Assess suitability for your use context here]
```

---

### E.4 — Has this dataset been misused, and are there explicit restrictions?

Flag if data have been used inappropriately or require explicit disclaimers.

**Example:**
> No known misuse. However, we recommend that any publication using these data include an explicit statement: "This analysis is based on cell line data and requires validation in patient-derived samples and/or clinical cohorts before any clinical translation."

**Your response:**
```
[Document any prior misuse or required disclaimers here]
```

---

## Section F: Distribution and Access

### F.1 — How and where can users access the dataset?

Specify repository, formats, download procedures, and file sizes.

| Aspect | Details |
|---|---|
| **Primary repository** | Gene Expression Omnibus (GEO) |
| **Accession** | GSE234567 |
| **URL** | https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE234567 |
| **Data formats** | Raw FASTQ; aligned BAM; count matrix (CSV/TSV) |
| **Total size** | ~80 GB (FASTQ); ~3 GB (BAM); ~50 MB (counts) |
| **Download method** | FTP (GEO); Aspera; public links; SRA-toolkit |
| **Mirror repositories** | Zenodo [DOI:...] (backup copy); figshare [record ID] |

**Your response:**
```
[Specify access locations and procedures here]
```

---

### F.2 — Are there version or snapshot considerations?

Document versioning, which version to cite, and errata.

**Example:**
> **Current version:** v2.1 (released July 2024)  
> **Recommended version:** v2.1 (v2.0 contains alignment bug in 2 samples; corrected in v2.1)  
> **Citation:** Use accession GSE234567 + version tag in publications  
> **Errata:** v2.0 BAM files for EWING-TC-32-02 and EWING-RH1-03 contain adapter contamination; corrected BAM files in v2.1

**Your response:**
```
[Describe versioning and snapshot information here]
```

---

### F.3 — Will the dataset be updated or maintained?

Specify whether dataset is static or evolving.

**Example:**
> **Status:** Archived (static after publication). No ongoing updates planned. Original repository (GEO) guarantees long-term preservation. Contact Dr. Jane Smith (jsmith@bcm.edu) for questions.

**Your response:**
```
[Specify maintenance status here]
```

---

## Section G: Known Issues and Limitations

### G.1 — What are the key limitations?

Honestly document restrictions on applicability and generalizability.

**Example:**
> 1. **Limited genetic diversity:** Five cell lines from unknown genetic ancestry. Not suitable for population genetics or ancestry-specific analyses.
> 2. **Cell line artifacts:** Established lines accumulate mutations over passages. Data represent a point-in-time snapshot (passage 8–15, 2024).
> 3. **Bulk RNA resolution:** No single-cell analysis. Cell-type-specific signals are averaged; validation recommended via flow cytometry or immunohistochemistry.
> 4. **No germline data:** Only somatic mutations in tumor cells; no normal controls.
> 5. **No copy-number calls:** Variant annotations not provided; users must call variants de novo if needed.

**Your response:**
```
[Document key limitations here]
```

---

### G.2 — Are there data quality issues?

Detail problems, anomalies, or concerns.

| Issue | Affected Data | Severity | Recommended Action | Status |
|---|---|---|---|---|
| Adapter contamination | 2 samples (EWING-TC-32-02, RH1-03) | Low | Trim adapters before use | Fixed in v2.1 |
| Low RNA integrity | 1 sample (EWING-TC-32-02, RIN=7.1) | Low | Flag in analyses | Ongoing |

**Your response:**
```
[Describe data quality issues here]
```

---

### G.3 — Are there gaps in data or documentation?

Honestly note what's missing.

**Example:**
> - Somatic variant calls not provided; users must call variants de novo if needed
> - Exome sequencing not performed; only transcript-level data available
> - Metadata on passage number not linked to sequencing results; passage effects on expression not formally analyzed
> - No single-cell data; cell-type composition averaged

**Your response:**
```
[Document gaps and missing data here]
```

---

## Section H: Molecular Annotation (for Biomedical/Genomic Datasets)

### H.1 — What disease or condition does this dataset represent?

Describe the biology and disease context.

**Example:**
> Ewing sarcoma (ES), a malignant bone sarcoma of childhood and young adulthood. All five cell lines carry the recurrent EWSR1-FLI1 fusion translocation t(11;22)(q24;q12), which is pathognomonic for classical Ewing sarcoma. This fusion encodes an oncogenic EWS-FLI1 transcription factor that drives the disease.

**Your response:**
```
[Describe the disease or biological context here]
```

---

### H.2 — What are key molecular features?

Summarize the genetic and molecular landscape.

| Feature | Value |
|---|---|
| **Primary condition** | Ewing sarcoma |
| **Recurrent fusion(s)** | EWSR1-FLI1 (t(11;22)) |
| **Secondary mutations** | TP53 loss in 3/5 lines (detected by WES) |
| **Assay type(s)** | RNA-seq (bulk total RNA) |
| **Reference genome** | GRCh38.p14 (hg38) |
| **Cohort size** | 5 cell lines; 15 RNA-seq libraries |

**Your response:**
```
[Describe molecular features and mutations here]
```

---

### H.3 — Special considerations: germline, somatic, or population-level?

Flag considerations for genetic/privacy analysis.

**Example:**
> **Germline:** No germline data (cell lines only). Not suitable for population genetics or ancestry analysis.
>
> **Somatic:** Somatic mutations present but not formally annotated in this release. Variant calls available upon request.
>
> **Population:** Five cell lines of unknown genetic background. All established commercial stocks. Biases toward passage-accumulated mutations.

**Your response:**
```
[Describe germline/somatic/population considerations here]
```

---

## Section I: Consent and Ethics

### I.1 — What consent model was used?

Describe how participants (if any) consented to data use.

**For patient data:**
> **Informed consent:** Broad research use consent (allows secondary research without re-contacting participants)  
> **Restrictions:** Excludes commercial use without additional approval  
> **De-identification:** Coded patient IDs; no direct identifiers; meets HIPAA Safe Harbor  
> **Reconsent:** Not required for research use; required for commercial applications

**For cell lines:**
> N/A (commercial cell lines; no human participants)

**Your response:**
```
[Describe consent model and restrictions here]
```

---

### I.2 — What are the ethical or privacy considerations?

Flag any special considerations for responsible data use.

**Example:**
> - **Cell line authentication:** All lines authenticated by STR profiling; documented in lab records.
> - **No re-identification risk:** Established commercial lines; no patient data; no unique identifiers.
> - **Responsible research practices:** Recommend acknowledgment of original study in publications.

**Your response:**
```
[Document ethical and privacy considerations here]
```

---

## Section J: Citation and Attribution

### J.1 — How should users cite this dataset?

Provide standard citation format(s).

**Example Citation:**
```
Smith, Jane, et al. (2024). RNA-seq from Ewing Sarcoma Cell Lines with EWSR1-FLI1 Fusion. 
Gene Expression Omnibus. Accession GSE234567. 
https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE234567
```

**For publications:**
> Smith, J., Johnson, M., Brown, K., & Lee, S. (2024). RNA-seq from Ewing Sarcoma Cell Lines with EWSR1-FLI1 Fusion. *Gene Expression Omnibus*. GSE234567. Retrieved from https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE234567

**For code/data repositories:**
> Smith et al. (2024). RNA-seq from Ewing Sarcoma Cell Lines. GEO GSE234567. https://doi.org/[dataset-doi]

**Your response:**
```
[Provide citation format(s) here]
```

---

### J.2 — What is the disclaimer for clinical use?

Include standard research-only disclaimer.

**Standard disclaimer:**
> **This dataset is provided for research and educational purposes only.** This metadata is research documentation, not medical advice. Datasets in the Ewing Open Data Catalog are for research and educational use. Any clinical applications require:
> 1. Independent expert validation
> 2. Institutional review board (IRB) or research ethics committee approval
> 3. Appropriate regulatory approval (e.g., FDA for clinical studies)
>
> Users assume full responsibility for compliance with applicable laws, regulations, and ethical standards in their jurisdiction. Cell line data do not represent patient biology and should not be used to support clinical claims without patient-derived validation.

**Your response:**
```
[Confirm or customize the disclaimer here]
```

---

## Section K: Worked Example(s)

### K.1 — Canonical Metadata Model Example (JSON)

Provide a complete, synthetic example conforming to the canonical metadata model specification.

**Example:**
```json
{
  "id": "ewing-bcm-2024-cell-lines-rnaseq",
  "title": "RNA-seq from Ewing Sarcoma Cell Lines with EWSR1-FLI1 Fusion",
  "accession": "GEO:GSE234567",
  "repository": {
    "url": "https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE234567",
    "type": "geo",
    "format": ["FASTQ", "BAM", "CSV"]
  },
  "submitterOrConsortium": {
    "name": "Dr. Jane Smith",
    "affiliation": "Baylor College of Medicine, Center for Pediatric Cancer",
    "contactEmail": "jsmith@bcm.edu",
    "orcid": "0000-0001-2345-6789",
    "consortium": false
  },
  "accessTier": {
    "tier": "public",
    "evidenceUrl": "https://www.ncbi.nlm.nih.gov/geo/"
  },
  "license": {
    "id": "CC0-1.0",
    "url": "https://creativecommons.org/publicdomain/zero/1.0/",
    "permitsDerivatives": true,
    "permitsCommercial": true,
    "requiresAttribution": false,
    "snapshotRef": "https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE234567"
  },
  "provenance": {
    "retrievedAt": "2026-07-24T15:30:00Z",
    "version": "2.1",
    "publicationPmidDoi": ["PMID:35678901"],
    "consortiumPolicyUrl": null,
    "attribution": {
      "generatedCredit": "Smith et al. (2024). RNA-seq from Ewing Sarcoma Cell Lines with EWSR1-FLI1 Fusion. Gene Expression Omnibus GSE234567.",
      "standardCitation": "Smith, Jane, et al. (2024). RNA-seq from Ewing Sarcoma Cell Lines with EWSR1-FLI1 Fusion. Gene Expression Omnibus. Accession GSE234567."
    }
  },
  "lineage": {
    "duplicateOf": null,
    "supersedes": ["ewing-bcm-2024-cell-lines-rnaseq-v2.0"],
    "derivedFrom": null,
    "relatedDatasets": ["ewing-bcm-2024-ewing-patient-rnaseq"]
  },
  "reidentification": {
    "riskLevel": "minimal",
    "basis": "Established cell lines; no patient data; no germline; commercial research materials",
    "smallCellsFlag": false,
    "germlinePresent": false,
    "notes": "STR profiling confirms cell line identity"
  },
  "molecular": {
    "tumorType": "Ewing sarcoma",
    "driverFusion": ["EWSR1-FLI1"],
    "assay": ["RNA-seq"],
    "cohortSizeAggregate": 15,
    "sourcePublication": "PMID:35678901"
  },
  "specVersions": ["canonical-model-v1.0"],
  "completenessScore": {
    "before": 60,
    "after": 95,
    "curatedBy": "Dr. Jane Smith"
  },
  "disclaimer": "This dataset is provided for research and educational purposes only. This metadata is research documentation, not medical advice. Any clinical applications require independent expert validation, institutional review, and appropriate regulatory approval."
}
```

---

### K.2 — Sample Data Table (First 10 rows of count matrix)

**Synthetic example of typical data structure:**

| gene_id | gene_name | EWING-A673-01 | EWING-A673-02 | EWING-A673-03 | EWING-TC-71-01 | EWING-TC-71-02 | ... |
|---|---|---|---|---|---|---|---|
| ENSG00000000003 | TSPAN6 | 145 | 167 | 142 | 201 | 198 | ... |
| ENSG00000000005 | TNMD | 0 | 0 | 0 | 0 | 0 | ... |
| ENSG00000000419 | DPM1 | 892 | 1056 | 845 | 1123 | 1087 | ... |
| ENSG00000000457 | SCYL3 | 42 | 53 | 48 | 67 | 71 | ... |
| ENSG00000000460 | C1orf112 | 201 | 245 | 198 | 267 | 289 | ... |
| ENSG00000000461 | FUCA2 | 0 | 0 | 1 | 0 | 2 | ... |
| ... (continuing for ~20,000 genes) | ... | ... | ... | ... | ... | ... | ... |

---

## Section L: Compliance Checklist

Before submitting your datasheet, verify:

- [ ] All required fields in Section A completed (motivation, team, dates)
- [ ] Section B fully describes the data (rows, counts, columns)
- [ ] Section C includes detailed methods and preprocessing pipeline
- [ ] Section D documents provenance and prior uses
- [ ] Section E specifies license and access restrictions clearly
- [ ] Section F provides exact URLs and download instructions
- [ ] Section G honestly documents limitations and known issues
- [ ] Section H includes molecular annotation (for genomic data)
- [ ] Section I documents consent and ethical review
- [ ] Section J specifies citation format and includes disclaimer
- [ ] Section K includes at least one complete worked example
- [ ] All URLs and accessions have been verified/tested
- [ ] Disclaimer includes "research documentation only — not medical advice"
- [ ] License is specified (data license and this template's CC-BY-4.0)
- [ ] No confidential or identifiable information included

---

## References

- **Gebru, T., et al. (2019).** Datasheets for Datasets. *arXiv preprint arXiv:1803.09010*. https://arxiv.org/abs/1803.09010
- **Wilkinson, M. D., et al. (2016).** The FAIR Guiding Principles for scientific data management and stewardship. *Scientific Data*, 3, 160018. https://www.nature.com/articles/sdata201618
- **NIH Data Management and Sharing Policy.** https://sharing.nih.gov/data-management-and-sharing-policy
- **GA4GH Data Interchange Formats.** https://www.ga4gh.org/

---

**Document Version:** 1.0  
**License:** CC-BY-4.0  
**Last Updated:** 2026-07-24

Questions or feedback? Contact the Ewing Open Data Catalog team or submit an issue to the catalog repository.

**Example Response:**
> 47 tumor samples (47 unique patients); 1 sample per patient. Data includes: (i) RNA-seq reads aligned to hg38 with gene-level TPM counts (top 15,000 genes); (ii) clinical metadata (age, gender, primary tumor site, metastases at diagnosis, treatment response); (iii) fusion gene status (FISH-confirmed or inferred from RNA-seq). No normal/healthy controls included.

**Your Response:**
```
[Describe composition and instance counts]
```

---

### A3. Data Collection & Measurement

**Question:** How was the data collected? What measurement instruments or protocols were used?

**Guidance:** Describe the wet-lab or computational protocols, sample preparation, sequencing platform, depth, and any quality control steps.

**Example Response:**
> Tumor samples were collected at primary diagnosis or relapse. RNA was extracted using TRIzol, quality-assessed with Agilent Bioanalyzer (RIN > 6), and subjected to Illumina TruSeq RNA library prep (polyA enrichment). Sequencing was performed on Illumina HiSeq 2500 (2 × 100 bp paired-end) at an average depth of 40M reads per sample. Reads were aligned to GRCh38 using STAR (v2.5.2a) and quantified with HTSeq.

**Your Response:**
```
[Describe collection and measurement protocols]
```

---

## Part 2: Composition (Datasheets-for-Datasets Part B)

### B1. Instance Types

**Question:** What are the instances (rows, records, or individual data points) in the dataset?

**Guidance:** Define the unit of observation (e.g., tumor sample, patient, gene-sample pair).

**Example Response:**
> Instances are tumor samples. Each row represents one sample with expression counts (columns) for 15,000 genes.

**Your Response:**
```
[Define instance type and unit of observation]
```

---

### B2. Number of Instances

**Question:** How many instances are in the dataset?

**Example Response:**
> 47 samples (columns: gene identifiers; rows: samples).

**Your Response:**
```
[Specify instance count]
```

---

### B3. Data Dictionary & Fields

**Question:** What fields (columns) does the dataset contain?

**Guidance:** For each major field, provide: field name, data type, units (if numerical), allowed values (if categorical), definition, and any transformations applied.

**Format:**

| Field Name | Data Type | Units / Allowed Values | Description | Caveat or Transformation |
|---|---|---|---|---|
| sample_id | string | N/A | De-identified sample identifier linked to GEO accession | Linked to GSM accession; original patient identifiers redacted |
| gene_symbol | string | HGNC approved symbol | Official gene symbol per NCBI Gene | Top 15,000 genes by variance across samples; non-coding genes excluded |
| expression_tpm | float | log10(TPM + 1) | Transcript abundance (TPM = transcripts per million) | Zero-inflated; missing (N/A) for genes with zero reads across all samples |
| driver_fusion | string | EWSR1-FLI1, EWSR1-ERG | Predicted driver fusion from RNA-seq fusion callers | Inferred from STAR-Fusion output; FISH confirmation status in clinical metadata |
| age_at_diagnosis | integer | years | Patient age when Ewing sarcoma was diagnosed | Binned into 5-year bands for privacy (k ≥ 5 per bin) |
| primary_tumor_site | string | Long bone, pelvis, soft tissue, other | Anatomic location of primary tumor | Aggregated category (not sub-site specificity) to protect small-cell risk |

**Your Response:**

| Field Name | Data Type | Units / Allowed Values | Description | Caveat or Transformation |
|---|---|---|---|---|
| | | | | |

---

### B4. Missing Data & Not Applicable Values

**Question:** Are there missing values? How are they represented?

**Guidance:** Describe encoding of missing data (NULL, "N/A", 0, -9999, etc.) and reasons (not measured, not applicable, redacted, failed QC, etc.).

**Example Response:**
> Missing values encoded as "N/A". Reasons: (i) "expression_tpm" is N/A for genes with zero reads across all samples; (ii) "driver_fusion" is N/A for samples with ambiguous fusion callers' output or multiple predicted fusions; (iii) "metastases_at_diagnosis" is N/A for 3 samples lacking clinical staging information at time of sample collection.

**Your Response:**
```
[Describe missing data encoding and reasons]
```

---

## Part 3: Collection Process (Datasheets-for-Datasets Part C)

### C1. Ethical Review & Informed Consent

**Question:** What informed consent and ethics approvals governed data collection and sharing?

**Guidance:** Reference IRB approval number, consent scope (research use, publication, secondary use, commercial use), and any restrictions (re-contact requirement, genetic-discovery embargo, etc.). If data was collected under a Data Use Agreement (DUA), describe its scope.

**Example Response:**
> Original study approved by COG Institutional Review Board (IRB #2009-P-000123). Parental informed consent permitted: (i) research use and analysis; (ii) publication and data sharing with qualified researchers; (iii) secondary use in genome-wide association studies and machine-learning applications. No embargo period; no re-contact clause. Data shared under CC-BY-4.0 license; public access permitted.

**Your Response:**
```
[Describe informed consent, IRB approval, and consent scope]
```

---

### C2. Data Acquisition Timeline

**Question:** When was the data collected and over what time span?

**Example Response:**
> Tumor samples collected 2010–2015 at COG member institutions. RNA extraction and sequencing performed 2016–2017. Publicly released to NCBI GEO in 2017; archived version used for catalog curation (retrieved 2026-07-20).

**Your Response:**
```
[Describe collection dates and data release timeline]
```

---

### C3. Any Confidentiality or Privacy Measures

**Question:** What de-identification, anonymization, or privacy protections were applied?

**Guidance:** Describe removal of PII (names, dates of birth, medical record numbers), aggregation of small counts, binning of continuous variables, and any residual re-identification risks.

**Example Response:**
> Patient identifiers (name, MRN, date of birth) removed entirely. Age binned into 5-year bands (k ≥ 5 per bin, no minimum age disclosure). Geographic site redacted to COG region (not specific institution). Sample IDs are GEO-assigned (GSM accession) with no link to clinical identifiers. Germline variants not reported. Linkage risk flagged: rare disease + fusion genotype + age range may enable re-identification with knowledge of study sites and enrollment years; caution advised for phenotype-fusion correlation studies.

**Your Response:**
```
[Describe de-identification and privacy measures]
```

---

## Part 4: Preprocessing & Quality Control

### D1. Data Cleaning & Transformations

**Question:** What preprocessing, quality control, or cleaning steps were applied?

**Guidance:** Describe filtering (e.g., low-count genes, low-quality samples), normalization (log, TPM, quantile), batch correction, imputation, or any feature selection.

**Example Response:**
> QC steps: (i) Samples with > 50% missing values excluded (1 sample failed). (ii) Genes with median count < 1 TPM across samples excluded (5,000+ low-abundance genes removed). (iii) RNA-seq counts normalized to TPM and log-transformed (log10(TPM + 1)) to stabilize variance. (iv) Batch effect from 2016 vs. 2019 sequencing runs detected via ComBat-seq but NOT corrected (documented in known issues). (v) Top 15,000 genes by variance retained; remaining 30,000+ genes excluded.

**Your Response:**
```
[Describe preprocessing and QC steps applied]
```

---

### D2. Any Artifacts or Limitations Introduced

**Question:** Are there known data artifacts, batch effects, or limitations from preprocessing?

**Example Response:**
> Batch effect from 2016 vs. 2019 sequencing runs present; not corrected to preserve fusion-gene discovery signal. Fusion status inferred from RNA-seq, not confirmed by FISH for all samples (FISH confirmation available for subset only). Age binning introduces loss of temporal precision and may limit survival-curve granularity.

**Your Response:**
```
[Describe known artifacts and preprocessing limitations]
```

---

## Part 5: Uses (Datasheets-for-Datasets Part E)

### E1. Primary & Intended Uses

**Question:** What are the intended uses for this dataset?

**Guidance:** Cite the original study's intent (e.g., discovery of molecular subtypes, outcome prediction, drug response modeling).

**Example Response:**
> Intended uses: (i) Molecular subtype discovery and validation for EWSR1-FLI1-driven Ewing sarcomas; (ii) transcriptomic outcome prediction and prognostic modeling; (iii) cross-cohort meta-analysis of Ewing transcriptomes; (iv) machine-learning applications (e.g., neural network classifiers for fusion detection); (v) secondary uses in multi-cancer studies and oncology data integration efforts.

**Your Response:**
```
[List intended uses and applications]
```

---

### E2. Out-of-Scope & Prohibited Uses

**Question:** Are there uses that should NOT be pursued with this dataset?

**Guidance:** Describe uses that pose re-identification risk, misuse potential, or conflict with informed consent or licenses (e.g., commercial drug development, clinical decision-making without validation, re-identification attempts).

**Example Response:**
> Out-of-scope uses: (i) Clinical decision-making or patient care without independent validation and IRB review. (ii) Use in commercial drug development or licensing without consultation with source institution and original consent holders. (iii) Attempts to re-identify individuals. (iv) Comparison with germline genetic databases to infer inherited predisposition (no germline data provided; re-identification risk). (v) Application in resource-limited settings without data sovereignty consultation with original source country/institution (not applicable here; U.S. source; open-access license).

**Your Response:**
```
[Describe prohibited or out-of-scope uses]
```

---

## Part 6: Distribution

### F1. How is the Dataset Distributed?

**Question:** How can the dataset be accessed?

**Guidance:** Specify access method (download from repository, API access, request-based), access tier (open vs. controlled), and any registration or DUA requirement.

**Example Response:**
> Dataset is openly accessible via:
> 1. NCBI GEO (https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE24221) — direct download of raw and processed files
> 2. cBioPortal (https://www.cbioportal.org/study/summary?id=mskcc-10001) — interactive data exploration and visualization API
> 3. R Bioconductor package ExpressionAtlas::loadExpressionData() — programmatic access
> Access tier: OPEN (no registration or approval required)
> License: CC-BY-4.0 (attribute source; derivative works permitted)

**Your Response:**
```
[Describe distribution channels, access tier, and license]
```

---

### F2. Is There Any Restriction on Access or Use?

**Question:** Are there data use agreements, commercial restrictions, or publication embargoes?

**Example Response:**
> No access restrictions. Public data (NCBI GEO). License: CC-BY-4.0 (attribute source; no commercial restriction; derivatives permitted). No embargo period. Recommended citation: GEO GSE24221 and PMID: 29438695.

**Your Response:**
```
[Describe any restrictions on access or use]
```

---

## Part 7: Maintenance

### G1. Is This Dataset Maintained, Updated, or Versioned?

**Question:** Will the dataset be updated? If so, how often and under what versioning scheme?

**Example Response:**
> Dataset is stable; no new samples will be added. Original repository (GEO) maintains a frozen version GSE24221. Catalog curation version (1.0, retrieved 2026-07-20) documents metadata as of that date. Future updates to catalog record (e.g., DOI mint, Croissant JSON-LD export) will be versioned separately (v1.0, v1.1, etc.) and linked to source frozen release.

**Your Response:**
```
[Describe dataset maintenance and versioning plan]
```

---

### G2. Who Should Be Contacted for Questions or Issues?

**Question:** Who maintains the dataset and how should issues or questions be reported?

**Example Response:**
> Original dataset: Dr. Jane Smith (jane.smith@cog.org), Children's Oncology Group. Catalog curation: [Catalog Reviewer TO BE SECURED]. Report issues via: (i) GitHub pull request on this repository; (ii) NCBI GEO report form (https://www.ncbi.nlm.nih.gov/geo/info/seq.html#notify).

**Your Response:**
```
[Provide contact information for dataset questions or issues]
```

---

## Part 8: Molecular Annotation (Ewing-Specific Metadata)

### M1. Tumor Type & Fusion Status

**Question:** What is the tumor type and primary driver fusion in this cohort?

**Guidance:** Confirm Ewing sarcoma; note driver fusion(s), cohort composition (monosomatic vs. multi-fusion), and any non-Ewing cases included.

**Example Response:**
> Tumor type: Ewing sarcoma.  
> Driver fusion: EWSR1-FLI1 in 35/47 samples (74%); EWSR1-ERG in 8/47 (17%); ambiguous in 4/47 (9%).  
> Cohort homogeneity: Predominantly EWSR1-FLI1-positive; multi-fusion cohort.  
> Non-Ewing: None included.

**Your Response:**
```
[Describe tumor type, fusion status, and cohort composition]
```

---

### M2. Assay Details

**Question:** What primary assay(s) are used and at what depth/resolution?

**Guidance:** List sequencing type (RNA-seq, WES, WGS, targeted panel), sequencing platform, depth, read length, and any validation approaches.

**Example Response:**
> Primary assay: RNA-seq (Illumina TruSeq, 2 × 100 bp paired-end)  
> Sequencing platform: HiSeq 2500  
> Average depth: 40M reads per sample  
> Analysis: STAR alignment (hg38), HTSeq quantification, TPM normalization  
> Validation: Fusion status validated via FISH (subset of 20/47 samples); remaining inferred from STAR-Fusion output  
> Secondary assays: None (expression-only dataset)

**Your Response:**
```
[Describe assay type, depth, platform, and validation approaches]
```

---

### M3. Cohort Size & Sample Metadata

**Question:** What is the cohort size and what clinical/demographic metadata is available?

**Guidance:** Total sample count, patient demographics (age, gender, race/ethnicity), and clinical features (stage, treatment, outcome).

**Example Response:**
> Cohort size: 47 samples (47 unique patients).  
> Demographics: Median age 18 years (range 5–45). Gender: 26 male, 21 female. Race/ethnicity: not disclosed (privacy protection per original IRB approval).  
> Clinical metadata: Primary tumor site (long bone vs. pelvis vs. soft tissue); metastases at diagnosis (present/absent); treatment regimen (chemotherapy backbone + radiation ± surgery); event-free and overall survival (median follow-up 60 months).

**Your Response:**
```
[Describe cohort size, demographics, and clinical metadata]
```

---

### M4. Known Variants, Pathogenic Mutations, or Molecular Subtypes

**Question:** Are pathogenic variants, subtype classifications, or other molecular annotations reported?

**Guidance:** List any germline/somatic mutations, subtype calls (if applicable), pathway annotations, or known pathogenic variants.

**Example Response:**
> Variants reported: None (expression/fusion-centric dataset; no variant calls or germline data).  
> Molecular subtypes: Implicit subtypes based on fusion status (EWSR1-FLI1 vs. EWSR1-ERG); no formal subtype classification. Fusion-specific expression signatures can be derived but not pre-computed.  
> Pathogenic annotations: Not included; dataset focused on discovery of fusion-specific transcriptional programs, not clinical mutation interpretation.

**Your Response:**
```
[Describe variant, subtype, and pathogenic annotations]
```

---

## Part 9: Known Issues & Limitations

### I1. Data Quality Issues

**Question:** What known data quality issues or artifacts exist?

**Guidance:** Describe batch effects, outlier samples, missing clinical data, technical failures, or measurement artifacts.

**Example Response:**
> - Batch effect: 2016 vs. 2019 sequencing runs show platform/chemistry differences; not corrected.
> - Outlier samples: 1 sample (GSM1234567) shows > 50% missing values (< 5M reads); included but flagged.
> - Fusion ambiguity: 4 samples lack consensus fusion calls; marked as "ambiguous."
> - Clinical data gaps: 3 samples lack complete staging information; survival follow-up incomplete for 2 patients.
> - RNA degradation: RIN > 6 required, but 2 samples RIN 6.0–6.5 (borderline quality).

**Your Response:**
```
[Describe known data quality issues and artifacts]
```

---

### I2. Generalizability & Applicability

**Question:** How representative is this cohort? What populations or tumor subtypes might be underrepresented?

**Guidance:** Note cohort demographics, selection bias, geographic/temporal scope, and limitations on generalizability.

**Example Response:**
> Cohort scope: COG member institutions (primarily U.S.), 2010–2015.  
> Demographics: Predominantly pediatric (median age 18); few samples > 40 years (adult Ewing rare). Gender: roughly balanced. Race/ethnicity: not disclosed.  
> Fusion composition: Primarily EWSR1-FLI1 (74%); underrepresentation of EWSR1-ERG and rare fusions.  
> Selection bias: Tumors requiring RNA extraction and sequencing at time of study (may exclude rapidly fatal or highly chemosensitive cases with minimal biopsy material).  
> Generalizability: Results may not generalize to adult-onset Ewing, international cohorts, or rare-fusion subtypes.

**Your Response:**
```
[Describe cohort representativeness and generalizability limits]
```

---

### I3. Re-identification & Privacy Risks

**Question:** What residual re-identification risks remain despite de-identification?

**Guidance:** Describe linkage risk (rare disease + phenotype + age range), possible de-anonymization via auxiliary data, and mitigation strategies.

**Example Response:**
> Residual risks:
> - Rare disease + phenotype linkage: Ewing sarcoma is rare (~500 cases/year in U.S.); combination of fusion status + age range + primary site + outcome may enable re-identification via cross-reference with clinical literature or institutional records.
> - Age binning: 5-year bins minimize temporal specificity but do not eliminate re-identification in small bins.
> - Germline risk: None (no germline data). Somatic fusion genotypes not individually unique but informative in combination with phenotype.
> - Mitigation: Dataset is expression summary (not individual variant calls); phenotype limited to site, stage, age range (no fine-grain clinical details); data publicly available (no expectation of privacy). End-users should exercise caution when combining with external datasets or disease registries.

**Your Response:**
```
[Describe residual re-identification risks and mitigations]
```

---

### I4. Ethical Considerations & Recommendations for Use

**Question:** Are there special ethical considerations or recommendations for responsible use?

**Example Response:**
> Ethical considerations:
> - Rare-disease stewardship: Ewing sarcoma is a life-threatening condition with active research efforts; responsible use should cite source studies and engage with Ewing research community.
> - Pediatric population: Cohort includes minors (median age 18); secondary uses should respect pediatric research ethics principles (benefit, minimal risk, assent/consent).
> - Clinical misapplication: Derived outcome predictions or subtype models should NOT be used clinically without independent validation and IRB review.
> Recommendation: Use in multi-cohort analyses to increase power and reduce individual-cohort bias; cite and engage original authors for interpretation and collaborative studies.

**Your Response:**
```
[Describe ethical considerations and responsible-use recommendations]
```

---

## Part 10: Lineage & Relationships

### L1. Dataset Relationships

**Question:** Is this dataset a duplicate, update, mirror, or derived work of another dataset?

**Guidance:** Link to related records in the catalog or external repositories.

**Example Response:**
> - **Canonical version**: NCBI GEO GSE24221 (original submission, 2017).
> - **Mirrors**: cBioPortal study "mskcc-10001" (same data, different interface).
> - **Derived works**: Zenodo deposit "doi:10.5281/zenodo.7123456" (2022 snapshot for reproducibility).
> - **Supersedes**: None.
> - **Superseded by**: None (dataset is stable).

**Your Response:**
```
[Describe dataset relationships and lineage]
```

---

## Part 11: Canonical Metadata Record

Below is the structured metadata record in JSON format corresponding to the canonical metadata model. Fill in all fields:

```json
{
  "id": "[unique catalog identifier, e.g., GEO:GSE24221]",
  "title": "[dataset title as it appears in source]",
  "accession": "[public repository accession code]",
  "repository": "[repository name and base URL]",
  "submitterOrConsortium": "[author or consortium name]",
  "accessTier": {
    "tier": "[open|controlled]",
    "evidenceUrl": "[URL to source proving open access]"
  },
  "license": {
    "id": "[SPDX license ID or name, e.g., CC-BY-4.0]",
    "url": "[URL to license text]",
    "permitsDerivatives": "[true|false]",
    "snapshotRef": "[date or version snapshot]",
    "dataUseConditions": "[plain-text summary of restrictions or attribution requirements]"
  },
  "provenance": {
    "retrievedAt": "[ISO 8601 UTC datetime of metadata retrieval]",
    "version": "[dataset version as declared by source]",
    "publicationPmidDoi": "[PMID: ####### or DOI: 10.####/... or N/A]",
    "consortiumPolicyUrl": "[URL to source repository's metadata or policy documentation]",
    "attribution": "[recommended citation format from source]"
  },
  "reidentification": {
    "riskLevel": "[excluded|high|moderate|low]",
    "basis": "[plain-text explanation of risk assessment]",
    "smallCellsFlag": "[true|false — true if cohort size k < 5]",
    "germlinePresent": "[true|false — true if germline variants at individual level present]",
    "notes": "[additional context on privacy, consent scope, or re-id precautions]"
  },
  "molecular": {
    "tumorType": "[Ewing sarcoma or recognized subtype]",
    "driverFusion": "[fusion name, Mixed, or Not reported]",
    "assay": "[primary sequencing/measurement type]",
    "cohortSizeAggregate": "[integer: total unique individuals]",
    "sourcePublication": "[DOI or PMID or Zenodo citation]"
  },
  "fields": [
    {
      "name": "[field name]",
      "type": "[data type: string, integer, float, boolean, date]",
      "units": "[units or null]",
      "allowedValues": "[array of enum values or null]",
      "nullable": "[true|false]",
      "description": "[field description]",
      "caveats": "[transformations or limitations or null]"
    }
  ],
  "knownIssues": [
    "[issue 1 description]",
    "[issue 2 description]"
  ],
  "lineage": {
    "duplicateOf": "[id of canonical version or null]",
    "supersedes": "[array of superseded ids or empty array]"
  },
  "examples": [
    {
      "description": "[example description]",
      "uri": "[URL or file path to worked example]"
    }
  ],
  "specVersions": {
    "canonicalMetadataModel": "1.0",
    "croissantML": "[version or null]",
    "geoApi": "[version or null]",
    "cbioportalApi": "[version or null]",
    "gdcApi": "[version or null]",
    "icgcApi": "[version or null]"
  },
  "completenessScore": {
    "before": "[integer 0-100: completeness of source metadata]",
    "after": "[integer 0-100: completeness after curation]"
  },
  "disclaimer": "This record is research metadata only. It is not medical advice, clinical data, or intended for clinical use. Interpretation or application of any dataset information for patient care, clinical decision-making, or medical diagnosis requires qualified professional review. Ewing sarcoma is a rare, life-threatening tumor; no dataset summary should substitute for consultation with qualified oncology professionals and institutional review boards."
}
```

**Your Metadata Record:**

```json
{
  "id": "",
  "title": "",
  "accession": "",
  "repository": "",
  "submitterOrConsortium": "",
  "accessTier": {
    "tier": "",
    "evidenceUrl": ""
  },
  "license": {
    "id": "",
    "url": "",
    "permitsDerivatives": true,
    "snapshotRef": "",
    "dataUseConditions": ""
  },
  "provenance": {
    "retrievedAt": "",
    "version": "",
    "publicationPmidDoi": "",
    "consortiumPolicyUrl": "",
    "attribution": ""
  },
  "reidentification": {
    "riskLevel": "",
    "basis": "",
    "smallCellsFlag": false,
    "germlinePresent": false,
    "notes": ""
  },
  "molecular": {
    "tumorType": "Ewing sarcoma",
    "driverFusion": "",
    "assay": "",
    "cohortSizeAggregate": 0,
    "sourcePublication": ""
  },
  "fields": [],
  "knownIssues": [],
  "lineage": {
    "duplicateOf": null,
    "supersedes": []
  },
  "examples": [],
  "specVersions": {
    "canonicalMetadataModel": "1.0",
    "croissantML": null,
    "geoApi": null,
    "cbioportalApi": null,
    "gdcApi": null,
    "icgcApi": null
  },
  "completenessScore": {
    "before": 0,
    "after": 0
  },
  "disclaimer": "This record is research metadata only. It is not medical advice, clinical data, or intended for clinical use. Interpretation or application of any dataset information for patient care, clinical decision-making, or medical diagnosis requires qualified professional review. Ewing sarcoma is a rare, life-threatening tumor; no dataset summary should substitute for consultation with qualified oncology professionals and institutional review boards."
}
```

---

## Example: Synthetic Ewing Sarcoma Cohort Study

Below is a **worked example** of a complete datasheet for a synthetic dataset, demonstrating how to populate all sections.

### Example Dataset: "Synthetic Ewing Sarcoma Gene Expression & Fusion Annotation Cohort"

---

#### A1. Motivation & Dataset Curation (Example)

> **Synthetic Example:** This is a de-novo synthetic dataset created for demonstration purposes. It mimics the structure and metadata of real Ewing sarcoma expression studies (e.g., COG datasets, ICGC ARGO Ewing projects) without using actual patient data. Included in the Ewing catalog as a reference example for metadata completeness and template validation.

---

#### A2. Composition & Instances (Example)

> **Synthetic Example:** 50 synthetic tumor samples (50 unique simulated patients); 1 sample per patient. Data includes: (i) RNA-seq counts aligned to hg38 with gene-level TPM for 20,000 genes (top variance genes); (ii) clinical metadata (age, gender, primary tumor site, metastases at diagnosis, event-free survival); (iii) fusion gene status (synthetic driver fusion assignments: 35 EWSR1-FLI1, 10 EWSR1-ERG, 5 ambiguous). No normal/healthy controls. No germline variants. All data is synthetic; no real individuals represented.

---

#### A3. Data Collection & Measurement (Example)

> **Synthetic Example:** Synthetic data generated via a probabilistic RNA-seq simulator (splatter package, R; Zappia et al., 2017). Simulated tumors assigned random fusion status (70% EWSR1-FLI1, 20% EWSR1-ERG) and expression profiles sampled from empirical distributions derived from published Ewing datasets. Simulated as Illumina TruSeq 2 × 100 bp paired-end at 50M read depth per sample, aligned to GRCh38 via STAR mock-up, and quantified with HTSeq mock counts (no actual sequencing). Age, gender, and clinical outcomes simulated from published epidemiological parameters (Paulussen et al., Oncogene 2018).

---

#### B1–B3. Instance Types, Count, & Data Dictionary (Example)

| Field Name | Data Type | Units / Allowed Values | Description | Caveat or Transformation |
|---|---|---|---|---|
| sample_id | string | N/A | De-identified synthetic sample identifier | Format: SYN_EW_001 to SYN_EW_050 (simulated IDs; no real data) |
| gene_symbol | string | HGNC approved symbol | Synthetic gene identifier | 20,000 genes sampled from HGNC database; no non-coding or uncharacterized genes |
| expression_log2_tpm | float | log2(TPM + 0.1) | Synthetic transcript abundance (log2-transformed TPM) | Sampled from Gaussian process; zero-inflated (30% zeros) |
| driver_fusion | string | EWSR1-FLI1, EWSR1-ERG, ambiguous | Synthetic driver fusion assignment | 35 EWSR1-FLI1, 10 EWSR1-ERG, 5 ambiguous; randomly assigned with no link to expression profiles (unrealistic but demonstrates data structure) |
| age_at_diagnosis_years | integer | 1–40 | Synthetic patient age when tumor diagnosed | Sampled from truncated normal distribution (μ = 18, σ = 8, range 1–40) mimicking pediatric Ewing epidemiology |
| primary_tumor_site | string | long_bone, pelvis, soft_tissue, other | Synthetic primary tumor site | Sampled: 60% long bone, 25% pelvis, 10% soft tissue, 5% other |
| metastases_at_diagnosis | string | present, absent | Synthetic metastatic status at time of diagnosis | Sampled: 30% present, 70% absent (simplified; real data more granular) |
| event_free_survival_months | float | months | Simulated time to relapse, progression, or last follow-up | Sampled from Weibull distribution; 20% censored (no event by end of follow-up) |
| overall_survival_months | float | months | Simulated time to death or last follow-up | Sampled from Weibull distribution; 15% censored (alive at end of follow-up) |

**Count:** 50 samples (instances = rows; genes/measurements = columns in matrix form).

---

#### B4. Missing Data (Example)

> **Synthetic Example:** Missing values encoded as "N/A" or null. Reasons: (i) "expression_log2_tpm" is N/A for 6,000 genes per sample (zero-expression genes; zero-inflated component of simulator). (ii) "metastases_at_diagnosis" is N/A for 2 synthetic samples (missing clinical staging, simulating real-world data gaps). (iii) "primary_tumor_site" is "other" for 3 samples (data quality limitation in simulated clinical metadata). (iv) "event_free_survival_months" and "overall_survival_months" are censored (last-follow-up value, not terminal event) for 10 and 7 samples respectively.

---

#### C1. Ethical Review & Informed Consent (Example)

> **Synthetic Example:** This is a synthetic dataset; no real individuals or data were collected. Ethical approvals not applicable. If based on empirical distributions from published studies (Paulussen et al., Zappia et al.), those source studies obtained appropriate IRB approval and informed consent. This synthetic derivative is published under CC-BY-4.0 license with no privacy concerns.

---

#### C2. Data Acquisition Timeline (Example)

> **Synthetic Example:** Synthetic data generated 2026-06-15 using splatter R package v1.16.0 and custom simulation scripts. No real acquisition timeline; published for catalog template validation 2026-07-24.

---

#### C3. Confidentiality & Privacy Measures (Example)

> **Synthetic Example:** Data is entirely synthetic; no privacy concerns. Sample IDs (SYN_EW_001 to SYN_EW_050) are arbitrary strings with no link to real individuals. All clinical metadata (age, site, outcomes) are simulated; resemblance to real patient records is coincidental. No germline variants. No re-identification risk (not real data).

---

#### D1. Data Cleaning & Transformations (Example)

> **Synthetic Example:** QC steps: (i) Genes with median expression < 0.1 log2(TPM) excluded (5,000 low-abundance genes removed from original 25,000). (ii) Samples with > 50% missing expression values excluded (none in this synthetic dataset). (iii) Expression counts log2-transformed (log2(TPM + 0.1)) to stabilize variance. (iv) No batch effect correction applied (single synthetic batch). (v) Top 20,000 genes by variance retained; lowest 5,000 genes removed.

---

#### D2. Artifacts & Limitations (Example)

> **Synthetic Example:** Known limitations: (i) Synthetic data does not capture real biological complexity (e.g., gene-fusion interactions, isoform-specific expression, cell-type composition effects). (ii) Driver fusion assignment is independent of expression profile (unrealistic; real data shows fusion-specific expression signatures). (iii) Clinical outcomes simulated from epidemiological parameters, not from real cohort survival data. (iv) Age, site, and metastatic status generated independently (real data shows disease-biology associations). Use for template validation and training only; not for biological discovery.

---

#### E1. Primary & Intended Uses (Example)

> **Synthetic Example:** Intended uses: (i) Demonstration of datasheet template completeness; (ii) Validation of metadata JSON schema and canonical model implementation; (iii) Training example for contributors documenting real Ewing datasets; (iv) CI/testing fixture for Croissant ML validator and curation pipeline. NOT intended for biological discovery or clinical application.

---

#### E2. Out-of-Scope & Prohibited Uses (Example)

> **Synthetic Example:** Out-of-scope uses: (i) Any biological discovery or clinical interpretation (data is synthetic and does not represent true biology). (ii) Clinical decision-making or patient care (data is not real patient data; using synthetic examples clinically is unethical). (iii) Reproduction of published results from real Ewing studies (this synthetic dataset does not replicate any specific published cohort). (iv) Comparative analysis with real data without explicit acknowledgment that comparisons are with synthetic, unrealistic data. (v) Licensing or patent claims using this synthetic data as evidence.

---

#### F1. Distribution (Example)

> **Synthetic Example:** Dataset is openly distributed via:
> 1. GitHub repository (this project): `/docs/example-dataset-metadata.md` (this file)
> 2. Zenodo deposit (once minted, with DOI)
> 3. FAIR data portal / project website (if applicable)
> Access tier: OPEN (no registration or approval required)
> License: CC-BY-4.0 (attribute source; derivative works permitted)

---

#### F2. Restrictions on Access or Use (Example)

> **Synthetic Example:** No access restrictions. Public dataset. License: CC-BY-4.0 (attribute source; no commercial restriction; derivatives permitted). Recommended citation: "Ewing Sarcoma Open Data Catalog Synthetic Example Dataset (v1.0), Generated 2026-06-15. CC-BY-4.0."

---

#### G1. Maintenance (Example)

> **Synthetic Example:** Dataset is stable; version 1.0 is final unless template structure changes require regeneration. Catalog metadata version (retrieved 2026-07-24) documents this example as of that date. If template updated, this example may be regenerated (v2.0) to match new schema.

---

#### G2. Contact (Example)

> **Synthetic Example:** Dataset maintenance: Ewing Sarcoma Open Data Catalog team (contact: [TO BE SECURED]). Report issues via GitHub pull request on this repository.

---

#### M1. Tumor Type & Fusion Status (Example)

> **Synthetic Example:** Tumor type: Ewing sarcoma. Driver fusion: EWSR1-FLI1 in 35/50 samples (70%); EWSR1-ERG in 10/50 (20%); ambiguous in 5/50 (10%). Cohort homogeneity: Multi-fusion cohort with dominant EWSR1-FLI1 representation. Non-Ewing: None included (pure Ewing sarcoma cohort by design).

---

#### M2. Assay Details (Example)

> **Synthetic Example:** Primary assay: Simulated RNA-seq (Illumina TruSeq, 2 × 100 bp paired-end). Simulated platform: HiSeq 2500. Simulated depth: 50M reads per sample. Analysis: STAR alignment mock (hg38), HTSeq quantification mock, TPM normalization. Validation: No FISH confirmation (synthetic data only). Secondary assays: None.

---

#### M3. Cohort Size & Sample Metadata (Example)

> **Synthetic Example:** Cohort size: 50 samples (50 simulated unique patients). Simulated demographics: Median age 17 years (range 2–40). Gender: 26 male, 24 female (balanced). Race/ethnicity: Not simulated (privacy protection). Simulated clinical metadata: Primary tumor site (30 long bone, 12 pelvis, 5 soft tissue, 3 other); metastases at diagnosis (15 present, 35 absent); treatment: not recorded in this dataset; event-free survival (median 36 months, range 3–60); overall survival (median 48 months, range 6–60).

---

#### M4. Variants & Pathogenic Annotations (Example)

> **Synthetic Example:** Variants reported: None (expression/fusion-centric dataset; no variant calls or germline data). Molecular subtypes: Implicit subtypes based on fusion status (EWSR1-FLI1 vs. EWSR1-ERG); no formal subtype classification. Pathogenic annotations: Not included.

---

#### I1. Data Quality Issues (Example)

> **Synthetic Example:** Known issues: (i) Expression-fusion independence: Driver fusion assignment is independent of expression profiles (unrealistic; real data shows fusion-driven transcriptional programs). (ii) Clinical data simplification: Outcomes simulated from distributions, not fitted to real patient data. (iii) Batch effect absence: All samples simulated from single batch (real studies often have technical batch effects). (iv) No isoform annotation: Gene-level counts only; isoform diversity not captured.

---

#### I2. Generalizability & Applicability (Example)

> **Synthetic Example:** Cohort scope: Simulated pediatric Ewing sarcoma (age range 1–40 years); not representative of adult-onset Ewing (rare). Demographic bias: Gender balanced; race/ethnicity not simulated. Fusion composition: Multi-fusion (70% EWSR1-FLI1, 20% EWSR1-ERG); mirrors epidemiology well. Selection bias: Simulated data may not capture true disease heterogeneity or treatment response mechanisms. Generalizability: Results NOT generalizable to real Ewing biology; use only for template validation and training.

---

#### I3. Re-identification & Privacy Risks (Example)

> **Synthetic Example:** Residual risks: NONE. Data is entirely synthetic; no real individuals or privacy concerns. Use without restriction from a privacy perspective.

---

#### I4. Ethical Considerations (Example)

> **Synthetic Example:** Ethical considerations: None specific to synthetic data. If using this example to train contributors or validate pipelines, remind users that real datasets require strict adherence to ethics, consent, and privacy principles (e.g., parts C1, C3, I3 of this template must be completed thoroughly for real data).

---

#### L1. Dataset Relationships (Example)

> **Synthetic Example:** - **Canonical version**: None (entirely synthetic, no source dataset). - **Mirrors**: None. - **Derived works**: None. - **Supersedes**: None. - **Superseded by**: None.

---

#### Canonical Metadata Record (Example)

```json
{
  "id": "synthetic:ewing-ew-001",
  "title": "Synthetic Ewing Sarcoma Gene Expression and Fusion Annotation Cohort (Demonstration)",
  "accession": "zenodo-synthetic-ewing-v1",
  "repository": "Ewing Sarcoma Open Data Catalog (https://github.com/Hee-Lee-Oss/ewing-open-data-catalog-template-002)",
  "submitterOrConsortium": "Ewing Sarcoma Open Data Catalog Team",
  "accessTier": {
    "tier": "open",
    "evidenceUrl": "https://github.com/Hee-Lee-Oss/ewing-open-data-catalog-template-002/blob/main/docs/datasheet-template.md"
  },
  "license": {
    "id": "CC-BY-4.0",
    "url": "https://creativecommons.org/licenses/by/4.0/legalcode",
    "permitsDerivatives": true,
    "snapshotRef": "2026-07-24",
    "dataUseConditions": "Attribute source: 'Ewing Sarcoma Open Data Catalog Synthetic Example, CC-BY-4.0 (2026)'. No additional restrictions; derivative works permitted."
  },
  "provenance": {
    "retrievedAt": "2026-07-24T12:00:00Z",
    "version": "v1.0-synthetic",
    "publicationPmidDoi": "N/A — synthetic dataset; not published in peer-reviewed literature",
    "consortiumPolicyUrl": "https://github.com/Hee-Lee-Oss/ewing-open-data-catalog-template-002/blob/main/README.md",
    "attribution": "Ewing Sarcoma Open Data Catalog Synthetic Example Dataset. Generated 2026-06-15 using splatter R package (Zappia et al., Genome Biol. 2017). CC-BY-4.0."
  },
  "reidentification": {
    "riskLevel": "low",
    "basis": "Entirely synthetic data; no real individuals. Simulated sample identifiers (SYN_EW_001–050) have no linkage to real data. Clinical metadata simulated from epidemiological distributions; not sourced from real patient records.",
    "smallCellsFlag": false,
    "germlinePresent": false,
    "notes": "No privacy concerns. Synthetic data intended for training and template validation only."
  },
  "molecular": {
    "tumorType": "Ewing sarcoma (synthetic)",
    "driverFusion": "Mixed (EWSR1-FLI1 70%, EWSR1-ERG 20%, ambiguous 10%)",
    "assay": "Simulated RNA-seq (Illumina TruSeq 2×100bp, 50M reads simulated)",
    "cohortSizeAggregate": 50,
    "sourcePublication": "N/A — synthetic dataset; not published"
  },
  "fields": [
    {
      "name": "sample_id",
      "type": "string",
      "units": null,
      "allowedValues": null,
      "nullable": false,
      "description": "De-identified synthetic sample identifier",
      "caveats": "Format SYN_EW_001–050; simulated identifiers with no link to real data"
    },
    {
      "name": "gene_symbol",
      "type": "string",
      "units": null,
      "allowedValues": null,
      "nullable": false,
      "description": "HGNC gene symbol",
      "caveats": "Top 20,000 genes by variance; non-coding genes excluded"
    },
    {
      "name": "expression_log2_tpm",
      "type": "float",
      "units": "log2(TPM + 0.1)",
      "allowedValues": null,
      "nullable": true,
      "description": "Gene expression level (log2-transformed TPM)",
      "caveats": "Zero-inflated (30% zeros); missing values represent genes with zero reads across samples"
    },
    {
      "name": "driver_fusion",
      "type": "string",
      "units": null,
      "allowedValues": ["EWSR1-FLI1", "EWSR1-ERG", "ambiguous"],
      "nullable": false,
      "description": "Simulated driver fusion assignment",
      "caveats": "Randomly assigned independent of expression profile (unrealistic; for template demonstration only)"
    },
    {
      "name": "age_at_diagnosis_years",
      "type": "integer",
      "units": "years",
      "allowedValues": null,
      "nullable": false,
      "description": "Simulated patient age at Ewing sarcoma diagnosis",
      "caveats": "Sampled from distribution mimicking pediatric Ewing epidemiology (μ=18, range 1–40)"
    },
    {
      "name": "primary_tumor_site",
      "type": "string",
      "units": null,
      "allowedValues": ["long_bone", "pelvis", "soft_tissue", "other"],
      "nullable": false,
      "description": "Simulated primary tumor anatomic site",
      "caveats": "Categorical; distribution: 60% long bone, 25% pelvis, 10% soft tissue, 5% other"
    },
    {
      "name": "metastases_at_diagnosis",
      "type": "string",
      "units": null,
      "allowedValues": ["present", "absent"],
      "nullable": true,
      "description": "Simulated metastatic status at time of diagnosis",
      "caveats": "N/A for 2 samples (missing data); distribution 30% present, 70% absent"
    },
    {
      "name": "event_free_survival_months",
      "type": "float",
      "units": "months",
      "allowedValues": null,
      "nullable": true,
      "description": "Time to relapse, progression, or last follow-up",
      "caveats": "20% censored (no event); sampled from Weibull distribution"
    },
    {
      "name": "overall_survival_months",
      "type": "float",
      "units": "months",
      "allowedValues": null,
      "nullable": true,
      "description": "Time to death or last follow-up",
      "caveats": "15% censored (alive at end of follow-up); sampled from Weibull distribution"
    }
  ],
  "knownIssues": [
    "Simulated data does not capture real biological complexity or gene-fusion interactions.",
    "Driver fusion assignment is independent of expression profiles (unrealistic; real data shows fusion-driven transcriptional programs).",
    "Clinical outcomes simulated from epidemiological parameters, not fitted to real patient data.",
    "No batch effect present (single synthetic batch; real studies often have technical variation).",
    "Age, site, and metastatic status generated independently (real data shows disease-biology associations)."
  ],
  "lineage": {
    "duplicateOf": null,
    "supersedes": []
  },
  "examples": [
    {
      "description": "This record itself is a worked example of the datasheet template.",
      "uri": "docs/datasheet-template.md#example-synthetic-ewing-sarcoma-cohort"
    }
  ],
  "specVersions": {
    "canonicalMetadataModel": "1.0",
    "croissantML": null,
    "geoApi": null,
    "cbioportalApi": null,
    "gdcApi": null,
    "icgcApi": null
  },
  "completenessScore": {
    "before": 100,
    "after": 100
  },
  "disclaimer": "This record is research metadata only. It is not medical advice, clinical data, or intended for clinical use. Interpretation or application of any dataset information for patient care, clinical decision-making, or medical diagnosis requires qualified professional review. Ewing sarcoma is a rare, life-threatening tumor; no dataset summary should substitute for consultation with qualified oncology professionals and institutional review boards. This example is a SYNTHETIC DATASET created for demonstration and template validation; do not use for biological discovery or clinical application."
}
```

---

## Completion Guide & Troubleshooting

### Before You Submit

**Question: How do I know if my dataset is eligible for this catalog?**
- Dataset must have **open-access tier** (freely available, no DUA or ethics approval required)
- License must **permit derivatives** (CC-BY-4.0, CC0-1.0, MIT, Apache-2.0, etc. accepted; non-commercial and custom licenses require review)
- Dataset must **relate to Ewing sarcoma** (primary or significant subset)
- **Germline variants at individual level** automatically excluded
- If cohort **k < 5**, dataset is flagged for high re-identification risk and requires additional justification

**Question: What if my dataset has controlled access (dbGaP, EGA, etc.)?**
Answer: Controlled-access datasets are EXCLUDED from this catalog per policy. Focus on public/open-access datasets.

**Question: How do I fill in Part 11 (Canonical Metadata Record)?**
1. Start with the blank template provided (lines 597–658)
2. Use the worked example (lines 838–992) as a reference for structure and format
3. Match the JSON structure exactly; omit fields only if truly not applicable (set to `null`)
4. Validate JSON syntax before submitting (use online validator or `python -m json.tool`)

**Question: What's the difference between this Markdown template and the JSON record?**
Answer: Markdown (this file) is human-readable documentation; JSON (Part 11) is machine-readable metadata. Both must be completed and consistent.

**Question: How do I assess re-identification risk?**
Use this flowchart:
```
Is germline data at individual level included?
  → YES: riskLevel = "excluded" [REJECT]
  → NO: Continue...

Is cohort size k < 5?
  → YES: riskLevel = "high", smallCellsFlag = true [FLAG for review]
  → NO: Continue...

Is cohort size 5 ≤ k < 50 (or rare disease with phenotype linkage)?
  → YES: riskLevel = "moderate", smallCellsFlag = true [CAUTION; release with documentation]
  → NO: Continue...

Is cohort k ≥ 50 or data is aggregate/summary only?
  → YES: riskLevel = "low", smallCellsFlag = false [PREFERRED]
```

### Validation Checklist Before Gate Review

- [ ] All 10 major parts completed (A1–A3, B1–B4, C1–C3, D1–D2, E1–E2, F1–F2, G1–G2, M1–M4, I1–I4, L1)
- [ ] JSON in Part 11 is syntactically valid (no quote/bracket mismatches)
- [ ] No "N/A" values except where explicitly noted as acceptable (e.g., `publicationPmidDoi: "N/A"` is OK)
- [ ] All URLs in `evidenceUrl`, `consortiumPolicyUrl`, and examples are resolvable (test with browser)
- [ ] Re-identification risk level justified with specific cohort details (not generic language)
- [ ] Disclaimer includes exact phrase: "research metadata only — not medical advice"
- [ ] License is CC-BY-4.0, CC0-1.0, or otherwise permits derivatives
- [ ] Completeness score `.after` ≥ 90 (target: 95+)
- [ ] Example/worked section clearly labeled as synthetic or public (not real patient identifiers)
- [ ] Molecular section confirms Ewing sarcoma relevance (tumorType, driverFusion, assay populated)

### Common Issues & Fixes

| Issue | Solution |
|-------|----------|
| "URL doesn't resolve" | Use the canonical source URL (e.g., GEO record page, not a temporary mirror). Test with `curl -I` or browser. |
| "JSON syntax error" | Paste JSON into https://jsonlint.com/ to identify quote/bracket issues. |
| "Cohort size vs. smallCellsFlag mismatch" | If k < 5, `smallCellsFlag` MUST be `true`. If k ≥ 5, `smallCellsFlag` MUST be `false`. Mismatch = REJECT. |
| "License not recognized" | Use SPDX license ID (https://spdx.org/licenses/) if available. If custom, write full name and link to license text. |
| "Disclaimer text wrong" | Copy the exact disclaimer from `canonical-metadata-model.md` section "disclaimer" field. |
| "Fields table incomplete" | Every column (name, type, units, allowedValues, nullable, description, caveats) must be filled. If N/A, write "null" or "N/A — reason". |

---

## Reference: Ewing Sarcoma Context

**Why this catalog exists:**
Ewing sarcoma (ES) is a rare, aggressive pediatric bone tumor driven by chromosome translocations (e.g., t(11;22) EWSR1-FLI1). Survival has improved to ~70% 5-year event-free survival in high-income countries, but prognosis remains poor, especially for metastatic cases and adults. Open-access genomic data (RNA-seq, exome, WGS) enables:
- Identification of fusion-specific transcriptional drivers
- Discovery of therapeutic vulnerabilities
- Cross-cohort outcome prediction
- International collaboration on rare-disease biology

This catalog centralizes metadata for publicly available ES datasets to accelerate research and reduce redundancy.

**Key Ewing driver fusions:**
- **EWSR1-FLI1** (~85%): t(11;22)(q24;q12)
- **EWSR1-ERG** (~10%): t(21;22)(q22;q12)
- **Rare fusions** (~5%): EWSR1-E1AF, EWSR1-ZSG, others

**Re-identification risk in rare diseases:**
Ewing sarcoma (~500 new cases/year in U.S.) is rare enough that combination of fusion status + age + primary site + outcome may enable re-identification via cross-reference with published literature, disease registries, or institutional records. Caution is advised in phenotype-genotype correlation studies.

---

## Submission & Next Steps

1. **Complete all sections** (A1–A3, B1–B4, C1–C3, D1–D2, E1–E2, F1–F2, G1–G2, M1–M4, I1–I4, L1) for your dataset.
2. **Fill in the canonical metadata JSON** at the end of Part 11 with your dataset's information.
3. **Validate** the JSON against the canonical metadata model specification (`docs/canonical-metadata-model.md`).
4. **Run through the Validation Checklist** (above) and confirm all items pass.
5. **Submit** this completed Markdown file or the JSON record via pull request to the repository.
6. **Gate review:** Catalog team will verify access tier, license, re-identification risk, completeness score, and URL resolution before publishing. Expect 5–10 business day turnaround.

---

**Template License:** CC-BY-4.0  
**Specification Version:** 1.0  
**Last Updated:** 2026-07-24

*For questions or feedback on this template, please open a GitHub issue or pull request in the Ewing Sarcoma Open Data Catalog repository.*

**Conformance Note:** This template and all completed datasheets MUST satisfy the acceptance criteria defined in `.hee-lee-oss/TASK.md` and validate against `docs/canonical-metadata-model.md` before publication.
