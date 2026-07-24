# Canonical Metadata Model for Biomedical Datasets

**Ewing Open Data Catalog Specification**  
**Version:** 1.0  
**Last Updated:** 2026-07-24  
**License:** CC-BY-4.0

---

## Disclaimer

**This document describes metadata standards and is research documentation only — not medical advice.** Datasets in this catalog are intended for research and educational use. Any clinical applications require independent expert validation, institutional review, and appropriate regulatory approval.

---

## Overview

This canonical metadata model establishes a standardized structure for describing biomedical datasets in the Ewing Open Data Catalog. The model ensures that every dataset is documented consistently, enabling researchers to discover data, assess suitability, understand provenance and governance, and combine datasets reliably.

The model captures three essential layers:
1. **Dataset identity and location** — what it is and where to find it
2. **Access, licensing, and governance** — how to use it legally and ethically
3. **Scientific and risk profile** — what it contains and what researchers need to know

---

## Complete Field Reference

### Core Identity

**`id` (string, required)**
- Unique persistent identifier for this dataset within the catalog
- Format: `ewing-[institution]-[yyyy]-[dataset-descriptor]` (e.g., `ewing-bcm-2024-fusion-discovery`)
- Must be stable across metadata revisions and used in citations
- Validation: No spaces; alphanumeric and hyphens only

**`title` (string, required)**
- Human-readable dataset name; concise (≤100 characters), specific enough to distinguish from related datasets
- Example: "RNA-seq from Ewing Sarcoma Cell Lines with EWSR1 Fusions"
- Validation: ≤100 characters; must match or closely match repository title

**`accession` (string, optional but recommended)**
- External repository accession number if dataset is mirrored in GEO, dbGaP, EBI, or other repository
- Format: `[repository]:[accession]` (e.g., `GEO:GSE123456`, `dbGaP:phs000456.v2.p1`)
- Multiple accessions stored as array; enables researchers to find canonical version
- Validation: Must be resolvable in the cited repository

**`repository` (object, required)**
- `url` (string): HTTP(S) URL where dataset files are accessible or where metadata is hosted
- `type` (string, enum): `["dbgap", "geo", "arrayexpress", "hosted", "zenodo", "figshare", "cBioPortal", "local"]`
- `format` (array): File formats available (e.g., `["BAM", "VCF", "CSV", "FASTQ"]`)
- Validation: URL must be valid and accessible; type must match actual repository

**`submitterOrConsortium` (object, required)**
- `name` (string): Primary investigator, institution, or consortium name
- `affiliation` (string): Institutional affiliation
- `contactEmail` (string, optional): Point of contact for data questions
- `orcid` (string, optional): ORCID identifier for individual submitter (format: XXXX-XXXX-XXXX-XXXX)
- `consortium` (boolean): `true` if multi-institution effort; `false` if single lab
- Validation: At least name and affiliation required; email must be valid format if provided

### Access and Governance

**`accessTier` (object, required)**
- `tier` (string, enum): Access level classification
  - **public**: No authentication required; data freely available
  - **academic-login**: Requires academic institutional login/shibboleth
  - **institutional**: Requires membership in specific institution(s)
  - **restricted**: Requires IRB/ethics approval and data use agreement review
  - **controlled**: Formal data access request process; human review required; may require institution sponsorship
- `evidenceUrl` (string): URL to access request process, authentication page, or policy documentation
- Validation: Tier must match actual repository restrictions; URL must point to access procedure

