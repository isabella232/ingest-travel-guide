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