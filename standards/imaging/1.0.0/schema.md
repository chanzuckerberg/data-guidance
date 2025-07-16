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

| Ontology | OBO Prefix |
|:--|:--|
| [C. elegans Development Ontology] | WBls |
| [C. elegans Gross Anatomy Ontology] | WBbt |
| [Cell Ontology] | CL |
| [Drosophila Anatomy Ontology] | FBbt |
| [Drosophila Development Ontology] | FBdv |
| [Experimental Factor Ontology] | EFO |
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

[Drosophila Anatomy Ontology]: https://obofoundry.org/ontology/fbbt.html

[Drosophila Development Ontology]: https://obofoundry.org/ontology/fbdv.html

[Experimental Factor Ontology]: https://www.ebi.ac.uk/ols4/ontologies/efo

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

## Changelog

v1.0.0

* Published minimal set of metadata requirements
