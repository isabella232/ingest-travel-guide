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
