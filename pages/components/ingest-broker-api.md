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