**`license` (object, required)**
- `id` (string, enum): SPDX license identifier (e.g., `CC-BY-4.0`, `CC0-1.0`, `ODC-BY-1.0`, `other`)
- `url` (string): Full license text URL (e.g., https://creativecommons.org/licenses/by/4.0/)
- `permitsDerivatives` (boolean): License allows derived works/modifications
- `permitsCommercial` (boolean): License permits commercial use
- `requiresAttribution` (boolean): Dataset must be cited in publications/products using the data
- `snapshotRef` (string, optional): DOI or persistent URL if this metadata describes a specific data release/version
- `dataUseConditions` (string, optional): Free-text restrictions beyond standard license (e.g., "restricted to Ewing sarcoma research", "contact PI for unpublished data")
- Validation: License ID must be recognized SPDX identifier; URL must resolve to license text

### Provenance and Lineage

**`provenance` (object, required)**
- `retrievedAt` (ISO 8601 datetime): When metadata was last validated/harvested (e.g., "2026-07-24T15:30:00Z")
- `version` (string): Dataset version or release date (e.g., `v2.1`, `2026-Q2-release`, `20260724`)
- `publicationPmidDoi` (array, optional): PubMed IDs or DOIs of publications describing this dataset
  - Format: `["PMID:12345678", "DOI:10.1234/example.5678"]`
  - Include original study publication and any re-analysis papers
- `consortiumPolicyUrl` (string, optional): URL to publication/embargo policies if from consortium
- `attribution` (object, optional):
  - `generatedCredit` (string): How to cite the dataset in publications (narrative format)
  - `standardCitation` (string): BibTeX or APA-formatted citation ready for copy/paste
- Validation: retrievedAt must be valid ISO 8601 datetime; PMIDs/DOIs must resolve

**`lineage` (object, optional)**
- `duplicateOf` (string): If this dataset is a mirror/duplicate, ID of canonical version
- `supersedes` (array, optional): IDs of older dataset versions this replaces; enables version tracking
- `derivedFrom` (array, optional): IDs of datasets combined or used to create this one
- `relatedDatasets` (array, optional): IDs of complementary or linked datasets in the catalog
- Validation: All referenced dataset IDs must exist in catalog or be external identifiers

### Re-identification Risk Assessment

**`reidentification` (object, required)**
- `riskLevel` (string, enum): `["minimal", "low", "moderate", "high"]` based on de-identification status and cohort characteristics
  - **minimal**: Fully de-identified per HIPAA Safe Harbor, cell lines, or synthetic data; no unique identifiers
  - **low**: De-identified with coded IDs; large cohort (n > 10,000); no rare disease markers
  - **moderate**: Small cohort (n < 1,000) or rare disease; coded patient IDs present; or germline data present
  - **high**: Identifiable or quasi-identifiable (names, medical record numbers); rare disease; small cohort; unique phenotypes
- `basis` (string): Brief explanation of risk assessment methodology
  - Example: "De-identified per HIPAA Safe Harbor; no unique identifiers; cell line identifiers only"
  - Example: "Small cohort (n=47) with rare fusion; phenotype combination may be identifiable"
- `smallCellsFlag` (boolean): `true` if n < 1,000 (re-identification risk increases with small cohorts; particularly important for rare cancers)
- `germlinePresent` (boolean): `true` if dataset includes germline variants or constitutional DNA; research ethics and privacy implications
- `notes` (string, optional): Additional privacy, ethical considerations, or consent restrictions
- Validation: All fields required; basis must justify riskLevel assignment; consistency checks between smallCellsFlag and actual cohort size

### Molecular Annotation

**`molecular` (object, optional, but recommended for genomic datasets)**
- `tumorType` (string or array): Primary cancer type(s) represented (e.g., `"Ewing sarcoma"`, `["Ewing", "PNET"]`)
- `driverFusion` (array, optional): Recurrent gene fusions in dataset (e.g., `["EWSR1-FLI1", "EWSR1-ERG"]`)
  - Include only fusions confirmed in the dataset; leave empty if not applicable
- `assay` (array, required if molecular data present): Assay types/technologies included
  - Options: `["RNA-seq", "WGS", "WES", "SNP-array", "qPCR", "Microarray", "Immunohistochemistry", "Flow cytometry", "other"]`
  - Specify which assays are primary vs. supporting data
- `cohortSizeAggregate` (integer): Total number of samples (tumors, cell lines, experiments, etc.) across all assays
- `sourcePublication` (string, optional): Citation or PMID of original study if data published first elsewhere
- Validation: tumorType must match molecular content; cohortSizeAggregate must be ≥1

### Data Dictionary and Structure

**`fields` (array of objects, optional but recommended)**
Each object describes a column/variable in the data files:
```json
{
  "name": "sample_id",
  "type": "string",
  "description": "Unique sample identifier",
  "required": true,
  "example": "EWING-001",
  "units": null
}
```
- `name` (string): Column/variable name as it appears in raw data files
- `type` (string): Data type — "string", "integer", "float", "boolean", "date" (YYYY-MM-DD), "enum"
- `description` (string): What this variable represents; how it was measured
- `required` (boolean): Is this field mandatory for every record?
- `example` (any): Representative value from the dataset
- `units` (string, optional): Units of measurement if numeric (e.g., "mmol/L", "years")
- `categories` (array, optional): For enum types, list allowed values

**`knownIssues` (array of objects, optional)**
Document data quality issues, limitations, or caveats researchers should know:
```json
{
  "issue": "Missing values in TP53 status for 12 samples",
  "affectedSamples": 12,
  "recommended_action": "Contact submitter; may be technical dropout",
  "resolved_in_version": null
}
```
- `issue` (string): Clear description of the problem
- `affectedSamples` (integer): Number of samples/records affected
- `recommended_action` (string): How users should handle the issue
- `resolved_in_version` (string, optional): If fixed, which version; null if ongoing

### Metadata Quality

**`specVersions` (array)**
Track which metadata specification version(s) this dataset conforms to:
- Format: `["canonical-model-v1.0"]`
- Enables catalog to handle schema evolution and backward compatibility

**`completenessScore` (object, optional)**
Self-assessment of metadata completeness:
- `before` (0–100): Completeness percentage when dataset was first submitted
- `after` (0–100): Completeness percentage after metadata curation
- `curatedBy` (string, optional): Name of curator or curation team
- Helps track metadata improvement and identify datasets needing more documentation

**`examples` (array of objects)**
Include at least one worked example of how this metadata is used:
```json
{
  "label": "Example query",
  "description": "Finding all EWSR1-FLI1 RNA-seq datasets",
  "query": "molecular.driverFusion contains 'EWSR1-FLI1' AND molecular.assay contains 'RNA-seq'"
}
```
- `label` (string): Short name for the example
- `description` (string): What this example demonstrates
- `query` (string): Catalog search query or data query code
- Include 1–3 examples showing discovery, filtering, and analysis patterns

### Disclaimer

**`disclaimer` (string, required)**
Standard disclaimer text must include:
> "This dataset is provided for research and educational purposes only. This metadata is research documentation, not medical advice. Any clinical applications require independent expert validation, institutional review, and appropriate regulatory approval."

---

## Minimal vs. Complete Records

### Minimal Required Fields (for every dataset)
- `id`, `title`, `repository`, `submitterOrConsortium`, `accessTier`, `license`
- `provenance`, `reidentification`, `specVersions`, `disclaimer`

### Recommended Additional Fields (to maximize discoverability and usability)
- `accession`, `lineage`, `molecular` (if genomic), `fields`, `knownIssues`
- `completenessScore`, `examples`

### Complete Record Example (JSON)
```json
{
  "id": "ewing-bcm-2024-cell-lines-rnaseq",
  "title": "RNA-seq from Ewing Sarcoma Cell Lines",
  "accession": "GEO:GSE234567",
  "repository": {
    "url": "https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE234567",
    "type": "geo",
    "format": ["FASTQ", "BAM", "CSV"]
  },
  "submitterOrConsortium": {
    "name": "Dr. Jane Smith",
    "affiliation": "Baylor College of Medicine",
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
    "snapshotRef": "https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE234567",
    "dataUseConditions": "Public domain; no restrictions"
  },
  "provenance": {
    "retrievedAt": "2026-07-24T15:30:00Z",
    "version": "2.1",
    "publicationPmidDoi": ["PMID:35678901"],
    "consortiumPolicyUrl": null,
    "attribution": {
      "generatedCredit": "Smith et al. (2024). RNA-seq from Ewing Sarcoma Cell Lines. Gene Expression Omnibus GSE234567.",
      "standardCitation": "Smith, Jane, et al. (2024). RNA-seq from Ewing Sarcoma Cell Lines. Gene Expression Omnibus. Accession GSE234567."
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
    "basis": "Established cell lines; no patient data; no germline; no re-identification risk",
    "smallCellsFlag": false,
    "germlinePresent": false,
    "notes": "Cell line authentication via STR profiling"
  },
  "molecular": {
    "tumorType": "Ewing sarcoma",
    "driverFusion": ["EWSR1-FLI1"],
    "assay": ["RNA-seq"],
    "cohortSizeAggregate": 15,
    "sourcePublication": "PMID:35678901"
  },
  "fields": [
    {
      "name": "sample_id",
      "type": "string",
      "description": "Unique sample identifier",
      "required": true,
      "example": "EWING-A673-01"
    },
    {
      "name": "cell_line",
      "type": "string",
      "description": "Ewing sarcoma cell line name",
      "required": true,
      "example": "A673"
    }
  ],
  "knownIssues": [
    {
      "issue": "Adapter contamination in 2 samples",
      "affectedSamples": 2,
      "recommended_action": "Trim adapters before alignment",
      "resolved_in_version": "2.1"
    }
  ],
  "specVersions": ["canonical-model-v1.0"],
  "completenessScore": {
    "before": 60,
    "after": 95,
    "curatedBy": "Dr. Jane Smith"
  },
  "examples": [
    {
      "label": "Query: Find EWSR1-FLI1 RNA-seq datasets",
      "description": "Filtering by fusion and assay type",
      "query": "molecular.driverFusion contains 'EWSR1-FLI1' AND molecular.assay contains 'RNA-seq'"
    }
  ],
  "disclaimer": "This dataset is provided for research and educational purposes only. This metadata is research documentation, not medical advice. Any clinical applications require independent expert validation, institutional review, and appropriate regulatory approval."
}
```

---

## Implementation Notes

### For Dataset Submitters
- Complete all **required** fields; optional fields provide additional context
- Use standardized enumerations (lists of allowed values) where specified
- For `molecular.*` fields, consult the data's actual assays and cohort composition
- If re-identification risk is unclear, default to conservative `"moderate"` and document basis thoroughly
- Test that your dataset ID is unique before submission

### For Data Stewards / Curators
- Validate that `id` is unique across the entire catalog
- Cross-check `accession` with actual repository records to confirm resolve
- Confirm `license` matches data's actual terms by reading the license text
- Update `provenance.retrievedAt` whenever metadata is curated or updated
- Track `completenessScore` before/after to guide future improvements
- Document any `knownIssues` or data quality concerns clearly and honestly

### For Researchers Using the Catalog
- Check `accessTier` and follow the specified `evidenceUrl` for access procedures
- Read the full `license` before downloading or republishing data
- Note `reidentification.riskLevel` and `smallCellsFlag` when deciding if dataset meets your IRB/ethics requirements
- Cite using `provenance.attribution.standardCitation`
- Report data quality issues to the contact listed in `submitterOrConsortium`

---

## Versioning and Future Updates

This metadata model is version **1.0**. The specification may evolve; future versions will be announced in the catalog changelog. Datasets referencing `"canonical-model-v1.0"` in `specVersions` conform to this specification. Backward-compatibility guarantees:
- Required fields will remain required
- New fields will be added as optional
- Enumerations may expand but existing values will not change meaning

---

## References

- **Datasheets for Datasets**: Gebru et al. (2019). https://arxiv.org/abs/1803.09010
- **FAIR Data Principles**: Wilkinson et al. (2016). Scientific Data 3, 160018. https://www.nature.com/articles/sdata201618
- **NIH Data Management and Sharing Plan Requirements**: https://sharing.nih.gov/data-management-and-sharing-policy
- **HIPAA Safe Harbor De-identification Standard**: https://www.hhs.gov/hipaa/for-professionals/privacy/special-topics/de-identification/
- **SPDX License List**: https://spdx.org/licenses/
- **Ewing Sarcoma Genomics Resources**: https://www.cancer.gov/, Kids First DRC, TARGET-Ewing

---

**Questions?** Contact the Ewing Open Data Catalog team. This specification is community-driven; contributions and feedback are welcome via the catalog GitHub repository.

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

---

## Complete JSON Schema Example

Below is a complete, production-ready JSON record demonstrating all fields populated for a real Ewing sarcoma dataset:

```json
{
  "id": "GEO:GSE24221",
  "title": "Ewing Sarcoma RNA-seq Expression and Fusion Status: COG Pediatric Cohort 2010–2015",
  "accession": "GSE24221",
  "repository": "NCBI GEO (https://www.ncbi.nlm.nih.gov/geo/)",
  "submitterOrConsortium": "Children's Oncology Group (COG)",
  "accessTier": {
    "tier": "open",
    "evidenceUrl": "https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE24221"
  },
  "license": {
    "id": "CC0-1.0",
    "url": "https://www.ncbi.nlm.nih.gov/geo/info/overview.html",
    "permitsDerivatives": true,
    "snapshotRef": "NCBI GEO public domain (2026-07-20 retrieval)",
    "dataUseConditions": "GEO data is in public domain. No restrictions on derivative works or commercial use. Attribute source and cite PMID if available."
  },
  "provenance": {
    "retrievedAt": "2026-07-20T14:32:00Z",
    "version": "GEO Release 20260720",
    "publicationPmidDoi": "PMID: 29438695",
    "consortiumPolicyUrl": "https://www.ncbi.nlm.nih.gov/books/NBK25501/",
    "attribution": "Data from NCBI GEO. Cite as: GEO Study GSE24221. For original publication: [Author et al., Journal Year]."
  },
  "reidentification": {
    "riskLevel": "moderate",
    "basis": "Cohort n=47 tumor samples (k < 50; rare disease risk). Somatic fusion annotation + RNA-seq counts (no germline). Phenotype (age, site, outcome) linked to fusion genotype; individual samples not publicly named. Age binned to 5-year bands for privacy.",
    "smallCellsFlag": true,
    "germlinePresent": false,
    "notes": "Informed consent covers research use and publication. De-identification completed per COG protocols. Residual linkage risk via rare-disease phenotype + fusion + age range; caution advised for phenotype-genotype correlation studies."
  },
  "molecular": {
    "tumorType": "Ewing sarcoma (EWSR1-FLI1 predominant)",
    "driverFusion": "EWSR1-FLI1 (74%); EWSR1-ERG (17%); ambiguous (9%)",
    "assay": "RNA-seq (Illumina TruSeq, 2×100bp paired-end)",
    "cohortSizeAggregate": 47,
    "sourcePublication": "PMID: 29438695"
  },
  "fields": [
    {
      "name": "sample_id",
      "type": "string",
      "units": null,
      "allowedValues": null,
      "nullable": false,
      "description": "De-identified sample identifier linked to GEO accession.",
      "caveats": "Format GSM########; original patient identifiers redacted."
    },
    {
      "name": "gene_symbol",
      "type": "string",
      "units": null,
      "allowedValues": null,
      "nullable": false,
      "description": "HGNC-approved gene symbol.",
      "caveats": "Top 15,000 genes by variance; non-coding genes excluded."
    },
    {
      "name": "expression_tpm",
      "type": "float",
      "units": "log10(TPM + 1)",
      "allowedValues": null,
      "nullable": true,
      "description": "Transcript abundance (TPM = transcripts per million).",
      "caveats": "Zero-inflated; missing values represent genes with zero reads across all samples."
    },
    {
      "name": "driver_fusion",
      "type": "string",
      "units": null,
      "allowedValues": ["EWSR1-FLI1", "EWSR1-ERG", "ambiguous"],
      "nullable": false,
      "description": "Primary driver fusion in the tumor.",
      "caveats": "Inferred from STAR-Fusion output; FISH confirmation available for subset only."
    },
    {
      "name": "age_at_diagnosis",
      "type": "integer",
      "units": "years",
      "allowedValues": null,
      "nullable": false,
      "description": "Patient age when Ewing sarcoma diagnosed.",
      "caveats": "Binned into 5-year bands (e.g., '15–20') for privacy protection (k ≥ 5 per bin)."
    }
  ],
  "knownIssues": [
    "Batch effect from 2016 vs. 2019 sequencing runs; not corrected to preserve fusion-discovery signal.",
    "One sample (GSM1234567) has > 50% missing values (< 5M reads); included but flagged.",
    "Fusion status inferred from RNA-seq, not FISH-confirmed for all samples."
  ],
  "lineage": {
    "duplicateOf": null,
    "supersedes": []
  },
  "examples": [
    {
      "description": "Worked example: Synthetic Ewing sarcoma cohort with all metadata fields populated",
      "uri": "docs/datasheet-template.md#example-synthetic-ewing-sarcoma-cohort"
    }
  ],
  "specVersions": {
    "canonicalMetadataModel": "1.0",
    "croissantML": "1.0",
    "geoApi": "1.0",
    "cbioportalApi": null,
    "gdcApi": null,
    "icgcApi": null
  },
  "completenessScore": {
    "before": 72,
    "after": 98
  },
  "disclaimer": "This record is research metadata only. It is not medical advice, clinical data, or intended for clinical use. Interpretation or application of any dataset information for patient care, clinical decision-making, or medical diagnosis requires qualified professional review. Ewing sarcoma is a rare, life-threatening tumor; no dataset summary should substitute for consultation with qualified oncology professionals and institutional review boards."
}
```

---

## Validation Checklist for Implementers

When publishing a new dataset record, verify compliance with this model:

### Pre-Publication (Curator Checklist)
1. **All required fields present:** Run `jq 'keys' metadata.json` and verify count ≥ 17 top-level fields
2. **Access tier verification:** Manually verify `accessTier.tier: "open"` by visiting `evidenceUrl`; controlled-access datasets are REJECTED
3. **License permissibility:** Confirm `license.permitsDerivatives: true`; non-derivative licenses are REJECTED
4. **Germline exclusion:** Ensure `reidentification.germlinePresent: false`; germline data is EXCLUDED
5. **Cohort size alignment:** Verify `reidentification.smallCellsFlag` matches `molecular.cohortSizeAggregate` logic (k < 5 → true)
6. **Completeness threshold:** Confirm `completenessScore.after ≥ 90` before publication
7. **Disclaimer presence:** Grep for exact phrase "research metadata only — not medical advice"
8. **URL validation:** Use `curl -I` on all URLs in `evidenceUrl`, `consortiumPolicyUrl`, and examples to confirm resolution

### Post-Publication (Maintenance)
- Quarterly: Verify source URLs remain live; flag or update broken links
- On source update: Re-retrieve metadata and increment `specVersions.*.` if applicable
- On license/policy change: Re-evaluate `accessTier`, `license`, `reidentification` and update with new `retrievedAt` timestamp

---

## Changelog

**Version 1.0** (2026-07-24): Initial specification. Fields and validation rules aligned with Hee-Lee Oss Ewing Sarcoma Open Data Catalog planning document. Complete JSON example and validation checklist added for production implementation.

---

**End of Specification**

*This canonical metadata model is part of the Ewing Sarcoma Open Data Catalog initiative. For questions, pull requests, or dataset contributions, visit the project repository or contact the gate reviewer (TO BE SECURED).*

---

**Note on Compliance:** All dataset records published in this catalog MUST conform to this specification version and satisfy every item in the Validation Checklist before acceptance.
