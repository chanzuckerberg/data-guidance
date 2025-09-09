# Imaging Modality Schema

Contact: cchiu@chanzuckerberg.com

Document Status: __drafting__

Version: 1.0.0

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED" "MAY", and "OPTIONAL" in this document are to be interpreted as described in [BCP 14](https://tools.ietf.org/html/bcp14), [RFC2119](https://www.rfc-editor.org/rfc/rfc2119.txt), and [RFC8174](https://www.rfc-editor.org/rfc/rfc8174.txt) when, and only when, they appear in all capitals, as shown here.

## Schema versioning

The imaging modality schema version is based on [Semantic Versioning](https://semver.org/).

**Major version** is incremented when incompatible schema updates are introduced:
  * Renaming metadata fields
  * Deprecating metadata fields
  * Changing the type or format of a metadata field
 
**Minor version** is incremented when additive schema updates are introduced:
  * Adding metadata fields
  * Changing the validation requirements for a metadata field
  
**Patch version** is incremented for editorial updates.

All changes are documented in the schema [Changelog](#appendix-a-changelog).


## Overview
The following descriptive metadata are associated with all imaging datasets to ensure that datasets can be found by searching for common characteristics of datasets. These metadata MUST be programmatically validated to ensure compliance. Additional metadata MAY be annotated at the discretion of data stewards.

**Categories of metadata:**
- **Data description** — dataset-level metadata (source, license, compliance).  
- **Subject** — species, genotype, sex, age.  
- **Procedure** — pre-acquisition treatments, labeling, specimen preparation.  
- **Instrument** — imaging device metadata.  
- **Acquisition** — acquisition software and hardware configuration.  
- **Channel description** — per-channel settings.  
<br>

For data in Zarr format, the metadata defined by [OME-Zarr](https://ngff.openmicroscopy.org/0.1/) SHOULD be implemented.<br>
<br>

**For general images:**
- All metadata are stored at the OME-Zarr group level.

**For high content screening (HCS):**
- Plate-level metadata: data description, instrument, acquisition.  
- Well-level metadata: subject, procedure, channel description.

**For CryoET data:**
- The full set of metadata for CryoET data is described [here](TBD). <br>

The mapping of CryoET data and DCA data to the XMS is specified [here](TBD).

## Data description
Description: Administrative metadata about the source of the data, funding, relevant licenses, and restrictions on use.

Cross-modality metadata: 
Security & Compliance Metadata and Technical Metadata outlined in the [Data registration needs](https://czi.atlassian.net/wiki/spaces/SCI/pages/3896868957/Data+Registration+Needs+Metadata) are captured here.

### imaging_method
<table><tbody>
    <tr>
      <th>Key</th>
      <td>imaging_method</td>
    </tr>
    <tr>
      <th>Description</th>
      <td>Defines the imaging method that was used to create the dataset</td>
    </tr>
    <tr>
      <th>Annotator</th>
      <td>Submitter MUST annotate.</td>
    </tr>
    <tr>
      <th>Value</th>
        <td><code>List[String]</code>. 
         The List element MUST be a term in <a href="https://webprotege.stanford.edu/#projects/ee9f28eb-bcfe-469d-a9b4-48929f100eec/edit/Classes">the imaging methods list </a>.
        </td>
    </tr>
</tbody></table>
<br>

### file_format
<table><tbody>
    <tr>
      <th>Key</th>
      <td>file_format</td>
    </tr>
    <tr>
      <th>Description</th>
      <td>Specify the file format</td>
    </tr>
    <tr>
      <th>Annotator</th>
      <td>Submitter MUST annotate.</td>
    </tr>
    <tr>
      <th>Value</th>
        <td><code>List[String]</code>. 
         Examples: Zarr_V2, Zarr_V3, mrc.
        </td>
    </tr>
</tbody></table>
<br>

### creation_time
<table><tbody>
    <tr>
      <th>Key</th>
      <td>creation_time</td>
    </tr>
    <tr>
      <th>Description</th>
      <td>The start time of data acquisition, used to uniquely identify the data.</td>
    </tr>
    <tr>
      <th>Annotator</th>
      <td>Submitter MUST annotate.</td>
    </tr>
    <tr>
      <th>Value</th>
        <td><code>datetime</code>
        </td>
    </tr>
</tbody></table>
<br>

## Subject
Description: Species, genotype, age, sex, and source.

Cross-modality metadata: 
[Cross-modality schema metadata](https://github.com/chanzuckerberg/data-guidance/tree/main/standards/cross-modality) are captured here.


### non_biological_subject
<table><tbody>
    <tr>
      <th>Key</th>
      <td>non_biological_subject</td>
    </tr>
    <tr>
      <th>Description</th>
      <td>Specify the non-biological object in the data.</td>
    </tr>
    <tr>
      <th>Annotator</th>
      <td>OPTIONAL.</td>
    </tr>
    <tr>
      <th>Value</th>
        <td><code>List[String]</code>. 
        </td>
    </tr>
</tbody></table>
<br>

## Procedure
Metadata about any procedures performed prior to data acquisition, including subject procedures (surgeries, behavior training, etc.) and specimen procedures (tissue preparation, staining, etc.).

### subject_procedure
<table><tbody>
    <tr>
      <th>Key</th>
      <td>subject_procedure</td>
    </tr>
    <tr>
      <th>Description</th>
      <td>Procedures performed on a live subject. May have multiple procedures per data.</td>
    </tr>
    <tr>
      <th>Annotator</th>
      <td>OPTIONAL.</td>
    </tr>
    <tr>
      <th>Value</th>
        <td><code>List[String]</code>. 
         Examples: infection, chemical treatment.
        </td>
    </tr>
</tbody></table>
<br>

### specimen_procedure
<table><tbody>
    <tr>
      <th>Key</th>
      <td>specimen_procedure</td>
    </tr>
    <tr>
      <th>Description</th>
      <td>Procedures performed on a fixed sample. May have multiple procedures per data.</td>
    </tr>
    <tr>
      <th>Annotator</th>
      <td>OPTIONAL.</td>
    </tr>
    <tr>
      <th>Value</th>
        <td><code>List[String]</code>. 
         Examples: tissue clearing, in situ hybridization.
        </td>
    </tr>
</tbody></table>
<br>

### label
<table><tbody>
    <tr>
      <th>Key</th>
      <td>label</td>
    </tr>
    <tr>
      <th>Description</th>
      <td>Labels such as fluorescent proteins, dyes, or antibodies used.</td>
    </tr>
    <tr>
      <th>Annotator</th>
      <td>Submitter MUST annotate.</td>
    </tr>
    <tr>
      <th>Value</th>
        <td><code>List[String]</code>. 
         Examples: RFP, nanogold. The List element MUST be "na" for label-free imaging.
        </td>
    </tr>
</tbody></table>
<br>

### labeled_component
<table><tbody>
    <tr>
      <th>Key</th>
      <td>labeled_component</td>
    </tr>
    <tr>
      <th>Description</th>
      <td>Proteins or other biomolecules tagged with labels.</td>
    </tr>
    <tr>
      <th>Annotator</th>
      <td>Submitter MUST annotate.</td>
    </tr>
    <tr>
      <th>Value</th>
        <td><code>List[String]</code>. 
         The List element MUST be "na" for label-free imaging.
        </td>
    </tr>
</tbody></table>
<br>

## Instrument
Metadata describing the equipment used to acquire data, including part names, serial numbers.

### instrument_name
<table><tbody>
    <tr>
      <th>Key</th>
      <td>instrument_name</td>
    </tr>
    <tr>
      <th>Description</th>
      <td>The instrument that is used for imaging data acquisition.</td>
    </tr>
    <tr>
      <th>Annotator</th>
      <td>For CZI internally generated data: Submitter MUST annotate.<br>
       For external data: Submitter SHOULD annotate when the information is available.
      </td>
    </tr>
    <tr>
      <th>Value</th>
        <td><code>String</code>. 
         Examples: DaXi, Mantis.
        </td>
    </tr>
</tbody></table>
<br>

### instrument_version
<table><tbody>
    <tr>
      <th>Key</th>
      <td>instrument_version</td>
    </tr>
    <tr>
      <th>Description</th>
      <td>instrument_name + instrument_version should correspond to a unique description similar to [this](https://github.com/AllenNeuralDynamics/aind-data-schema/blob/dev/examples/aind_smartspim_instrument.py).</td>
    </tr>
    <tr>
      <th>Annotator</th>
      <td>Submitter SHOULD annotate when the information is available.
      </td>
    </tr>
    <tr>
      <th>Value</th>
        <td><code>String</code>. 
        </td>
    </tr>
</tbody></table>
<br>

## Acquisition
Metadata describing the devices and hardware components active during image acquisition, along with their specific configurations and settings. This information supports experimental reproducibility, enables accurate interpretation of imaging data, and documents the source and characteristics of each channel.

### acquisition_software
<table><tbody>
    <tr>
      <th>Key</th>
      <td>acquisition_software</td>
    </tr>
    <tr>
      <th>Description</th>
      <td>List exact versions. For custom code that has been deposited into a community repository, provide accession details.</td>
    </tr>
    <tr>
      <th>Annotator</th>
      <td>Submitter MUST annotate.</td>
    </tr>
    <tr>
      <th>Value</th>
        <td><code>String</code>. 
        </td>
    </tr>
</tbody></table>
<br>

## Channel description
Metadata describing the channel information. <br>

### channel_name
<table><tbody>
    <tr>
      <th>Key</th>
      <td>channel_name</td>
    </tr>
    <tr>
      <th>Description</th>
      <td>Name of the imaging channel.</td>
    </tr>
    <tr>
      <th>Annotator</th>
      <td>Submitter MUST annotate.</td>
    </tr>
    <tr>
      <th>Value</th>
        <td><code>List[String]</code>. 
        </td>
    </tr>
</tbody></table>
<br>

### channel_source
<table><tbody>
    <tr>
      <th>Key</th>
      <td>channel_source</td>
    </tr>
    <tr>
      <th>Description</th>
      <td>Source or method used to generate this channel.</td>
    </tr>
    <tr>
      <th>Annotator</th>
      <td>Submitter MUST annotate.</td>
    </tr>
    <tr>
      <th>Value</th>
        <td><code>List[String]</code>. Channel sources that are direct outputs of the instrument MUST be annotated with the value "raw". 
        </td>
    </tr>
</tbody></table>
<br>

### intended_measurement
<table><tbody>
    <tr>
      <th>Key</th>
      <td>intended_measurement</td>
    </tr>
    <tr>
      <th>Description</th>
      <td>What this channel is intended to measure.</td>
    </tr>
    <tr>
      <th>Annotator</th>
      <td>Submitter MUST annotate.</td>
    </tr>
    <tr>
      <th>Value</th>
        <td><code>List[String]</code>. 
        </td>
    </tr>
</tbody></table>
<br>

OPTIONAL: Follow [OMERO metadata specification](https://ngff.openmicroscopy.org/latest/#omero-md).
