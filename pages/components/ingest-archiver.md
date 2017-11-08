# 5. [Ingest Archiver](https://github.com/HumanCellAtlas/ingest-archiver)

* Performs submission to non-HCA archives. retreiving and storing accessions where available.

[![Ingest Archiver Build Status](https://travis-ci.org/HumanCellAtlas/ingest-archiver.svg?branch=master)](https://travis-ci.org/HumanCellAtlas/ingest-archiver)
[![Maintainability](https://api.codeclimate.com/v1/badges/8ce423001595db4e6de7/maintainability)](https://codeclimate.com/github/HumanCellAtlas/ingest-archiver/maintainability)
[![Test Coverage](https://api.codeclimate.com/v1/badges/8ce423001595db4e6de7/test_coverage)](https://codeclimate.com/github/HumanCellAtlas/ingest-archiver/test_coverage)

## State Transition

![alt text](../../../images/ingest-accessioner-states.png "Ingest Archiver State Transition")

## 5.1 [HCA to USI Converter](https://github.com/HumanCellAtlas/ingest-archiver/blob/master/archiver/converter.py)
Takes HCA sample JSON and returns USI sample JSON
* __Input__
    * [Submission UUID](../../data/#submission-uuid)
    * [Sample UUID](../../data/#sample-uuid)
    * [HCA sample](../../data/#hca-format-sample-json)
* __Input Example__
```json
{
	"submission-uuid": "a8797226-ebd3-45ff-94bf-ed03292b532e",
	"sample-uuid": "fcb2f565-71b7-4ea3-b298-091b23657fc4",
	"hca-sample": {
		"is_living": "yes",
		"ncbi_taxon": 9606,
		"id": "Q3_DEMO-donor_MGH30",
		"species": {
			"text": "Homo sapiens",
			"ontology": 9606
		}
	}
}
```
* __Process__
    * Convert HCA sample JSON into USI sample JSON
* __Output__
    * [Submission UUID](../../data/#submission-uuid)
    * [Sample UUID](../../data/#sample-uuid)
    * [USI sample](../../data/#usi-format-sample-json)
 * __Output Example__
```json
{
	"submission-uuid": "a8797226-ebd3-45ff-94bf-ed03292b532e",
	"sample-uuid": "fcb2f565-71b7-4ea3-b298-091b23657fc4",
	"usi-sample": {
		"alias": "fcb2f565-71b7-4ea3-b298-091b23657fc4",
		"team": {
			"name": "self.hca-user"
		},
		"title": "Q3_DEMO-donor_MGH30",
		"description": "",
		"attributes": [{
			"name": "is_living",
			"value": "yes",
			"terms": []
		}, {
			"name": "ncbi_taxon",
			"value": 9606,
			"terms": []
		}],
		"releaseDate": "2017-10-17",
		"sampleRelationships": [],
		"taxonId": 9606,
		"taxon": "Homo sapiens"
	}
}
```

## 5.2 USI Submitter
Takes USI sample JSON and submits to USI in a new submission
* __Input__
    * [Submission UUID](../../data/#submission-uuid)
    * [Sample UUID](../../data/#sample-uuid)
    * [USI sample](../../data/#usi-format-sample-json)
* __Input Example__
```json
{
	"submission-uuid": "a8797226-ebd3-45ff-94bf-ed03292b532e",
	"sample-uuid": "fcb2f565-71b7-4ea3-b298-091b23657fc4",
	"usi-sample": {
		"alias": "fcb2f565-71b7-4ea3-b298-091b23657fc4",
		"team": {
			"name": "self.hca-user"
		},
		"title": "Q3_DEMO-donor_MGH30",
		"description": "",
		"attributes": [{
			"name": "is_living",
			"value": "yes",
			"terms": []
		}, {
			"name": "ncbi_taxon",
			"value": 9606,
			"terms": []
		}],
		"releaseDate": "2017-10-17",
		"sampleRelationships": [],
		"taxonId": 9606,
		"taxon": "Homo sapiens"
	}
}
```
* __Process__
    * Create a new USI submission via the REST API
    * Add [USI sample](../../data/#usi-format-sample-json) to the submission
    * Submit the USI submission
* __Output__
    * [Submission UUID](../../data/#submission-uuid)
    * [Sample UUID](../../data/#sample-uuid)
    * [USI Submission ID](../../data/#usi-submission-id)
* __Output Example__
```json
{
	"submission-uuid": "a8797226-ebd3-45ff-94bf-ed03292b532e",
	"sample-uuid": "fcb2f565-71b7-4ea3-b298-091b23657fc4",
	"usi-submission-id": "xxx"
}
```
    
## 5.3 USI Poller
Polls USI for the accession of a sample
* __Input__
    * [Submission UUID](../../data/#submission-uuid)](../data.md/#submission-uuid)
    * [Sample UUID](../../data/#sample-uuid)
    * [USI Submission ID](../../data/#usi-submission-id)
* __Input Example__
```json
{
	"submission-uuid": "a8797226-ebd3-45ff-94bf-ed03292b532e",
	"sample-uuid": "fcb2f565-71b7-4ea3-b298-091b23657fc4",
	"usi-submission-id": "c714224b-8dee-4c55-8849-422fe1d39ace"
}
```    
* __Process__
    * Poll USI REST API for the submission status until a [Biosamples Accession](../../data/#biosamples-accession) is available
* __Output__
    * [Submission UUID](../../data/#submission-uuid)
    * [Sample UUID](../../data/#sample-uuid)
    * [USI Submission ID](../../data/#usi-submission-id)
    * [Biosamples Accession](../../data/#biosamples-accession)
* __Output Examples__
    * Waiting for accession
```json
{
	"submission-uuid": "a8797226-ebd3-45ff-94bf-ed03292b532e",
	"sample-uuid": "fcb2f565-71b7-4ea3-b298-091b23657fc4",
	"usi-submission-id": "c714224b-8dee-4c55-8849-422fe1d39ace",
    "state": "pending"
}
```
    * Accession available
```json
{
    "submission-uuid": "a8797226-ebd3-45ff-94bf-ed03292b532e",
    "sample-uuid": "fcb2f565-71b7-4ea3-b298-091b23657fc4",
    "usi-submission-id": "c714224b-8dee-4c55-8849-422fe1d39ace",
    "state": "complete"
}
```  

## 5.4 USI Accession Persister
Stores the mapping between sample UUID and [Biosamples Accession](../../data/#biosamples-accession)
* __Input__
    * [Submission UUID](../../data/#submission-uuid)
    * [Sample UUID](../../data/#sample-uuid)
    * [USI Submission ID](../../data/#usi-submission-id)
    * [Biosamples Accession](../../data/#biosamples-accession)
* __Input Example__
```json
{
	"submission-uuid": "a8797226-ebd3-45ff-94bf-ed03292b532e",
	"sample-uuid": "fcb2f565-71b7-4ea3-b298-091b23657fc4",
	"usi-submission-id": "c714224b-8dee-4c55-8849-422fe1d39ace",
    "biosample-accession": "SAMEA3206556"
}
```  
* __Process__
    * Persist the mapping between sample UUID and [Biosamples Accession](../../data/#biosamples-accession) to a data store
* __Output__
    * [Submission UUID](../../data/#submission-uuid)
    * [Sample UUID](../../data/#sample-uuid)
    * [USI Submission ID](../../data/#usi-submission-id)
    * [Biosamples Accession](../../data/#biosamples-accession)
* __Output Example__
```json
{
	"submission-uuid": "a8797226-ebd3-45ff-94bf-ed03292b532e",
	"sample-uuid": "fcb2f565-71b7-4ea3-b298-091b23657fc4",
	"usi-submission-id": "c714224b-8dee-4c55-8849-422fe1d39ace",
    "biosample-accession": "SAMEA3206556"
}
```  