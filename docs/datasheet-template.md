# Datasheet Template: Ewing Sarcoma Dataset Documentation

**Disclaimer:** This document template provides metadata specifications for research purposes only. Metadata and dataset information contained herein is research metadata only — not medical advice. Use or interpretation of dataset information for clinical decision-making requires qualified professional review.

**License:** CC-BY-4.0  
**Template Version:** 1.0  
**Last Updated:** 2026-07-24

---

## Instructions for Contributors

This template guides documentation of Ewing sarcoma datasets for the Ewing Sarcoma Open Data Catalog. Use it to complete a **datasheet** — a structured set of questions about your dataset's provenance, composition, consent, limitations, and intended uses.

**What this is:** A documentation template describing dataset metadata, provenance, and known limitations.  
**What this is NOT:** A data submission form. Data is not submitted here; only metadata, pointers to data, and access information.

**Before starting:**
1. Identify the dataset you're documenting (GEO series, cBioPortal study, Zenodo record, etc.)
2. Have access to the original source documentation (paper, README, repository)
3. Answer every question below; if truly not applicable, write "N/A — reason"
4. Submit the completed datasheet as a Markdown file to the catalog PR

**Output License:** This datasheet is licensed CC-BY-4.0. You may reuse and adapt it for other datasets.

---

## Part 1: Motivation & Purpose (Datasheets-for-Datasets Part A)

### A1. Motivation & Dataset Curation

**Question:** Why was this dataset created or curated? What problem does it solve or what question does it address?

**Guidance:** Reference the original study, author intent, or consortium mission. For re-published datasets (e.g., GEO hosted, cBioPortal integrated), note the original purpose and the rationale for including it in the Ewing catalog.

**Example Response:**
> This dataset compiles RNA-seq from 47 Ewing sarcoma tumors treated at Children's Oncology Group sites 2010–2015. The original study (PMID: 29438695) identified EWSR1-FLI1-specific transcriptional signatures associated with prognosis. The dataset is included in the Ewing catalog as a reference transcriptome for fusion-positive Ewing sarcomas and to enable cross-cohort survival and molecular outcome studies.

**Your Response:**
```
[Provide motivation and curation rationale here]
```

---

### A2. Composition & Instances

**Question:** What data does the dataset contain (individuals, samples, records) and how many?

**Guidance:** Specify the number of unique patients/individuals, samples, observations, or records. For multi-source datasets, itemize by source.

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
