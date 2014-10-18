# CKAN

CKAN is open data portal software from OKFN: http://ckan.org/

This document is the start of a description of the CKAN object model.

## Objects

### Datasets

CKAN uses the words "package" and "dataset" interchangeably in its API and
source code for historical reasons.

Dataset fields come with a default set of validation rules, but CKAN sites
can override these rules and add other fields that will appear alongside
these fields.

Datasets may be referenced by passing either the id or name values as the
id parameter to API calls.

Dataset Field | Description
--- | ---
id | UUID generated when dataset is created (typically)
name | unique lowercase string used as the dataset slug
title | descriptive string used to generate the name field
notes | markdown format longer descriptive text (optional)
license_id | ...
owner_org | UUID of organization that may edit this dataset if applicable
tags | ...
groups | ...
url | link to the source of the dataset, typically a web site (optional)
version | a version number for the data (optional)
author | author name (optional)
author_email | (optional)
maintainer | maintainer name (optional)
maintainer_email | (optional)
resources | a list of resource objects, see below

Resources are repeating records that appear within datasets and link
to the actual data being cataloged.

Resource field validation may also be customized by the site owner.
Extra fields may appear alongside these fields in each resource.

Resource Field | Description
--- | ---
id | a UUID generated when the resource is created
url | link to the data file if applicable
name | text description of this data file (optional)
description | markdown format longer descriptive text for this file (optional)
format | file format such as CSV, XML, etc.

When the contents of tabular data files have been uploaded into the CKAN
datastore they are available by the datastore API. The table names in the
datastore are based on the resource id values.

[The datastore API](http://docs.ckan.org/en/latest/maintaining/datastore.html#the-datastore-api)
allows the type to be set for each column, or data may be loaded
automatically and the types will be guessed.

Datastore Column Type | Description
--- | ---
text | unicode string
json | JSON data
date | YYYY-MM-DD
time | HH:MM:SS
timestamp | ISO 8601 format date
int | integer
float | IEEE 754 floating point
bool | 'true' or 'false'

These types are based on [PostgreSQL data types](http://www.postgresql.org/docs/9.3/static/datatype.html)

## Established Mappings

Dataset Field | Mapping
--- | ---
url | foaf:homepage
author | dc:creator
author_email | dc:creator
maintainer | dc:contributor
maintainer_email | dc:contributor
