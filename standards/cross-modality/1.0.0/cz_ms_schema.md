# Chan Zuckerberg Biohub Mass Spectrometry Platform Schema

Contact: [carlos.gonzalez@czbiohub.org](mailto:carlos.gonzalez@czbiohub.org)

Document Status: *Draft*

Version: 1.0.0

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED" "MAY", and "OPTIONAL" in this document are to be interpreted as described in [BCP 14](https://tools.ietf.org/html/bcp14), [RFC2119](https://www.rfc-editor.org/rfc/rfc2119.txt), and [RFC8174](https://www.rfc-editor.org/rfc/rfc8174.txt) when, and only when, they appear in all capitals, as shown here.

## Schema versioning

The Chan Zuckerberg Biohub Mass Spectrometry Platform (CZB-MS) schema version is based on [Semantic Versioning](https://semver.org/).

**Major version** is incremented when schema updates are incompatible with the [MAGE-TAB Proteomics SDRF](https://github.com/bigbio/proteomics-sample-metadata) (**SDRF**) encodings or incompatible with current pipeline components. Examples include:

* Renaming metadata fields  
* Deprecating metadata fields  
* Changing the type or format of a metadata field  
* Loss of metadata fields from mass spectrometer data output  
* Significant loss in metadata fields previously reported by processing software (e.g., FragPipe, DIA-NN, MaxQuant) due to changes to their schemas  
* Changes to schemas of input objects such as FASTA file encodings

**Minor version** is incremented when schema updates may require changes only to the CZB-MS metadata acquisition systems (BS3, BulkLoader). Examples include:

* Additions to SDRF metadata fields  
* Updating pinned ontologies or gene references  
* Changing the validation requirements for a metadata field  
* Changes to the source of metadata (e.g., source1 \-\> source2 or the inverse)

**Patch version** is incremented for editorial updates and when adding organisms that do not require new metadata fields.

All changes are documented in the schema [Changelog](https://docs.google.com/document/d/1QDtqwKMZoZqkZ6Zi_vy4E2Dr_dpEJOSMyuwkgaOW1zQ/edit#appendix-a-changelog).

## Background

CZB-MS aims to support the consistent generation, sharing, and exploration of mass spectrometry data across the Biohub Network (**BHN**) and beyond. In keeping with this goal, we seek to unify all aspects of data collection, storage, feature annotation, and pre-processing efforts across BHN mass spectrometry sites.

In order to accomplish these goals, all mass spectrometer sites across BHN are **REQUIRED** to record metadata about samples, experiments, and projects acquired on BHN mass spectrometers. This document describes the schema, a type of contract and blueprint, that CZB-MS requires all datasets to adhere to so that it will **enable findability** and **downstream integration of datasets** into analyses and models.

## Overview

This schema supports multiple levels of metadata including **sample, experiment, and project**. Each level records various aspects of metadata pertinent to understanding a data set and its larger context within a corpus of data.

This document is organized into two sections: **mass spectrometry-specific metadata** and **sample/experiment/project focused metadata** and has the following sections

* [Definitions](#definitions): defines terms for greater document clarity  
* [Ontologies](#ontologies): defines the ontologies used to describe data  
* [Mass spectrometer-specific files](#mass-spectrometer-specific-files): description of files used for the purposes of mass spectrometry data acquisition and spectral searching (e.g., search engines)  
* [Sample-level metadata](#sample-level-metadata): description of categories collected for each sample, includes cross-modality mapping.  
* [Experiment- and project-level metadata](#experiment--and-project-level-metadata): description of categories collected for a group of experiments and samples  
* Post-search output tables: description of files generated post spectral alignment

## Additional Important Notes

**Redundant Metadata**. It is RECOMMENDED to avoid multiple metadata fields containing identical or similar information.However, for the purposes of the SDRF this is often unavoidable as sample characteristics are often also experimental factors (for example, characteristic[treatment] is both a sample property and an experimental factor). Additionally, while the original SDRF allowed for columns with the same characteristics term, the CZB-MS subset of SDRF MUST NOT have multiple columns with the same characteristics. Instead, we RECOMMEND the use of distinguishing terms derived from any of the ontology sources listed below.

**No Personal Identifiable Information (PII)**. This is not strictly enforced by validation because it is difficult for software to predict what is and is not PII; however, curators MUST agree to the data acquisition policies of CZB-MS which includes the requirement to remove [direct personal identifiers](https://docs.google.com/document/d/1sboOmbafvMh3VYjK1-3MAUt0I13UUJfkQseq8ANLPl8/edit) of study subjects in metadata.

**A note on types.** The types below are python3 types. Note that a python3 `str` is a sequence of Unicode code points, which is stored as UTF-8-encoded tab/comma-separated files.

## Definitions

**Sample-level metadata**. This refers to tabular metadata that describes a specific mass spectrometry sample. It is recorded in the [SDRF format](https://github.com/bigbio/proteomics-sample-metadata) derived by the Human Proteome Organization’s Proteomic Standards Initiative working group.

**Experiment-level metadata**. This refers to metadata that records information about a specific experiment, which is defined as a group of samples. This is recorded using a tabular format described below.

**Project-level metadata**. This refers to metadata that records information about a specific project, which is defined as a group of experiments all aimed at a broader scientific goal. This is recorded using a tabular format described below.

## Ontologies

Ontologies used for mass spectrometry data are pinned for this version/release data of the schema:

| Ontology | OBO Prefix | Version/Release | Download |
| :---- | :---- | :---- | :---- |
| [Experimental Factor Ontology](https://www.ebi.ac.uk/ols4/ontologies/efo) | EFO | [2025-04-15](https://github.com/EBISPOT/efo/releases/tag/v3.77.0) | [efo.owl](https://github.com/EBISPOT/efo/releases/download/v3.77.0/efo.owl) |
| [Cell Ontology](https://obofoundry.org/ontology/cl.html) | CL | [2025-04-10](https://github.com/obophenotype/cell-ontology/releases/tag/v2025-04-10) | [cl.owl](https://github.com/obophenotype/cell-ontology/releases/download/v2025-04-10/cl.owl) |
| [NCBI Organismal Classification](https://obofoundry.org/ontology/ncbitaxon.html) | NCBITaxon | [2025-03-13](https://github.com/obophenotype/ncbitaxon/releases/tag/v2025-03-13) | [ncbitaxon.owl](https://github.com/obophenotype/ncbitaxon/releases/download/v2025-03-13/ncbitaxon.owl) |
| [Uberon anatomy ontology](https://obofoundry.org/ontology/uberon.html) | UBERON | [2025-04-09](https://github.com/obophenotype/uberon/releases/tag/v2025-04-09) | [uberon.owl](https://github.com/obophenotype/uberon/releases/download/v2025-04-09/uberon.owl) |
| [NCI Thesaurus OBO Edition](https://obofoundry.org/ontology/ncit.html) | NCIT | [2024-05-07](https://github.com/NCI-Thesaurus/thesaurus-obo-edition/releases/tag/v2024-05-07) | [ncit.owl](https://github.com/NCI-Thesaurus/thesaurus-obo-edition/releases/download/v2024-05-07/ncit.owl) |
| [MS](https://obofoundry.org/ontology/ms.html) | MS | [4.1.191](https://github.com/HUPO-PSI/psi-ms-CV/releases/tag/v4.1.191) | [ms.owl](https://github.com/HUPO-PSI/psi-ms-CV/releases/download/v4.1.191/ms.owl) |
| [Mondo Disease Ontology](https://obofoundry.org/ontology/mondo.html) | MONDO | [2025-04-01](https://github.com/monarch-initiative/mondo/releases/tag/v2025-04-01) | [mondo.owl](https://github.com/monarch-initiative/mondo/releases/download/v2025-04-01/mondo.owl) |
| [PRIDE](https://github.com/PRIDE-Archive/pride-ontology) | PRIDE | [2025-02-17](https://github.com/PRIDE-Archive/pride-ontology/releases/tag/v2025-02-17) | [Zip file](https://github.com/PRIDE-Archive/pride-ontology/archive/refs/tags/v2025-02-17.zip) |
| [Phenotype And Trait Ontology](https://obofoundry.org/ontology/pato.html) | PATO | [2025-02-01](https://github.com/pato-ontology/pato/releases/tag/v2025-02-01) | [Zip file](https://github.com/pato-ontology/pato/archive/refs/tags/v2025-02-01.zip) |
| [Human Ancestry Ontology](https://obofoundry.org/ontology/hancestro.html) | HANCESTRO | [2025-04-01](https://github.com/EBISPOT/hancestro/releases/tag/v2025-04-01) | [Zip file](https://github.com/EBISPOT/hancestro/archive/refs/tags/v2025-04-01.zip) |
| [Human Developmental Stages](https://obofoundry.org/ontology/hsapdv.html) | HsapDV | [2025-01-23](https://github.com/obophenotype/developmental-stage-ontologies/releases/tag/v2025-01-23) | [hsapdv.owl](https://github.com/obophenotype/developmental-stage-ontologies/releases/download/v2025-01-23/hsapdv.owl) |
| [Mouse Developmental Stages](https://obofoundry.org/ontology/mmusdv.html) | MmusDv | [2025-01-23](https://github.com/obophenotype/developmental-stage-ontologies/releases/tag/v2025-01-23) | [mmusdv.owl](https://github.com/obophenotype/developmental-stage-ontologies/releases/download/v2025-01-23/mmusdv.owl) |
| [Zebrafish Anatomy Ontology](https://obofoundry.org/ontology/zfa.html) | ZFA | [2025-01-28](https://github.com/ZFIN/zebrafish-anatomical-ontology/releases/tag/v2025-01-28) | [Zip file](https://github.com/ZFIN/zebrafish-anatomical-ontology/archive/refs/tags/v2025-01-28.zip) |
| [Zebrafish Developmental Stages Ontology](https://www.ebi.ac.uk/ols4/ontologies/zfs) | ZFS | [2020-3-10](https://www.ebi.ac.uk/ols4/ontologies/zfs) | [zfs.owl](http://purl.obolibrary.org/obo/zfs/releases/2020-03-10/zfs.owl) |
| [C. elegans Development Ontology](https://obofoundry.org/ontology/wbls.html) | WBLS | [2025-04-01](https://github.com/obophenotype/c-elegans-development-ontology/releases/tag/v2025-04-01) | [wbls.owl](http://purl.obolibrary.org/obo/wbls/releases/2025-04-01/wbls.owl) |
| [C. elegans Gross Anatomy Ontology](https://obofoundry.org/ontology/wbbt.html) | WBbt | [2025-03-26](https://github.com/obophenotype/c-elegans-gross-anatomy-ontology/releases/tag/v2025-03-26) | [wbbt.owl](http://purl.obolibrary.org/obo/wbbt/releases/2025-03-26/wbbt.owl) |
| [Drosophila Anatomy Ontology](https://obofoundry.org/ontology/fbbt.html) | FBBT | [2025-03-27](https://github.com/FlyBase/drosophila-anatomy-developmental-ontology/releases/tag/v2025-03-27) | [fbbt.owl](https://github.com/FlyBase/drosophila-anatomy-developmental-ontology/releases/download/v2025-03-27/fbbt.owl) |
| [Drosophila Development Ontology](https://obofoundry.org/ontology/fbdv.html) | FBdv | [2025-03-26](https://github.com/FlyBase/drosophila-developmental-ontology/releases/tag/v2025-03-26) | [fbbd.owl](https://github.com/FlyBase/drosophila-developmental-ontology/releases/download/v2025-03-26/fbdv.owl) |

## Cross-modality mapping

This refers specifically to how ontology terms from tables/fields defined in this sample-level metadata table below map to [cross-modality ontology schema](https://docs.google.com/document/d/10PfruMm_OmJaBdLvxVfk_gKzfnW3N7q4QBkCfInfCSY/edit?usp=sharing). 

| CZB-MS | CZI Crossmodal | Matching Ontology? |
| :---- | :---- | :---- |
| commnent[technology type] | assay | Yes (EFO) |
| factor value[technology_type_id] | assay_ontology_term_id | Yes (EFO) |
| characteristics[disease] | disease | Yes (MONDO, PATO) |
| factor value[disease_ontology_term_id] | disease_ontology_term_id | Yes (MONDO, PATO) |
| characteristics[organism] | organism | Yes (NCBITaxon) |
| factor value[organism_ontology_term_id]  | organism_ontology_term_id | Yes (NCBITaxon) |
| characteristics[developmental_stage] | development_stage | Yes(HsapDV, MmusDv, ZFS,  WBLS, FBDV) |
| factor value[developmental_stage_ontology_term_id] | development_stage_ontology_term_id | Yes (HsapDV, MmusDv, ZFS,  WBLS, FBDV) |
| characteristics[organism part] | tissue | Yes (UBERON, ZFA, FBbt, WBbt) |
| factor value[organism_part_ontology_term_id] | tissue_ontology_term_id | Yes (UBERON, ZFA, FBbt, WBbt) |
| factor value[tissue_class] | tissue_type | Yes (NA) |

## Mass spectrometer-specific files

Mass spectrometers use several file types as inputs to processing pipelines, which range from protein sequences files (.FASTA files) to workflows and parameter files. Below are the specifications for files that may have an impact on downstream analyses.

### FASTA files

FASTA are files plain-text readable files analogous to genome files for sequencing, containing a standardized header and a protein sequence (amino acid sequence) which allow the assignment of collected spectra to peptides and proteins. For CZB-MS, we STRONGLY RECOMMEND that all FASTA files follow the standard Uniprot format. Doing so allows for extensive tool development and failing to adhere to these standards will limit analysis options. To understand this format better, we provide the following example FASTA entry:  
```
>sp|P05067|A4_HUMAN Amyloid-beta precursor protein OS=Homo sapiens OX=9606 GN=APP PE=1 SV=3  
MLPGLALLLLAAWTARALEVPTDGNAGLLAEPQIAMFCGRLNMHMNVQNGKWDSDPSGTK   
EFVSDALLVPDKCKFLHQERMDVCETHLHWHTVAKETCSEKST…(truncated)  
```
* **\>**: Indicates the beginning of a FASTA header line.  
* **sp**: Source database.  
* **P05067**: This is the **UniProt accession number**  
* **A4_HUMAN**: The **UniProt entry name**, also known as the mnemonic.  
* **Amyloid-beta precursor protein**: The full name of the protein.  
* **OS=Homo sapiens**: Organism Species name.  
* **OX=9606**: Organism taxonomy identifier.  
* **GN=APP**: Gene Name.  
* **PE=1**: Protein Existence evidence level.  
* **SV=3**: Sequence Version.

This format is present in all FASTA files downloaded from Uniprot.org and is **STRONGLY RECOMMENDED**. To accommodate custom FASTA we have developed the following system to record FASTA file names:

#### Standard (“Base”) FASTA filename conventions:

* Ensures consistent searches across common organisms across CZB-MS.  
* Serves as a common base for concatenated FASTA files.  
* Focuses on single species.  
* Format: DownloadDate_source_TaxonName_additionalAttributes_standard.fasta  
  * “AdditionalAttributes” can be expanded using dashes to include extra information.  
  * Each section uses camelCase (e.g., HomoSapiens).  
  * The scientific taxon name will be used as the primary source identifier  
  * Date should be formatted using ISO8601 standards (YYYYMMDD).  
  * **Examples:**
    ```
    20240727_uniprot_HomoSapiens_Swissprot_standard.fasta  
    20240624_uniprot_DanioRerio_Swissprot-Trembl_standard.fasta
    ```

#### Custom FASTA filename conventions:

* Provides flexibility in searching sequences, with the added benefit of being concatenated from a common sequence source.  
* Sequestered to a custom folder to be reusable without intermingling with standard sequences.  
* Date corresponding to file creation date.  
* Sections use dashes to include additional data sources.  
* Custom files may have relevant information appended to the “AdditionalAttributes” section, such as custom sequences, concatenated versions of standard FASTA files, or a combination thereof.  
* Format: CreationDate_sourceTaxa_additionalAttributes_custom.fasta  
  * As before, “AdditionalAttributes” can be extended by using dashes.  
  * Date should be formatted using ISO8601 standards (YYYYMMDD).  
  * **Examples:**
    ```
    20240730_uniprot-Cov2Sequencing_HomoSapiens-COV2_CowContam-rev-unrev_custom.fasta  
    20240520_refseq-wgc_HomoSapiens-Cohort34_TLG34_custom.fasta
    ```

#### Spectral Libraries - Proteomics

Spectra libraries MUST be formatted in a similar manner to those of custom FASTA files. Since proteomic spectral libraries are sourced from standard FASTA files, this file MUST be referenced via a combination of the source acronym and species name.
Acceptable source acronyms are:

* UP = Uniprot  
* RS = RefSeq

Alternatively, the FASTA database indexID can be used:

* Formats:  
  * Date_FastaID_taxa_AdditionalInfo_custom.tsv or .speclib  
  * Date_sources_taxa_AdditionalInfo_custom.tsv or .speclib  
  * Date should be formatted using ISO8601 standards (YYYYMMDD).  
  * **Examples:**
    ```
    20240345_23-43-45_HomoSapiens-EscherichiaColi-DanioRerio_SISO003_custom.tsv  
    20240523_UP-UP_DanioRerio-KlebsiellaPneumoniae_SIFA002_custom.speclib
    ```

#### Spectral Libraries - Metabolomics

Metabolites have little to no species specificity and thus do not require species-specific spectral libraries. CZB-MS metabolite spectral libraries come from local and global sources.

* Local metabolite spectra: Spectra collected from authentic standards using conserved chromatography (e.g., Biohub-HILIC or Biohub-C18), allowing the highest confidence annotations by matching retention time, MS1, and MS2 spectra.   
* Global metabolite spectra: generated from external sources without known retention times, resulting in lower confidence annotations. See [metabolomics standards initiative publications (2007, 2014)](https://link.springer.com/article/10.1007/s11306-007-0070-6) for more details.  
  * These files MUST adhere to the following convention: ModeLibrary_Chromatography_VersionDate.msp  
  * **Example:**
    ```
    negMSP_HILIC_Oct2023.msp
    ```

#### Spectral Libraries - Lipidomics

Spectral libraries for lipidomics are IBM2 (.ibm2) files embedded in the MS-Dial version used. They are date- and time-stamped at the time of processing. Formatting MUST adhere to the following convention: year_month_day_hour_minute_second_Loaded.msp2

**Example:**
```
2024_8_5_14_14_20_Loaded.msp2
```

## Sample-level Metadata

Sample-level metadata is defined as a CSV file containing the sample-specific characteristics for each file in an experiment. The schema used here is the Proteomics-optimized Sample-Data-Relationship Format ([SDRF](https://github.com/bigbio/proteomics-sample-metadata)), created by the Human Proteome Organization’s Proteomic Standards Initiative working group to serve as a common platform to store sample-level metadata. It can be explored at the link above, here we will give the pertinent details. It is broken down into three distinct sections:

### Sample Characteristics (characteristics[attribute])

Sample characteristics refer to the intrinsic properties of a sample such as its origin, cell type, species origin, etc. Each header column beyond ‘source name’ is formatted in the following manner: characteristics[attribute]. It is **REQUIRED** to contain the following characteristics at a minimum:

| Column | Description | Constraints and Comments |
| :---- | :---- | :---- |
| source name | Name restricted to a single source sample. Can be entered in multiple rows due to fractions and technical replicates. | - String<br> - Free text<br> - Auto-generated by MS platform<br> - **Example:** “sample_1” |
| characteristics[organism] | NCBI-derived taxonomy term | - String<br> - **NCBITaxon derived label**<br> - Free text fall back label accepted but discouraged by UI<br> - Submitter MUST annotate Other accepted values: ‘not available’ and ‘not applicable’<br> - **Example:** Homo sapiens |
| characteristics[disease] | MONDO derived disease term | - String<br> **MONDO- and PATO-derived label**, Submitter MUST annotate, Other accepted values: ‘healthy’ (PATO), ‘normal’ (PATO), ‘not available’ and ‘not applicable’<br> - **Example:** cancer |
| characteristics[development_stage] | Refers to discrete organismal developmental stage | - String <br> - **Derived label from one of the following ontologies** (depending on organism selected): HsapDV, MmusDv, ZFS, WBls, FBbv |
| charactersitics[tissue type] | Refers to CZI-specific tissue type term | - String<br> - **CZB-SF specific label**<br> - Acceptable values: ‘tissue’, ‘organoid’, and ‘cell culture’ |
| characteristics[organism part] | Refers to source organ or tissue, as noted by UBERON ontology. In the case of cell lines, refer to the original tissue type. | - String<br> - **UBERON derived label**<br> - Free text fall back<br> - Submitter MUST annotate<br> - Other accepted values: ‘not available’ and ‘not applicable’<br> - **Example:** colon |
| characteristics[cell type] | Refers to the ‘type’ of ontology-driven cell (e.g., columnar, cuboidal, epithelial etc.) | - String<br> - **CL derived label**<br> - Free text fall back<br> - Submitter MUST annotate<br> - Other accepted values: ‘not available’ and ‘not applicable’<br> - **Example:** transitional epithelial cell |
| characteristics[biological replicate] | Refers to the biological replicate. | - String<br> - Free text<br> - Submitter MUST annotate<br> - **Example:** Replicate 1 |

### Data File Characteristics (comment[attribute])

Data file characteristics refer to technical properties of the sample, often reflecting file names, sample processing agents, and spectral searching parameters. Data file characteristics are formatted in the following manner: comment[attribute].  It is **REQUIRED** to contain the following characteristics at a minimum:

| Column | Description | Constraints and Comments |
| :--- | :--- | :--- |
| assay name | Unique run identifier applied by CZB-MS pipeline.  | - String<br> - Free text incrementor<br> - Auto-generated by MS platform<br> - **Example**: run1 |
| comment[fraction identifier] | Fraction number for a corresponding entry in ‘source name’ | - Numeric<br> - Submitter MUST annotate<br> - **Example:** 1 |
| comment[label] | Refers to a sample’s labeling strategies such as isobaric labeling, SILAC, ITRAQ, etc. Non-labeled samples are also included in this category | - String<br> - **PRIDE derived label**<br> - STRONGLY RECOMMENDED to be auto-generated by platform<br> - **Example:** “AC=MS:1002038;NT=label free sample”, “TMT126” |
| comment[data file] | Name of data file generated by CZB-MS pipeline  | - String<br> - Generated by platform<br> - **Example:** 20170424_Lumos_shotgun_TMT1_global_Fr9.raw |
| comment[instrument] | Name of instrument the sample was captured on | - String<br> - **MS derived label**<br> - Other accepted values: ‘not available’, ‘not applicable’, ‘unknown’<br> - **Example:** “Orbitrap Fusion Lumos” |
| technology type | Refers to ontology terms used that describe the assay technology | - String<br> - **EFO derived label AND non-standrd supported terms**<br> - Supported value: ‘proteomic profiling by mass spectrometry’, metabolomic profiling by mass spectrometry’, lipidomic profiling by mass spectrometry’<br> - Issue currently [open](https://github.com/EBISPOT/efo/issues/2383) on EFO to add the latter two terms |

### Experimental factors (factor value[attribute])

Experimental factor values refer to categories of metadata dealing with experimental variables and are the target for downstream analyses. Under normal circumstances, factor values are directly duplicated from characteristics[attribute] columns designated by the experimentalist (for example characteristics[disease] is equvalent to the experimental groups factor value[disease]). Experimental factors are formatted as **factor value[attribute]**. Experimental factors *by design* do not follow any ontologies other than what they inherit from characteristics. However, we have co-opted factor values to store additional ontology term ID information in order to adhere to CZ-wide cross-modality requirements and thus the following factors are REQUIRED:

| Column | Description | Constraints and Comments |
| :---- | :---- | :---- |
| factor value[assay_ontology_term_id] | comment[technology type] label’s associated ontology term ID OR duplicate label | - String<br> - EFO or MS derived term ID<br> - Submitter MUST annotate |
| factor value[development_stage_ontology_term_id]  | characteristics[developmental stage] associated ontology term ID | - String<br> - **Derived term ID from one of the following ontologies**: HsapDV, MmusDv, ZFS, WBls, FBbv |
| factor value[disease_ontology_term_id] | characteristics[disease] associated ontology term ID | - String<br> - MONDO or PATO derived term ID |
| factor value[organism_ontology_term_id] | characteristics[organism] related term ID |- String<br> - NCBITaxon derived term ID |
| factor value[tissue_ontology_term_id] | characteristics[tissue type] referencing or cellular compartment | - String<br> - UBERON or CL derived term ID |

### CZB MS Platform Specific Categories

In addition to the standard metadata categories (characteristics, comment, and factor value) we append additional, non-SDRF-validatable columns that record information critical to running the mass spectrometers, but are not included in SDRFs recorded in the forthcoming Biobhub Metadata Portal (e.g., they are removed from outputs). These are labeled BL[term]

| Column | Constraints and Comments |
| :---- | :---- |
| BL[sample_description] | - String<br> - Optional<br> - Appended by submitter  |
| BL[preparation description]  | - String<br> - Optional<br> - Appended by submitter  |
| BL[fraction description] | - String<br> - Optional<br> - Appended by submitter  |
| BL[notes] | - String<br> - Optional<br> - Appended by submitter  |
| BL[vessel format] | - String<br> - Optional<br> - Appended by submitter  |
| BL[form] | - String<br> - Optional<br> - Appended by submitter  |
| BL[quantity submitted] | - Numeric<br> - Optional<br> - Appended by submitter  |
| BL[unit] |  - String<br> - Optional<br> - Appended by submitter  |
| BL[plate id] |  - String<br> - Optional<br> - Appended by submitter   |
| BL[well position] |  - String<br> - Optional<br> - Appended by submitter    |
| BL[injection volume] |  - Numeric<br> - Optional<br> - Appended by submitter    |
| BL[experiment alias] |  - String<br> - Optional<br> - Appended by submitter   |
| BL[method file] | - String<br> - Appended by platform personnel  |
| BL[fasta] | - String<br> - Appended by platform personnel  |
| BL[workflow] | - String<br> - Appended by platform personnel  |

### Optional categorical variables (all)

While the above list is limited to the REQUIRED categories, the SDRF is by design extensible to the degree necessary within the limits of the SDRF documentation. Below is a list of other commonly seen metadata categories observed by CZB-SF, along with associated ontologies used. “NA” is noted if the category is not from an ontology.

| Category | Commonly seen attribute |
| :---- | :---- |
| characteristics (ontology source, if any) | developmental stage (TBD), sex (**PATO**), age, ancestry category (**HANCESTRO**), cell line (**CL**), enrichment process (**EFO**), individual (NA), material type (NA) |
| comment (ontology source, if any) | technical replicate (NA), modification parameters (NA), precursor mass tolerance (NA), fragment mass tolerance (NA), collision energy (NA), file uri (NA), fractionation method (**PRIDE**), cleavage agents (**PRIDE**), dissociation method (NA), proteomics data acquisition method (**PRIDE**) |

### Post-translational modifications and cleavage agents

Modifications and cleavage agents are often automatically added by the search engine (e.g., FragPipe) to a technical-focused SDRF, which is appended to the sample-focused SDRF generated by the CZB-MS. They are written as strings in the following convention:
```
“NT=Glu→pyro-Glu; MT=fixed; PP=Anywhere;AC=Unimod:27; TA=E”.
```
An extensive explanation of these is beyond the scope of this document but can be read about [here](https://github.com/bigbio/proteomics-sample-metadata/blob/master/sdrf-proteomics/README.adoc#104-additional-data-files-technical-properties).

### Augmentations for Metabolomics and Lipidomics 

Currently SDRF tables are officially defined for proteomics. However, their structure can un-officially accommodate additional omics types such as metabolomics and lipidomics, with some minor additions and modifications. The benefit is we have a unified format for all mass spectrometry data as opposed to fragmentation (no pun intended). To this end, we will also record metabolomics data using the SDRF with the following additions

| Column | Constraints and Comments |
| :---- | :---- |
| technology type | - String<br> - **NCIT derived label**<br> - Supported values: ‘Metabolomics’ and ‘Lipidomics’ |
| comment[polarity] | - String<br> - Supported values: “positive” and “negative” |
| comment[chromatography type] | - String<br> - **PRIDE derived label**<br> - **Example**: hydrophilic interaction chromatography |
| comment[extraction protocol] | - String<br> - Free text<br> - Future: will reference [Protocols.io](http://Protocols.io) DOI<br> - **Example:** methanol crash protocol |

## Experiment- and Project-level Metadata

Project-level metadata is focused on assigning attributes to a *group* of related (by the project goal) experiments and their associated assays. This file will also be output as a tab-separated table. 

| Column | Description | Constraints and Comments |
| :---- | :---- | :---- |
| project[identifier] | Project Identifier assigned by CZB Metadata Portal | - String<br> - Platform assigned at time of submission to Metadata Portal |
| project[Title] | Title of project given by user at Metadata Portal | - String <br> - Submitter MUST provide |
| project[description] | Description of experiment given by user at Metadata Portal | - String<br> - Submitter MUST provide |
| experiment[Identifier] | Experiment Identifier assigned by CZB Metadata Portal. Can be used to link to multimodal projects | - String<br> - Platform assigned at time of experiment submission to Metadata Portal |
| experiment[title] | Title of experiment given by user at Metadata Portal | - String<br> - Submitter MUST provide |
| experiment[description] | Description of experiment given by user at Metadata Portal | - String<br> - Submitter MUST provide |
| assay[identifier] | Identifier of data set | - String<br> - Platform assigned at time of submission to BS3 |
| assay[measurement type] | Type of technology used to profile samples | - String<br> - TBD where this is assigned<br> - Accepted terms: “proteomic profiling by mass spectrometry” “metabolomic profiling by mass spectrometry” and “lipidomic profiling by mass spectrometry” |
| assay[technology platform] | Name of mass spectrometer acquiring data for experiment as assigned by MS ontology | - String<br> - **MS- OR EFO-driven ontology label**<br> - Platform assigned |
| assay[Experiment Protocol] | TBD in version 2.0 | - TBD in version 2.0 |
| assay[sdrf table] | Name of SDRF metadata table | - String<br> - Platform generated |
| assay[raw data] | Location of raw files in cloud of local cluster (e.g., Bruno hpc) | - String<br> - Platform generated |
| assay[processed data] | Location of processed tables in cloud of local cluster (e.g., Bruno hpc) | - String<br> - Platform generated |

## Proteomics post-search output tables

Post-search refers to the various tables generated after spectral data has been acquired and subjected to spectral matching via software/algorithms. For the purposes of this document, when referring to CZB-MS proteomics this is specifically identifying the following standardized tables generated from [FragPipe v.22](https://github.com/Nesvilab/FragPipe/releases/tag/22.0) that will be recorded for all proteomic experiments:

* Data dependent acquisition (DDA) tables  
  * [Peptide-spectral matching (PSM) tables](https://fragpipe.nesvilab.org/docs/tutorial_fragpipe_outputs.html#combined_iontsv) (external reference)  
  * [Peptide quantification tables](https://fragpipe.nesvilab.org/docs/tutorial_fragpipe_outputs.html#combined_peptidetsv) (external reference)  
  * [Protein quantification tables](https://fragpipe.nesvilab.org/docs/tutorial_fragpipe_outputs.html#combined_proteintsv) (external reference)  
  * [MSstats](https://www.bioconductor.org/packages/release/bioc/html/MSstats.html)-processed outputs  
* Data independent acquisition (DIA, using DIANN module included in FragPipe) tables  
  * [Main outputs](https://github.com/vdemichev/DiaNN?tab=readme-ov-file#main-output-reference) (external reference)  
  * [MSstats](https://www.bioconductor.org/packages/release/bioc/html/MSstats.html)-processed outputs

### DDA and DIA MSstats output tables

Equivalent tables are output for DDA and DIA.  While MSstats outputs several tables, we will highlight the tables delivered that are likely to be of most interest for analyses and model ingestion.

#### Peptide quantification table

Refers to a **long-form table** that contains peptide quantification data output by MSstats (post-filtering).  
File name: `MSstats_peptide_feature_data.csv`

| Column | Description |
| :---- | :---- |
| PROTEIN | - String<br> - Parsed FASTA file header (e.g., sp|P61981|1433G_HUMAN)<br> - CZB-MS pipeline assigned |
| PEPTIDE | - String<br> - Peptide (peptide + mods + charge, example: AAWEEPSSGN[0.9840]GTAR_2)  |
| TRANSITION | - String<br> - Transitions assigned by MSstats |
| FEATURE | - String<br> - Unique concatenated peptide + mods + charge + transitions |
| LABEL | - String<br> - Refers to isotope label |
| GROUP | - String<br> - Experimental grouping assigned CZB-MS<br> - Assigned Derived from user input metadata<br> - **Example:** LP117SpikeMcherryCargo |
| RUN | - Integer<br> - Unique run ID for individual raw file<br> - MSstats assigned |
| SUBJECT | - Integer<br> - Replicate ID |
| FRACTION | - Integer<br> - Fraction ID |
| originalRUN | - String<br> - Sample file name<br> - Platform assigned |
| censored | - Boolean<br> - Refers to censored status for the purposes of imputation processing (e.g., left-censored data) |
| INTENSITY | - Numeric or NA<br> - Pre-correction quantification value |
| ABUNDANCE | - Numeric or NA<br> - Log2-transformed INTENSITY value |
| newABUNDANCE | - Numeric Original or imputed log2 abundance |
| predicted | - Numeric Predicted value for imputation |
| feature_quality | - String<br> - Refers to features ability to inform protein quantification<br> - Accepted values: ‘Informative’ or ‘Uninformative’ |
| is_outlier | - Boolean<br> - Refers to feature quantification outlier status assigned during data processing |

#### Protein quantification table

Refers to a protein x sample wide-format protein abundance table derived from ‘peptide \-\> protein roll up’ by MSstats (feature summing). The ‘Protein’ column contains the protein and other columns represent samples with values represented log2(intensity). **NA values are present.**  
File name: `Msstats_wide.csv`

#### Sample metadata

Refers to the sample metadata used to process MSstats data and downstream CZB-MS efforts including all CZB-MAP outputs  
File name: `MSstats_metadata.csv`

| Column | Description |
| :---- | :---- |
| File | - String<br> - Refers to file name<br> - May not match original file if fractions were present, look for “_merged” appendage |
| Rep | - Integer<br> - Refers to biological replicate ID |
| Condition | - String<br> - Experimental group sample is associated with |
| short_id | - String<br> Shortened identifier for graphs and tables Proxy for unique group \+ replicate sample |
| wide_id | - String<br> - Deprecated |
| Timepoint | - Integer<br> - Time series identifier |

## Appendix A. Changelog

### schema v1.0.0

Initial approved schema

* "must", "should", and select other words have a defined, standard meaning.  

