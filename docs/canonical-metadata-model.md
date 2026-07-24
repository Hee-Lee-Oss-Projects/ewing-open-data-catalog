# Canonical Metadata Model: Ewing Sarcoma Open Data Catalog

**Disclaimer:** This document describes metadata specifications for research purposes only. Metadata contained herein is research metadata only — not medical advice. Use or interpretation of dataset information for clinical decision-making requires qualified professional review.

**License:** CC-BY-4.0  
**Specification Version:** 1.0  
**Last Updated:** 2026-07-24  
**Status:** Research metadata specification (requestor: TO BE SECURED)

---

## Overview

This document defines the canonical metadata model for the Ewing Sarcoma Open Data Catalog. Every dataset documented in the catalog must include metadata fields specified here, ensuring structural compatibility, license clarity, access-control verification, and re-identification risk assessment. The model prioritizes:

1. **Verifiable Access Tiers** — Every dataset explicitly declares open vs. controlled access with evidence URL
2. **License Transparency** — Derivatives clause must be parseable from the license terms
3. **Re-identification Safety** — Rare-disease cohort size and germline presence flagged
4. **Molecular Provenance** — Ewing-specific annotations (driver fusions, tumor type, assay)
5. **Audit Trail** — Version, retrieval date, and source publication recorded for every record

---

## Field Specification

### Identity & Access

#### `id` (required)
**Type:** String (UUID or repository-unique identifier)  
**Description:** Machine-readable unique identifier for the dataset within the catalog. If the dataset has a public accession (GEO, cBioPortal, ICGC), prefer that; otherwise mint a local UUID.  
**Example:** `GEO:GSE24221`, `icgc:EWT-AU`, `catalog:ewing-ccle-001`  
**Validation:** Must be unique across the catalog; no whitespace.

#### `title` (required)
**Type:** String  
**Description:** Human-readable title of the dataset as it appears in the source repository, or a clear descriptive title if the source has none.  
**Example:** `"Ewing Sarcoma RNA-seq Cohort: Children's Oncology Group"`, `"EWSR1-FLI1 Fusion Variants, ICGC ARGO"`  
**Validation:** ≤250 characters; no HTML tags.

#### `accession` (required)
**Type:** String  
**Description:** Public repository accession code (GEO, cBioPortal study ID, ICGC project code, Zenodo record ID, etc.).  
**Example:** `GSE24221`, `mskcc-10001`, `EWT-AU`, `zenodo.5000001`  
**Validation:** Must resolve to the source repository; cite repository base URL in `provenance.consortiumPolicyUrl`.

#### `repository` (required)
**Type:** String  
**Description:** Name and base URL of the source repository.  
**Example:** `"NCBI GEO (https://www.ncbi.nlm.nih.gov/geo/)"`, `"cBioPortal (https://www.cbioportal.org/)"`  
**Validation:** Must include both repository name and base URL.

#### `submitterOrConsortium` (required)
**Type:** String  
**Description:** Author(s), institution, or consortium that created, submitted, or curated the dataset.  
**Example:** `"Children's Oncology Group (COG)"`, `"Treehouse Childhood Cancer Project"`, `"ICGC ARGO Consortium"`  
**Validation:** ≤500 characters; if multiple authors, comma-separated.

---

### Access Control

#### `accessTier` (required)
**Type:** Object  
**Description:** Declares whether the dataset is openly available or controlled-access. Controlled-access datasets (dbGaP, EGA, DACO, TARGET DUA) are excluded from the catalog.

**Properties:**

- **`tier`** (required): Enum `"open"` | `"controlled"`
  - `"open"` — Data is freely downloadable or API-accessible without registration/approval
  - `"controlled"` — Data requires data use agreement, ethics approval, or access committee review (EXCLUDED from catalog)
  
