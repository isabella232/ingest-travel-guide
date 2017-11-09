# 2. [Ingest Broker](https://github.com/HumanCellAtlas/ingest-broker)

Performs brokering between user supplied spreadsheet data and JSON objects for submission to [Ingest Core](#7-ingest-core). 

## 2.1 Credentials Poller
* __Trigger__
    * Event: Submission created
* __Input__
    * Submission uuid
* __Process__
    * Obtain credentials from staging service
* __Output__
    * URL for staging area
    * Credentials for access 

## 2.2 Spreadsheet to JSON Converter
See [HCA-203](https://www.ebi.ac.uk/panda/jira/browse/HCA-203)
* __Input__
    * Valid submission UUID
    * A reference to a XLSX spreadsheet file in an accessible store
* __Process__
    * Convert each entry into the appropriate metadata JSON entities
    * Validate that each spreadsheet entry results in valid JSON
* __Output__
    * Success: Event: Metadata collection generated
    * A collection of metadata JSON entities
* __Error conditions__
    * Error: Event: Spreadsheet conversion failed
    * Not all entries resulted in a valid JSON
        * Reference to spreadsheet file is invalid (file not found)
        * Spreadsheet cannot be processed (format incorrect)
        
## 2.3 Metadata JSON Collection Validator
* __Input__
    * Valid submission UUID
    * A collection of metadata JSON entities
* __Process__
    * Validate that ids exist where expected in each JSON entity
    * Validate all references resolve to one of these ids
* __Output__
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
            
## 2.4 Metadata JSON Collection UUID Scheduler
* __Trigger__
    * Event: Metadata collection valid
* __Input__
    * A valid submission uuid
    * A valid collection of JSON entities
* __Output__
    * For each JSON entity:
        * Event: Metadata uuid requested
        * A valid submission uuid
        * A metadata JSON entity
        
## 2.5 Metadata JSON UUID Assigner
* __Trigger__
    * Event: Metadata uuid requested
* __Input__
    * A valid submission uuid
    * A metadata JSON entity
* __Process__
    * Generate uuid for each entity
* __Output__
    * Event: Metadata uuid assigned
    * Metadata uuid
    * Metadata JSON

## 2.6 Metadata JSON Persister
* __Trigger__
    * Event: Metadata uuid assigned
    * Event: Metadata update requested
    * Event: Metadata delete requested
* __Input__
    * A valid submission uuid
    * A metadata uuid
    * A metadata JSON entity (for create or update)
* __Process__ 
    * Create/update/delete JSON entity in data store
    * If create: create mapping of submission uuid to metadata metadata uuid
* __Output__
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
