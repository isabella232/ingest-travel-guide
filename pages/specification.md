# Ingest Specification

WARNING: This is the 0.1v specification and has not yet been updated to reflect Q3 demo or Q4 goals.

## Overview
The Ingestion Component will be responsible for the intake of biomolecular data into the Human Cell Atlas (HCA) Data Coordination Platform (DCP). In particular, the Ingest API will validate all biomolecular data received before attempting to persist the data into the HCA DCP data storage system (DSS).

The Ingestion Component has 6 major subcomponents:
* Ingest Brokers - any submitter-facing tool for capturing data into the DCP
* Staging Service - service for staging of data-files
* Ingest API - REST API by which data and metadata is pushed to the HCA DCP, either by brokers or by systems programmed to interact directly with the HCA, e.g. LIMS systems
* Accessioning service - a service for assigning both UUIDs and human-readable accession numbers to supplied metadata documents
* Ingest Datastore - a system used to collect and temporarily store metadata internally by the Ingestion Service during the ingest process.
* Validation Service - Service within the ingest service that supports data and metadata validation
* Tracking Service - service for tracking state of any submission known to the ingest service

## Requirements
### General
1. Where possible, adhere to the HCA principle of bringing compute to data, instead of data to compute.
2. The Ingestion Service should provide its own web UI, knowns as the “broker”, but should also provide an API upon which 3rd parties can build their own brokers.
3. All code and software used in the development of the Ingestion API should be completely open source and hosted on public repositories.

### Ingest Broker Requirements
There will be many brokers, all of which will communicate with the ingest API. The first implementation is expected to be a form-based web UI that will be used by submitters to supply metadata to ingest. This broker implementation will be expect users to upload bulky data files directly to the staging area.

Brokers are free to define their own submitter-facing interface that exposes as much or as little of the underlying ingest API as they deem appropriate. It is expected that brokers will proxy most requests to ingest rather than exposing the ingest API directly, to support compositional approaches to metadata upload (e.g. batch submission of samples) that the ingest API may not support directly. Additionally, it is the responsibility of brokers to perform end-user authentication of submitters, as the ingest API will not support this functionality.

Individual broker implementations are free to define additional requirements, but all brokers must support the following requirements.

### Authentication
Brokers must authenticate submitters and provide user-authentication tokens to the underlying ingest API.

### Broker Web UI
It is anticipated that all brokers will define some form of web UI, even those that only require spreadsheet upload. It is not desirable to support submission of metadata via email, and likely not possible to do so for large data files. Brokers must therefore support the following requirements:
1. Provides UI for viewing metadata schemata, all versions.
2. Provides submission metadata examples.
3. Provides a downloadable template for each metadata file.
4. User can start a new submission (request a new submission envelope). User receives a submission ID and a staging area URL.
5. User can deposit data files using a form/widget in the broker UI.
6. User can upload or reupload metadata files, as spreadsheets or JSON files.
    * Broker converts non-JSON files into HCA schema JSON files.
7. User can see validation status of metadata and data files.
    * User can see details of the problems with each metadata/data file.
8. User can submit a validated submission.
9. User can attempt to cancel a submitted submission.
10. User can see status of submitted submission.

### Broker REST API
We envisage that brokers will expose those parts of the Ingest API that it makes sense for a submitter to call directly (e.g. data file upload). Brokers may therefore expose REST API functions to perform:
* List / view metadata schemata.
* Start / submit / cancel a submission.
* Upload / reupload JSON metadata files.
* Get status of a submission, including metadata and data validation.

