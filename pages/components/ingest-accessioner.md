# 3. [Ingest Accessioner](https://github.com/HumanCellAtlas/ingest-accessioner)

* Provides HCA format accession numbers where accessions are not available from archives.

## 3.1 HCA Accessioner
* __Trigger__
   * Event: Metadata validation successful?
* __Input__
   * A valid submission uuid
   * A metadata uuid
* __Process__ 
   * Generate a new HCA accession
   * Persist mapping of metadata uuid to HCA accession
* __Output__
   * Event: Metadata accessioned
   * Metadata uuid
   * HCA accession