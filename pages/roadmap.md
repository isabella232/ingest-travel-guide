# Ingest Roadmap

## Key
###  Functionality
* 0 - Not Implemented
* M - Mock
* P - Prototype
* C - Complete
### Dependency
* v3 - For Metadata Schema Version 3
* v4 - For Metadata Schema Version 4

|Cell|Q3/18|M1|M2|M3|M4|M5|M6|M7|
|----|--|--|--|--|--|--|--|--|
|_[1. Ingest Broker API](#1-ingest-broker-apihttpsgithubcomhumancellatlasingest-broker-api)_||
|[1.1 Submission Create](#11-submission-create)|0|F| | | | | | |
|[1.2 Get Credentials](#12-get-credentials)|0|F| | | | | | |
|[1.3 Template Spreadsheet Download](#13-template-spreadsheet-download)|0|F| | | | | | |
|[1.4 Spreadsheet Upload](#14-spreadsheet-upload)|0|F| | | | | | |
|[1.5 Metadata Create](#15-metadata-create)|0|F| | | | | | |
|[1.6 Metadata Update](#16-metadata-update)|0|P| | | | | | |
|[1.7 Metadata Delete](#17-metadata-delete)|0|0| | | | | | |
|[1.8 Validate Sample](#18-validate-sample)|0|P| | | | | | |
|[1.9 Complete Submission](#19-complete-submission)|0|F| | | | | | |
|[1.10 List All Submissions](#110-list-all-submissions)|0|F| | | | | | |
|[1.11 Get Submission Details](#111-get-submission-details)|0|F| | | | | | |
|[1.12 List Project for Submission](#112-list-project-for-submission)|0|F| | | | | | |
|[1.13 List Samples for Submission](#113-list-samples-for-submission)|0|F| | | | | | |
|[1.14 List Files for Submission](#114-list-files-for-submission)|0|F| | | | | | |
|[1.15 List Analyses for Submission](#115-list-analyses-for-submission)|0|F| | | | | | |
|[1.16 List Bundles for Submission](#116-list-bundles-for-submission)|0|F| | | | | | |
|_[2. Ingest Broker](#2-ingest-brokerhttpsgithubcomhumancellatlasingest-broker)_||
|[2.1 Credentials Poller](#21-credentials-poller)|P|P| | | | | | |
|[2.2 Spreadsheet to JSON Converter](#22-spreadsheet-to-json-converter)|P v3|F v4| | | | | | |
|[2.3 Metadata JSON Collection Validator](#23-metadata-json-collection-validator)|P v3|F v4 | | | | | | |
|[2.4 Metadata JSON Collection UUID Scheduler](#24-metadata-json-collection-uuid-scheduler)|0|F | | | | | | |
|[2.5 Metadata JSON UUID Assigner](#25-metadata-json-uuid-assigner)|P|F| | | | | | |
|[2.6 Metadata JSON Persister](#26-metadata-json-persister)|P|P| | | | | | |
|_[3. Ingest Accessioner](#3-ingest-accessionerhttpsgithubcomhumancellatlasingest-accessioner)_| | | | | | | |
|[3.1 HCA Accessioner](#31-hca-accessioner)|M|P| | | | | | |
|_[4. Ingest Validator](#4-ingest-validatorhttpsgithubcomhumancellatlasingest-validator)_| | | | | | | |
|[4.1 Metadata Validator/s](#41-metadata-validators)|M|P v4| | | | | | |
|[4.2 FASTQ File Validator](#42-fastq-file-validator)|0|P| | | | | | |
|_[5. Ingest Archiver](#5-ingest-archiverhttpsgithubcomhumancellatlasingest-archiver)_||
|[5.1 HCA to USI Converter](#51-hca-to-usi-converterhttpsgithubcomhumancellatlasingest-archiverblobmasterarchiverconverterpy)|P v3|F v4| | | | | | |
|[5.2 USI Submitter](#52-usi-submitter)|0|F| | | | | | |
|[5.3 USI Poller](#53-usi-poller)|0|F| | | | | | |
|[5.4 USI Accession Persister](#54-usi-accession-persister)|0|P| | | | | | |
|_[6. Ingest Exporter](#6-ingest-exporterhttpsgithubcomhumancellatlasingest-exporter)_||
|[6.1 Bundle Generator](#61-bundle-generator)|P v3|F v4| | | | | | |
|[6.2 Bundle Stager](#62-bundle-stager)|P|P| | | | | | |
|[6.3 Bundle Result](#63-bundle-result)|P|P| | | | | | |
|[6.4 Cleanup](#64-cleanup)|P|F| | | | | | |
|_[7. Ingest Core](#7-ingest-core)_||
|_[8. Ingest Broker UI](#8-ingest-broker-ui)_| | | | | | | |
|[8.1 Action: Create Submission](#81-action-create-submission)|P|P| | | | | | |
|[8.2 Action: Download Spreadsheet](#82-action-download-spreadsheet)|P|P| | | | | | |
|[8.3 Action: Submit Spreadsheet](#83-action-submit-spreadsheet)|P|P| | | | | | |
|[8.4 Action: Complete Submission](#84-action-complete-submission)|P|P| | | | | | |
|[8.5 Action: Update Ontology in Sample](#85-action-update-ontology-in-sample)|0|P| | | | | | |
|[8.6 Display: Submission List](#86-display-submission-list)|P|P| | | | | | |
|[8.7 Display: Submission Details](#87-display-submission-details)|P|P| | | | | | |
|[8.8 Display: File Details](#88-display-file-details)|P|P| | | | | | |
|[8.9 Display: Credentials](#89-display-credentials)|P|P| | | | | | |
|[8.10 Display: Validation Errors](#810-display-validation-errors)|0|P| | | | | | |
|_[9. Cross Cutting Concerns](#9-cross-cutting-concerns)_||
|[9.1 Logging](#91-logging)|0|0|P| | | | | |
|[9.2 Authentication](#92-authentication)|0|P|P|| | | | | |  
|[9.3 Authorisation](#93-authorisation)|0|0|P|| | | | | |  