### Staging Service Requirements
Staging Service requirements are described in the document [Data File Staging Service (DFSS) Specifications](https://docs.google.com/document/d/1lj_CRiyLexXJDnT68gT_35tWQD5iBAOXnt4Mv7DLNfc/edit#).

### Ingest API Requirements
Biomolecular experimental metadata refers to documents that describe any experimental process or study. Biomolecular experimental metadata will be referred to as simply “metadata” henceforth.

An experimental process to assay biological materials (henceforth called samples) can generate raw data files as it’s output. The metadata that describes these materials (projects, assays and samples) and their associated data files will be referred to a “primary data” in this document. In contrast, “secondary data” refers to data that has been generated by an analysis of primary data, and to the metadata that describes this analysis.

The ingest API must not force brokers or submitters to collect and retain data or metadata throughout their experimental processes. As such, the ingest API must support referencing of submitted data and metadata outside of a single submission envelope. For example, sample metadata will be collected in clinical scenarios and can be submitted by a pathologist (or a broker built specifically to support pathologists collecting samples). These samples may then be sent to a laboratory that performs the sample preparation, then a large centre to generate the sequencing data. The ingest API must accept data and metadata at each step of this process to avoid complex handoff of data between centers outside of the HCA DCP infrastructure (e.g. LIMS systems) to avoid information loss and formatting errors. The ingest API therefore has to provision a mechanism to allow referencing of metadata and data documents across multiple submission envelopes.

The processes for submission of both primary and secondary data is the same, and has the following requirements:

1. User can authenticate to the Ingest API.
2. Provide ability to list and retrieve schemata for metadata.
3. Provide well documented endpoints for Brokers/automata to submit their metadata to the HCA DCP as JSON documents.
4. Coordinate and group related metadata under a single entity, called a “submission envelope”
5. Allow for modifications and deletions of submitted metadata and tracking changes to metadata documents
6. Provide a mechanism for users to link metadata documents to each other, reflecting the fact that these metadata may be generated separately over time
7. Provide a mechanism for users to link metadata to bulk sequencing/image (assay) data files
8. Provisioning of accessions for submitted metadata documents
9. Accommodate several scenarios of data submission; including 
    * A user wants to submit only metadata, 
    * A user wants to submit only data files, and link these files to existing metadata documents
    * A user wants to submit metadata that refers to bulk data that has not yet been submitted, then submit the relevant bulk data second 
    * A user wants to upload bulk data first, followed by metadata that refers to these bulk data
10. Allow for the referencing of existing metadata documents, both in the same submission envelope or in different envelopes, by accession ID, rather than redundant re-uploading of metadata documents.
11. Allow for the referencing of existing metadata documents in the same envelope by a local alias provided by the submitter

Additionally, to support specific secondary data requirements, the ingestion service also must:
1. Provide a mechanism whereby there is a bi-directional reference between any secondary data submission and its primary data
2. Provide a system that notifies users when any or all elements of their submission have been used in a completed analysis job
3. Provide a system that links submissions to the results of any analysis that used any or all of that submissions content

### Accessioning Service Requirements
The accessioning service must provide human readable HCA format accession numbers to objects that do not have an external accessioning authority. For example, the EBI and NCBI BioSample databases serve as the joint accessioning authority for biological samples, so HCA should not define new accessions for these objects. However, every sample submitted through the HCA ingest service should be assigned a UUID for identification with the HCA system.

The accessioning service must therefore:
1. Provide every submitted object with a UUID
2. Delegate accession assignment to an external accessioning authority wherever appropriate. This will be dependent on external services, so may not happen immediately.
3. Provide a service for generating an accession in the HCA namespace for any object without an external authority (e.g. analyses)
4. Provide a service for mapping between accessions (both external or HCA assigned) and UUIDs

### Validation Service Requirements
1. Insure that submitted metadata adheres to standards set by the HCA metadata working group
2. Validation of the syntax, semantics and constitution of metadata documents
3. Facilitate a means by which users can define their own metadata schema or “rules” for metadata documents
4. Provide a service that will validate metadata documents against user defined schemas in (12)
5. Allow for pre-validation of metadata documents before uploading metadata documents

### Tracking Service Requirements
1. Provide a comprehensive feedback system for querying the status of a submission as it’s ingested
2. Provide feedback on the results of validation processes run on metadata and bulk data files
3. Provide feedback on the provenance of a submission, including which bundles contain data and metadata present in that submission, and to which other submissions a submission is linked based on references between metadata objects
4. Allow a user to attempt to change the state of a submission

## Ingest Dataflow

### Overview

Some parts of the flow are asynchronous and are not bound by the order listed below, in particular the metadata upload and file upload flow; the sequential ordering of the two flows are interchangeable so the absence of metadata should not cause data upload to fail and vice versa.

### Steps in Data Flow
The following steps correlate to the legend in the diagram. 
1. User logs in, asks broker to create an empty submission/envelope
2. Broker asks Ingestion to create a new envelope for the user, Ingest returns submission ID
3. Request tmp space allocation on staging for file uploads
4. Receive staging area ID, plus a URL where it resides, credentials for access associated with submission
5. Data from 4 returned to user
6. User deposits data in staging at given URL
7. User prepares metadata, references sequence data staging URL
8. Broker pushes metadata files to Ingestion
9. For each metadata file, validate (syntax, semantics, JSON schema, check references)
10. For each metadata file with associated file data, check if file exists
11. For each existing data file, perform file validation
12. Poll for validation report - validation status for each metadata and data file, validation status for overall submission/envelope
13. User clicks the submit button
14. Broker triggers a submit in Ingest
15. Broker polls for the status of the submission
16. Stage necessary metadata files then generate and transmit a data bundle to DSS
    * An empty bundle for the envelope is created on the DSS
    * Metadata documents in the envelope are retrieved from the Ingest DB and then placed in a staging area for transmission to the DSS
    * The DSS is informed of the staging locations of all metadata and data files in the envelope 
17. The metadata in Ingest is updated to link to the new cloud URLs for data files
18. Polling of DSS for storage status of the bundle
19. Cleanup of staging files once the confirmed that DSS has received the bundle
20. The analysis pipelines poll for events from DSS
21. Pipeline fetch necessary data files from the DSS
22. Pipelines do their analysis, and begin the Ingestion process again at step 1. (Staging steps may be skipped at a later stage but for now green will behave just like a broker)

![Ingestion Flow]({{ "/images/Ingestion Flow.webp" | absolute_url }})

### User flow
The above section outlines how systems are expected to interact with each other. The user interactions with this process are described in the user flow diagram.

## Functional Specification
### Core entities
#### Metadata documents
A uniquely identifiable metadata document will describe an informational aspect of an experimental run or analysis. For example, a sample metadata object will describe information about the source of a biological material used in an experiment. It may also refer to the project for which this sample was taken. An assay metadata document could describe the assaying process, as well as refer to a collection of sample metadata documents which identify and describe the samples used. It is intended that there will be a set number of types of metadata document that can be ingested and processed into the HCA. It is also anticipated that the number of such types will increase over time. 

#### Submission Envelope
In the ingestion service, a uniquely identifiable submission envelope tracks a collection of metadata documents which describe a single payload of information provided by a submitter. The granularity of a submission envelope is intentionally not specified so as to allow submitters or brokers to provide data and metadata in ways that support respective data generation processes. Submission envelopes can therefore be “data only”, “metadata only”, or combinations of both at various levels of detail.

All metadata documents created through the Ingestion service must relate back to a submission object. Submission objects contain a reference to the creating user, the user’s email, the user’s team and the user’s ID in the identity management service. A submission object has a status field which tracks the state of the submission throughout the ingestion process, and is largely determined by the state of the referencing metadata documents. At any time, a user can attempt to finalise a submission by requesting to change the state of a submission to “submitted”.

Submission envelopes will be assigned a UUID at the point of creation and can be accessed via a URL through the ingest API only.

#### Validation Report
A validation report, or validation result, document describes the outcome of a validation job that has been run on a metadata document or on a bulk data file. Each piece of metadata and bulk data file will be linked to a uniquely identified validation report. The validation report will include details on the types of validation that were run, the outcomes of those validation jobs and any errors, warnings or suggestions raised. 
Aggregated Validation Report
An aggregated validation report will be created for every submission. It will contain the overall validation result of an entire submission, determined by the validation result of the metadata documents and bulk data files in the submission. Included will be links to its depending “child” validation reports.

#### Metadata Schema
A schema will set constraints on the structure, content and semantics of a metadata document, and will be defined by the metadata working group. Users will be able to upload their own schemata to support project specific requirements. User submitted schemata will be subject to review by the metadata working group following the metadata validation rules and schema SOP. Users submitting documents associated with a project with its own metadata schema will have to adhere to these constraints. An example constraint for a project relating to the sampling and assaying of human liver tissue may be a constraint on “taxon_id” to be 9606 (human) and “organ” to be an ontology term for the human liver. 

### Ingest Broker Functionality
Brokers are free to define their own range of functionality.

It is anticipated that most brokers will wish to support at least the following:
Provide a listing of metadata schemata that will apply to submissions,
Provide an example metadata file for each type of entity being collected,
Provide a downloadable template (e.g. as a spreadsheet) for each metadata file type,
Provide an indication of validation success or validation errors / warnings for each metadata file uploaded or created

### Staging Service Functionality
Staging Service functionality is described in the document Data File Staging Service Specifications.

### Ingest API Functionality
A REST API will be provided to enable the creation and manipulation of metadata documents. Metadata documents will be resources in the Ingestion service, representing a set number of document types defined by the metadata working group. The REST API will expose endpoints which will enable the standard CRUD operations on metadata documents. An OpenAPI specification will be available for all API endpoints exposed by the ingest API.

API endpoints will be prefixed with a path such as: /api/ingest/v1/. 

|Endpoint|Supported operations|Description|
|--------|--------------------|-----------|
|/schemata|GET<br/>POST|List metadata schemata (JSON schema format). Create a new metadata schema. The payload of the request will be a metadata specification that either extends an existing type or proposes a new type. This operation will return a 202 Accepted response, and the schema proposed sent to the metadata working group for review.|
|/schemata/{schema_id}|GET|Retrieve a metadata schema specification.|
|/submissions|GET<br/>POST|List submission envelopes.<br/>Create a new submission envelope.<br/>The submission envelope is associated with the user by user-attributes in the POST payload e.g email, team, ID in the identity management system.|
|/submissions/{sub_id}|GET<br/>DELETE|Retrieve a submission envelope.<br/>Delete a submission envelope. Internal use only.|
|/submissions/{sub_id}/status|GET<br/>PUT|View the status of a submission envelope.<br/>Update a submission envelope status e.g. when validation has completed. Internal use only.<br/>Status objects are created when a submission envelope is created, and therefore cannot be explicitly created.|
|/projects<br/>/samples<br/>/assays<br/>/analyses|GET<br/>POST|List metadata documents of the appropriate type.<br/>Create a metadata document of the appropriate type. A POST request to the sample resource creates a sample metadata document that, at minimum, adheres to standards defined by the metadata working group. Similar for assay, analysis and all the other metadata types defined by the metadata working group.<br/>The payload of the requests will contain the experimental metadata itself, as well as a reference to the containing submission and references to any other metadata documents linked to the one being created.<br/>A POST request will trigger a validation of the newly created metadata document.|
|/projects/{project_id}<br/>/samples/{sample_id}<br/>/assays/{assay_id}<br/>/analyses{analysis_id}|GET<br/>PUT<br/>DELETE|Retrieve metadata documents of the appropriate type.<br/>Update a metadata document. Triggers revalidation of the metadata document and the envelope containing it.<br/>Remove a metadata document. Triggers revalidation of the envelope that contained this document.|
|/projects/{project_id}/status<br/>/samples/{sample_id}/status<br/>/assays/{assay_id}/status<br/>/analyses{analysis_id}/status|GET<br/>PUT|View the status of a metadata document as it progresses through ingestion.<br/>Update the status of a metadata document. Internal use only.<br/>Status objects are created when a metadata document is created, and therefore cannot be explicitly created|

### Accessioning Service Functionality
The accessioning service will not be accessible from outside ingest, as accessions will be assigned automatically as part of the ingest process. Assigned accessions and UUIDs will be provided as part of the response for individual metadata documents through the ingest API as described above.

### Ingest Datastore Functionality
The ingest datastore provides local storage, within ingest, for metadata documents that are not yet ready for storage in the DSS. This allows submitters to provide metadata descriptions at the point of generation, and means they are not required to pass metadata documents through systems not designed to handle this information e.g. LIMS systems. It also provides a clean separation of concerns; specific brokers can be designed for metadata collected by pathologists, and sequencing centres can implement data file connections that write directly to the staging area without having to reproduce earlier metadata.
The ingest datastore will be a MongoDB instance that stores normalized metadata documents. The ingest datastore will be agnostic to the actual document contents, as these will be determined by the metadata working group and are expected to change frequently. However, in order to store metadata documents in a normalized fashion, the ingest datastore needs to understand how metadata documents refer to each other, so the ingest API endpoints will accept a request body that encapsulates the user supplied content with operational content such as the metadata document identity (it’s UUID) and the references to other objects.

To allow the ingest service to store and interpret supplied metadata content, the ingest API will define a JSON format that allows it to interpret and reason over operational content (like identity, provenance and relationship information) independently from having to interpret metadata content as specified by the metadata working group.

The ingest API will accept JSON documents in the following format:
```json
{
  "identity": {
  "type": "sample",
  "accession": "GSM1957573",
  "submission_date": "2017-27-08T20:28:17.563Z",
  "last_update_date": "2015-12-07T00:00:00.000Z",
  "uuid": "c440e605-51fe-4420-ad32-eed24e88fe9d"
 },
 "references": [
  {
   "type":"sample",
   "relationship":"derived from",
   "uuid":"6860fb7c-6167-4b6c-9bae-58098f35cc05"
  }
 ],
 "content": {
  "body_part": {
   "name": "neocortex",
   "organ": "brain"
  },
  "long_label": "12 week post conception fetal neocortex",
  "ncbi_biosample": "SAMN04303778",
  ... other user supplied content here
 }
}
```
The ‘identity’ and ‘references’ sections support the addition of operationally required information. The ‘content’ section allows submitters to provide metadata in any of the supported HCA metadata formats, but the ingest API itself ignores this (although the validation service will not). The JSON schema for this format is TBD.

The ingest datastore will use reference blocks to identify links between metadata documents that may occur in independent submissions, but will need to be denormalized when dispatched to the datastore.

### Validation Service Functionality
The validation service will allow the generation of comprehensive reports on the validation processes spawned during the ingestion lifecycle. Reports will be generated at both a submission envelope level and at a metadata level.
 
Metadata validation reports will be generated in response to the creation or update of any submission envelope or metadata document. Data file validation reports will be generated whenever a data file is referred to from a metadata object (for example, assay metadata objects will refer to the data files they produce). Reports for data file validation will be attached to the report for the referring metadata object.

The Validation API will also cater for user defined metadata schemas and rules. Users of the Ingestion Service will be able to define their own metadata schemas that will extend the core schema and rules defined by the metadata working group.

Validation reports will be exposed to users via /status endpoints in the Ingest API, attached to submission envelopes and metadata objects.

### Tracking Service Functionality
The tracking service will allow the monitoring and reporting on the current state of a submission envelope. As a single submission may result in the creation of several bundles, and as a single bundle may be composed of information derived from several submission envelopes, the tracking service will also allow the mapping and reporting of links between submissions and bundles. Tracking reports will be generated at the level of a submission envelope and at the level of a metadata document.

#### Submission Envelope states
Submission envelope states represent a summary over the states of the metadata objects and data files they encapsulate. State transitions happen in response to user interactions or as the result of automated processing.

|State|Description|Transition|
|-----|-----------|----------|
|PENDING|A newly created submission envelope, containing no metadata or data file references. Pending submission envelopes are assigned a UUID but may not yet have been allocated staging space etc.|Transitions from PENDING to DRAFT when the envelope is ready to accept upload of either metadata or data files|
|DRAFT|A submission envelope that contains recently supplied metadata or data file references|Transitions from DRAFT to VALIDATING dynamically as soon as the ingest validation service detects new metadata documents and has capacity.|
|VALIDATING|A submission envelope that contains metadata or data file references, at least one of which is currently in the process of being validated|Transitions from VALIDATING to VALID/INVALID once validation has completed on all available documents|
|VALID|A submission envelope that contains metadata or data file references, all of which have been validated successfully|Transitions from VALID to DRAFT in response to the addition of new metadata or data files, or SUBMITTED in response to an event from the broker|
|INVALID|A submission envelope that contains metadata or data file references, at least one of which has failed validation with a critical error.|Transitions from INVALID to DRAFT in response to addition/update of metadata or datafiles. If datafiles are added without metadata changing, a user interaction ‘retry’ event must be posted.|
|SUBMITTED|A submission envelope that has successfully validated and which has been submitted by a broker|Transitions from SUBMITTED to PROCESSING dynamically, once the HCA agent begins the process of storage to DSS|
|PROCESSING|A submission envelope that is in the process of having its contents permanently archived in the DSS|Transitions from PROCESSING to CLEANUP once DSS has notified ingest that storage is complete. In the event of an error from DSS, transitions back to VALID.|
|CLEANUP|A submission envelope that is currently being cleaned up. This involves the removal of any unnecessary files from the staging service|Transitions to COMPLETE once staging service has notified ingest that cleanup is complete. In the event of an error from staging, transitions back to VALID|
|COMPLETE|A submission envelope that has completed submission processes. All appropriate elements of this submission are stored in the DSS and available for secondary analysis

Status reports will be exposed to users via /status endpoints in the Ingest API, attached to submission envelopes and metadata objects.

#### Metadata Document States
Metadata document states represent the individual state each metadata document may hold. State transitions occur in response to the output of the validation service.

|State|Description|Transition|
|-----|-----------|----------|
|DRAFT|A metadata document that has been recently created or updated|Transitions from DRAFT to VALIDATING dynamically, as soon as validation service has availability.|
|VALIDATING|A metadata document that is in the process of being validated|Transitions from VALIDATING to VALID once this document has successfully passed validation, or INVALID if it fails|
|VALID|A metadata document that has been successfully validated|Transitions from VALID to PROCESSING once the submission envelope is submitted and the request to store in DSS has been sent|
|INVALID|A metadata document that has undergone validation and failed|Transitions from INVALID to DRAFT in response to addition/update of content|
|PROCESSING|A metadata document that is in the process of being permanently archived in the DSS.|Transitions from PROCESSING to COMPLETE once the DSS confirms receipt of the dispatched metadata document|
|COMPLETE|A metadata document that has been successfully archived in the DSS|Transitions from COMPLETE to DRAFT if the content of this document is updated. Changes in related objects might also trigger this transition (for example, where multiple samples are stored in the same physical sample.json document, an update to one sample will trigger an update to the others).|

