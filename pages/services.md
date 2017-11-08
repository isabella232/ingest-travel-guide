# Services
The services of the Ingest component broken down into functions.

Functions are self-contained steps that:
* Take input as JSON
* Output results as JSON

This approach allows for functions to be written in different languages and seperates deployment details from functionality. 


## Contents
* [1. Ingest Broker API](#1-ingest-broker-apihttpsgithubcomhumancellatlasingest-broker-api)
  + [1.1 Submission Create](#11-submission-create)
  + [1.2 Get Credentials](#12-get-credentials)
  + [1.3 Template Spreadsheet Download](#13-template-spreadsheet-download)
  + [1.4 Spreadsheet Upload](#14-spreadsheet-upload)
  + [1.5 Metadata Create](#15-metadata-create)
  + [1.6 Metadata Update](#16-metadata-update)
  + [1.7 Metadata Delete](#17-metadata-delete)
  + [1.8 Validate Sample](#18-validate-sample)
  + [1.9 Complete Submission](#19-complete-submission)
  + [1.10 List All Submissions](#110-list-all-submissions)
  + [1.11 Get Submission Details](#111-get-submission-details)
  + [1.12 List Project for Submission](#112-list-project-for-submission)
  + [1.13 List Samples for Submission](#113-list-samples-for-submission)
  + [1.14 List Files for Submission](#114-list-files-for-submission)
  + [1.15 List Analyses for Submission](#115-list-analyses-for-submission)
  + [1.16 List Bundles for Submission](#116-list-bundles-for-submission)
* [2. Ingest Broker](#2-ingest-brokerhttpsgithubcomhumancellatlasingest-broker)
  + [2.1 Credentials Poller](#21-credentials-poller)
  + [2.2 Spreadsheet to JSON Converter](#22-spreadsheet-to-json-converter)
  + [2.3 Metadata JSON Collection Validator](#23-metadata-json-collection-validator)
  + [2.4 Metadata JSON Collection UUID Scheduler](#24-metadata-json-collection-uuid-scheduler)
  + [2.5 Metadata JSON UUID Assigner](#25-metadata-json-uuid-assigner)
  + [2.6 Metadata JSON Persister](#26-metadata-json-persister)
* [3. Ingest Accessioner](#3-ingest-accessionerhttpsgithubcomhumancellatlasingest-accessioner)
  + [3.1 HCA Accessioner](#31-hca-accessioner)
* [4. Ingest Validator](#4-ingest-validatorhttpsgithubcomhumancellatlasingest-validator)
  + [4.1 Metadata Validator/s](#41-metadata-validators)
  + [4.2 FASTQ File Validator](#42-fastq-file-validator)
  + [4.3 Image File Validator](#todo)
* [5. Ingest Archiver](#5-ingest-archiverhttpsgithubcomhumancellatlasingest-archiver)
  + [5.1 HCA to USI Converter](#51-hca-to-usi-converterhttpsgithubcomhumancellatlasingest-archiverblobmasterarchiverconverterpy)
  + [5.2 USI Submitter](#52-usi-submitter)
  + [5.3 USI Poller](#53-usi-poller)
  + [5.4 USI Accession Persister](#54-usi-accession-persister)
* [6. Ingest Exporter](#6-ingest-exporterhttpsgithubcomhumancellatlasingest-exporter)
  + [6.1 Bundle Generator](#61-bundle-generator)
  + [6.2 Bundle Stager](#62-bundle-stager)
  + [6.3 Bundle Result](#63-bundle-result)
  + [6.4 Cleanup](#64-cleanup)
* [7. Ingest Core](#7-ingest-core)
  + [7.1 Ingest Core API](#todo)
  + [7.2 Persistence](#todo)
  + [7.3 State Management](#todo) 
* [8. Ingest Broker UI](#8-ingest-broker-ui)
  + [8.1 Action: Create Submission](#81-action-create-submission)
  + [8.2 Action: Download Spreadsheet](#82-action-download-spreadsheet)
  + [8.3 Action: Submit Spreadsheet](#83-action-submit-spreadsheet)
  + [8.4 Action: Complete Submission](#84-action-complete-submission)
  + [8.5 Action: Update Ontology in Sample](#85-action-update-ontology-in-sample)
  + [8.6 Display: Submission List](#86-display-submission-list)
  + [8.7 Display: Submission Details](#87-display-submission-details)
  + [8.8 Display: File Details](#88-display-file-details)
  + [8.9 Display: Credentials](#89-display-credentials)
  + [8.10 Display: Validation Errors](#810-display-validation-errors)
* [9. Cross Cutting Concerns](#9-cross-cutting-concerns)
  + [9.1 Logging](#91-logging)
  + [9.2 Authentication](#todo)
  + [9.3 Authorisation](#todo)  

## 1. [Ingest Broker API](https://github.com/HumanCellAtlas/ingest-broker-api)

* Provides an [API Gateway](http://microservices.io/patterns/apigateway.html) between [Ingest Broker UI](#8-ingest-broker-ui) and [Ingest Core](#7-ingest-core).

### 1.1 Submission Create
* _Trigger_
    * HTTP POST
* _Input_
    * none
* _Process_
    * Generate a submission uuid
    * Persist uuid
* _Output_
    * Event: Submission created
    * Submission uuid

### 1.2 Get Credentials
* _Trigger_
    * HTTP POST
* _Input_
    * Submission uuid
* _Ouput_
    * Credentials
    
### 1.3 Template Spreadsheet Download
* _Trigger_
    * HTTP GET
* _Input_
    * none
* _Output_
    * A template XLSX spreadsheet      
    
### 1.4 Spreadsheet Upload
* _Trigger_
    * HTTP POST
* _Input_
    * Submission uuid
    * A XLSX spreadsheet file
* _Process_
    * Check uuid is in the correct format
    * Check submission uuid is known to the system
    * Check file is a valid XLSX format file 
    * Accept file and persist it to an accessible store
* _Output_
    * Event: New spreadsheet uploaded
    * A reference to the XLSX spreadsheet file in an accessible store
* _Error conditions_
    * Submission uuid is invalid
    * Submission uuid is unknown
    * Uploaded file is something other than a XLSX spreadsheet

### 1.5 Metadata Create
* _Trigger_
    * HTTP POST
* _Input_
    * A valid submission uuid
    * A metadata JSON entity
* _Output_
    * Event: Metadata uuid requested
    * A valid submission uuid
    * A metadata JSON entity

### 1.6 Metadata Update
* _Trigger_
    * HTTP PUT
* _Input_
    * A valid submission uuid
    * A metadata uuid
    * A metadata JSON entity
* _Output_
    * Event: Metadata update requested
    * A valid submission uuid
    * A metadata uuid
    * A metadata JSON entity

### 1.7 Metadata Delete
* _Trigger_
    * HTTP DELETE
* _Input_
    * A valid submission uuid
    * A metadata uuid
* _Output_
    * Event: Metadata delete requested
    * A valid submission uuid
    * A metadata uuid

### 1.8 Validate Sample
* _Trigger_
    * HTTP POST
* _Input_
    * A valid submission uuid
    * A sample metadata
* _Output_
    * Validation results
    
### 1.9 Complete Submission
* _Trigger_
    * HTTP POST
* _Input_
    * A valid submission uuid
* _Output_

### 1.10 List All Submissions
* _Trigger_
    * HTTP GET
* _Input_
    * none
* _Output_
    * A list of submissions
    
### 1.11 Get Submission Details
* _Trigger_
    * HTTP GET
* _Input_
    * A valid submission uuid
* _Output_
    * Details of a submission

### 1.12 List Project for Submission
* _Trigger_
    * HTTP GET
* _Input_
    * A valid submission uuid
* _Output_
    * A project

### 1.13 List Samples for Submission
* _Trigger_
    * HTTP GET
* _Input_
    * A valid submission uuid
* _Output_
    * A list of samples

### 1.14 List Files for Submission
* _Trigger_
    * HTTP GET
* _Input_
    * A valid submission uuid
* _Output_
    * A list of files

### 1.15 List Analyses for Submission
* _Trigger_
    * HTTP GET
* _Input_
    * A valid submission uuid
* _Output_
    * A list of analyses
    
### 1.16 List Bundles for Submission
* _Trigger_
    * HTTP GET
* _Input_
    * A valid submission uuid
* _Output_
    * A list of bundles  

## 2. [Ingest Broker](https://github.com/HumanCellAtlas/ingest-broker)

* Performs brokering between user supplied spreadsheet data and JSON objects for submission to [Ingest Core](#7-ingest-core). 

### 2.1 Credentials Poller
* _Trigger_
    * Event: Submission created
* _Input_
    * Submission uuid
* _Process_
    * Obtain credentials from staging service
* _Output_
    * URL for staging area
    * Credentials for access 

### 2.2 Spreadsheet to JSON Converter
See [HCA-203](https://www.ebi.ac.uk/panda/jira/browse/HCA-203)
* _Input_
    * Valid submission UUID
    * A reference to a XLSX spreadsheet file in an accessible store
* _Process_
    * Convert each entry into the appropriate metadata JSON entities
    * Validate that each spreadsheet entry results in valid JSON
* _Output_
    * Success: Event: Metadata collection generated
    * A collection of metadata JSON entities
* _Error conditions_
    * Error: Event: Spreadsheet conversion failed
    * Not all entries resulted in a valid JSON
        * Reference to spreadsheet file is invalid (file not found)
        * Spreadsheet cannot be processed (format incorrect)
        
### 2.3 Metadata JSON Collection Validator
* _Input_
    * Valid submission UUID
    * A collection of metadata JSON entities
* _Process_
    * Validate that ids exist where expected in each JSON entity
    * Validate all references resolve to one of these ids
* _Output_
    * Valid:
        * Event: Metadata collection valid
        * Submission uuid
        * Collection of metadata JSON entities
    * Not valid
        * Event: Metadata collection invalid
        * Submission uuid
        * Validation results:
            * Which ids are missing
            * Which references are invalid
            
### 2.4 Metadata JSON Collection UUID Scheduler
* _Trigger_
    * Event: Metadata collection valid
* _Input_
    * A valid submission uuid
    * A valid collection of JSON entities
* _Output_
    * For each JSON entity:
        * Event: Metadata uuid requested
        * A valid submission uuid
        * A metadata JSON entity
        
### 2.5 Metadata JSON UUID Assigner
* _Trigger_
    * Event: Metadata uuid requested
* _Input_
    * A valid submission uuid
    * A metadata JSON entity
* _Process_
    * Generate uuid for each entity
* _Output_
    * Event: Metadata uuid assigned
    * Metadata uuid
    * Metadata JSON

### 2.6 Metadata JSON Persister
* _Trigger_
    * Event: Metadata uuid assigned
    * Event: Metadata update requested
    * Event: Metadata delete requested
* _Input_
    * A valid submission uuid
    * A metadata uuid
    * A metadata JSON entity (for create or update)
* _Process_ 
    * Create/update/delete JSON entity in data store
    * If create: create mapping of submission uuid to metadata metadata uuid
* _Output_
    * If create:
        * Event: Metadata created
        * Submission uuid
        * Metadata uuid
    * If update:
        * Event: Metadata updated
        * Submission uuid
        * Metadata uuid
    * If delete:
        * Event: Metadata deleted
        * Submission uuid
        * Metadata uuid

## 3. [Ingest Accessioner](https://github.com/HumanCellAtlas/ingest-accessioner)

* Provides HCA format accession numbers where accessions are not available from archives.

### 3.1 HCA Accessioner
* _Trigger_
   * Event: Metadata validation successful?
* _Input_
   * A valid submission uuid
   * A metadata uuid
* _Process_ 
   * Generate a new HCA accession
   * Persist mapping of metadata uuid to HCA accession
* _Output_
   * Event: Metadata accessioned
   * Metadata uuid
   * HCA accession

## 4. [Ingest Validator](https://github.com/HumanCellAtlas/ingest-validator)

* Provides validation for HCA DCP metadata and data files. 

### 4.1 Metadata Validator/s
* _Trigger_
    * Event: Metadata created
    * Event: Metadata updated
    * HTTP POST
* _Input_
    * A valid submission uuid
    * Metadata uuid (if exists)
    * Metadata JSON entity
* _Process_
Perform the appropriate JSON Schema metadata validation
* _Output_
    * Valid
        * Event: Metadata validation successful
        * Submission uuid
        * Metadata uuid (if exists)
        * Metadata JSON entity
    * Not valid:
        * Event: Metadata validation failed
        * Submission uuid
        * Metadata uuid (if exists)
        * Metadata JSON entity
        * Validation results JSON
        
### 4.2 FASTQ File Validator
* _Trigger_
    * Event: File updated
* _Input_
    * A valid submission uuid
    * A reference to a data file in an accessible store
* _Process_
    * Validate data file to [defined FASTQ validation rules](#)
* _Output_
    * Valid
        * Event: File validation successful
        * Submission uuid
        * A reference to a data file in an accessible store
    * Not valid:
        * Event: File validation failed
        * Submission uuid
        * A reference to a data file in an accessible store
        * Validation results JSON

## 5. [Ingest Archiver](https://github.com/HumanCellAtlas/ingest-archiver)
[![Ingest Archiver Build Status](https://travis-ci.org/HumanCellAtlas/ingest-archiver.svg?branch=master)](https://travis-ci.org/HumanCellAtlas/ingest-archiver)
[![Maintainability](https://api.codeclimate.com/v1/badges/8ce423001595db4e6de7/maintainability)](https://codeclimate.com/github/HumanCellAtlas/ingest-archiver/maintainability)
[![Test Coverage](https://api.codeclimate.com/v1/badges/8ce423001595db4e6de7/test_coverage)](https://codeclimate.com/github/HumanCellAtlas/ingest-archiver/test_coverage)

* Performs submission to non-HCA archives and returning accessions where available.

### 5.1 [HCA to USI Converter](https://github.com/HumanCellAtlas/ingest-archiver/blob/master/archiver/converter.py)
* Takes HCA sample JSON and returns USI sample JSON
* _Input_
    * Valid submission UUID
    * Valid sample UUID
    * HCA format sample JSON
* _Process_
    * Convert HCA sample JSON to USI sample JSON
* _Output_
    * Valid submission UUID
    * Valid sample UUID
    * USI format sample JSON

### 5.2 USI Submitter
* Takes USI sample JSON and submits to USI in a new submission
* _Input_
    * Valid submission UUID
    * Valid sample UUID
    * USI format sample JSON
* _Process_
    * Create a new USI submission via the REST API
    * Add USI format sample JSON to the submission
    * Submit the USI submission
* _Output_
    * Valid submission UUID
    * Valid sample UUID
    * USI submission id
    
### 5.3 USI Poller
* Polls USI for the accession of a sample
* _Input_
    * Valid submission UUID
    * Valid sample UUID
    * USI submission id
* _Process_
    * Poll USI REST API for the submission status until a BioSamples accession is available
* _Output_
    * Valid submission UUID
    * Valid sample UUID
    * USI submission id
    * Biosamples accession

### 5.4 USI Accession Persister
* Store the mapping between sample UUID and BioSamples accession
* _Input_
    * Valid submission UUID
    * Valid sample UUID
    * USI submission id
    * Biosamples accession
* _Process_
    * Persist the mapping between sample UUID and BioSamples accession to a data store
* _Output_
    * Valid submission UUID
    * Valid sample UUID
    * USI submission id
    * Biosamples accession

## 6. [Ingest Exporter](https://github.com/HumanCellAtlas/ingest-exporter) 

* Exports data bundles to the HCA DCP data store.

### 6.1 Bundle Generator
* _Input_
    * A valid submission uuid
* _Process_
    * Collect all metadata for submission uuid
    * Generate a bundle from the metadata
* _Output_
    * Event: Bundle generated
    * A JSON bundle file
    
### 6.2 Bundle Stager
* _Trigger_
    * Event: Bundle generated
* _Input_
    * A valid submission uuid
    * A JSON bundle file
* _Process_
    * Place bundle in staging area
    * Inform DSS of staging location
* _Output_
    * Event: staging complete
    * submission uuid
    
### 6.3 Bundle Result
* _Trigger_
    * Message from DSS
* _Input_
    * Submission uuid
    * Bundle uuid
    * Status
* _Output_
    * If successful
        * Event: DSS submission successful
        * Submission uuid
        * Bundle uuid
    * If unsuccessful
        * Event: DSS submission failed
        * Submission uuid
        * Bundle uuid

### 6.4 Cleanup
* _Trigger_
    * Event: DSS submission successful
* _Input_
    * A valid submission uuid
    * Bundle uuid
* _Process_
    * Remove anything that needs to be cleaned up
* _Output_
* If successful
    * Event: Cleanup successful
    * Submission uuid
* If unsuccessful
    * Event: Cleanup unsuccessful
    * Submission uuid
    
## [7. Ingest Core](https://github.com/HumanCellAtlas/ingest-core)

* Stores and retrieves metadata information and tracks submission state.

## [8. Ingest Broker UI](#8-ingest-broker-ui)

* Provides a web user interface to the [Ingest Broker API](#1-ingest-broker-api).
* Components are UI components that call a method on the broker API to perform an action or to retreive data for rendering.

### 8.1 Action: Create Submission
* _Calls_
   * [1.1 Submission Create](#11-submission-create)
   
### 8.2 Action: Download Spreadsheet
* _Calls_
   * [1.3 Template Spreadsheet Download](#13-template-spreadsheet-download)
   
### 8.3 Action: Submit Spreadsheet
* _Calls_
   * [1.4 Spreadsheet Upload](#14-spreadsheet-upload)
   
### 8.4 Action: Complete Submission
* _Calls_
   * [1.8 Complete Submission](#18-complete-submission)
   
### 8.5 Action: Update Ontology in Sample
* _Calls_
   * [1.6 Metadata Update](#16-metadata-update)
   
### 8.6 Display: Submission List
* _Calls_
   * [1.10 List All Submissions](#110-list-all-submissions)
   
### 8.7 Display: Submission Details
* _Calls_
   * [1.11 Get Submission Details](#111-get-submission-details)
   
### 8.8 Display: File Details
* _Calls_
   * [1.10 List All Submissions](#110-list-files-for-submission)
   
### 8.9 Display: Credentials
* _Calls_
   * [1.2 Get Credentials](#12-get-credentials)
   
### 8.10 Display: Validation Errors
* _Calls_
   * [1.8 Validate Sample](#18-validate-sample)

## 9. Cross Cutting Concerns

### 9.1 Logging
* Define a common format for logging of events and errors

### 9.2 Authentication and Authorisation
* Secure external facing [Ingest Broker API](#1-ingest-broker-api) endpoints
