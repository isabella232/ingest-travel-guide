# 4. [Ingest Validator](https://github.com/HumanCellAtlas/ingest-validator)

Provides validation for HCA DCP metadata and data files. 

## 4.1 Metadata Validator
* __Trigger__
    * Event: Metadata created
    * Event: Metadata updated
    * HTTP POST
* __Input__
    * A valid submission uuid
    * Metadata uuid (if exists)
    * Metadata JSON entity
* __Process__
Perform the appropriate JSON Schema metadata validation
* __Output__
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
        
## 4.2 FASTQ File Validator
* __Trigger__
    * Event: File updated
* __Input__
    * A valid submission uuid
    * A reference to a data file in an accessible store
* __Process__
    * Validate data file to [defined FASTQ validation rules](#)
* __Output__
    * Valid
        * Event: File validation successful
        * Submission uuid
        * A reference to a data file in an accessible store
    * Not valid:
        * Event: File validation failed
        * Submission uuid
        * A reference to a data file in an accessible store
        * Validation results JSON
        
## 4.3 Image File Validator
 * TODO
