# Cross-Modality Schema

Contact: brianraymor@chanzuckerberg.com

Document Status: _Approved_

Version: 1.1.0

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


## Descriptive Metadata

The following descriptive metadata MUST be associated with all "registered - sharing" datasets to ensure that <u><b>datasets can be found by searching for common experimental and biological characteristics of datasets</b></u>. This list is intentionally limited to metadata that SHOULD be annotated at the time data are generated. These metadata MUST be programmatically validated to ensure compliance. Additional metadata MAY be annotated at the discretion of data stewards.

## Required Ontologies

With the exception of Cellosaurus, ontology terms for metadata MUST use [OBO-format identifiers](http://www.obofoundry.org/id-policy.html), meaning a CURIE (prefixed identifier) of the form **Ontology:Identifier**. For example, [EFO:0000001](https://www.ebi.ac.uk/ols4/ontologies/efo/classes?obo_id=EFO%3A0000001) is a term in the Experimental Factor Ontology (EFO). Cellosaurus requires a prefixed identifier of the form **Ontology_Identifier** such as [CVCL_1P02](https://www.cellosaurus.org/CVCL_1P02).<br><br>
 If ontologies are missing required terms, then ontologists are responsive to New Term Requests [NTR] such as [[NTR] Version specific Visium assays](https://github.com/EBISPOT/efo/issues/2178) which was created for CELLxGENE Discover requirements.

 The following ontologies are referenced in this schema:

| Ontology | Prefix |
|:--|:--|
| [C. elegans Development Ontology] | WBls: |
| [C. elegans Gross Anatomy Ontology] | WBbt: |
| [Cell Ontology] | CL: |
| [Cellosaurus] | CVCL_ |
| [Drosophila Anatomy Ontology] | FBbt: |
| [Drosophila Development Ontology] | FBdv: |
| [Experimental Factor Ontology] | EFO: |
| [Gene Ontology] | GO: |
| [Human Developmental Stages] |  HsapDv: |
| [Mondo Disease Ontology] | MONDO: |
| [Mouse Developmental Stages]| MmusDv: |
| [NCBI organismal classification] |  NCBITaxon: |
| [Phenotype And Trait Ontology] | PATO: |
| [Uberon multi-species anatomy ontology] |  UBERON: |
| [Zebrafish Anatomy Ontology] | ZFA:<br>ZFS: |
| | |

[C. elegans Development Ontology]: https://obofoundry.org/ontology/wbls.html

[C. elegans Gross Anatomy Ontology]: https://obofoundry.org/ontology/wbbt.html

[Cell Ontology]: http://obofoundry.org/ontology/cl.html

[Cellosaurus]: https://www.cellosaurus.org/

[Drosophila Anatomy Ontology]: https://obofoundry.org/ontology/fbbt.html

[Drosophila Development Ontology]: https://obofoundry.org/ontology/fbdv.html

[Experimental Factor Ontology]: http://www.ebi.ac.uk/efo

[Gene Ontology]: https://geneontology.org/

[Human Ancestry Ontology]: http://www.obofoundry.org/ontology/hancestro.html

[Human Developmental Stages]: http://obofoundry.org/ontology/hsapdv.html

[Mondo Disease Ontology]: http://obofoundry.org/ontology/mondo.html

[Mouse Developmental Stages]: http://obofoundry.org/ontology/mmusdv.html

[NCBI organismal classification]: http://obofoundry.org/ontology/ncbitaxon.html

[Phenotype And Trait Ontology]: http://www.obofoundry.org/ontology/pato.html

[Uberon multi-species anatomy ontology]: http://www.obofoundry.org/ontology/uberon.html

[Zebrafish Anatomy Ontology]: https://obofoundry.org/ontology/zfa.html

## assay_ontology_term_id

<table><tbody>
    <tr>
      <th>Key</th>
      <td>assay_ontology_term_id</td>
    </tr>
    <tr>
      <th>Description</th>
      <td>Defines the assay that was used to create the dataset</td>
    </tr>
    <tr>
      <th>Annotator</th>
      <td>Submitter MUST annotate.</td>
    </tr>
    <tr>
      <th>Value</th>
        <td><code>List[String]</code>. The List element MUST be an <a href="https://www.ebi.ac.uk/ols4/ontologies/efo/">Experimental Factor Ontology (EFO)</a> term such as <code>“EFO:0022605”</code>.
        </td>
    </tr>
</tbody></table>
<br>

## assay

<table><tbody>
    <tr>
      <th>Key</th>
      <td>assay</td>
    </tr>
    <tr>
      <th>Annotator</th>
      <td>System MUST annotate.</td>
    </tr>
    <tr>
      <th>Value</th>
        <td><code>List[String]</code>. The List element MUST be the human-readable name assigned to the corresponding element in <code>assay_ontology_term_id</code>.
        </td>
    </tr>
</tbody></table>
<br>

## development_stage_ontology_term_id

<table><tbody>
    <tr>
      <th>Key</th>
      <td>development_stage_ontology_term_id</td>
    </tr>
    <tr>
      <th>Description</th>
      <td>Defines the development stage(s) of the patients or organisms from which assayed biosamples were derived</td>
    </tr>
    <tr>
      <th>Annotator</th>
      <td>Submiter MUST annotate.</td>
    </tr>
    <tr>
      <th>Value</th>
      <td>
        <code>List[String]</code><br><br>If corresponding <code>tissue_type</code> is <code>"cell line"</code>, the List element MUST be <code>"na"</code>.<br><br>
        If unavailable, the List element MUST be <code>"unknown"</code>.<br><br>
        <table>
          <thead>
            <tr>
              <th>For the corresponding<br><code>organism_ontology_term_id</code></th>
              <th>Value</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>
                <a href="https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A6239"><code>"NCBITaxon:6239"</code></a><br>for <i>Caenorhabditis elegans</i>
              </td>
              <td>
                The List element MUST be <a href="https://www.ebi.ac.uk/ols4/ontologies/wbls/classes?obo_id=WBls%3A0000669"><code>WBls:0000669</code></a> for <i>unfertilized egg Ce</i>,<br>the most accurate descendant of <a href="https://www.ebi.ac.uk/ols4/ontologies/wbls/classes?obo_id=WBls%3A0000803"><code>WBls:0000803</code></a><br>for <i>C. elegans life stage occurring during embryogenesis</i>, or<br>the most accurate descendant of <a href="https://www.ebi.ac.uk/ols4/ontologies/wbls/classes?obo_id=WBls%3A0000804"><code>WBls:0000804</code></a><br>for <i>C. elegans life stage occurring post embryogenesis</i> 
              </td>
            </tr>
            <tr>
              <td>
                <a href="https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A7955"><code>"NCBITaxon:7955"</code></a><br>for <i>Danio rerio</i>
              </td>
              <td>
                The List element MUST be the most accurate descendant of <a href="https://www.ebi.ac.uk/ols4/ontologies/zfs/classes?obo_id=ZFS%3A0100000"><code>ZFS:0100000</code></a><br>for <i>zebrafish stage</i> excluding <a href="https://www.ebi.ac.uk/ols4/ontologies/zfs/classes?obo_id=ZFS%3A0000000"><code>ZFS:0000000</code></a> for <i>Unknown</i>
              </td>
            </tr>
            <tr>
              <td>
                <a href="https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A7227"><code>"NCBITaxon:7227"</code></a><br>for <i>Drosophila melanogaster</i>
              </td>
              <td>
                The List element MUST be either the most accurate descendant of <a href="https://www.ebi.ac.uk/ols4/ontologies/fbdv/classes?obo_id=FBdv%3A00007014"><code>FBdv:00007014</code></a> <br>for <i>adult age in days</i> or the most accurate descendant of <a href="https://www.ebi.ac.uk/ols4/ontologies/fbdv/classes?obo_id=FBdv%3A00005259"><code>FBdv:00005259</code></a> <br>for <i>developmental stage</i> excluding <a href="https://www.ebi.ac.uk/ols4/ontologies/fbdv/classes?obo_id=FBdv%3A00007012"><code>FBdv:00007012</code></a> for <i>life stage</i>
              </td>
            </tr>
            <tr>
              <td>
                <a href="https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A9606"><code>"NCBITaxon:9606"</code></a><br>for <i>Homo sapiens</i>
              </td>
              <td>
                The List element MUST be the most accurate descendant of <a href="https://www.ebi.ac.uk/ols4/ontologies/hsapdv/classes?obo_id=HsapDv%3A0000001"><code>HsapDv:0000001</code></a><br>for <i>life cycle</i>
              </td>
            </tr>
            <tr>
              <td>
                <a href="https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A10090"><code>"NCBITaxon:10090"</code></a><br>for <i>Mus musculus</i> or<br>one of its descendants
              </td>
              <td>
                The List element MUST be the accurate descendant of <a href="https://www.ebi.ac.uk/ols4/ontologies/mmusdv/classes?obo_id=MmusDv%3A0000001"><code>MmusDv:0000001</code></a><br>for <i>life cycle</i>
              </td>
            </tr>
            <tr>
              <td>
              For all other organisms
              </td>
              <td>
              The List element MUST be the most accurate descendant of <a href="https://www.ebi.ac.uk/ols4/ontologies/uberon/classes?obo_id=UBERON%3A0000105"><code>UBERON:0000105</code></a> <br>for <i>life cycle stage</i>, excluding <a href="https://www.ebi.ac.uk/ols4/ontologies/uberon/classes?obo_id=UBERON%3A0000071"><code>UBERON:0000071</code></a> for <i>death stage</i>.
              </td>
            </tr>
          </tbody>
        </table>
      </td>
  </tr>
</tbody></table>
<br>

## development_stage

<table><tbody>
    <tr>
      <th>Key</th>
      <td>development_stage</td>
    </tr>
    <tr>
      <th>Annotator</th>
      <td>System MUST annotate.</td>
    </tr>
    <tr>
      <th>Value</th>
        <td><code>List[String]</code>. <br><br>The List element MUST be <code>"na"</code> if the value of <code>development_stage_ontology_term_id</code> is <code>"na"</code>.<br><br>
        The List element MUST be <code>"unknown"</code> if the value of <code>development_stage_ontology_term_id</code> is <code>"unknown"</code>.<br><br>Otherwise, the List element MUST be the human-readable name assigned to the corresponding element in <code>development_stage_ontology_term_id</code>.
        </td>
    </tr>
</tbody></table>
<br>

## disease_ontology_term_id

<table><tbody>
    <tr>
      <th>Key</th>
      <td>disease_ontology_term_id</td>
    </tr>
    <tr>
      <th>Description</th>
      <td>Defines the disease of the patients or organisms from which assayed biosamples were derived</td>
    </tr>
    <tr>
      <th>Annotator</th>
      <td>Submitter MUST annotate.</td>
    </tr>
    <tr>
      <th>Value</th>
        <td><code>List[String]</code>. The List element MUST be one of:<br>
        <ul>
          <li><a href="https://www.ebi.ac.uk/ols4/ontologies/pato/classes?obo_id=PATO%3A0000461"><code>"PATO:0000461"</code></a> for <i>normal</i> or <i>healthy</i>.</li>
          <li>the most accurate descendant of <a href="https://www.ebi.ac.uk/ols4/ontologies/mondo/classes?obo_id=MONDO%3A0000001"><code>"MONDO:0000001"</code></a> for <i>disease</i></li>
          <li><a href="https://www.ebi.ac.uk/ols4/ontologies/mondo/classes?obo_id=MONDO%3A0021178"><code>"MONDO:0021178"</code></a> for <i>injury</i> or <b>preferably</b> its most accurate descendant</li>
       </ul>
        </td>
    </tr>
</tbody></table>
<br>

## disease

<table><tbody>
    <tr>
      <th>Key</th>
      <td>disease</td>
    </tr>
    <tr>
      <th>Annotator</th>
      <td>System MUST annotate.</td>
    </tr>
    <tr>
      <th>Value</th>
        <td><code>List[String]</code>. The List element MUST be the human-readable name assigned to the corresponding element in <code>disease_ontology_term_id</code>.
        </td>
    </tr>
</tbody></table>
<br>

## organism_ontology_term_id

<table><tbody>
    <tr>
      <th>Key</th>
      <td>organism_ontology_term_id</td>
    </tr>
    <tr>
      <th>Description</th>
      <td>Defines the organism from which assayed biosamples were derived</td>
    </tr>
    <tr>
      <th>Annotator</th>
      <td>Submitter MUST annotate.</td>
    </tr>
    <tr>
      <th>Value</th>
        <td><code>List[String]</code>. The List element MUST be an <a href="https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon">NCBI organismal classification</a> term such as <code>"NCBITaxon:9606"</code>.
        </td>
          </tr>
          </tbody></table>
        </td>
    </tr>
</tbody></table>
<br>

## organism

<table><tbody>
    <tr>
      <th>Key</th>
      <td>organism</td>
    </tr>
    <tr>
      <th>Annotator</th>
      <td>System MUST annotate.</td>
    </tr>
    <tr>
      <th>Value</th>
        <td><code>List[String]</code>. The List element MUST be the human-readable name assigned to the corresponding element in <code>organism_ontology_term_id</code>.
        </td>
    </tr>
</tbody></table>
<br>

## tissue_ontology_term_id

<table><tbody>
    <tr>
      <th>Key</th>
      <td>tissue_ontology_term_id</td>
    </tr>
    <tr>
      <th>Description</th>
      <td>Defines the tissues from which assayed biosamples were derived</td>
    </tr>
    <tr>
      <th>Annotator</th>
      <td>Submitter MUST annotate.</td>
    </tr>
    <tr>
      <th>Value</th>
      <td>
        <code>List[String]</code><br><br>If the corresponding <code>tissue_type</code> is <code>"cell line"</code>, the List element MUST be a Cellosaurus term.<br><br>
        If the corresponding <code>tissue_type</code> is <code>"organelle"</code>, the List element MUST be a descendant of <a href="https://www.ebi.ac.uk/ols4/ontologies/efo/classes/http%253A%252F%252Fpurl.obolibrary.org%252Fobo%252FGO_0005575"><code>GO:0005575</code></a><br>for <i>cellular_component</i>.
<br><br>If the corresponding <code>tissue_type</code> is <code>"tissue"</code> or <code>"organoid"</code> then:<br><br>
        <table>
          <thead>
            <tr>
              <th>For the corresponding<br><code>organism_ontology_term_id</code></th>
              <th>Value</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>
                <a href="https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A6239"><code>"NCBITaxon:6239"</code></a><br>for <i>Caenorhabditis elegans</i>
              </td>
              <td>
                The List element MUST be either an UBERON term or the most accurate descendant<br>of <a href="https://www.ebi.ac.uk/ols4/ontologies/wbbt/classes?obo_id=WBBT%3A0005766"><code>WBbt:0005766</code></a> for <i>Anatomy</i> excluding <a href="https://www.ebi.ac.uk/ols4/ontologies/wbbt/classes?obo_id=WBBT%3A0007849"><code>WBbt:0007849</code></a> for <i>hermaphrodite</i>,<br><a href="https://www.ebi.ac.uk/ols4/ontologies/wbbt/classes?obo_id=WBBT%3A0007850"><code>WBbt:0007850</code></a> for <i>male</i>, <a href="https://www.ebi.ac.uk/ols4/ontologies/wbbt/classes?obo_id=WBBT%3A0008595"><code>WBbt:0008595</code></a> for <i>female</i>, <a href="https://www.ebi.ac.uk/ols4/ontologies/wbbt/classes?obo_id=WBBT%3A0004017"><code>WBbt:0004017</code></a> for <i>Cell</i><br>and its descendants, and <a href="https://www.ebi.ac.uk/ols4/ontologies/wbbt/classes?obo_id=WBBT%3A0006803"><code>WBbt:00006803</code></a> for <i>Nucleus</i> and its descendants
              </td>
            <tr>
              <td>
                <a href="https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A7955"><code>"NCBITaxon:7955"</code></a><br>for <i>Danio rerio</i>
              </td>
              <td>
                The List element MUST be either an UBERON term or the most accurate descendant<br>of <a href="https://www.ebi.ac.uk/ols4/ontologies/zfa/classes?obo_id=ZFA%3A0100000"><code>ZFA:0100000</code></a> for <i>zebrafish anatomical entity</i> excluding <a href="https://www.ebi.ac.uk/ols4/ontologies/zfa/classes?obo_id=ZFA%3A0001093"><code>ZFA:0001093</code></a> for <br><i>unspecified</i> and <a href="https://www.ebi.ac.uk/ols4/ontologies/zfa/classes?obo_id=ZFA%3A0009000"><code>ZFA:0009000</code></a> for <i>cell</i> and its descendants
              </td>
            </tr>
            <tr>
              <td>
                <a href="https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A7227"><code>"NCBITaxon:7227"</code></a><br>for <i>Drosophila melanogaster</i>
              </td>
              <td>
                The List element MUST be either an UBERON term or the most accurate descendant<br>of <a href="https://www.ebi.ac.uk/ols4/ontologies/fbbt/classes?obo_id=FBBT%3A10000000"><code>FBbt:10000000</code></a> for <i>anatomical entity</i> excluding <a href="https://www.ebi.ac.uk/ols4/ontologies/fbbt/classes?obo_id=FBbt%3A00007002"><code>FBbt:00007002</code></a> for <i>cell</i> and its<br>descendants
              </td>
            </tr>
            <tr>
              <td>
              For all other organisms
              </td>
              <td>
              The List element MUST be the most accurate descendant of <a href="https://www.ebi.ac.uk/ols4/ontologies/uberon/classes?obo_id=UBERON%3A0001062"><code>UBERON:0001062</code></a> <br>for <i>anatomical entity</i>
              </td>
            </tr>
          </tbody>
        </table><br>
        If the corresponding <code>tissue_type</code> is <code>"cell culture"</code>, the following <a href="https://www.ebi.ac.uk/ols4/ontologies/cl/">Cell Ontology (CL)</a> terms MUST NOT be used:
        <ul><li>
          <a href="https://www.ebi.ac.uk/ols4/ontologies/cl/terms?obo_id=CL:0000255"><code>"CL:0000255"</code></a> for <i>eukaryotic cell</i>
        </li>
        <li>
          <a href="https://www.ebi.ac.uk/ols4/ontologies/cl/terms?obo_id=CL:0000257"><code>"CL:0000257"</code></a> for <i>Eumycetozoan cell</i>
        </li>
        <li>
            <a href="https://www.ebi.ac.uk/ols4/ontologies/cl/terms?obo_id=CL:0000548"><code>"CL:0000548"</code></a> for <i>animal cell</i>
         </li></ul><br>
          <table>
        <thead><tr>
          <th>For the corresponding<br><code>organism_ontology_term_id</code></th>
          <th>Value</th>
        </tr></thead>
        <tbody>
          <tr>
            <td>
              <a href="https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A6239"><code>"NCBITaxon:6239"</code></a><br>for <i>Caenorhabditis elegans</i>
            </td>
            <td>
              The List element MUST be either a CL term or the most accurate descendant of <br><a href="https://www.ebi.ac.uk/ols4/ontologies/wbbt/classes?obo_id=WBbt%3A0004017"><code>WBbt:0004017</code></a> for <i>Cell</i> excluding <a href="https://www.ebi.ac.uk/ols4/ontologies/wbbt/classes?obo_id=WBbt%3A0006803"><code>WBbt:0006803</code></a> for <i>Nucleus</i> and its descendants
            </td>
          </tr>
          <tr>
            <td>
              <a href="https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A7955"><code>"NCBITaxon:7955"</code></a><br>for <i>Danio rerio</i>
            </td>
            <td>
              The List element MUST be either a CL term or the most accurate descendant of <br><a href="https://www.ebi.ac.uk/ols4/ontologies/zfa/classes?obo_id=ZFA%3A0009000"><code>ZFA:0009000</code></a> for <i>cell</i>
            </td>
          </tr>
          <tr>
            <td>
              <a href="https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A7227"><code>"NCBITaxon:7227"</code></a><br>for <i>Drosophila melanogaster</i>
            </td>
            <td>
              The List element MUST be either a CL term or the most accurate descendant of <br><a href="https://www.ebi.ac.uk/ols4/ontologies/fbbt/classes/http%253A%252F%252Fpurl.obolibrary.org%252Fobo%252FFBbt_00007002?lang=en"><code>FBbt:00007002</code></a> for <i>cell</i>
            </td>
          </tr>
          <tr>
            <td>
            For all other organisms
           </td>
            <td>
            The List element MUST be a CL term.
           </td>
         </tr>
        </tbody>
      </table>
      </td>
  </tr>
</tbody></table>
<br>

## tissue

<table><tbody>
    <tr>
      <th>Key</th>
      <td>tissue</td>
    </tr>
    <tr>
      <th>Annotator</th>
      <td>System MUST annotate.</td>
    </tr>
    <tr>
      <th>Value</th>
        <td><code>List[String]</code>. The List element MUST be the human-readable name assigned to the corresponding element in <code>tissue_ontology_term_id</code>.
        </td>
    </tr>
</tbody></table>
<br>

## tissue_type

<table><tbody>
    <tr>
      <th>Key</th>
      <td>tissue_type</td>
    </tr>
    <tr>
      <th>Annotator</th>
      <td>Submitter MUST annotate.</td>
    </tr>
    <tr>
    <tr>
      <th>Value</th>
        <td><code>List[String]</code>. The List element MUST be one of:
          <ul>
            <li><code>"cell culture"</code></li>
            <li><code>"cell line"</code></li>
            <li><code>"organelle"</code></li>
            <li><code>"organoid"</code></li>
            <li><code>"tissue"</code></li>
         </ul>
    </tr>
</tbody></table>
<br>

## Appendix A. Changelog

### schema v1.1.0
* Required Ontologies
  * Added requirements for prefixed ontology identifiers to address the Cellosaurus exception
  * Added Cellosaurus
  * Added Gene Ontology
* development_stage_ontology_term_id
  * Require <code>"na"</code> when the corresponding <code>tissue_type</code> is <code>"cell line"</code>
* development_stage
  * Require <code>"na"</code> when the corresponding <code>development_stage__ontology_term_id</code> is <code>"na"</code>
* tissue_ontology_term_id
  * Require a Cellosaurus term identifier when the corresponding <code>tissue_type</code> is <code>"cell line"</code>
  * Require a descendant of <code>GO:0005575</code></a> for <i>cellular_component</i> when the corresponding <code>tissue_type</code> is <code>"organelle"</code>
* tissue_type
  * Added <code>"cell line"</code>
  * Added <code>"organelle"</code>


### schema v1.0.0

* Published minimal set of metadata requirements