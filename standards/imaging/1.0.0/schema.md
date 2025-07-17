# Imaging Schema

Contact: mcaton@chanzuckerberg.com and utz.ermel@czii.org

Document Status: _Draft_

Version: 1.0.0

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED" "MAY", and "OPTIONAL" in this document are to be interpreted as described in [BCP 14](https://tools.ietf.org/html/bcp14), [RFC2119](https://www.rfc-editor.org/rfc/rfc2119.txt), and [RFC8174](https://www.rfc-editor.org/rfc/rfc8174.txt) when, and only when, they appear in all capitals, as shown here.

## Schema versioning

The cross modality schema version is based on [Semantic Versioning](https://semver.org/).

**Major version** is incremented when incompatiable schema updates are introduced:
  * Renaming metadata fields
  * Deprecating metadata fields
  * Changing the type or format of a metadata field
 
**Minor version** is incremented when additive schema updates are introduced:
  * Adding metadata fields
  * Changing the validation requirements for a metadata field
  
**Patch version** is incremented for editorial updates.

All changes are documented in the schema [Changelog](#appendix-a-changelog).

## Background
Across the CZI network, we aim to standardize imaging data and metadata for ease of sharing, management, and downstream model training. Inline with this goal, we have outlined how the Dynamic Cell Atlas and the CryoET Portal implement the REQUIRED cross-modality schema. Given the variety of data formats and experimental metadata, we will continue to add to this set of requirments in the imaging working group. This document serves as a working draft and set of minimal standards. 

## Overview

This document is organized into two sections: cross-modality mapping for Dynamic Cell Atlas and cross-modality mapping for the CryoET portal.

## Ontologies

These are the ontologies used.

With the exception of Cellosaurus, ontology terms for metadata MUST use [OBO-format identifiers](http://www.obofoundry.org/id-policy.html), meaning a CURIE (prefixed identifier) of the form **Ontology:Identifier**. For example, [EFO:0000001](https://www.ebi.ac.uk/ols4/ontologies/efo/classes?obo_id=EFO%3A0000001) is a term in the Experimental Factor Ontology (EFO). Cellosaurus requires a prefixed identifier of the form **Ontology_Identifier** such as [CVCL_1P02](https://www.cellosaurus.org/CVCL_1P02).<br><br>
 If ontologies are missing required terms, then ontologists are responsive to New Term Requests [NTR] such as [[NTR] Version specific Visium assays](https://github.com/EBISPOT/efo/issues/2178) which was created for CELLxGENE Discover requirements.


| Ontology | OBO Prefix |
|:--|:--|
| [C. elegans Development Ontology] | WBls |
| [C. elegans Gross Anatomy Ontology] | WBbt |
| [Cell Ontology] | CL |
| [Cellosaurus] | CVCL_ |
| [Drosophila Anatomy Ontology] | FBbt |
| [Drosophila Development Ontology] | FBdv |
| [Experimental Factor Ontology] | EFO |
| [Gene Ontology]                         | GO         |
| [Human Developmental Stages] |  HsapDv |
| [Mondo Disease Ontology] | MONDO |
| [Mouse Developmental Stages]| MmusDv |
| [NCBI organismal classification] |  NCBITaxon |
| [Phenotype And Trait Ontology] | PATO |
| [Uberon multi-species anatomy ontology] |  UBERON |
| [Zebrafish Anatomy Ontology] | ZFA<br>ZFS |
| [Cell Line Ontology] | CLO |
| | |

[C. elegans Development Ontology]: https://obofoundry.org/ontology/wbls.html

[C. elegans Gross Anatomy Ontology]: https://obofoundry.org/ontology/wbbt.html

[Cell Ontology]: http://obofoundry.org/ontology/cl.html

[Cellosaurus]: https://www.cellosaurus.org/

[Drosophila Anatomy Ontology]: https://obofoundry.org/ontology/fbbt.html

[Drosophila Development Ontology]: https://obofoundry.org/ontology/fbdv.html

[Experimental Factor Ontology]: https://www.ebi.ac.uk/ols4/ontologies/efo

[Gene Ontology]: https://geneontology.org/

[Human Ancestry Ontology]: http://www.obofoundry.org/ontology/hancestro.html

[Human Developmental Stages]: http://obofoundry.org/ontology/hsapdv.html

[Mondo Disease Ontology]: http://obofoundry.org/ontology/mondo.html

[Mouse Developmental Stages]: http://obofoundry.org/ontology/mmusdv.html

[NCBI organismal classification]: http://obofoundry.org/ontology/ncbitaxon.html

[Phenotype And Trait Ontology]: http://www.obofoundry.org/ontology/pato.html

[Uberon multi-species anatomy ontology]: http://www.obofoundry.org/ontology/uberon.html

[Zebrafish Anatomy Ontology]: https://obofoundry.org/ontology/zfa.html

[Cell Line Ontology]: https://www.ebi.ac.uk/ols4/ontologies/clo


## Cross-modality mapping for Dynamic Cell Atlas

This refers specifically to how ontology terms from tables/fields defined in this sample-level metadata table below map to [cross-modality ontology schema](https://docs.google.com/document/d/10PfruMm_OmJaBdLvxVfk_gKzfnW3N7q4QBkCfInfCSY/edit?usp=sharing) for the Dynamic Cell Atlas project. 

| DCA | CZI Crossmodal | Matching Ontology? |
| :---- | :---- | :---- |
| factor value[assay_ontology_term_id] | assay_ontology_term_id | Yes (will update microscopy terms) |
| factor value[assay] | assay | No (FBbi) |
| factor value[developmental_stage_ontology_term_id] | development_stage_ontology_term_id | Yes (HsapDV, MmusDv, ZFS,  WBLS, FBDV) |
| factor value[developmental_stage] | development_stage | Yes(HsapDV, MmusDv, ZFS,  WBLS, FBDV) |
| factor value[disease_ontology_term_id] | disease_ontology_term_id | Yes (MONDO, PATO) |
| factor value[disease] | disease | Yes (MONDO, PATO) |
| factor value[organism_ontology_term_id]  | organism_ontology_term_id | Yes (NCBITaxon) |
| factor value[organism] | organism | Yes (NCBITaxon) |
| factor value[tissue_ontology_term_id] | tissue_ontology_term_id | Yes (UBERON) |
| factor value[tissue] | tissue | Yes (UBERON) |
| factor value[tissue_type] | tissue_type | Yes (NA) |

## Additional Dynamic Cell Atlas Schema
The Dynamic Cell Atlas is comprised of multiple fluorescence microscopy datasets transformed into standard zarrv3 format. Therefore, we also include the minimum additional variables for identifying the original images and communicating channel metadata. A shared ontology and schema for recording channel metadata is still under development. In this section, we will describe the current method.

### Pathways:
  * For each converted zarrv3 image, the atlas tracks the pathways to the original, source data for data provenance.

  ### Source_Raw_Path
  - **Key:** `Source_Raw_Path`  
  - **Description:** This is the path to the original raw image, which is usually on an external S3 bucket, Google Drive, or website. Most of the original files are .tif or .zarr (version 2), which can be identified from the file path. This information is recorded for data provenance. 
  - **Value:** List[String]. Each pathway SHOULD end in ".zip", ".tif", ".zarr", etc. 

  ### Source_Seg_Path
  - **Key:** `Source_Seg_Path`  
  - **Description:** This is the path to the original segmentation image, which is usually on an external S3 bucket, Google Drive, or website. Most of the original files are .tif or .zarr (version 2), which can be identified from the file path. This information is recorded for data provenance. During the zarr conversion these arrays are embedded within the zarrv3 store as labels or segmentations. If the image does not have related segmentations or masks, the column will be left as "Not Applicable".
  - **Value:** List[String]. Each pathway should end in ".zip", ".tif", ".zarr", etc.

  ### Internal_S3_Path
  - **Key:** `Internal_S3_Path`  
  - **Description:** This is the path to the zarrv3 converted image in the Dynamic Cell Atlas database. Each of these images lives in an internal S3 bucket that CZI owns for MDR registration. Note that if a file path is provided under Source_Seg_Path, there will also be a "labels" or "segmentations" folder embedded in the zarr store that has the corresponding converted array.
  - **Value:** List[String]. Each pathway MUST end in ".zarr" or "ome.zarr".


### Channel Metadata Fields:
  * For each image, the atlas metadata tracks the illumination type and target for n number of present channels. The channel # corresponds to the order of each in the zarr image
  (starting with 0). 

  ### Channel Illumination Type
  - **Key:** `Raw_Image_Channel#_IlluminationType`  
  - **Description:** The illumnation type is the method used to capture the channel.
  - **Value:** List[String]. Each element can be one of the following: Transmitted, Fluorescence, Oblique, Nonlinear, and Other.
  
  ### Channel Targets
  - **Key:** `Raw_Image_Channel#_Target`  
  - **Description:** The target field is a descriptive channel parameter rather than an ontology-driven factor. It specifies the molecular or cellular feature imaged in that channel. The most common targets are: DNA, membrane, or a particular gene. 
  - **Value:** List[String]. Each element SHOULD be one of the following: DNA, Membrane, or the approved gene symbol (HGNC) or UniProt accession for images with a fluorescence illumination type. For images with a brightfield illumination type, these channels will have "Transmitted Light" in this field.

### Cell Line Fields:
  * For each image with tissue type "cell culture", the atlas metadata tracks the cell line and cell ontology id from the Cell Ontology (http://obofoundry.org/ontology/cl.html).

  - **Key:** `cell_ontology_id`  
    - **Description:** this is the CL id from here: http://obofoundry.org/ontology/cl.html
    - **Value:** List[String]. 
  
  - **Key:** `cell_line`  
    - **Description:** this is the Cellosaurus name of the cell line here: https://www.cellosaurus.org/
    - **Value:** List[String].

| DCA | CZI Crossmodal | Matching Ontology? |
| :---- | :---- | :---- |
| characteristics[Source_Raw_Path] | Not Applicable | No |
| characteristics[Source_Seg_Path] | Not Applicable | No |
| characteristics[Internal_S3_Path] | Not Applicable | No |
| characteristics[Raw_Image_Channel#_IlluminationType] | Not Applicable | No |
| characteristics[Raw_Image_Channel#_Target] | Not Applicable | No |
| factor[cell_ontology_id] | Not Applicable | Yes (CL)
| factor[cell_line] | Not Applicable | No (Cellosaurus)


## Cross-modality mapping for cryoET data portal

### On-Disk Dataset Metadata

#### AssayDetails Metadata

| XMS-1.1.0 Field          | cryoET Field              | Requirement | Description                                                                | Constraints and Comments |
|:-------------------------|:--------------------------|:------------|:---------------------------------------------------------------------------|:-------------------------|
| `assay`                  | assay                     | **MUST**    | Defines the human-readable assay name that was used to create the dataset. | `string`                 |
| `assay_ontology_term_id` | assay\_ontology\_term\_id | **MUST**    | EFO ID corresponding to the assay(s) used.                                 | `string`, MUST be EFO ID |

#### Author Metadata

| cryoET Field                  | Requirement | Description                                                            | Constraints and Comments                                                                                                           |
|:------------------------------|:------------|:-----------------------------------------------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------|
| name                          | MUST        | The full name of the author.                                           | string                                                                                                                             |
| orcid                         | RECOMMENDED | The author’s [ORCID](https://orcid.org/).                              | String, **MUST** match [ORCID format.](https://support.orcid.org/hc/en-us/articles/360006897674-Structure-of-the-ORCID-Identifier) |
| primary\_author\_status       | SHOULD      | Whether author should be considered first author.                      | bool                                                                                                                               |
| corresponding\_author\_status | SHOULD      | Whether author should be considered corresponding author.              | bool                                                                                                                               |
| kaggle\_id                    | OPTIONAL    | The author’s kaggle user id.                                           | string                                                                                                                             |
| email                         | OPTIONAL    | The author’s email address.                                            | string                                                                                                                             |
| affiliation\_name             | OPTIONAL    | The name of the institution the author is affiliated with.             | string                                                                                                                             |
| affiliation\_identifier       | OPTIONAL    | A [Research Organization Registry (ROR)](https://ror.org/) identifier. | string                                                                                                                             |
| affiliation\_address          | OPTIONAL    | The address of the institution the author is affiliated with.          | string                                                                                                                             |

#### CellComponent Metadata

| cryoET Field | Requirement | Description                                                      | Constraints and Comments             |
|:-------------|:------------|:-----------------------------------------------------------------|:-------------------------------------|
| name         | MUST        | Name of the cellular component.                                  | `string`                             |
| id           | MUST        | The GO identifier for the cellular component or `”not_reported”` | `string`, see CellComponent.id below |

**CellComponent.id**

If the dataset's cryoET `sample_type` is `"organelle"`, then the value MUST be a valid descendant of `"GO:0005575"` for `cellular component`.

---

If the dataset's cryoET `sample_type` is `"virus"`, then the value MUST be `"GO:0044423"` for `virion component`.

---

If the dataset's cryoET `sample_type` is any other type, then the value MUST be `"not_reported"`.

---

#### CellStrain Metadata

| cryoET Field | Requirement | Description                                                      | Constraints and Comments          |
|:-------------|:------------|:-----------------------------------------------------------------|:----------------------------------|
| name         | MUST        | Strain information for the sample.                               | `string`                          |
| id           | MUST        | The cell line's cellosaurus term, strain ID, or `“not_reported”` | `string`, see CellStrain.id below |

**CellStrain.id**

If the dataset's cryoET `sample_type` is `"cell_line"`, then the value MUST be a valid [Cellosaurus](https://www.cellosaurus.org/) term.

---

If the dataset's cryoET `sample_type` is any other type, then the value may be any other strain ID or `"not_reported"`.

---

#### CellType Metadata

| XMS-1.1.0 Field           | cryoET Field | Requirement | Description                                                                                                                     | Constraints and Comments            |
|:--------------------------|:-------------|:------------|:--------------------------------------------------------------------------------------------------------------------------------|:------------------------------------|
| `tissue`                  | name         | MUST        | Name of the cell type from which a biological sample used in a CryoET study is derived from, or the name of the cell line used. | `string`                            |
| `tissue_ontology_term_id` | id           | MUST        | The UBERON or Cell Ontology identifier for the tissue or `"not_reported"`                                                       | `string`, see **CellType.id** below |

**CellType.id**

If the dataset's cryoET `sample_type` is `"primary_cell_culture”`, the following [Cell Ontology (CL)](https://www.ebi.ac.uk/ols4/ontologies/cl/) terms MUST NOT be used:

- [`"CL:0000255"`](https://www.ebi.ac.uk/ols4/ontologies/cl/terms?obo_id=CL:0000255) for *eukaryotic cell*  
- [`"CL:0000257"`](https://www.ebi.ac.uk/ols4/ontologies/cl/terms?obo_id=CL:0000257) for *Eumycetozoan cell*  
- [`"CL:0000548"`](https://www.ebi.ac.uk/ols4/ontologies/cl/terms?obo_id=CL:0000548) for *animal cell*

| For the corresponding `OrganismDetails.taxonomy_id`                                                                                   | Value                                                                                                                                                                                                                                                                                                              |
|:--------------------------------------------------------------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [`"NCBITaxon:6239"`](https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A6239) for \*Caenorhabditis elegans\*  | The value MUST be either a CL term or the most accurate descendant of [`WBbt:0004017`](https://www.ebi.ac.uk/ols4/ontologies/wbbt/classes?obo_id=WBbt%3A0004017) for *Cell* excluding [`WBbt:0006803`](https://www.ebi.ac.uk/ols4/ontologies/wbbt/classes?obo_id=WBbt%3A0006803) for *Nucleus* and its descendants |
| [`"NCBITaxon:7955"`](https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A7955) for \*Danio rerio\*             | The value MUST be either a CL term or the most accurate descendant of [`ZFA:0009000`](https://www.ebi.ac.uk/ols4/ontologies/zfa/classes?obo_id=ZFA%3A0009000) for *cell*                                                                                                                                           |
| [`"NCBITaxon:7227"`](https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A7227) for \*Drosophila melanogaster\* | The value MUST be either a CL term or the most accurate descendant of [`FBbt:00007002`](https://www.ebi.ac.uk/ols4/ontologies/fbbt/classes/http%253A%252F%252Fpurl.obolibrary.org%252Fobo%252FFBbt_00007002?lang=en) for *cell*                                                                                    |

Otherwise, for all other organisms, the value MUST be a CL or UBERON term.

---

If the dataset's cryoET `sample_type` is any other type, the value MAY follow the same rules as above, otherwise MUST be `"not_reported"`.

---

#### CrossReferences Metadata 

| cryoET Field               | Requirement | Description                                                                | Constraints and Comments                                                       |
|:---------------------------|:------------|:---------------------------------------------------------------------------|:-------------------------------------------------------------------------------|
| publications               | RECOMMENDED | Comma-separated list of DOIs for publications associated with the dataset. | string, **MUST** be DOI format                                                 |
| related\_database\_entries | RECOMMENDED | Comma-separated list of related database entries for the dataset.          | string, **MUST** be in appropriate format (EMPIAR-XXXXX, PDB-XXXX, EMDB-XXXXX) |
| related\_database\_links   | OPTIONAL    | Comma-separated list of related database links for the dataset.            | string                                                                         |
| dataset\_citations         | OPTIONAL    | Comma-separated list of DOIs for publications citing the dataset.          | string                                                                         |

---

#### DateStamp Metadata 

| cryoET Field         | Requirement | Description                                                           | Constraints and Comments |
|:---------------------|:------------|:----------------------------------------------------------------------|:-------------------------|
| deposition\_date     | MUST        | The date a data item was received by the cryoET data portal.          | date                     |
| release\_date        | MUST        | The date a data item was received by the cryoET data portal.          | date                     |
| last\_modified\_date | MUST        | The date a piece of data was last modified on the cryoET data portal. | date                     |

---

#### DevelopmentStageDetails Metadata

| XMS-1.1.0 Field                      | cryoET Field                           | Requirement | Description                                                                                               | Constraints and Comments                                        |
|:-------------------------------------|:---------------------------------------|:------------|:----------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------|
| `development_stage`                  | development\_stage                     | **MUST**    | Defines the development stage(s) of the patients or organisms from which assayed biosamples were derived. | `string`                                                        |
| `development_stage_ontology_term_id` | development\_stage\_ontology\_term\_id | **MUST**    | Organism-specific ontology ID corresponding to the development stage(s).                                  | `string`, See **development\_stage\_ontology\_term\_id** below. |

**DevelopmentStageDetails.development\_stage\_ontology\_term\_id**  
Type: `string`

If the dataset's cryoET `sample_type` is `"cell_line"`, the value MUST be `"na"`.

If unavailable, the value MUST be `"unknown"`.

| For the corresponding `OrganismDetails.taxonomy_id`                                                                                                  | Value                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|:-----------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [`"NCBITaxon:6239"`](https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A6239) for *Caenorhabditis elegans*                   | The value MUST be [`WBls:0000669`](https://www.ebi.ac.uk/ols4/ontologies/wbls/classes?obo_id=WBls%3A0000669) for *unfertilized egg Ce*, the most accurate descendant of [`WBls:0000803`](https://www.ebi.ac.uk/ols4/ontologies/wbls/classes?obo_id=WBls%3A0000803) for *C. elegans life stage occurring during embryogenesis*, or the most accurate descendant of [`WBls:0000804`](https://www.ebi.ac.uk/ols4/ontologies/wbls/classes?obo_id=WBls%3A0000804) for *C. elegans life stage occurring post embryogenesis* |
| [`"NCBITaxon:7955"`](https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A7955) for *Danio rerio*                              | The value MUST be the most accurate descendant of [`ZFS:0100000`](https://www.ebi.ac.uk/ols4/ontologies/zfs/classes?obo_id=ZFS%3A0100000) for *zebrafish stage* excluding [`ZFS:0000000`](https://www.ebi.ac.uk/ols4/ontologies/zfs/classes?obo_id=ZFS%3A0000000) for *Unknown*                                                                                                                                                                                                                                       |
| [`"NCBITaxon:7227"`](https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A7227) for *Drosophila melanogaster*                  | The value MUST be either the most accurate descendant of [`FBdv:00007014`](https://www.ebi.ac.uk/ols4/ontologies/fbdv/classes?obo_id=FBdv%3A00007014) for *adult age in days* or the most accurate descendant of [`FBdv:00005259`](https://www.ebi.ac.uk/ols4/ontologies/fbdv/classes?obo_id=FBdv%3A00005259) for *developmental stage* excluding [`FBdv:00007012`](https://www.ebi.ac.uk/ols4/ontologies/fbdv/classes?obo_id=FBdv%3A00007012) for *life stage*                                                       |
| [`"NCBITaxon:9606"`](https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A9606) for *Homo sapiens*                             | The value MUST be the most accurate descendant of [`HsapDv:0000001`](https://www.ebi.ac.uk/ols4/ontologies/hsapdv/classes?obo_id=HsapDv%3A0000001) for *life cycle*                                                                                                                                                                                                                                                                                                                                                   |
| [`"NCBITaxon:10090"`](https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A10090) for *Mus musculus* or one of its descendants | The value MUST be the accurate descendant of [`MmusDv:0000001`](https://www.ebi.ac.uk/ols4/ontologies/mmusdv/classes?obo_id=MmusDv%3A0000001) for *life cycle*                                                                                                                                                                                                                                                                                                                                                        |

Otherwise, for all other organisms, the value MUST be the most accurate descendant of [`UBERON:0000105`](https://www.ebi.ac.uk/ols4/ontologies/uberon/classes?obo_id=UBERON%3A0000105) for *life cycle stage*, excluding [`UBERON:0000071`](https://www.ebi.ac.uk/ols4/ontologies/uberon/classes?obo_id=UBERON%3A0000071) for *death stage*.

---

#### DiseaseDetails Metadata

| XMS-1.1.0 Field            | cryoET Field                | Requirement | Description                                                                                     | Constraints and Comments                                                                                                                                                                                     |
|:---------------------------|:----------------------------|:------------|:------------------------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `disease`                  | disease                     | **MUST**    | Defines the disease(s) of the patients or organisms from which assayed biosamples were derived. | `string`                                                                                                                                                                                                     |
| `disease_ontology_term_id` | disease\_ontology\_term\_id | **MUST**    | The ontology term ID(s) corresponding to the disease state(s).                                  | `string`, The value MUST be one of: "PATO:0000461" for normal or healthy, the most accurate descendant of "MONDO:0000001" for disease, "MONDO:0021178" for injury or preferably its most accurate descendant |

---

#### FundingDetails Metadata 

| cryoET Field          | Requirement | Description                                     | Constraints and Comments |
|:----------------------|:------------|:------------------------------------------------|:-------------------------|
| funding\_agency\_name | RECOMMENDED | The name of the funding source.                 | string                   |
| grant\_id             | RECOMMENDED | Grant identifier provided by the funding agency | string                   |

---

#### OrganismDetails Metadata

| XMS-1.1.0 Field             | cryoET Field | Requirement | Description                                                                                                       | Constraints and Comments                 |
|:----------------------------|:-------------|:------------|:------------------------------------------------------------------------------------------------------------------|:-----------------------------------------|
| `organism`                  | name         | **MUST**    | Name of the organism(s) from which a biological sample used in a CryoET study is derived from, e.g. homo sapiens. | `string`, `not_reported` if id is `None` |
| `organism_ontology_term_id` | taxonomy\_id | **MUST**    | The NCBI taxon ID(s) of the organism(s)                                                                           | `integer`See **taxonomy\_id** below.    |

**OrganismDetails.taxonomy\_id**  
Type: `integer`

If the corresponding `sample_type` is `"organism"`, `"tissue"`, `"cell"`, `"organoid"`, `"organelle"` or `"virus"` the value **MUST** be an NCBI organismal classification term such as `"9606"`  

---

If the corresponding `sample_type` is `"in_vitro"`,  `"in_silico"` or `"other"`, the value **MAY** be an NCBI organismal classification term such as `"9606"`, otherwise it **MUST** be `None`.  

---

#### PicturePath 

| cryoET Field | Requirement | Description                                                                   | Constraints and Comments                                                                           |
|:-------------|:------------|:------------------------------------------------------------------------------|:---------------------------------------------------------------------------------------------------|
| snapshot     | RECOMMENDED | Path to the preview image relative to the entity directory root.              | string,  **\- API: MUST** be URL format \- **Metadata**: MUST be relative  path from dataset root. |
| thumbnail    | RECOMMENDED | Path to the thumbnail of preview image relative to the entity directory root. | string,  **\- API: MUST** be URL format \- **Metadata**: MUST be relative  path from dataset root. |

---

#### SampleType Enum

| XMS-1.1.0 `tissue_type` value  | cryoET value         | Description                                                                |
|:-------------------------------|:---------------------|:---------------------------------------------------------------------------|
| `tissue`                       | organism             | Tomographic data of sections through multicellular organisms               |
| `tissue`                       | tissue               | Tomographic data of tissue sections                                        |
| `cell line`                    | cell_line            | Tomographic data of immortalized cells or immortalized cell sections       |
| `cell culture`                 | primary_cell_culture | Tomographic data of whole primary cells or primary cell sections           |
| `organoid`                     | organoid             | Tomographic data of organoid-derived samples                               |
| `organelle`                    | organelle            | Tomographic data of purified organelles                                    |
| `organelle`                    | virus                | Tomographic data of purified viruses or VLPs                               |
| not registered/mapped in 1.1.0 | in\_vitro            | Tomographic data of in vitro reconstituted systems or mixtures of proteins |
| not registered/mapped in 1.1.0 | in\_silico           | Simulated tomographic data                                                 |
| not registered/mapped in 1.1.0 | other                | Other type of sample                                                       |

---

#### TissueDetails Metadata

| XMS-1.1.0 Field           | cryoET Field | Requirement | Description                                                                               | Constraints and Comments                 |
|:--------------------------|:-------------|:------------|:------------------------------------------------------------------------------------------|:-----------------------------------------|
| `tissue`                  | name         | **MUST**    | Name of the tissue from which a biological sample used in a CryoET study is derived from. | `string`                                 |
| `tissue_ontology_term_id` | id           | **MUST**    | The UBERON identifier for the tissue or `"not_reported"`                                  | `string` See **TissueDetails.id** below. |

**TissueDetails.id**

Type: `string`

If the dataset's cryoET `sample_type` is `"organism"`, `"tissue"` or `"organoid"` then:

| For the corresponding `OrganismDetails.taxonomy_id`                                                                                   | Value                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|:--------------------------------------------------------------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [`"NCBITaxon:6239"`](https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A6239) for \*Caenorhabditis elegans\*  | The value MUST be either an UBERON term or the most accurate descendant of [`WBbt:0005766`](https://www.ebi.ac.uk/ols4/ontologies/wbbt/classes?obo_id=WBBT%3A0005766) for *Anatomy* excluding [`WBbt:0007849`](https://www.ebi.ac.uk/ols4/ontologies/wbbt/classes?obo_id=WBBT%3A0007849) for *hermaphrodite*, [`WBbt:0007850`](https://www.ebi.ac.uk/ols4/ontologies/wbbt/classes?obo_id=WBBT%3A0007850) for *male*, [`WBbt:0008595`](https://www.ebi.ac.uk/ols4/ontologies/wbbt/classes?obo_id=WBBT%3A0008595) for *female*, [`WBbt:0004017`](https://www.ebi.ac.uk/ols4/ontologies/wbbt/classes?obo_id=WBBT%3A0004017) for *Cell* and its descendants, and [`WBbt:00006803`](https://www.ebi.ac.uk/ols4/ontologies/wbbt/classes?obo_id=WBBT%3A0006803) for *Nucleus* and its descendants |
| [`"NCBITaxon:7955"`](https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A7955) for \*Danio rerio\*             | The value MUST be either an UBERON term or the most accurate descendant of [`ZFA:0100000`](https://www.ebi.ac.uk/ols4/ontologies/zfa/classes?obo_id=ZFA%3A0100000) for *zebrafish anatomical entity* excluding [`ZFA:0001093`](https://www.ebi.ac.uk/ols4/ontologies/zfa/classes?obo_id=ZFA%3A0001093) for *unspecified* and [`ZFA:0009000`](https://www.ebi.ac.uk/ols4/ontologies/zfa/classes?obo_id=ZFA%3A0009000) for *cell* and its descendants                                                                                                                                                                                                                                                                                                                                        |
| [`"NCBITaxon:7227"`](https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A7227) for \*Drosophila melanogaster\* | The value MUST be either an UBERON term or the most accurate descendant of [`FBbt:10000000`](https://www.ebi.ac.uk/ols4/ontologies/fbbt/classes?obo_id=FBBT%3A10000000) for *anatomical entity* excluding [`FBbt:00007002`](https://www.ebi.ac.uk/ols4/ontologies/fbbt/classes?obo_id=FBbt%3A00007002) for *cell* and its descendants                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| For all other organisms                                                                                                               | The value **MUST** be the most accurate descendant of [`UBERON:0001062`](https://www.ebi.ac.uk/ols4/ontologies/uberon/classes?obo_id=UBERON%3A0001062) for *anatomical entity*.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |

---

If the dataset's cryoET `sample_type` is `"primary_cell_culture”`, `"cell_line"` or `"organelle"` the value **MAY** follow the definition for `"tissue"`, otherwise it **MUST** be `"not_reported"`.

---

If the dataset's cryoET `sample_type` is `"virus"`, `"in_vitro"`, `"in_silico"` or `"other"` then the value MUST be `"not_reported"`.  

---

#### Dataset Metadata 

| cryoET Field         | Requirement     | Description                                                                                                                            | Constraints and Comments                                                |
|:---------------------|:----------------|:---------------------------------------------------------------------------------------------------------------------------------------|:------------------------------------------------------------------------|
| deposition\_id       | **MUST**        | An identifier for a CryoET deposition, assigned by the Data Portal. Used to identify the deposition the entity is a part of.           | integer                                                                 |
| last\_updated\_at    | **MUST**        | POSIX timestamp of the last time this metadata file was updated.                                                                       | float                                                                   |
| key\_photos          | **MUST**        | A set of paths to representative images of a piece of data for metadata files.                                                         | [`PicturePath`](#picturepath) metadata                                  |
| dataset\_identifier  | **MUST**        | An identifier for a CryoET dataset, assigned by the Data Portal. Used to identify the dataset as the directory name in data tree.      | integer                                                                 |
| dataset\_title       | **MUST**        | Title of a CryoET dataset.                                                                                                             | string                                                                  |
| dataset\_description | **MUST**        | A short description of a CryoET dataset, similar to an abstract for a journal article or dataset.                                      | string                                                                  |
| dates                | **MUST**        | A set of dates at which a data item was deposited, published and last modified.                                                        | [`DateStamp`](#datestamp-metadata)                                      |
| authors              | **MUST**        | Author of a scientific data entity.                                                                                                    | list of [`Author`](#author-metadata) metadata , min length=1            |
| funding              | **RECOMMENDED** | A funding source for a scientific data entity (base for JSON and DB representation).                                                   | list of [`FundingDetails`](#fundingdetails-metadata) metadata           |
| cross\_references    | **OPTIONAL**    | A set of cross-references to other databases and publications.                                                                         | [`CrossReferences`](#crossreferences-metadata) metadata                 |
| sample\_type         | **MUST**        | Type of sample imaged in a CryoET study.                                                                                               | `SampleTypeEnum` value                                                  |
| sample\_preparation  | **RECOMMENDED** | Describes how the sample was prepared.                                                                                                 | string                                                                  |
| grid\_preparation    | **RECOMMENDED** | Describes Cryo-ET grid preparation.                                                                                                    | string                                                                  |
| other\_setup         | **RECOMMENDED** | Describes other setup not covered by sample preparation or grid preparation that may make this dataset unique in the same publication. | string                                                                  |
| organism             | **MUST**        | The species from which the sample was derived.                                                                                         | [`OrganismDetails`](#organismdetails-metadata) metadata                 |
| tissue               | **MUST**        | The type of tissue from which the sample was derived.                                                                                  | [`TissueDetails`](#tissuedetails-metadata) metadata                     |
| cell\_type           | **MUST**        | The cell type from which the sample was derived.                                                                                       | [`CellType`](#celltype-metadata) metadata                               |
| cell\_strain         | **MUST**        | The strain or cell line from which the sample was derived.                                                                             | [`CellStrain`](#cellstrain-metadata) metadata                           |
| cell\_component      | **MUST**        | The cellular component from which the sample was derived.                                                                              | [`CellComponent`](#cellcomponent-metadata) metadata                     |
| assay                | **MUST**        | Defines the assay(s) that was used to create the dataset.                                                                              | [`AssayDetails`](#assaydetails-metadata) metadata                       |
| development\_stage   | **MUST**        | Defines the development stage(s) of the patients or organisms from which assayed biosamples were derived.                              | [`DevelopmentStageDetails`](#developmentstagedetails-metadata) metadata |
| disease              | **MUST**        | Defines the disease(s) of the patients or organisms from which assayed biosamples were derived.                                        | [`DiseaseDetails`](#diseasedetails-metadata) metadata                   |


#### Database and API Mapping 

Mapping of the `Dataset` metadata to the database, GraphQL API and python API client is as shown below.

| DB Column                            | DB Type    | PK/FK | Nullable? | GraphQL API Field                | GraphQL API Type    | Python Client Field                          | Python Client Type | Mapped AWS S3 Metadata Field                                                                        |
|:-------------------------------------|:-----------|:------|:----------|:---------------------------------|:--------------------|:---------------------------------------------|:-------------------|:----------------------------------------------------------------------------------------------------|
| `id`                                 | `Integer`  | PK    | No        | `id`                             | `Int!`              | `Dataset.id`                                 | `int`              | [`Dataset.dataset_identifier`](#dataset-metadata)                                                   |
| `deposition_id`                      | `Integer`  | FK    | No        | `depositionId`                   | `ID`                | `Dataset.deposition_id`                      | `int`              | [`Dataset.deposition_id`](#dataset-metadata)                                                        |
| `title`                              | `String`   |       | No        | `title`                          | `String!`           | `Dataset.title`                              | `str`              | [`Dataset.dataset_title`](#dataset-metadata)                                                        |
| `description`                        | `String`   |       | No        | `description`                    | `String!`           | `Dataset.description`                        | `str`              | [`Dataset.dataset_description`](#dataset-metadata)                                                  |
| `organism_name`                      | `String`   |       | No        | `organismName`                   | `String!`           | `Dataset.organism_name`                      | `str`              | [`Dataset.organism.name`](#organismdetails-metadata)                                                |
| `organism_taxid`                     | `Integer`  |       | No        | `organismTaxid`                  | `Int!`              | `Dataset.organism_taxid`                     | `int`              | [`Dataset.organism.taxonomy_id`](#organismdetails-metadata)                                         |
| `tissue_name`                        | `String`   |       | No        | `tissueName`                     | `String!`           | `Dataset.tissue_name`                        | `str`              | [`Dataset.tissue.name`](#tissuedetails-metadata)                                                    |
| `tissue_id`                          | `String`   |       | No        | `tissueId`                       | `String!`           | `Dataset.tissue_id`                          | `str`              | [`Dataset.tissue.id`](#tissuedetails-metadata)                                                      |
| `cell_name`                          | `String`   |       | No        | `cellName`                       | `String!`           | `Dataset.cell_name`                          | `str`              | [`Dataset.cell_type.name`](#celltype-metadata)                                                      |
| `cell_type_id`                       | `String`   |       | No        | `cellTypeId`                     | `String!`           | `Dataset.cell_type_id`                       | `str`              | [`Dataset.cell_type.id`](#celltype-metadata)                                                        |
| `cell_strain_name`                   | `String`   |       | No        | `cellStrainName`                 | `String!`           | `Dataset.cell_strain_name`                   | `str`              | [`Dataset.cell_strain.name`](#cellstrain-metadata)                                                  |
| `cell_strain_id`                     | `String`   |       | No        | `cellStrainId`                   | `String!`           | `Dataset.cell_strain_id`                     | `str`              | [`Dataset.cell_strain.id`](#cellstrain-metadata)                                                    |
| `sample_type`                        | `Enum`     |       | No        | `sampleType`                     | `sample_type_enum!` | `Dataset.sample_type`                        | `str`              | [`Dataset.sample_type`](#dataset-metadata)                                                          |
| `sample_preparation`                 | `String`   |       | Yes       | `samplePreparation`              | `String`            | `Dataset.sample_preparation`                 | `str`              | [`Dataset.sample_preparation`](#dataset-metadata)                                                   |
| `grid_preparation`                   | `String`   |       | Yes       | `gridPreparation`                | `String`            | `Dataset.grid_preparation`                   | `str`              | [`Dataset.grid_preparation`](#dataset-metadata)                                                     |
| `other_setup`                        | `String`   |       | Yes       | `otherSetup`                     | `String`            | `Dataset.other_setup`                        | `str`              | [`Dataset.other_setup`](#dataset-metadata)                                                          |
| `key_photo_url`                      | `String`   |       | Yes       | `keyPhotoUrl`                    | `String`            | `Dataset.key_photo_url`                      | `str`              | [`Dataset.key_photos.snapshot`](#picturepath)                                                       |
| `key_photo_thumbnail_url`            | `String`   |       | Yes       | `keyPhotoThumbnailUrl`           | `String`            | `Dataset.key_photo_thumbnail_url`            | `str`              | [`Dataset.key_photos.thumbnail`](#picturepath)                                                      |
| `cell_component_name`                | `String`   |       | No        | `cellComponentName`              | `String!`           | `Dataset.cell_component_name`                | `str`              | [`Dataset.cell_component.name`](#cellcomponent-metadata)                                            |
| `cell_component_id`                  | `String`   |       | No        | `cellComponentId`                | `String!`           | `Dataset.cell_component_id`                  | `str`              | [`Dataset.cell_component.id`](#cellcomponent-metadata)                                              |
| `deposition_date`                    | `DateTime` |       | No        | `depositionDate`                 | `DateTime!`         | `Dataset.deposition_date`                    | `date`             | [`Dataset.dates.deposition_date`](#datestamp-metadata)                                              |
| `release_date`                       | `DateTime` |       | No        | `releaseDate`                    | `DateTime!`         | `Dataset.release_date`                       | `date`             | [`Dataset.dates.release_date`](#datestamp-metadata)                                                 |
| `last_modified_date`                 | `DateTime` |       | No        | `lastModifiedDate`               | `DateTime!`         | `Dataset.last_modified_date`                 | `date`             | [`Dataset.dates.last_modified_date`](#datestamp-metadata)                                           |
| `dataset_publications`               | `String`   |       | Yes       | `datasetPublications`            | `String`            | `Dataset.dataset_publications`               | `str`              | [`Dataset.cross_references.publications`](#crossreferences-metadata)                                |
| `related_database_entries`           | `String`   |       | Yes       | `relatedDatabaseEntries`         | `String`            | `Dataset.related_database_entries`           | `str`              | [`Dataset.cross_references.related_database_entries`](#crossreferences-metadata)                    |
| `s3_prefix`                          | `String`   |       | No        | `s3Prefix`                       | `String!`           | `Dataset.s3_prefix`                          | `str`              | `Dataset.s3_prefix`                                                                                 |
| `https_prefix`                       | `String`   |       | No        | `httpsPrefix`                    | `String!`           | `Dataset.https_prefix`                       | `str`              | `Dataset.https_prefix`                                                                              |
| `file_size`                          | `Float`    |       | Yes       | `fileSize`                       | `Float`             | `Dataset.file_size`                          | `float`            | computed during DB import                                                                           |
| `assay_name`                         | `String`   |       | No        | `assayName`                      | `String!`           | `Dataset.assay_name`                         | `str`              | [`Dataset.assay.assay`](#assaydetails-metadata)                                                     |
| `assay_ontology_term_id`             | `String`   |       | No        | `assayOntologyTermId`            | `String!`           | `Dataset.assay_ontology_term_id`             | `str`              | [`Dataset.assay.assay_ontology_term_id`](#assaydetails-metadata)                                    |
| `development_stage`                  | `String`   |       | No        | `developmentStage`               | `String!`           | `Dataset.development_stage`                  | `str`              | [`Dataset.development_stage.development_stage`](#developmentstagedetails-metadata)                  |
| `development_stage_ontology_term_id` | `String`   |       | No        | `developmentStageOntologyTermId` | `String!`           | `Dataset.development_stage_ontology_term_id` | `str`              | [`Dataset.development_stage.development_stage_ontology_term_id`](#developmentstagedetails-metadata) |
| `disease`                            | `String`   |       | No        | `disease`                        | `String!`           | `Dataset.disease`                            | `str`              | [`Dataset.disease.disease`](#diseasedetails-metadata)                                               |
| `disease_ontology_term_id`           | `String`   |       | No        | `diseaseOntologyTermId`          | `String!`           | `Dataset.disease_ontology_term_id`           | `str`              | [`Dataset.disease.disease_ontology_term_id`](#diseasedetails-metadata)                              |


### Mapping to XMS 1.1.0

#### XMS-1.1.0 metadata Mapping

Mapping will be specified in terms of Python API client fields (as that is what will be used in automatic MDR registration).

| XMS-1.1.0                            | Python Client Field                          | Notes                                                                        |
|:-------------------------------------|:---------------------------------------------|:-----------------------------------------------------------------------------|
| `assay_name`                         | `Dataset.assay_name`                         | convert to list of string                                                    |
| `assay_ontology_term_id`             | `Dataset.assay_ontology_term_id`             | convert to list of string                                                    |
| `development_stage`                  | `Dataset.development_stage`                  | convert to list of string                                                    |
| `development_stage_ontology_term_id` | `Dataset.development_stage_ontology_term_id` | convert to list of string                                                    |
| `disease`                            | `Dataset.disease`                            | convert to list of string                                                    |
| `disease_ontology_term_id`           | `Dataset.disease_ontology_term_id`           | convert to list of string                                                    |
| `organism`                           | `Dataset.organism_name`                      | convert to list of string                                                    |
| `organism_ontology_term_id`          | `Dataset.organism_taxid`                     | Convert to list of string, prepend “NCBITaxon:”. If `None`, exclude dataset. |
| `tissue`                             | depends on `Dataset.sample_type`             | See `tissue` mapping rules below                                             |
| `tissue_ontology_term_id`            | depends on `Dataset.sample_type`             | See `tissue_ontology_term_id` mapping rules below                            |
| `tissue_type`                        | depends on `Dataset.sample_type`             | See `tissue_type` mapping rules below                                        |

#### XMS-1.1.0 `tissue_type` mapping

Sample types are mapped as follows:

| XMS-1.1.0 `tissue_type` value  | cryoET value         | Description                                                                |
|:-------------------------------|:---------------------|:---------------------------------------------------------------------------|
| `tissue`                       | organism             | Tomographic data of sections through multicellular organisms               |
| `tissue`                       | tissue               | Tomographic data of tissue sections                                        |
| `cell line`                    | cell_line            | Tomographic data of immortalized cells or immortalized cell sections       |
| `cell culture`                 | primary_cell_culture | Tomographic data of whole primary cells or primary cell sections           |
| `organoid`                     | organoid             | Tomographic data of organoid-derived samples                               |
| `organelle`                    | organelle            | Tomographic data of purified organelles                                    |
| `organelle`                    | virus                | Tomographic data of purified viruses or VLPs                               |
| not registered/mapped in 1.1.0 | in\_vitro            | Tomographic data of in vitro reconstituted systems or mixtures of proteins |
| not registered/mapped in 1.1.0 | in\_silico           | Simulated tomographic data                                                 |
| not registered/mapped in 1.1.0 | other                | Other type of sample                                                       |

#### XMS-1.1.0 `tissue_ontology_term_id` mapping

If cryoET `sample_type` is `”organism”` or `“tissue”`, XMS-1.1.0 `tissue_type` is `”tissue”`. 
XMS-1.1.0 `tissue` and `tissue_ontology_term_id` are mapped to the following Python client fields:

| XMS-1.1.0                 | Python Client Field   | Notes                     |
|:--------------------------|:----------------------|:--------------------------|
| `tissue`                  | `Dataset.tissue_name` | convert to list of string |
| `tissue_ontology_term_id` | `Dataset.tissue_id`   | convert to list of string |

If cryoET `sample_type` is `”cell_line”`, XMS-1.1.0 `tissue_type` is `”cell line”`.
XMS-1.1.0 `tissue` and `tissue_ontology_term_id` are mapped to the following Python client fields:

| XMS-1.1.0                 | Python Client Field        | Notes                     |
|:--------------------------|:---------------------------|:--------------------------|
| `tissue`                  | `Dataset.cell_strain_name` | convert to list of string |
| `tissue_ontology_term_id` | `Dataset.cell_strain_id`   | convert to list of string |

If cryoET `sample_type` is `”primary_cell_culture”`, XMS-1.1.0 `tissue_type` is `”cell culture”`.
XMS-1.1.0 `tissue` and `tissue_ontology_term_id` are mapped to the following Python client fields:

| XMS-1.1.0                 | Python Client Field    | Notes                     |
|:--------------------------|:-----------------------|:--------------------------|
| `tissue`                  | `Dataset.cell_name`    | convert to list of string |
| `tissue_ontology_term_id` | `Dataset.cell_type_id` | convert to list of string |

If cryoET `sample_type` is `”organoid”`, XMS-1.1.0 `tissue_type` is `”organoid”`.
XMS-1.1.0 `tissue` and `tissue_ontology_term_id` are mapped to the following Python client fields:

| XMS-1.1.0                 | Python Client Field   | Notes                     |
|:--------------------------|:----------------------|:--------------------------|
| `tissue`                  | `Dataset.tissue_name` | convert to list of string |
| `tissue_ontology_term_id` | `Dataset.tissue_id`   | convert to list of string |

If cryoET `sample_type` is `”organelle”` or `"virus"`, XMS-1.1.0 `tissue_type` is `”organelle”`.
XMS-1.1.0 `tissue` and `tissue_ontology_term_id` are mapped to the following Python client fields:

| XMS-1.1.0                 | Python Client Field           | Notes                     |
|:--------------------------|:------------------------------|:--------------------------|
| `tissue`                  | `Dataset.cell_component_name` | convert to list of string |
| `tissue_ontology_term_id` | `Dataset.cell_component_id`   | convert to list of string |

## Changelog

v1.0.0

* Published minimal set of metadata requirements
