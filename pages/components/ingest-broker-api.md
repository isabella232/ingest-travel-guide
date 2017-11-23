# 1. [Ingest Broker API](https://github.com/HumanCellAtlas/ingest-broker-api)

Provides REST endpoint for the Ingest Broker UI beyond those provided by in Ingest API in [Ingest Core](#7-ingest-core).

## 1.1 Get Credentials
* __Trigger__
    * HTTP POST
* __Input__
    * Submission uuid
* __Ouput__
    * Credentials
    
## 1.2 Template Spreadsheet Download
* __Trigger__
    * HTTP GET
* __Input__
    * none
* __Output__
    * A template XLSX spreadsheet      
    
## 1.3 Spreadsheet Upload
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

## 1.4 Validate Sample
* __Trigger__
    * HTTP POST
* __Input__
    * A valid submission uuid
    * A sample metadata
* __Output__
    * Validation results