- **`evidenceUrl`** (required): String (URL)
  - Hyperlink to the page or document proving the declared access tier (e.g., GEO record page, cBioPortal study page, repository's open-data statement)
  - Example: `"https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE24221#data"`

**Example:**
```json
{
  "tier": "open",
  "evidenceUrl": "https://www.cbioportal.org/study/summary?id=mskcc-10001"
}
```

**Validation:** `tier` must be one of the two values above; `evidenceUrl` must be a resolvable HTTP(S) URL.

---

### Legal & Terms

#### `license` (required)
**Type:** Object  
**Description:** License terms governing the dataset. Must permit re-use and derivative creation; non-commercial or custom licenses are flagged.

**Properties:**

- **`id`** (required): String (SPDX identifier or name)
  - SPDX license ID if available (e.g., `"CC-BY-4.0"`, `"MIT"`, `"CC0-1.0"`)
  - If non-standard, use a short descriptive name (e.g., `"Custom DUA"`, `"COSMIC Non-Commercial"`)
  
- **`url`** (required): String (URL)
  - Direct link to the license text or data use agreement terms
  - Example: `"https://creativecommons.org/licenses/by/4.0/legalcode"`

- **`permitsDerivatives`** (required): Boolean
  - `true` if the license explicitly allows derivative works or reuse in research
  - `false` if license forbids modifications or limits reuse (e.g., non-commercial restrictions)
  - If unclear or missing, set to `false` and flag for review

- **`snapshotRef`** (required): String  
  - Version, date, or commit hash of the exact license document retrieved
  - Protects against retroactive license changes
  - Example: `"2026-07-24 snapshot"`, `"version 4.0"`, `"CC-BY-4.0 dated 2013-12-16"`

- **`dataUseConditions`** (required): String  
  - Plain-text summary of restrictions (if any), consent requirements, or special terms (e.g., attribution clause, publication embargo, disease-specific restrictions)
  - If unrestricted, write `"No additional restrictions. Attribute to source."`
  - Example: `"Must cite source; germline variant publication requires consent review."`

**Example:**
```json
{
  "id": "CC-BY-4.0",
  "url": "https://creativecommons.org/licenses/by/4.0/legalcode",
  "permitsDerivatives": true,
  "snapshotRef": "2026-07-24",
  "dataUseConditions": "Must attribute source and date of retrieval. Subset extraction permitted."
}
```

**Validation:** `permitsDerivatives` is boolean; `url` must be resolvable; `id` must be recognized or justify custom value; `dataUseConditions` must be non-empty.

---

### Provenance & Versioning

#### `provenance` (required)
**Type:** Object  
**Description:** Tracks the source, version, and retrieval context of the dataset.

**Properties:**

- **`retrievedAt`** (required): String (ISO 8601 datetime)
  - Timestamp when dataset metadata was last inspected and verified
  - Example: `"2026-07-20T14:32:00Z"`
  - Validation: Must be in UTC/ISO 8601 format

- **`version`** (required): String  
  - Version or release date of the dataset as declared by the source repository
  - Example: `"v2.3"`, `"2024-06-15"`, `"GEO Release 20260720"`
  - Validation: Must match or cite source repo's version scheme

- **`publicationPmidDoi`** (required): String  
  - PubMed ID (PMID) or DOI of the primary publication describing the dataset, if available
  - If no primary publication, write `"N/A — primary citation not available"` or `"Zenodo DOI: 10.5281/zenodo.XXXXXX"`
  - Example: `"PMID: 29438695"`, `"DOI: 10.1016/j.cell.2019.01.003"`
  - Validation: PMID format = `PMID: [0-9]+`; DOI format = `DOI: 10.[0-9]+/...`

- **`consortiumPolicyUrl`** (required): String (URL)  
  - Link to the data source's or data provider's open-data policy, terms of use, or public metadata schema documentation
  - Example: `"https://www.ncbi.nlm.nih.gov/books/NBK25501/` (GEO API docs), `"https://docs.cbioportal.org/reference-implementation/rest-api/"`
  - Validation: Must be a resolvable HTTP(S) URL

- **`attribution`** (required): String  
  - Recommended citation format or attribution statement as provided by the source
  - Example: `"St. Jude Cloud: Cite as 'St. Jude Children's Research Hospital' and DOI: 10.21203/rs.3.protocols/rs-1234567"`
  - Validation: Non-empty string; should match source repo's recommended citation

**Example:**
```json
{
  "retrievedAt": "2026-07-20T14:32:00Z",
  "version": "v2.1",
  "publicationPmidDoi": "PMID: 29438695",
  "consortiumPolicyUrl": "https://www.ncbi.nlm.nih.gov/books/NBK25501/",
  "attribution": "Data from NCBI GEO. Cite as: GEO Study GSE24221, submitted 2013."
}
```

**Validation:** `retrievedAt` is ISO 8601 UTC; `version` is non-empty; `publicationPmidDoi` follows PMID or DOI format (or "N/A"); `consortiumPolicyUrl` is resolvable; `attribution` is non-empty.

---

### Re-identification Risk Assessment

#### `reidentification` (required)
**Type:** Object  
**Description:** Flags the re-identification risk and presence of germline or small-cohort factors. Germline-variant-level data and cohorts with k < 5 are excluded or flagged.

**Properties:**

- **`riskLevel`** (required): Enum `"excluded"` | `"high"` | `"moderate"` | `"low"`
  - `"excluded"` — Dataset contains germline variants or individual genotypes at single-nucleotide level (EXCLUDED from catalog)
  - `"high"` — Cohort size k < 5 or variant-level somatic genotypes linked to individuals (FLAGGED for review)
  - `"moderate"` — Cohort size 5 ≤ k < 50 or rare disease with phenotype details (documented; released with caution)
  - `"low"` — Cohort size k ≥ 50 or aggregate/summary data only; individual-level clinical data redacted (preferred)

- **`basis`** (required): String  
  - Plain-text explanation of how the risk level was assigned. Include cohort size, data type (aggregate vs individual), and any rare-disease or genomic factors.
  - Example: `"Somatic fusion annotation only (no germline); n=47 samples. Ewing sarcoma rare disease; linkage risk flagged for phenotype+fusion records."`
  - Validation: Must reference specific cohort characteristics, not generic risk language.

- **`smallCellsFlag`** (required): Boolean  
  - `true` if cohort size k < 5 or if individual-level identifiers (sample IDs, clinical IDs) are publicly linked
  - `false` otherwise
  - Validation: Must align with cohort size stated in `molecular.cohortSizeAggregate`

- **`germlinePresent`** (required): Boolean  
  - `true` if dataset includes germline variant calls, inherited variants, or germline copy-number variants at individual level
  - `false` if somatic variants only, or if germline data is not provided at individual level
  - Validation: If `true`, `riskLevel` must be `"excluded"` (automatic exclusion)

- **`notes`** (required): String  
  - Additional context or caveats regarding privacy, informed consent scope, or variant interpretation
  - Example: `"Cohort consented to research use; re-contact clause present. No secondary phenotypes linked."`
  - Validation: Non-empty if risk level is "excluded" or "high"; may be empty if "low" with no caveats.

**Example:**
```json
{
  "riskLevel": "moderate",
  "basis": "Somatic fusion + RNA-seq counts (n=47 patients). Ewing sarcoma (rare disease; k < 50). Phenotype linked to fusion genotype in supplementary table; individual samples not named.",
  "smallCellsFlag": true,
  "germlinePresent": false,
  "notes": "Informed consent covers research use and publication. De-identification completed; sample metadata includes age at diagnosis and primary tumor site only."
}
```

**Validation:** `riskLevel` must be one of the four values; `germlinePresent: true` forces `riskLevel: "excluded"`; `smallCellsFlag: true` if cohort size < 5; `basis` and `notes` are non-empty strings.

---

### Molecular Metadata (Ewing Sarcoma Specific)

#### `molecular` (required)
**Type:** Object  
**Description:** Captures tumor-type, fusion gene, and assay-specific annotations for Ewing sarcoma datasets.

**Properties:**

- **`tumorType`** (required): String  
  - Must be `"Ewing sarcoma"` or a recognized Ewing subtype (e.g., `"Ewing sarcoma (EWSR1-FLI1)"`). Other tumor types must note if Ewing is a subset.
  - Example: `"Ewing sarcoma"`, `"Ewing sarcoma (EWSR1-ERG)"`
  - Validation: Must reference Ewing sarcoma or explicitly state if multi-tumor and note Ewing proportion.

- **`driverFusion`** (required): String  
  - Most common driver fusion(s) in the cohort or `"Mixed"` if cohort spans multiple fusions, or `"Not reported"` if fusion status unknown.
  - Example: `"EWSR1-FLI1"`, `"EWSR1-ERG"`, `"Mixed (EWSR1-FLI1, EWSR1-ERG)"`, `"Not reported"`
  - Validation: Must be a recognized Ewing fusion or one of the reserved values.

- **`assay`** (required): String  
  - Primary genomic or transcriptomic assay (e.g., `"RNA-seq"`, `"Whole Genome Sequencing (WGS)"`, `"SNP Array"`, `"Fusion panel"`).
  - If multiple, list separated by semicolon.
  - Example: `"RNA-seq; Fusion panel"`, `"Whole Exome Sequencing (WES)"`
  - Validation: Must be a recognized assay type.

- **`cohortSizeAggregate`** (required): Integer  
  - Total number of unique individuals (samples, patients) in the cohort. For studies with repeated measurements, use unique sample count.
  - Example: `47`, `103`, `1`
  - Validation: Must be a positive integer; feeds into re-identification risk assessment.

- **`sourcePublication`** (required): String  
  - Citation or DOI of the source publication describing the dataset. If unpublished, write `"Unpublished dataset"` or cite the data repository.
  - Example: `"DOI: 10.1016/j.cell.2019.01.003"`, `"PMID: 29438695"`, `"Zenodo: 10.5281/zenodo.5000001"`
  - Validation: Must be a valid citation format or reserved value.

**Example:**
```json
{
  "tumorType": "Ewing sarcoma (EWSR1-FLI1 predominant)",
  "driverFusion": "EWSR1-FLI1",
  "assay": "RNA-seq",
  "cohortSizeAggregate": 47,
  "sourcePublication": "PMID: 29438695"
}
```

**Validation:** `tumorType` references Ewing sarcoma; `cohortSizeAggregate` aligns with `reidentification.smallCellsFlag` logic.

---

### Data Dictionary & Structural Metadata

#### `fields` (required)
**Type:** Array of Objects  
**Description:** Summary metadata for each column/field in the dataset. For aggregate or summary datasets, list the summary columns; for individual-level data, list de-identified phenotype and molecular summaries.

**Array element properties:**

- **`name`** (required): String — Column name as it appears in the dataset.
- **`type`** (required): String — Data type (e.g., `"string"`, `"integer"`, `"float"`, `"boolean"`, `"date"`).
- **`units`** (optional): String — Units of measurement if applicable (e.g., `"log2(cpm)"`, `"years"`, `"percentage"`).
- **`allowedValues`** (optional): Array of Strings — Enumerated values if the column is categorical (e.g., `["EWSR1-FLI1", "EWSR1-ERG"]`).
- **`nullable`** (required): Boolean — `true` if the field may be missing or null.
- **`description`** (required): String — Plain-text description of what the field represents.
- **`caveats`** (optional): String — Known limitations or transformation applied (e.g., `"Top 100 genes by variance"`, `"Age binned into quintiles for privacy"`).

**Example:**
```json
{
  "name": "sample_id",
  "type": "string",
  "units": null,
  "allowedValues": null,
  "nullable": false,
  "description": "De-identified sample identifier.",
  "caveats": "Linked to NCBI GEO sample record via accession field."
},
{
  "name": "driver_fusion",
  "type": "string",
  "units": null,
  "allowedValues": ["EWSR1-FLI1", "EWSR1-ERG", "FUS-ERG"],
  "nullable": false,
  "description": "Primary driver fusion in the tumor.",
  "caveats": null
},
{
  "name": "log2_fold_change",
  "type": "float",
  "units": "log2(fold change vs. normal bone)",
  "allowedValues": null,
  "nullable": true,
  "description": "Differential expression measure.",
  "caveats": "Top 500 genes; missing values indicate no differential expression detected at FDR < 0.05."
}
```

**Validation:** Each field must have `name`, `type`, `nullable`, `description`; `allowedValues` is required if type is categorical.

#### `knownIssues` (required)
**Type:** Array of Strings  
**Description:** List of known data quality issues, processing artifacts, or caveats in plain language.

**Example:**
```json
[
  "Batch effect from 2016 vs. 2019 runs; not corrected.",
  "One sample (GSM1234567) has > 50% missing values; included but flagged.",
  "Fusion status inferred from RNA-seq, not confirmed by FISH or PCR."
]
```

**Validation:** Array of non-empty strings; if no known issues, use `[]`.

#### `lineage` (required)
**Type:** Object  
**Description:** Tracks relationships to other datasets (duplicates, superseded versions, etc.).

**Properties:**

- **`duplicateOf`** (required): String or null  
  - If this dataset is a duplicate or mirror of another, cite the canonical version's `id`.
  - Example: `"GEO:GSE24221"` (if this record is a Zenodo mirror of the same data)
  - Validation: Must reference another `id` in the catalog or `null` if unique.

- **`supersedes`** (required): Array of Strings or empty  
  - If this dataset replaces or corrects an earlier version, list the `id`s of the superseded versions.
  - Example: `["GEO:GSE24221"]` if this is a corrected re-release
  - Validation: Array of `id` strings or `[]` if no supersessions.

**Example:**
```json
{
  "duplicateOf": null,
  "supersedes": []
}
```

#### `examples` (required)
**Type:** Array of Objects  
**Description:** Pointers to example records or linked-data URIs demonstrating the full metadata structure.

**Array element properties:**

- **`description`** (required): String — Brief description of the example (e.g., `"Synthetic sample record with all fields populated"`).
- **`uri`** (required): String (URL) — Link to a worked example (file, Zenodo record, or inline in datasheet).

**Example:**
```json
[
  {
    "description": "Worked example: Synthetic Ewing Cohort with all metadata fields",
    "uri": "docs/datasheet-template.md#example-synthetic-ewing-sarcoma-cohort"
  }
]
```

**Validation:** Each example must have `description` and `uri`; if no examples exist yet, use `[]`.

#### `specVersions` (required)
**Type:** Object  
**Description:** Records the specification versions used to model the dataset.

**Properties:**

- **`canonicalMetadataModel`** (required): String  
  - Version of this canonical metadata model (e.g., `"1.0"`)

- **`croissantML`** (optional): String  
  - Version of MLCommons Croissant ML schema if a Croissant JSON-LD export exists (e.g., `"1.0"`)

- **`geoApi`** (optional): String  
  - NCBI E-utilities API version used to fetch GEO metadata (if applicable)

- **`cbioportalApi`** (optional): String  
  - cBioPortal web API version if data sourced from cBioPortal

- **`gdcApi`** (optional): String  
  - NCI GDC API version if data sourced from GDC

- **`icgcApi`** (optional): String  
  - ICGC/ARGO Data Portal API version if data sourced from ICGC

**Example:**
```json
{
  "canonicalMetadataModel": "1.0",
  "croissantML": "1.0",
  "geoApi": "1.0",
  "cbioportalApi": "2.0",
  "gdcApi": null,
  "icgcApi": null
}
```

#### `completenessScore` (required)
**Type:** Object  
**Description:** Tracks metadata completeness before and after curation.

**Properties:**

- **`before`** (required): Number (0–100)  
  - Fraction of canonical fields populated in the source before curation (as percentage).
  - Example: `75` (75% of fields were already populated by source)

- **`after`** (required): Number (0–100)  
  - Fraction of canonical fields populated after curation by the catalog team (target ≥ 90).
  - Example: `95`

**Example:**
```json
{
  "before": 60,
  "after": 98
}
```

**Validation:** Both must be integers 0–100 inclusive; `after` should be ≥ 90 for published records.

#### `disclaimer` (required)
**Type:** String  
**Description:** Boilerplate research-metadata disclaimer.

**Standard value:**
```
"This record is research metadata only. It is not medical advice, clinical data, or intended for clinical use. Interpretation or application of any dataset information for patient care, clinical decision-making, or medical diagnosis requires qualified professional review. Ewing sarcoma is a rare, life-threatening tumor; no dataset summary should substitute for consultation with qualified oncology professionals and institutional review boards."
```

**Validation:** Must include the phrase "research metadata only — not medical advice" and discourage clinical misuse.

---

## Acceptance Checklist

When completing a dataset record, verify:

- [ ] All 15 required top-level fields are present and non-null (id, title, accession, repository, submitterOrConsortium, accessTier, license, provenance, reidentification, molecular, fields, knownIssues, lineage, examples, specVersions, completenessScore, disclaimer)
- [ ] `accessTier.tier` is `"open"` (controlled-access datasets are excluded)
- [ ] `license.permitsDerivatives` is `true` (non-derivative licenses are excluded)
- [ ] `reidentification.germlinePresent: false` (germline-variant data is excluded)
- [ ] `reidentification.smallCellsFlag` aligns with `molecular.cohortSizeAggregate` (k < 5 → `true`)
- [ ] `molecular.tumorType` references Ewing sarcoma
- [ ] `completenessScore.after` ≥ 90
- [ ] All hyperlinks in `evidenceUrl`, `consortiumPolicyUrl`, and examples resolve
- [ ] Disclaimer is present and includes "research metadata only — not medical advice"

---

## Changelog

**Version 1.0** (2026-07-24): Initial specification. Fields and validation rules aligned with Hee-Lee Oss Ewing Sarcoma Open Data Catalog planning document.

---

**End of Specification**

*This canonical metadata model is part of the Ewing Sarcoma Open Data Catalog initiative. For questions, pull requests, or dataset contributions, visit the project repository or contact the gate reviewer (TO BE SECURED).*
