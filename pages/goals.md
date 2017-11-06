# Goals

## Q4 FY2017: Oct 1 - Dec 31 2017

1. Implement first version of ingest validation service 
  a.  Support validation that data files are correct fastq files
  * b\.  Support full metadata validation against metadata specification JSON schema
  * c\.  Support validation of relationships between entities
  * d\.  Support validation of fields that require an ontology term for all metadata types
* 2\. Implement next version of ingest accessioning service 
  * a\. Support accessioning of sample entities with the EBI/NCBI Biosamples database.
  * b\.  Assignment of “user-friendly” HCA namespace accessions to relevant entities
* 3\. Implement first version of broker submission UI (For more details see MVP Doc)
  * a\. Support template download, metadata upload, validation results and submission review based on broker UI mock-ups and on user interview feedback
  * b\. Support ingestion of metadata content via XLSX format spreadsheet upload and include validation reports
  * c\. Interface to add or edit fields that require an ontology terms before completing a submission. 
* 4\. Ingestion service stable and scales over exemplar datasets from pilot submitters (For more details see MVP Doc)
  * a\. Ingest service integrated with datastore and secondary analysis pipeline for complete data flow through designated APIs.
  * b\. Ingest all existing, public, single cell sequencing datasets that adhere to HCA guidelines
  * c\. Ingest a very large, newly generated dataset from at least one pilot submitter
  * d\. Ingest supports export of a single bundle to datastore from multiple “piecemeal” submissions
* 5\. Ensure clean separation between content metadata schemas and ingest created/required metadata (EBI/UCSC)
  * a\. Ingest API utilises pre- and post- ingest schemas for validation
  * b\. Ingest generates metadata schema compliant content including ingest-assigned fields (e.g. UUIDs, accessions, update dates)
* 6\. Establish integrated test suite for ingest service and its interactions with other components, including authentication.
* 7\. Specifications stable; all APIs sufficiently documented to support integration and broker submission efforts
