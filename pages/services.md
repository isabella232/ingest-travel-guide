# Ingest Services
The services of the Ingest component broken down into self-contained functions or "cells".

Please see the [Design Philosophy](../design/#design-philosophy) for an explaination for this approach.

Please see [Allocation](../allocation) for current responsibilites.

## Services and Cells
* __[1. Ingest Broker API](../components/ingest-broker-api)__
  + [1.1 Submission Create](../components/ingest-broker-api/#11-submission-create)
  + [1.2 Get Credentials](../components/ingest-broker-api/#12-get-credentials)
  + [1.3 Template Spreadsheet Download](../components/ingest-broker-api/#13-template-spreadsheet-download)
  + [1.4 Spreadsheet Upload](../components/ingest-broker-api/#14-spreadsheet-upload)
  + [1.5 Metadata Create](../components/ingest-broker-api/#15-metadata-create)
  + [1.6 Metadata Update](../components/ingest-broker-api/#16-metadata-update)
  + [1.7 Metadata Delete](../components/ingest-broker-api/#17-metadata-delete)
  + [1.8 Validate Sample](../components/ingest-broker-api/#18-validate-sample)
  + [1.9 Complete Submission](../components/ingest-broker-api/#19-complete-submission)
  + [1.10 List All Submissions](../components/ingest-broker-api/#110-list-all-submissions)
  + [1.11 Get Submission Details](../components/ingest-broker-api/#111-get-submission-details)
  + [1.12 List Project for Submission](../components/ingest-broker-api/#112-list-project-for-submission)
  + [1.13 List Samples for Submission](../components/ingest-broker-api/#113-list-samples-for-submission)
  + [1.14 List Files for Submission](../components/ingest-broker-api/#114-list-files-for-submission)
  + [1.15 List Analyses for Submission](../components/ingest-broker-api/#115-list-analyses-for-submission)
  + [1.16 List Bundles for Submission](../components/ingest-broker-api/#116-list-bundles-for-submission)
* __[2. Ingest Broker](../components/ingest-broker)__
  + [2.1 Credentials Poller](../components/ingest-broker/#21-credentials-poller)
  + [2.2 Spreadsheet to JSON Converter](../components/ingest-broker/#22-spreadsheet-to-json-converter)
  + [2.3 Metadata JSON Collection Validator](../components/ingest-broker/#23-metadata-json-collection-validator)
  + [2.4 Metadata JSON Collection UUID Scheduler](../components/ingest-broker/#24-metadata-json-collection-uuid-scheduler)
  + [2.5 Metadata JSON UUID Assigner](../components/ingest-broker/#25-metadata-json-uuid-assigner)
  + [2.6 Metadata JSON Persister](../components/ingest-broker/#26-metadata-json-persister)
* __[3. Ingest Accessioner](../components/ingest-accessioner)__
  + [3.1 HCA Accessioner](../components/ingest-accessioner/#31-hca-accessioner)
* __[4. Ingest Validator](../components/ingest-validator)__
  + [4.1 Metadata Validator/s](../components/ingest-validator/#41-metadata-validators)
  + [4.2 FASTQ File Validator](../components/ingest-validator/#42-fastq-file-validator)
  + [4.3 Image File Validator](../components/ingest-validator/#43-image-file-validator)
* __[5. Ingest Archiver](../components/ingest-archiver)__
  + [5.1 HCA to USI Converter](../components/ingest-archiver/#51-hca-to-usi-converterhttpsgithubcomhumancellatlasingest-archiverblobmasterarchiverconverterpy)
  + [5.2 USI Submitter](../components/ingest-archiver/#52-usi-submitter)
  + [5.3 USI Poller](../components/ingest-archiver/#53-usi-poller)
  + [5.4 USI Accession Persister](../components/ingest-archiver/#54-usi-accession-persister)
* __[6. Ingest Exporter](../components/ingest-exporter)__
  + [6.1 Bundle Generator](../components/ingest-exporter/#61-bundle-generator)
  + [6.2 Bundle Stager](../components/ingest-exporter/#62-bundle-stager)
  + [6.3 Bundle Result](../components/ingest-exporter/#63-bundle-result)
  + [6.4 Cleanup](../components/ingest-exporter/#64-cleanup)
* __[7. Ingest Core](../components/ingest-core)__
  + [7.1 Ingest Core API](../components/ingest-core/#71-ingest-core-api)
  + [7.2 Persistence](../components/ingest-core/#73-state-management)
  + [7.3 State Management](../components/ingest-core/#73-state-management) 
* __[8. Ingest UI](../components/ingest-ui)__
  + [8.1 Action: Create Submission](../components/ingest-ui/#81-action-create-submission)
  + [8.2 Action: Download Spreadsheet](../components/ingest-ui/#82-action-download-spreadsheet)
  + [8.3 Action: Submit Spreadsheet](../components/ingest-ui/#83-action-submit-spreadsheet)
  + [8.4 Action: Complete Submission](../components/ingest-ui/#84-action-complete-submission)
  + [8.5 Action: Update Ontology in Sample](../components/ingest-ui/#85-action-update-ontology-in-sample)
  + [8.6 Display: Submission List](../components/ingest-ui/#86-display-submission-list)
  + [8.7 Display: Submission Details](../components/ingest-ui/#87-display-submission-details)
  + [8.8 Display: File Details](../components/ingest-ui/#88-display-file-details)
  + [8.9 Display: Credentials](../components/ingest-ui/#89-display-credentials)
  + [8.10 Display: Validation Errors](../components/ingest-ui/#810-display-validation-errors)
* __[9. Cross-Cutting Concerns](../components/cross-cutting-concerns)__
  + [9.1 Logging](../components/cross-cutting-concerns/#91-logging)
  + [9.2 Authentication](../components/cross-cutting-concerns/#92-authentication)
  + [9.3 Authorisation](../components/cross-cutting-concerns/#93-authorisation) 
