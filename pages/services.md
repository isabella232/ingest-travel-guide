# Services
The services of the Ingest component broken down into functions.

Functions should be self contained steps that:
* Are passed all the information they need to process as JSON
* Output results as JSON

## 1. [Ingest Broker API](https://github.com/HumanCellAtlas/ingest-broker-api)

* Provides an [API Gateway](http://microservices.io/patterns/apigateway.html) between [Ingest Broker UI](#ingest-broker-ui) and [Ingest Core](#ingest-core).

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

### 1.2 Spreadsheet Upload
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

### 1.3 Metadata Create
* _Trigger_
    * HTTP POST
* _Input_
    * A valid submission uuid
    * A metadata JSON entity
* _Output_
    * Event: Metadata uuid requested
    * A valid submission uuid
    * A metadata JSON entity

### 1.4 Metadata Update
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

### 1.5 Metadata Delete
* _Trigger_
    * HTTP DELETE
* _Input_
    * A valid submission uuid
    * A metadata uuid
* _Output_
    * Event: Metadata delete requested
    * A valid submission uuid
    * A metadata uuid

## 2. [Ingest Broker](https://github.com/HumanCellAtlas/ingest-broker)

* Performs brokering between user supplied spreadsheet data and JSON objects for submission to Ingest Core. 

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

## 4. [Ingest Validator](https://github.com/HumanCellAtlas/ingest-validator)

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
        
### 4.2 Fastq File Validator
* _Trigger_
    * Event: File updated
* _Input_
    * A valid submission uuid
    * A reference to a data file in an accessible store
* _Process_
    * Validate data file to FASTQ validation rules
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

### 5.1 [USI Converter](https://github.com/HumanCellAtlas/ingest-archiver/blob/master/archiver/converter.py)
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
    * Persist the mapping between sample UUID and BioSamples accession to the data store
* _Output_
    * Valid submission UUID
    * Valid sample UUID
    * USI submission id
    * Biosamples accession

## 6. [Ingest Exporter](https://github.com/HumanCellAtlas/ingest-exporter) 

### 6.1 Bundle Generator
* _Trigger_
    * HTTP POST: Submit
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
    

## <a name="ingest-core"></a>7. Ingest Core 

[GitHub](https://github.com/HumanCellAtlas/ingest-core)

[Valid submission UUID]: e.g. c270052e-f69e-4323-a3b6-eb3d1b688cc5
