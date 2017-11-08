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
