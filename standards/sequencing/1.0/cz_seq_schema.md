# Sequencing Data and Metadata Schema

Contact: [joan.wong@czbiohub.org](mailto:joan.wong@czbiohub.org)

Document Status: *Draft*

Version: 1.0.0  (follows [Semantic Versioning](https://semver.org/))

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED" "MAY", and "OPTIONAL" in this document are to be interpreted as described in [BCP 14](https://tools.ietf.org/html/bcp14), [RFC2119](https://www.rfc-editor.org/rfc/rfc2119.txt), and [RFC8174](https://www.rfc-editor.org/rfc/rfc8174.txt) when, and only when, they appear in all capitals, as shown here.

---

## Background
Sequencing-based profiling of biological conditions plays a crucial role in many flagship projects in the CZ ecosystem, generating rich datasets that support both primary research and secondary applications such as cross-study multi-omic analysis and AI-driven biological model training. To maximize the utility and reusability of sequencing datasets, this document outlines the sequencing data and metadata standards used across the CZ ecosystem to promote consistency, interoperability, and long-term value.


## I. Key Terms
Definitions of terms used throughout this schema:
1. **Sample:** biological material collected from a donor or source organism, from which assays are performed
2. **Dataset:** file(s) generated from a <span style="text-decoration:underline;">single sequencing run</span>, representing the raw data output from the sequencer, which may include multiple files corresponding to different lanes, read pairs, or libraries multiplexed in the same run
3. **Raw data:** unprocessed output from the sequencing platform (typically FASTQ files)
4. **Assay:** laboratory method or protocol used to generate data from a sample
5. **Sequencing instrument:** hardware device used to perform sequencing
6. **Ontology term**: a standardized identifier and label used to define biological or experimental concepts

## II. Sample-level Metadata
Sample-level metadata describes the biological source and context of the data, providing the necessary information to find, group, and interpret samples across experiments and platforms. <span style="text-decoration:underline;">**Cross-modality metadata**</span> applies across all data types in the CZ ecosystem, including imaging, mass spectrometry, and sequencing. This includes information about the assay used, the developmental stage, organism, tissue, tissue type, and disease context. These fields must be annotated consistently during sample registration and remain stable throughout downstream processing. <span style="text-decoration:underline;">**Sequencing metadata**</span> captures general technical parameters required to interpret, reproduce, and process datasets from all sequencing runs, while <span style="text-decoration:underline;">assay-specific metadata</span> captures details that are unique to certain protocols such as 10x Genomics.

### Cross-Modality Metadata Requirements
(See [full guidance](https://github.com/chanzuckerberg/data-guidance/blob/main/standards/cross-modality/1.0.0/schema.md).)

#### assay_ontology_term_id
<table>
  <tr>
   <td><strong>Key</strong>
   </td>
   <td>assay_ontology_term_id
   </td>
  </tr>
  <tr>
   <td><strong>Description</strong>
   </td>
   <td>Assay that was used to create the dataset
   </td>
  </tr>
  <tr>
   <td><strong>Annotator</strong>
   </td>
   <td>Submitter MUST annotate.
   </td>
  </tr>
  <tr>
   <td><strong>Value</strong>
   </td>
   <td>List[String]. A List element MUST be an <a href="https://www.ebi.ac.uk/ols4/ontologies/efo">Experimental Factor Ontology</a> (EFO) term such as <code>"EFO:0022605"</code>.
   </td>
  </tr>
</table>

#### development_stage_ontology_term_id

<table>
  <tr>
   <td><strong>Key</strong>
   </td>
   <td colspan="2" >development_stage_ontology_term_id
   </td>
  </tr>
  <tr>
   <td><strong>Description</strong>
   </td>
   <td colspan="2" >Development stage(s) of the patients or organisms from which assayed biosamples were derived
   </td>
  </tr>
  <tr>
   <td><strong>Annotator</strong>
   </td>
   <td colspan="2" >Submitter MUST annotate.
   </td>
  </tr>
  <tr>
   <td><strong>Value</strong>
   </td>
   <td colspan="2" >List[String]. If unavailable, then the List element MUST be "unknown".

<table>
  <tr>
   <td><strong>For <code>organism_ontology_term_id</code></strong>
   </td>
   <td><strong>Value</strong>
   </td>
  </tr>
  <tr>
   <td><code><a href="https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A6239">"NCBITaxon:6239"</a></code> for <em>Caenorhabditis elegans</em>
   </td>
   <td>A List element MUST be <code><a href="https://www.ebi.ac.uk/ols4/ontologies/wbls/classes?obo_id=WBls%3A0000669">WBls:0000669</a></code> for <em>unfertilized egg Ce</em>, the most accurate descendant of <code><a href="https://www.ebi.ac.uk/ols4/ontologies/wbls/classes?obo_id=WBls%3A0000803">WBls:0000803</a></code> for <em>C. elegans life stage occurring during embryogenesis</em>, or the most accurate descendant of <code><a href="https://www.ebi.ac.uk/ols4/ontologies/wbls/classes?obo_id=WBls%3A0000804">WBls:0000804</a></code> for <em>C. elegans life stage occurring post-embryogenesis</em>.
   </td>
  </tr>
  <tr>
   <td><code><a href="https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A7955">"NCBITaxon:7955"</a></code> for <em>Danio rerio</em>
   </td>
   <td>A List element MUST be the most accurate descendant of <code><a href="https://www.ebi.ac.uk/ols4/ontologies/zfs/classes?obo_id=ZFS%3A0100000">ZFS:0100000</a></code> for <em>zebrafish stage</em> excluding <code><a href="https://www.ebi.ac.uk/ols4/ontologies/zfs/classes?obo_id=ZFS%3A0000000">ZFS:0000000</a></code> for <em>Unknown</em>.
   </td>
  </tr>
  <tr>
   <td><code><a href="https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A7227">"NCBITaxon:7227"</a></code> for <em>Drosophila melanogaster</em>
   </td>
   <td>A List element MUST be either the most accurate descendant of <code><a href="https://www.ebi.ac.uk/ols4/ontologies/fbdv/classes?obo_id=FBdv%3A00007014">FBdv:00007014</a></code> for <em>adult age in days</em> or the most accurate descendant of <code><a href="https://www.ebi.ac.uk/ols4/ontologies/fbdv/classes?obo_id=FBdv%3A00005259">FBdv:00005259</a></code> for <em>developmental stage</em> excluding <code><a href="https://www.ebi.ac.uk/ols4/ontologies/fbdv/classes?obo_id=FBdv%3A00007012">FBdv:00007012</a></code> for <em>life stage</em>.
   </td>
  </tr>
  <tr>
   <td><code><a href="https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A9606">"NCBITaxon:9606"</a></code> for <em>Homo sapiens</em>
   </td>
   <td>A List element MUST be the most accurate descendant of <code><a href="https://www.ebi.ac.uk/ols4/ontologies/hsapdv/classes?obo_id=HsapDv%3A0000001">HsapDv:0000001</a></code> for <em>life cycle</em>.
   </td>
  </tr>
  <tr>
   <td><code><a href="https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A10090">"NCBITaxon:10090"</a></code> for <em>Mus musculus</em> or one of its descendants
   </td>
   <td>A List element MUST be the accurate descendant of <code><a href="https://www.ebi.ac.uk/ols4/ontologies/mmusdv/classes?obo_id=MmusDv%3A0000001">MmusDv:0000001</a></code> for <em>life cycle</em>.
   </td>
  </tr>
</table>

For all other organisms, a List element MUST be the most accurate descendant of <code>[UBERON:0000105](https://www.ebi.ac.uk/ols4/ontologies/uberon/classes?obo_id=UBERON%3A0000105)</code> for *life cycle stage*, excluding <code>[UBERON:0000071](https://www.ebi.ac.uk/ols4/ontologies/uberon/classes?obo_id=UBERON%3A0000071)</code> for *death stage*.

   </td>
  </tr>
</table>

#### disease_ontology_term_id

<table>
  <tr>
   <td><strong>Key</strong>
   </td>
   <td>disease_ontology_term_id
   </td>
  </tr>
  <tr>
   <td><strong>Description</strong>
   </td>
   <td>Disease of the patients or organisms from which assayed biosamples were derived
   </td>
  </tr>
  <tr>
   <td><strong>Annotator</strong>
   </td>
   <td>Submitter MUST annotate.
   </td>
  </tr>
  <tr>
   <td><strong>Value</strong>
   </td>
   <td>List[String]. A List element MUST be one of:
<ul>

<li><code><a href="https://www.ebi.ac.uk/ols4/ontologies/pato/classes?obo_id=PATO%3A0000461">"PATO:0000461"</a></code> for <em>normal</em> or <em>healthy</em>

<li>the most accurate descendant of <code><a href="https://www.ebi.ac.uk/ols4/ontologies/mondo/classes?obo_id=MONDO%3A0000001">"MONDO:0000001"</a></code> for <em>disease</em></li>

<li><code><a href="https://www.ebi.ac.uk/ols4/ontologies/mondo/classes?obo_id=MONDO%3A0021178">"MONDO:0021178"</a></code> for <em>injury</em> or <strong>preferably</strong> its most accurate descendant.
</ul>
   </td>
  </tr>
</table>

#### organism_ontology_term_id

<table>
  <tr>
   <td><strong>Key</strong>
   </td>
   <td>organism_ontology_term_id
   </td>
  </tr>
  <tr>
   <td><strong>Description</strong>
   </td>
   <td>Organism from which assayed biosamples were derived
   </td>
  </tr>
  <tr>
   <td><strong>Annotator</strong>
   </td>
   <td>Submitter MUST annotate.
   </td>
  </tr>
  <tr>
   <td><strong>Value</strong>
   </td>
   <td>List[String]. A List element MUST be an<a href="https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon"> NCBI organismal classification</a> term such as <code>"NCBITaxon:9606"</code>.
   </td>
  </tr>
</table>

For registration, there MUST be a one-to-one mapping between the List of tissue_ontology_term_id(s) and the List of tissue_type(s). For example, tissue_type[0] MUST be the tissue type for tissue_ontology_term_id[0]. In the Discover API, this is modeled as:

     'tissue': [{'label': 'spleen',
        'ontology_term_id': 'UBERON:0002106',
        'tissue_type': 'tissue'}]

#### tissue_ontology_term_id

<table>
  <tr>
   <td><strong>Key</strong>
   </td>
   <td>tissue_ontology_term_id
   </td>
  </tr>
  <tr>
   <td><strong>Description</strong>
   </td>
   <td>Tissues from which assayed biosamples were derived
   </td>
  </tr>
  <tr>
   <td><strong>Annotator</strong>
   </td>
   <td>Submitter MUST annotate.
   </td>
  </tr>
  <tr>
   <td><strong>Value</strong>
   </td>
   <td>List[String]. If the corresponding tissue_type is <code>"tissue"</code> or <code>"organoid"</code> then:

<table>
  <tr>
   <td><strong>For <code>organism_ontology_term_id</code></strong>
   </td>
   <td><strong>Value</strong>
   </td>
  </tr>
  <tr>
   <td><code><a href="https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A6239">"NCBITaxon:6239"</a></code> for <em>Caenorhabditis elegans</em>
   </td>
   <td>A List element MUST be either an UBERON term or the most accurate descendant of <code><a href="https://www.ebi.ac.uk/ols4/ontologies/wbbt/classes?obo_id=WBBT%3A0005766">WBbt:0005766</a></code> for <em>anatomy</em> excluding <code><a href="https://www.ebi.ac.uk/ols4/ontologies/wbbt/classes?obo_id=WBBT%3A0007849">WBbt:0007849</a></code> for <em>hermaphrodite</em>,<code><a href="https://www.ebi.ac.uk/ols4/ontologies/wbbt/classes?obo_id=WBBT%3A0007850">WBbt:0007850</a></code> for <em>male</em>,<code><a href="https://www.ebi.ac.uk/ols4/ontologies/wbbt/classes?obo_id=WBBT%3A0008595">WBbt:0008595</a></code> for <em>female</em>,<code><a href="https://www.ebi.ac.uk/ols4/ontologies/wbbt/classes?obo_id=WBBT%3A0004017">WBbt:0004017</a></code> for <em>cell</em> and its descendants, and <code><a href="https://www.ebi.ac.uk/ols4/ontologies/wbbt/classes?obo_id=WBBT%3A0006803">WBbt:00006803</a></code> for <em>nucleus</em> and its descendants.
   </td>
  </tr>
  <tr>
   <td><code><a href="https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A7955">"NCBITaxon:7955"</a></code> for <em>Danio rerio</em>
   </td>
   <td>A List element MUST be either an UBERON term or the most accurate descendant of <code><a href="https://www.ebi.ac.uk/ols4/ontologies/zfa/classes?obo_id=ZFA%3A0100000">ZFA:0100000</a></code> for <em>zebrafish anatomical entity</em> excluding <code><a href="https://www.ebi.ac.uk/ols4/ontologies/zfa/classes?obo_id=ZFA%3A0001093">ZFA:0001093</a></code> for <em>unspecified</em> and <code><a href="https://www.ebi.ac.uk/ols4/ontologies/zfa/classes?obo_id=ZFA%3A0009000">ZFA:0009000</a></code> for <em>cell</em> and its descendants.
   </td>
  </tr>
  <tr>
   <td><code><a href="https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A7227">"NCBITaxon:7227"</a></code> for <em>Drosophila melanogaster</em>
   </td>
   <td>A List element MUST be either an UBERON term or the most accurate descendant of <code><a href="https://www.ebi.ac.uk/ols4/ontologies/fbbt/classes?obo_id=FBBT%3A10000000">FBbt:10000000</a></code> for <em>anatomical entity</em> excluding <code><a href="https://www.ebi.ac.uk/ols4/ontologies/fbbt/classes?obo_id=FBbt%3A00007002">FBbt:00007002</a></code> for <em>cell</em> and its descendants.
   </td>
  </tr>
</table>

For all other organisms, a List element MUST be the most accurate descendant of <code>[UBERON:0001062](https://www.ebi.ac.uk/ols4/ontologies/uberon/classes?obo_id=UBERON%3A0001062)</code> for *anatomical entity*.

If the corresponding tissue_type is `"cell culture"`, the following [Cell Ontology](https://www.ebi.ac.uk/ols4/ontologies/cl) (CL) terms MUST NOT be used:

* <code>["CL:0000255"](https://www.ebi.ac.uk/ols4/ontologies/cl/terms?obo_id=CL:0000255)</code> for *eukaryotic cell*
* <code>["CL:0000257"](https://www.ebi.ac.uk/ols4/ontologies/cl/terms?obo_id=CL:0000257)</code> for *Eumycetozoan cell*
* <code>["CL:0000548"](https://www.ebi.ac.uk/ols4/ontologies/cl/terms?obo_id=CL:0000548)</code> for *animal cell*

<table>
  <tr>
   <td>
<strong>For <code>organism_ontology_term_id</code></strong>
   </td>
   <td><strong>Value</strong>
   </td>
  </tr>
  <tr>
   <td><code><a href="https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A6239">"NCBITaxon:6239"</a></code> for <em>Caenorhabditis elegans</em>
   </td>
   <td>A List element MUST be either a CL term or the most accurate descendant of <code><a href="https://www.ebi.ac.uk/ols4/ontologies/wbbt/classes?obo_id=WBbt%3A0004017">WBbt:0004017</a></code> for <em>cell</em> excluding <code><a href="https://www.ebi.ac.uk/ols4/ontologies/wbbt/classes?obo_id=WBbt%3A0006803">WBbt:0006803</a></code> for <em>nucleus</em> and its descendants.
   </td>
  </tr>
  <tr>
   <td><code><a href="https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A7955">"NCBITaxon:7955"</a></code> for
<em>Danio rerio</em>
   </td>
   <td>A List element MUST be either a CL term or the most accurate descendant of <code><a href="https://www.ebi.ac.uk/ols4/ontologies/zfa/classes?obo_id=ZFA%3A0009000">ZFA:0009000</a></code> for <em>cell</em>.
   </td>
  </tr>
  <tr>
   <td><code><a href="https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A7227">"NCBITaxon:7227"</a></code> for <em>Drosophila melanogaster</em>
   </td>
   <td>A List element MUST be either a CL term or the most accurate descendant of <code><a href="https://www.ebi.ac.uk/ols4/ontologies/fbbt/classes/http%253A%252F%252Fpurl.obolibrary.org%252Fobo%252FFBbt_00007002?lang=en">FBbt:00007002</a></code> for <em>cell</em>.
   </td>
  </tr>
</table>

Otherwise, for all other organisms, a List element MUST be a CL term.

   </td>
  </tr>
</table>

#### tissue_type

<table>
  <tr>
   <td><strong>Key</strong>
   </td>
   <td>tissue_type
   </td>
  </tr>
  <tr>
   <td><strong>Description</strong>
   </td>
   <td>Type of tissue from which assayed biosamples were derived
   </td>
  </tr>
  <tr>
   <td><strong>Annotator</strong>
   </td>
   <td>Submitter MUST annotate.
   </td>
  </tr>
  <tr>
   <td><strong>Value</strong>
   </td>
   <td>List[String]. A List element MUST be one of <code>"tissue"</code>, <code>"organoid"</code>, or <code>"cell culture"</code>.
   </td>
  </tr>
</table>

In addition, all datasets MUST be programmatically annotated with human-readable metadata fields containing human-readable names assigned to the term identifiers by its ontology. For example, if assay_ontology_term_id[0] is <code>"EFO:0022605"</code>, then assay[0] MUST be <code>"10x 5' v3"</code>.

#### assay

<table>
  <tr>
   <td><strong>Key</strong>
   </td>
   <td>assay
   </td>
  </tr>
  <tr>
   <td><strong>Value</strong>
   </td>
   <td>List[String]. A List element MUST be the human-readable name assigned to the corresponding element in <code>assay_ontology_term_id</code>.
   </td>
  </tr>
</table>

#### development_stage

<table>
  <tr>
   <td><strong>Key</strong>
   </td>
   <td>development_stage
   </td>
  </tr>
  <tr>
   <td><strong>Value</strong>
   </td>
   <td>List[String]. A List element MUST be <code>"unknown"</code> if the corresponding element in <code>development_stage_ontology_term_id</code> is <code>"unknown"</code>; otherwise, it MUST be the human-readable name assigned to the corresponding element in <code>development_stage_ontology_term_id</code>.
   </td>
  </tr>
</table>

#### disease

<table>
  <tr>
   <td><strong>Key</strong>
   </td>
   <td>disease
   </td>
  </tr>
  <tr>
   <td><strong>Value</strong>
   </td>
   <td>List[String]. A List element MUST be the human-readable name assigned to the corresponding element in <code>disease_ontology_term_id</code>.
   </td>
  </tr>
</table>

#### organism

<table>
  <tr>
   <td><strong>Key</strong>
   </td>
   <td>organism
   </td>
  </tr>
  <tr>
   <td><strong>Value</strong>
   </td>
   <td>List[String]. A List element MUST be the human-readable name assigned to the corresponding element in <code>organism_ontology_term_id</code>.
   </td>
  </tr>
</table>

#### tissue

<table>
  <tr>
   <td><strong>Key</strong>
   </td>
   <td>tissue
   </td>
  </tr>
  <tr>
   <td><strong>Value</strong>
   </td>
   <td>List[String]. A List element MUST be the human-readable name assigned to the corresponding element in <code>tissue_ontology_term_id</code>.
   </td>
  </tr>
</table>

### Sequencing Metadata Requirements

The following requirements apply to all sequencing assays.

#### sequencing_instrument

<table>
  <tr>
   <td><strong>Key</strong>
   </td>
   <td>sequencing_instrument
   </td>
  </tr>
  <tr>
   <td><strong>Description</strong>
   </td>
   <td>Name of the technology platform and instrument used for sequencing
   </td>
  </tr>
  <tr>
   <td><strong>Annotator</strong>
   </td>
   <td>Submitter MUST annotate.
   </td>
  </tr>
  <tr>
   <td><strong>Value</strong>
   </td>
   <td>String. MUST be an EFO term classified under <code>EFO:0002699</code> (e.g., <code>"Illumina NovaSeq X"</code>).
   </td>
  </tr>
</table>

#### sequencing_run_id

<table>
  <tr>
   <td><strong>Key</strong>
   </td>
   <td>sequencing_run_id
   </td>
  </tr>
  <tr>
   <td><strong>Description</strong>
   </td>
   <td>Unique identifier for the sequencing run from which the dataset was generated, typically automatically assigned from the instrument
   </td>
  </tr>
  <tr>
   <td><strong>Annotator</strong>
   </td>
   <td>Submitter MUST annotate. Use "unavailable" if no run-level information exists.
   </td>
  </tr>
  <tr>
   <td><strong>Value</strong>
   </td>
   <td>String. MUST be unique within each sequencing facility. Illumina run IDs MUST follow the format: <code>YYMMDD_InstrumentSerial#Run#_FlowCell#</code>
   </td>
  </tr>
</table>

#### file_type

<table>
  <tr>
   <td><strong>Key</strong>
   </td>
   <td>file_type
   </td>
  </tr>
  <tr>
   <td><strong>Description</strong>
   </td>
   <td>Type of file submitted
   </td>
  </tr>
  <tr>
   <td><strong>Annotator</strong>
   </td>
   <td>Submitter MUST annotate.
   </td>
  </tr>
  <tr>
   <td><strong>Value</strong>
   </td>
   <td>String. MUST be one of <code>"fastq"</code>, <code>"bam"</code>, <code>"h5"</code>, or <code>"h5ad"</code>.
   </td>
  </tr>
</table>

## III. Additional Assay-Specific Metadata Requirements

### 10x Genomics single-cell RNA sequencing

This section applies to 10x Genomics 3’ and 5’ single-cell RNA sequencing assays (EFO term: <code>[10x transcription profiling](http://www.ebi.ac.uk/efo/EFO_0030080)</code>). The typical data processing workflow for these assays begins with generating paired-end FASTQ files, followed by using software such as Cell Ranger to align reads to a reference genome, assign reads to transcripts using a gene annotation file, and produce the main output files: aligned reads (.bam) and gene expression count matrices (.h5). If BAM and/or HDF5 files are included, to ensure that those files are interpretable and reproducible, submitters MUST provide the <span style="text-decoration:underline;">reference genome</span>, <span style="text-decoration:underline;">gene annotation</span>, and <span style="text-decoration:underline;">processing software</span> used during analysis. If neither BAM nor HDF5 files are included, these properties MUST NOT be submitted. These requirements are described below.

#### reference_genome

<table>
  <tr>
   <td><strong>Key</strong>
   </td>
   <td>reference_genome
   </td>
  </tr>
  <tr>
   <td><strong>Description</strong>
   </td>
   <td>Genome name and version used for alignment or quantification
   </td>
  </tr>
  <tr>
   <td><strong>Annotator</strong>
   </td>
   <td>Submitter MUST annotate.
   </td>
  </tr>
  <tr>
   <td><strong>Value</strong>
   </td>
   <td>String. Ensembl genomes MUST be selected from a list of genome builds (see Appendix A).<br>
       NCBI assembly accessions MUST follow one of two formats:<br>
       <code>[GCA][ _ ][nine digits][.][version number]</code><br>
       <code>[GCF][ _ ][nine digits][.][version number]</code>
   </td>
  </tr>
</table>

#### reference_annotation

<table>
  <tr>
   <td><strong>Key</strong>
   </td>
   <td>reference_annotation
   </td>
  </tr>
  <tr>
   <td><strong>Description</strong>
   </td>
   <td>Gene annotation and version used for the reference genome build
   </td>
  </tr>
  <tr>
   <td><strong>Annotator</strong>
   </td>
   <td>Submitter MUST annotate.
   </td>
  </tr>
  <tr>
   <td><strong>Value</strong>
   </td>
   <td>String. For Ensembl, MUST follow the format <code>"Ensembl vN"</code>, where N is the Ensembl release number, with supported values ranging from 75 to 117. The value MUST correspond to the source and version for the selected <code>reference_genome</code>.
   </td>
  </tr>
</table>

#### alignment_software

<table>
  <tr>
   <td><strong>Key</strong>
   </td>
   <td>alignment_software
   </td>
  </tr>
  <tr>
   <td><strong>Description</strong>
   </td>
   <td>Name and version of the software used to generate aligned reads
   </td>
  </tr>
  <tr>
   <td><strong>Annotator</strong>
   </td>
   <td>Submitter MUST annotate.
   </td>
  </tr>
  <tr>
   <td><strong>Value</strong>
   </td>
   <td>String. MUST include software name and version.
<p>
<strong>Examples:</strong> <code>"Cell Ranger v7.1.0"</code>, <code>"STARsolo v3.1"</code>, <code>"Kallisto v0.51.1"</code>
   </td>
  </tr>
</table>

## IV. Required Ontologies
To standardize collected data, we will follow biologically relevant ontology standards.

<table>
  <tr>
   <td><strong>Ontology</strong>
   </td>
   <td><strong>OBO Prefix</strong>
   </td>
   <td><strong>Description</strong>
   </td>
  </tr>
  <tr>
   <td><a href="https://obofoundry.org/ontology/wbls.html">C. elegans Development Ontology</a>
   </td>
   <td>WBls
   </td>
   <td>Standardized ontology of <em>Caenorhabditis elegans</em> developmental stages
   </td>
  </tr>
  <tr>
   <td><a href="https://obofoundry.org/ontology/wbbt.html">C. elegans Gross Anatomy Ontology</a>
   </td>
   <td>WBbt
   </td>
   <td>Standardized ontology of <em>C. elegans </em>anatomical structures
   </td>
  </tr>
  <tr>
   <td><a href="http://obofoundry.org/ontology/cl.html">Cell Ontology</a>
   </td>
   <td>CL
   </td>
   <td>Standardized ontology of cell types across animal species
   </td>
  </tr>
  <tr>
   <td><a href="https://obofoundry.org/ontology/fbbt.html">Drosophila Anatomy Ontology</a>
   </td>
   <td>FBbt
   </td>
   <td>Standardized ontology of <em>Drosophila melanogaster</em> anatomical structures
   </td>
  </tr>
  <tr>
   <td><a href="https://obofoundry.org/ontology/fbdv.html">Drosophila Development Ontology</a>
   </td>
   <td>FBdv
   </td>
   <td>Standardized ontology of <em>D. melanogaster</em> developmental stages
   </td>
  </tr>
  <tr>
   <td><a href="http://www.ebi.ac.uk/efo">Experimental Factor Ontology</a>
   </td>
   <td>EFO
   </td>
   <td>Standardized ontology covering experimental variables, assays, sample attributes, and other related terms in biomedical research
   </td>
  </tr>
  <tr>
   <td><a href="http://obofoundry.org/ontology/hsapdv.html">Human Developmental Stages</a>
   </td>
   <td>HsapDv
   </td>
   <td>Standardized ontology of human developmental stages
   </td>
  </tr>
  <tr>
   <td><a href="http://obofoundry.org/ontology/mondo.html">Mondo Disease Ontology</a>
   </td>
   <td>MONDO
   </td>
   <td>Comprehensive ontology that integrates multiple disease resources into a unified, logically defined vocabulary for human and animal diseases.
   </td>
  </tr>
  <tr>
   <td><a href="http://obofoundry.org/ontology/mmusdv.html">Mouse Developmental Stages</a>
   </td>
   <td>MmusDv
   </td>
   <td>Standardized ontology of mouse developmental stages
   </td>
  </tr>
  <tr>
   <td><a href="http://obofoundry.org/ontology/ncbitaxon.html">NCBI organismal classification</a>
   </td>
   <td>NCBITaxon
   </td>
   <td>Standardized taxonomy of organisms
   </td>
  </tr>
  <tr>
   <td><a href="http://www.obofoundry.org/ontology/pato.html">Phenotype and Trait Ontology</a>
   </td>
   <td>PATO
   </td>
   <td>Standardized ontology of phenotypic qualities and traits designed to support the logical representation and cross-species integration of phenotype data
   </td>
  </tr>
  <tr>
   <td><a href="http://www.obofoundry.org/ontology/uberon.html">Uberon multi-species anatomy ontology</a>
   </td>
   <td>UBERON
   </td>
   <td>Cross-species ontology covering anatomical structures in animals. It provides a standardized framework for describing anatomical entities and their relationships across different species.
   </td>
  </tr>
  <tr>
   <td><a href="https://obofoundry.org/ontology/zfa.html">Zebrafish Anatomy Ontology</a>
   </td>
   <td>ZFA
<p>
ZFS
   </td>
   <td>Standardized ontology of <em>Danio rerio</em> anatomical structures
   </td>
  </tr>
</table>

## V. Required File Formats

This section describes the required file formats for sequencing outputs, including raw reads and processed results. FASTQ files require `sequencing_run_id`, `sequencing_platform`, and `file_type`. BAM, H5 and H5AD files require `reference_genome`, `reference_annotation`, `alignment_software`, and `file_type`.

#### FASTQ

<table>
  <tr>
   <td><strong>Key</strong>
   </td>
   <td>file_type (fastq)
   </td>
  </tr>
  <tr>
   <td><strong>Description</strong>
   </td>
   <td>Raw sequencing read data, including base calls and quality scores
   </td>
  </tr>
  <tr>
   <td><strong>Value</strong>
   </td>
   <td>String. File must be in standard FASTQ format, typically gzip-compressed (.fastq.gz). Must contain 4-line entries per read. For paired-end data, R1 and R2 files must be clearly labeled. Files should be parsable with standard tools such as FastQC, seqtk, or fastp.
   </td>
  </tr>
</table>

#### BAM

<table>
  <tr>
   <td><strong>Key</strong>
   </td>
   <td>file_type (bam)
   </td>
  </tr>
  <tr>
   <td><strong>Description</strong>
   </td>
   <td>Aligned sequence data mapped to a reference genome
   </td>
  </tr>
  <tr>
   <td><strong>Value</strong>
   </td>
   <td>String. File must be in BAM format (binary SAM) with optional .bai index file. File must be sorted and contain a header with reference genome and aligner metadata. For 10x data, cell barcode and UMI tags (e.g., CB, UB) should be included. Must be readable with samtools or equivalent tools.
   </td>
  </tr>
</table>

#### H5

<table>
  <tr>
   <td><strong>Key</strong>
   </td>
   <td>file_type (h5)
   </td>
  </tr>
  <tr>
   <td><strong>Description</strong>
   </td>
   <td>Hierarchical data file in HDF5 format used for structured outputs
   </td>
  </tr>
  <tr>
   <td><strong>Value</strong>
   </td>
   <td>String. File must be a valid HDF5 (<code>.h5</code>) file that complies with the <a href="https://docs.hdfgroup.org/archive/support/HDF5/doc1.8/index.html">HDF5</a> v1.8+ standard. The internal structure of the file MUST be documented and, if it follows a known format (e.g., kallisto output, loom), it MUST conform to the schema expected by that tool. The file MUST be readable using standard HDF5 utilities such as <code>h5py</code>, <code>h5dump</code>, or HDFView.
   </td>
  </tr>
</table>

#### H5AD

<table>
  <tr>
   <td><strong>Key</strong>
   </td>
   <td>file_type (h5ad)
   </td>
  </tr>
  <tr>
   <td><strong>Description</strong>
   </td>
   <td>Hierarchical data file in AnnData (<code>.h5ad</code>) format
   </td>
  </tr>
  <tr>
   <td><strong>Value</strong>
   </td>
   <td>String. File must be a valid <code>.h5ad</code> file, which uses the HDF5 format to store data according to the <a href="https://anndata.readthedocs.io">AnnData schema</a>. It MUST include the <code>X</code> matrix (expression data), along with <code>obs</code> (cell-level metadata) and <code>var</code> (gene-level metadata). The file MUST be readable using standard Python tools such as <code>scanpy.read_h5ad()</code> or <code>anndata.read_h5ad()</code>.
   </td>
  </tr>
</table>
<br>

----

## Appendix A

Accepted values for `reference_genome` and `reference_annotation` are listed in this section and apply only to Ensembl genome builds. For non-Ensembl genomes, values must follow the specified format rather than being selected from a predefined list.

<table>
  <tr>
   <th>Species
   </th>
   <th>reference_genome
   </th>
   <th>reference_annotation
   </th>
   <th>Source
   </th>
   <th>Genome Release Dates
   </th>
  </tr>
  <tr>
   <td><em>Homo sapiens</em>
   </td>
   <td>GRCh38.p14
   </td>
   <td>Ensembl v110-v117
   </td>
   <td><a href="https://ensembl.org/Homo_sapiens/Info/Index">Ensembl</a>
   </td>
   <td>Jul 2023
   </td>
  </tr>
  <tr>
   <td><em>Homo sapiens</em>
   </td>
   <td>GRCh38.p13
   </td>
   <td>Ensembl v98-v109
   </td>
   <td><a href="https://ensembl.org/Homo_sapiens/Info/Index">Ensembl</a>
   </td>
   <td>Sep 2019
   </td>
  </tr>
  <tr>
   <td><em>Homo sapiens</em>
   </td>
   <td>GRCh38.p12
   </td>
   <td>Ensembl v92-97
   </td>
   <td><a href="https://ensembl.org/Homo_sapiens/Info/Index">Ensembl</a>
   </td>
   <td>Apr 2018
   </td>
  </tr>
  <tr>
   <td><em>Homo sapiens</em>
   </td>
   <td>GRCh38.p10
   </td>
   <td>Ensembl v88-91
   </td>
   <td><a href="https://ensembl.org/Homo_sapiens/Info/Index">Ensembl</a>
   </td>
   <td>Mar 2017
   </td>
  </tr>
  <tr>
   <td><em>Homo sapiens</em>
   </td>
   <td>GRCh38.p7
   </td>
   <td>Ensembl v85-87
   </td>
   <td><a href="https://ensembl.org/Homo_sapiens/Info/Index">Ensembl</a>
   </td>
   <td>Jul 2016
   </td>
  </tr>
  <tr>
   <td><em>Homo sapiens</em>
   </td>
   <td>GRCh38.p5
   </td>
   <td>Ensembl v83-84
   </td>
   <td><a href="https://ensembl.org/Homo_sapiens/Info/Index">Ensembl</a>
   </td>
   <td>Dec 2015
   </td>
  </tr>
  <tr>
   <td><em>Homo sapiens</em>
   </td>
   <td>GRCh38.p3
   </td>
   <td>Ensembl v81-82
   </td>
   <td><a href="https://ensembl.org/Homo_sapiens/Info/Index">Ensembl</a>
   </td>
   <td>Jul 2015
   </td>
  </tr>
  <tr>
   <td><em>Homo sapiens</em>
   </td>
   <td>GRCh38.p2
   </td>
   <td>Ensembl v79-80
   </td>
   <td><a href="https://ensembl.org/Homo_sapiens/Info/Index">Ensembl</a>
   </td>
   <td>Mar 2015
   </td>
  </tr>
  <tr>
   <td><em>Homo sapiens</em>
   </td>
   <td>GRCh38
   </td>
   <td>Ensembl v76-78
   </td>
   <td><a href="https://oct2014.archive.ensembl.org/Homo_sapiens/Info/Index">Ensembl</a>
   </td>
   <td>Aug 2014
   </td>
  </tr>
  <tr>
   <td><em>Homo sapiens</em>
   </td>
   <td>GRCh37.p13
   </td>
   <td>Ensembl v75-v117
   </td>
   <td><a href="https://grch37.ensembl.org/index.html">Ensembl</a>
   </td>
   <td>Dec 2013
   </td>
  </tr>
  <tr>
   <td><em>Caenorhabditis elegans</em>
   </td>
   <td>WBcel235
   </td>
   <td>Ensembl v85-117
   </td>
   <td><a href="https://www.ensembl.org/Caenorhabditis_elegans/Info/Index">Ensembl</a>
   </td>
   <td>Jul 2016
   </td>
  </tr>
  <tr>
   <td><em>Callithrix jacchus</em>
   </td>
   <td>mCalJac1.pat.X
   </td>
   <td>Ensembl v105-v117
   </td>
   <td><a href="https://www.ensembl.org/Callithrix_jacchus/Info/Index">Ensembl</a>
   </td>
   <td>Dec 2021
   </td>
  </tr>
  <tr>
   <td><em>Danio rerio</em>
   </td>
   <td>GRCz11
   </td>
   <td>Ensembl v92–v117
   </td>
   <td><a href="https://ensembl.org/Danio_rerio/Info/Index">Ensembl</a>
   </td>
   <td>Apr 2018
   </td>
  </tr>
  <tr>
   <td><em>Danio rerio</em>
   </td>
   <td>GRCz10
   </td>
   <td>Ensembl v85-v91
   </td>
   <td><a href="https://may2015.archive.ensembl.org/Danio_rerio/Info/Index">Ensembl</a>
   </td>
   <td>Jul 2016
   </td>
  </tr>
  <tr>
   <td><em>Drosophila melanogaster</em>
   </td>
   <td>BDGP6.46
   </td>
   <td>Ensembl v110-v113
   </td>
   <td><a href="https://www.ensembl.org/Drosophila_melanogaster/Info/Index">Ensembl</a>
   </td>
   <td>Jul 2023
   </td>
  </tr>
  <tr>
   <td><em>Drosophila melanogaster</em>
   </td>
   <td>BDGP6.54
   </td>
   <td>Ensembl v114-v117
   </td>
   <td><a href="https://www.ensembl.org/Drosophila_melanogaster/Info/Index">Ensembl</a>
   </td>
   <td>May 2025
   </td>
  </tr>
  <tr>
   <td><em>Gorilla gorilla gorilla</em>
   </td>
   <td>gorGor4
   </td>
   <td>Ensembl v91-117
   </td>
   <td><a href="https://www.ensembl.org/Gorilla_gorilla/Info/Index">Ensembl</a>
   </td>
   <td>Dec 2017
   </td>
  </tr>
  <tr>
   <td><em>Macaca fascicularis</em>
   </td>
   <td>Macaca_fascicularis_6.0
   </td>
   <td>Ensembl v103-117
   </td>
   <td><a href="https://www.ensembl.org/Macaca_fascicularis/Info/Index">Ensembl</a>
   </td>
   <td>Feb 2021
   </td>
  </tr>
  <tr>
   <td><em>Macaca mulatta</em>
   </td>
   <td>Mmul_10
   </td>
   <td>Ensembl v98-117
   </td>
   <td><a href="https://www.ensembl.org/Macaca_mulatta/Info/Index">Ensembl</a>
   </td>
   <td>Sep 2019
   </td>
  </tr>
  <tr>
   <td><em>Microcebus murinus</em>
   </td>
   <td>Mmur_3.0
   </td>
   <td>Ensembl v91-117
   </td>
   <td><a href="https://www.ensembl.org/Microcebus_murinus/Info/Index">Ensembl</a>
   </td>
   <td>Dec 2017
   </td>
  </tr>
  <tr>
   <td><em>Mus musculus</em>
   </td>
   <td>GRCm39
   </td>
   <td>Ensembl v103–v117
   </td>
   <td><a href="https://ensembl.org/Mus_musculus/Info/Index">Ensembl</a>
   </td>
   <td>Feb 2021
   </td>
  </tr>
  <tr>
   <td><em>Mus musculus</em>
   </td>
   <td>GRCm38.p6
   </td>
   <td>Ensembl v92–v102
   </td>
   <td><a href="https://ensembl.org/Mus_musculus/Info/Index">Ensembl</a>
   </td>
   <td>Apr 2018
   </td>
  </tr>
  <tr>
   <td><em>Mus musculus</em>
   </td>
   <td>GRCm38.p5
   </td>
   <td>Ensembl v87–v91
   </td>
   <td><a href="https://ensembl.org/Mus_musculus/Info/Index">Ensembl</a>
   </td>
   <td>Dec 2016
   </td>
  </tr>
  <tr>
   <td><em>Oryctolagus cuniculus</em>
   </td>
   <td>OryCun2.0
   </td>
   <td>Ensembl v85-117
   </td>
   <td><a href="https://www.ensembl.org/Oryctolagus_cuniculus/Info/Index">Ensembl</a>
   </td>
   <td>Jul 2016
   </td>
  </tr>
  <tr>
   <td><em>Pan troglodytes</em>
   </td>
   <td>Pan_tro_3.0
   </td>
   <td>Ensembl v91-117
   </td>
   <td><a href="https://ensembl.org/Pan_troglodytes/Info/Index">Ensembl</a>
   </td>
   <td>Dec 2017
   </td>
  </tr>
  <tr>
   <td><em>Rattus norvegicus</em>
   </td>
   <td>GRCr8
   </td>
   <td>Ensembl v114-v117
   </td>
   <td><a href="https://ensembl.org/Rattus_norvegicus/Info/Index">Ensembl</a>
   </td>
   <td>May 2025
   </td>
  </tr>
  <tr>
   <td><em>Rattus norvegicus</em>
   </td>
   <td>mRatBN7.2
   </td>
   <td>Ensembl v105-113
   </td>
   <td><a href="https://ensembl.org/Rattus_norvegicus/Info/Index">Ensembl</a>
   </td>
   <td>Dec 2021
   </td>
  </tr>
  <tr>
   <td><em>SARS-CoV-2</em>
   </td>
   <td>ASM985889v3
   </td>
   <td>N/A
   </td>
   <td><a href="https://covid-19.ensembl.org/Sars_cov_2/Info/Index">Ensembl</a>
   </td>
   <td>Apr 2020
   </td>
  </tr>
  <tr>
   <td><em>Sus scrofa</em>
   </td>
   <td>Sscrofa11.1
   </td>
   <td>Ensembl v90-114
   </td>
   <td><a href="https://www.ensembl.org/Sus_scrofa/Info/Index">Ensembl</a>
   </td>
   <td>Aug 2017
   </td>
  </tr>
  <tr>
   <td>synthetic construct
   </td>
   <td>ThermoFisher ERCC RNA Spike-In Control Mixes (Cat # 4456740, 4456739)
   </td>
   <td>N/A
   </td>
   <td><a href="https://www.thermofisher.com/order/catalog/product/4456740#/4456740">ThermoFisher ERCC</a>
<p>
<a href="https://www.thermofisher.com/order/catalog/product/4456740#/4456740">Spike-Ins</a>
   </td>
   <td>
   </td>
  </tr>
</table>
