# 1. [Ingest Broker API](https://github.com/HumanCellAtlas/ingest-broker-api)

Provides an [API Gateway](http://microservices.io/patterns/apigateway.html) between [Ingest UI](#8-ingest-ui) and [Ingest Core](#7-ingest-core).

## 1.1 Submission Create
* __Trigger__
    * HTTP POST
* __Input__
    * none
* __Process__
    * Generate a submission uuid
    * Persist uuid
* __Output__
    * Event: Submission created
    * Submission uuid

## 1.2 Get Credentials
* __Trigger__
    * HTTP POST
* __Input__
    * Submission uuid
* __Ouput__
    * Credentials
    
## 1.3 Template Spreadsheet Download
* __Trigger__
    * HTTP GET
* __Input__
    * none
* __Output__
    * A template XLSX spreadsheet      
    
## 1.4 Spreadsheet Upload
* __Trigger__
    * HTTP POST
* __Input__
    * Submission uuid
    * A XLSX spreadsheet file
* __Process__
    * Check uuid is in the correct format
    * Check submission uuid is known to the system
    * Check file is a valid XLSX format file 
    * Accept file and persist it to an accessible store
* __Output__
    * Event: New spreadsheet uploaded
    * A reference to the XLSX spreadsheet file in an accessible store
* __Error conditions__
    * Submission uuid is invalid
    * Submission uuid is unknown
    * Uploaded file is something other than a XLSX spreadsheet

## 1.5 Metadata Create
* __Trigger__
    * HTTP POST
* __Input__
    * A valid submission uuid
    * A metadata JSON entity
* __Output__
    * Event: Metadata uuid requested
    * A valid submission uuid
    * A metadata JSON entity

## 1.6 Metadata Update
* __Trigger__
    * HTTP PUT
* __Input__
    * A valid submission uuid
    * A metadata uuid
    * A metadata JSON entity
* __Output__
    * Event: Metadata update requested
    * A valid submission uuid
    * A metadata uuid
    * A metadata JSON entity

## 1.7 Metadata Delete
* __Trigger__
    * HTTP DELETE
* __Input__
    * A valid submission uuid
    * A metadata uuid
* __Output__
    * Event: Metadata delete requested
    * A valid submission uuid
    * A metadata uuid

## 1.8 Validate Sample
* __Trigger__
    * HTTP POST
* __Input__
    * A valid submission uuid
    * A sample metadata
* __Output__
    * Validation results
    
## 1.9 Complete Submission
* __Trigger__
    * HTTP POST
* __Input__
    * A valid submission uuid
* __Output__

## 1.10 List All Submissions
* __Trigger__
    * HTTP GET
* __Input__
    * none
* __Output__
    * A list of submissions
    
## 1.11 Get Submission Details
* __Trigger__
    * HTTP GET
* __Input__
    * A valid submission uuid
* __Output__
    * Details of a submission

## 1.12 List Project for Submission
* __Trigger__
    * HTTP GET
* __Input__
    * A valid submission uuid
* __Output__
    * A project

## 1.13 List Samples for Submission
* __Trigger__
    * HTTP GET
* __Input__
    * A valid submission uuid
* __Output__
    * A list of samples

## 1.14 List Files for Submission
* __Trigger__
    * HTTP GET
* __Input__
    * A valid submission uuid
* __Output__
    * A list of files

## 1.15 List Analyses for Submission
* __Trigger__
    * HTTP GET
* __Input__
    * A valid submission uuid
* __Output__
    * A list of analyses
    
## 1.16 List Bundles for Submission
* __Trigger__
    * HTTP GET
* __Input__
    * A valid submission uuid
* __Output__
    * A list of bundles  