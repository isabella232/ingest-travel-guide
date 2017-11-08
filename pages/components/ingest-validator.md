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