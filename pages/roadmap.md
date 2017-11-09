# Ingest Roadmap

## Key

###  Functionality
* X - Not Implemented
* M - Mock
* P - Prototype
* C - Complete

### Dependency
* v3 - For Metadata Schema Version 3
* v4 - For Metadata Schema Version 4
* US - Upload Service
* DS - Data Store (Blue Box)
* USI - EBI Universal Submission Interface

|Cell|Q3/17|M1|M2|M3|M4|M5|M6|M7|
|----|--|--|--|--|--|--|--|--|
|__[1. Ingest Broker API](../components/ingest-broker-api)__||
|[1.1 Submission Create](../components/ingest-broker-api/#11-submission-create)|x|C| | | | | | |
|[1.2 Get Credentials](../components/ingest-broker-api/#12-get-credentials)|x|C| | | | | | |
|[1.3 Template Spreadsheet Download](../components/ingest-broker-api/#13-template-spreadsheet-download)|x|C| | | | | | |
|[1.4 Spreadsheet Upload](../components/ingest-broker-api/#14-spreadsheet-upload)|x|C| | | | | | |
|[1.5 Metadata Create](../components/ingest-broker-api/#15-metadata-create)|x|C| | | | | | |
|[1.6 Metadata Update](../components/ingest-broker-api/#16-metadata-update)|x|P| | | | | | |
|[1.7 Metadata Delete](../components/ingest-broker-api/#17-metadata-delete)|x|x| | | | | | |
|[1.8 Validate Sample](../components/ingest-broker-api/#18-validate-sample)|x|P| | | | | | |
|[1.9 Complete Submission](../components/ingest-broker-api/#19-complete-submission)|x|C| | | | | | |
|[1.1x List All Submissions](../components/ingest-broker-api/#11x-list-all-submissions)|x|C| | | | | | |
|[1.11 Get Submission Details](../components/ingest-broker-api/#111-get-submission-details)|x|C| | | | | | |
|[1.12 List Project for Submission](../components/ingest-broker-api/#112-list-project-for-submission)|x|C| | | | | | |
|[1.13 List Samples for Submission](../components/ingest-broker-api/#113-list-samples-for-submission)|x|C| | | | | | |
|[1.14 List Files for Submission](../components/ingest-broker-api/#114-list-files-for-submission)|x|C| | | | | | |
|[1.15 List Analyses for Submission](../components/ingest-broker-api/#115-list-analyses-for-submission)|x|C| | | | | | |
|[1.16 List Bundles for Submission](../components/ingest-broker-api/#116-list-bundles-for-submission)|x|C| | | | | | |
|__[2. Ingest Broker](../components/ingest-broker)__||
|[2.1 Credentials Poller](../components/ingest-broker/##21-credentials-poller)|P|P US| | | | | | |
|[2.2 Spreadsheet to JSON Converter](../components/ingest-broker/##22-spreadsheet-to-json-converter)|P v3|F v4| | | | | | |
|[2.3 Metadata JSON Collection Validator](../components/ingest-broker/##23-metadata-json-collection-validator)|P v3|F v4 | | | | | | |
|[2.4 Metadata JSON Collection UUID Scheduler](../components/ingest-broker/##24-metadata-json-collection-uuid-scheduler)|x|F | | | | | | |
|[2.5 Metadata JSON UUID Assigner](../components/ingest-broker/##25-metadata-json-uuid-assigner)|P|C| | | | | | |
|[2.6 Metadata JSON Persister](../components/ingest-broker/##26-metadata-json-persister)|P|P| | | | | | |
|__[3. Ingest Accessioner](../components/ingest-accessioner)__| | | | | | | |
|[3.1 HCA Accessioner](../components/ingest-accessioner/#31-hca-accessioner)|M|P| | | | | | |
|__[4. Ingest Validator](../components/ingest-validator)__| | | | | | | |
|[4.1 Metadata Validator/s](../components/ingest-validator/#41-metadata-validators)|M|P v4| | | | | | |
|[4.2 FASTQ File Validator](../components/ingest-validator/#42-fastq-file-validator)|x|P| | | | | | |
|[4.3 Image File Validator](../components/ingest-validator/#43-image-file-validator)|x|x| | | | | | |
|__[5. Ingest Archiver](../components/ingest-archiver)__||
|[5.1 HCA to USI Converter](../components/ingest-archiver/#51-hca-to-usi-converterhttpsgithubcomhumancellatlasingest-archiverblobmasterarchiverconverterpy)|P v3|F v4,USI| | | | | | |
|[5.2 USI Submitter](../components/ingest-archiver/#52-usi-submitter)|x|C USI| | | | | | |
|[5.3 USI Poller](../components/ingest-archiver/#53-usi-poller)|x|C USI| | | | | | |
|[5.4 USI Accession Persister](../components/ingest-archiver/#54-usi-accession-persister)|x|P v4| | | | | | |
|__[6. Ingest Exporter](../components/ingest-exporter)__||
|[6.1 Bundle Generator](../components/ingest-exporter/#61-bundle-generator)|P v3|F v4| | | | | | |
|[6.2 Bundle Stager](../components/ingest-exporter/#62-bundle-stager)|P|P DS| | | | | | |
|[6.3 Bundle Result](../components/ingest-exporter/#63-bundle-result)|P|P DS| | | | | | |
|[6.4 Cleanup](../components/ingest-exporter/#64-cleanup)|P|C US| | | | | | |
|__[7. Ingest Core](../components/ingest-core)__||
|[7.1 Ingest Core API](../components/ingest-core/#71-ingest-core-api)|P|C| | | | | | |
|[7.2 Persistence](../components/ingest-core/#72-persistence)|P|C| | | | | | |
|[7.3 State Management](../components/ingest-core/#73-state-management)|P|C| | | | | | | 
|__[8. Ingest Broker UI](../components/ingest-broker-ui)__| | | | | | | |
|[8.1 Action: Create Submission](../components/ingest-broker-ui/#81-action-create-submission)|P|P| | | | | | |
|[8.2 Action: Download Spreadsheet](../components/ingest-broker-ui/#82-action-download-spreadsheet)|P|P| | | | | | |
|[8.3 Action: Submit Spreadsheet](../components/ingest-broker-ui/#83-action-submit-spreadsheet)|P|P| | | | | | |
|[8.4 Action: Complete Submission](../components/ingest-broker-ui/#84-action-complete-submission)|P|P| | | | | | |
|[8.5 Action: Update Ontology in Sample](../components/ingest-broker-ui/#85-action-update-ontology-in-sample)|x|P| | | | | | |
|[8.6 Display: Submission List](../components/ingest-broker-ui/#86-display-submission-list)|P|P| | | | | | |
|[8.7 Display: Submission Details](../components/ingest-broker-ui/#87-display-submission-details)|P|P| | | | | | |
|[8.8 Display: File Details](../components/ingest-broker-ui/#88-display-file-details)|P|P| | | | | | |
|[8.9 Display: Credentials](../components/ingest-broker-ui/#89-display-credentials)|P|P| | | | | | |
|[8.1x Display: Validation Errors](../components/ingest-broker-ui/#81x-display-validation-errors)|x|P| | | | | | |
|__[9. Cross Cutting Concerns](../components/cross-cutting-concerns)__||
|[9.1 Logging](../components/cross-cutting-concerns/#91-logging)|x|x|P| | | | | |
|[9.2 Authentication](../components/cross-cutting-concerns/#92-authentication)|x|P|P|| | | | | |  
|[9.3 Authorisation](../components/cross-cutting-concerns/#93-authorisation) |x|M|P|| | | | | |  
