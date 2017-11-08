# Ingest Roadmap

## Key
* M - Mock
* P - Prototype
* F - Full

|Cell|M1|M2|M3|M4|M5|M6|M7|
|----|--|--|--|--|--|--|--|
|[1. Ingest Broker API](#1-ingest-broker-apihttpsgithubcomhumancellatlasingest-broker-api)| | | | | | | |
|[1.1 Submission Create](#11-submission-create)|F| | | | | | |
|[1.2 Get Credentials](#12-get-credentials)|F| | | | | | |
|[1.3 Template Spreadsheet Download](#13-template-spreadsheet-download)|F| | | | | | |
|[1.4 Spreadsheet Upload](#14-spreadsheet-upload)|F| | | | | | |
|[1.5 Metadata Create](#15-metadata-create)|F| | | | | | |
|[1.6 Metadata Update](#16-metadata-update)|P| | | | | | |
|[1.7 Metadata Delete](#17-metadata-delete)|-| | | | | | |
|[1.8 Validate Sample](#18-validate-sample)|P| | | | | | |
|[1.9 Complete Submission](#19-complete-submission)|F| | | | | | |
|[1.10 List All Submissions](#110-list-all-submissions)|F| | | | | | |
|[1.11 Get Submission Details](#111-get-submission-details)| | | | | | | |
|[1.12 List Project for Submission](#112-list-project-for-submission)| | | | | | | |
|[1.13 List Samples for Submission](#113-list-samples-for-submission)| | | | | | | |
|[1.14 List Files for Submission](#114-list-files-for-submission)| | | | | | | |
|[1.15 List Analyses for Submission](#115-list-analyses-for-submission)| | | | | | | |
|[1.16 List Bundles for Submission](#116-list-bundles-for-submission)| | | | | | | |
|[2. Ingest Broker](#2-ingest-brokerhttpsgithubcomhumancellatlasingest-broker)| | | | | | | |
|[2.1 Credentials Poller](#21-credentials-poller)| | | | | | | |
|[2.2 Spreadsheet to JSON Converter](#22-spreadsheet-to-json-converter)|F v4| | | | | | |
|[2.3 Metadata JSON Collection Validator](#23-metadata-json-collection-validator)|F v4 | | | | | | |
|[2.4 Metadata JSON Collection UUID Scheduler](#24-metadata-json-collection-uuid-scheduler)|F | | | | | | |
|[2.5 Metadata JSON UUID Assigner](#25-metadata-json-uuid-assigner)|F| | | | | | |
|[2.6 Metadata JSON Persister](#26-metadata-json-persister)|P| | | | | | |
|[3. Ingest Accessioner](#3-ingest-accessionerhttpsgithubcomhumancellatlasingest-accessioner)| | | | | | | |
|[3.1 HCA Accessioner](#31-hca-accessioner)|P| | | | | | |
|[4. Ingest Validator](#4-ingest-validatorhttpsgithubcomhumancellatlasingest-validator)| | | | | | | |
|[4.1 Metadata Validator/s](#41-metadata-validators)|P| | | | | | |
|[4.2 FASTQ File Validator](#42-fastq-file-validator)|P| | | | | | |
|[5. Ingest Archiver](#5-ingest-archiverhttpsgithubcomhumancellatlasingest-archiver)| | | | | | | |
|[5.1 HCA to USI Converter](#51-hca-to-usi-converterhttpsgithubcomhumancellatlasingest-archiverblobmasterarchiverconverterpy)|F v4| | | | | | |
|[5.2 USI Submitter](#52-usi-submitter)|F| | | | | | |
|[5.3 USI Poller](#53-usi-poller)|F| | | | | | |
|[5.4 USI Accession Persister](#54-usi-accession-persister)|P| | | | | | |
|[6. Ingest Exporter](#6-ingest-exporterhttpsgithubcomhumancellatlasingest-exporter)| | | | | | | |
|[6.1 Bundle Generator](#61-bundle-generator)|F v4| | | | | | |
|[6.2 Bundle Stager](#62-bundle-stager)|P| | | | | | |
|[6.3 Bundle Result](#63-bundle-result)|P| | | | | | |
|[6.4 Cleanup](#64-cleanup)|F| | | | | | |
|[7. Ingest Core](#7-ingest-core)|P| | | | | | |
|[8. Ingest Broker UI](#8-ingest-broker-ui)| | | | | | | |
|[8.1 Action: Create Submission](#81-action-create-submission)|P| | | | | | |
|[8.2 Action: Download Spreadsheet](#82-action-download-spreadsheet)P| | | | | | |
|[8.3 Action: Submit Spreadsheet](#83-action-submit-spreadsheet)P| | | | | | |
|[8.4 Action: Complete Submission](#84-action-complete-submission)|P| | | | | | |
|[8.5 Action: Update Ontology in Sample](#85-action-update-ontology-in-sample)|P| | | | | | |
|[8.6 Display: Submission List](#86-display-submission-list)|P| | | | | | |
|[8.7 Display: Submission Details](#87-display-submission-details)|P| | | | | | |
|[8.8 Display: File Details](#88-display-file-details)|P| | | | | | |
|[8.9 Display: Credentials](#89-display-credentials)|P| | | | | | |
|[8.10 Display: Validation Errors](#810-display-validation-errors)|P| | | | | | |
|[9. Cross Cutting Concerns](#9-cross-cutting-concerns)|P| | | | | | |
|[9.1 Logging](#91-logging)|-|P| | | | | |
|[9.2 Authentication and Authorisation](#92-authentication-and-authorisation)|P|| | | | | |  