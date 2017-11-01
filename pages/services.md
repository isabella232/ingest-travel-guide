# Services
The services of the Ingest component broken down into functions.

## 1. [Ingest Core](https://github.com/HumanCellAtlas/ingest-core)

## 2. [Ingest Broker](https://github.com/HumanCellAtlas/ingest-broker)

## 3. [Ingest Accessioner](https://github.com/HumanCellAtlas/ingest-accessioner)

## 4. [Ingest Validator](https://github.com/HumanCellAtlas/ingest-validator)

## 5. [Ingest Archiver](https://github.com/HumanCellAtlas/ingest-archiver)
[![Ingest Archiver Build Status](https://travis-ci.org/HumanCellAtlas/ingest-archiver.svg?branch=master)](https://travis-ci.org/HumanCellAtlas/ingest-archiver)
[![Maintainability](https://api.codeclimate.com/v1/badges/8ce423001595db4e6de7/maintainability)](https://codeclimate.com/github/HumanCellAtlas/ingest-archiver/maintainability)
[![Test Coverage](https://api.codeclimate.com/v1/badges/8ce423001595db4e6de7/test_coverage)](https://codeclimate.com/github/HumanCellAtlas/ingest-archiver/test_coverage)

### 5.1 USI Converter
* Takes HCA sample JSON and returns USI sample JSON
* _Input_
    * Valid submission UUID
    * Valid sample UUID
    * HCA format sample JSON
* _Process_
    * Convert HCA sample JSON to USI sample JSON
* _Output_
    * Valid submission UUID
    * Valid sample UUID
    * USI format sample JSON

### 5.2 USI Submitter
* Takes USI sample JSON and submits to USI in a new submission
* _Input_
    * Valid submission UUID
    * Valid sample UUID
    * USI format sample JSON
* _Process_
    * Create a new USI submission via the REST API
    * Add USI format sample JSON to the submission
    * Submit the USI submission
* _Output_
    * Valid submission UUID
    * Valid sample UUID
    * USI submission id
    
### 5.3 USI Poller
* Polls USI for the accession of a sample
* _Input_
    * Valid submission UUID
    * Valid sample UUID
    * USI submission id
* _Process_
    * Poll USI REST API for the submission status until a BioSamples accession is available
* _Output_
    * Valid submission UUID
    * Valid sample UUID
    * USI submission id
    * Biosamples accession

### 5.4 USI Accession Persister
* Store the mapping between sample UUID and BioSamples accession
* _Input_
    * Valid submission UUID
    * Valid sample UUID
    * USI submission id
    * Biosamples accession
* _Process_
    * Persist the mapping between sample UUID and BioSamples accession to the data store
* _Output_
    * Valid submission UUID
    * Valid sample UUID
    * USI submission id
    * Biosamples accession

## 6. [Ingest Exporter](https://github.com/HumanCellAtlas/ingest-exporter) 


