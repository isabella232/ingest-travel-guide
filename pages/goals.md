# Ingest Goals

## Q4 FY2017: Oct 1 - Dec 31 2017
The quarterly goals that follow are mapped to the service or function that implements the goal.

### 1. Implement first version of ingest validation service [HCA-263](https://www.ebi.ac.uk/panda/jira/browse/HCA-263)
#### a. Support validation that data files are correct fastq files
* [4.2 FASTQ File Validator](../components/ingest-validator/#42-fastq-file-validator)

#### b. Support full metadata validation against metadata specification JSON schema
* [4.1 Metadata Validator/s](../components/ingest-validator/#41-metadata-validators)

#### c. Support validation of relationships between entities
* [4.1 Metadata Validator/s](../components/ingest-validator/#41-metadata-validators)
* [2.3 Metadata JSON Collection Validator](../components/ingest-broker/##23-metadata-json-collection-validator)

#### d. Support validation of fields that require an ontology term for all metadata types
* [4.1 Metadata Validator/s](../components/ingest-validator/#41-metadata-validators)

### 2. Implement next version of ingest accessioning service [HCA-264](https://www.ebi.ac.uk/panda/jira/browse/HCA-264)
#### a. Support accessioning of sample entities with the EBI/NCBI Biosamples database.
* [5. Ingest Archiver](../components/ingest-archiver)

#### b.  Assignment of “user-friendly” HCA namespace accessions to relevant entities
* [3.1 HCA Accessioner](../components/ingest-accessioner/#31-hca-accessioner)

### 3. Implement first version of broker submission UI (For more details see MVP Doc) [HCA-265](https://www.ebi.ac.uk/panda/jira/browse/HCA-265)
#### a. Support template download, metadata upload, validation results and submission review based on broker UI mock-ups and on user interview feedback
* [1. Ingest Broker API](../components/ingest-broker-api)
* [8. Ingest Broker UI](../components/ingest-broker-ui)

#### b. Support ingestion of metadata content via XLSX format spreadsheet upload and include validation reports
* [1.3 Template Spreadsheet Download](../components/ingest-broker-api/#13-template-spreadsheet-download)
* [1.4 Spreadsheet Upload](../components/ingest-broker-api/#14-spreadsheet-upload)
* [2.2 Spreadsheet to JSON Converter](../components/ingest-broker/##22-spreadsheet-to-json-converter)

#### c. Interface to add or edit fields that require an ontology terms before completing a submission.
* [8.4 Action: Complete Submission](../components/ingest-broker-ui/#84-action-complete-submission)

### 4. Ingestion service stable and scales over exemplar datasets from pilot submitters (For more details see MVP Doc) [HCA-266](https://www.ebi.ac.uk/panda/jira/browse/HCA-266)
#### a. Ingest service integrated with datastore and secondary analysis pipeline for complete data flow through designated APIs.
* [7. Ingest Core](../components/ingest-core)

#### b. Ingest all existing, public, single cell sequencing datasets that adhere to HCA guidelines
#### c. Ingest a very large, newly generated dataset from at least one pilot submitter
#### d. Ingest supports export of a single bundle to datastore from multiple “piecemeal” submissions
* [6. Ingest Exporter](../components/ingest-exporter)

### 5. Ensure clean separation between content metadata schemas and ingest created/required metadata (EBI/UCSC) [HCA-267](https://www.ebi.ac.uk/panda/jira/browse/HCA-267)
#### a. Ingest API utilises pre- and post- ingest schemas for validation
* [4.1 Metadata Validator/s](../components/ingest-validator/#41-metadata-validators)

#### b. Ingest generates metadata schema compliant content including ingest-assigned fields (e.g. UUIDs, accessions, update dates)
* [6.1 Bundle Generator](../components/ingest-exporter/#61-bundle-generator)

### 6. Establish integrated test suite for ingest service and its interactions with other components, including authentication. [HCA-269](https://www.ebi.ac.uk/panda/jira/browse/HCA-269)
* [1. Ingest Broker API](../components/ingest-broker-api) 

### 7. Specifications stable; all APIs sufficiently documented to support integration and broker submission efforts [HCA-270](https://www.ebi.ac.uk/panda/jira/browse/HCA-270)
* [1. Ingest Broker API](../components/ingest-broker-api)
