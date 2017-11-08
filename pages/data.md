# Data

The data concepts in the system

## Submission UUID
A generated submission UUID known to the Ingest API
* __Example__
```
a8797226-ebd3-45ff-94bf-ed03292b532e
```

## Sample UUID
A generated sample UUID known to the Ingest API
* __Example__
```
fcb2f565-71b7-4ea3-b298-091b23657fc4
```

## USI Submission ID
A submission UUID provided by USI.
* __Example__
```
c714224b-8dee-4c55-8849-422fe1d39ace
```

## Biosamples Accession
An accession provided by the [Biosamples Database](https://www.ebi.ac.uk/biosamples/)
* __Example__
```
SAMEA3206556
```

## HCA format sample JSON
An HCA format sample compling to the v4 metadata schema.
```json
{
	"is_living": "yes",
	"ncbi_taxon": 9606,
	"id": "Q3_DEMO-donor_MGH30",
	"species": {
		"text": "Homo sapiens",
		"ontology": 9606
	}
}
```
## USI format sample JSON
A USI format sample JSON document
```json
{
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

```