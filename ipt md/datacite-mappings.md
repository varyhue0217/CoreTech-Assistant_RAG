# DataCite to EML mappings

To understand how the IPT produces the DataCite metadata from the EML and IPT resource properties you can refer to the mappings below.

## Mappings

Legend:

* **DataCite property**: lists the name of the DataCite metadata property
* **Obl.**: Obligation, the property is (M) mandatory, \(R) recommended, and (O) optional
* **Occ**: Occurrence/cardinality, the property is (1-n) required and repeatable, (1) required but not repeatable, (0-n) optional and repeatable, (0-1) optional but not repeatable
* **IPT/EML property**: IPT resource property, or EML property the DataCite property maps to

|     |
| --- |
| DataCite property |
| Obl. |
| Occ. |
| IPT/EML property |
| identifier |
| M |
| 1 |
| resource DOI |
| identifierType |
| M |
| 1 |
| “DOI” - controlled value |
| creator |
| M |
| 1-n |
| resource creator (plus associate parties with role originator) |
| creatorName |
| M |
| 1 |
| resource creator name |
| nameIdentifier |
| R |
| 0-1 |
| resource creator ORCID |
| nameIdentifierScheme |
| M |
| 1 |
| ORCID (mandatory if nameIdentifier is used) |
| schemeURI |
| O |
| 0-1 |
| http://www.orcid.org |
| contributor |
| R |
| 0-n |
| resource contact, metadataProvider, and associatedParties with various roles |
| contributorName |
| R |
| 1 |
| resource contact name (mandatory if contributor is used) |
| contributorType |
| R |
| 1 |
| “ContactPerson” - controlled value (mandatory if contributor is used). Other role to controlled value mappings: author→"Other", contentProvider → “DataCollector”, custodianSteward → “DataManager”, distributor → “Distributor”, editor → “Editor”, metadataProvider → “DataCurator”, owner → “RightsHolder”, principalInvestigator → “ProjectLeader”, processor → “Producer”, publisher → “Editor”, user → “Other”, programmer → “Producer”, curator → “DataCurator” |
| nameIdentifier |
| R |
| 0-1 |
| resource contact  ORCID |
| nameIdentifierScheme |
| R |
| 1 |
| ORCID (mandatory if nameIdentifier is used) |
| schemeURI |
| R |
| 0-1 |
| http://www.orcid.org |
| title |
| M |
| 1-n |
| resource title, and titles in other languages using xml:lang attribute |
| titleType |
| O |
| 0-1 |
| “translatedTitle” |
| publisher |
| M |
| 1 |
| resource’s publishing organization. The choice of publisher must correspond to the organization against which the dataset is ultimately registered. |
| publicationYear |
| M |
| 1 |
| resource’s publication year |
| subject |
| R |
| 0-n |
| resource’s keyword(s) |
| subjectScheme |
| R |
| 0-1 |
| Thesaurus/Vocabulary if not URI |
| schemeURI |
| R |
| 0-1 |
| Thesaurus/Vocabulary if URI |
| date |
| M |
| 0-n |
| resource publication date (could also do temporal coverage dates) |
| dateType |
| M |
| 1 |
| “created” for initial publication, and “updated” for subsequent publications (mandatory if date is used). Other temporal coverage date types to controlled value mappings: Single date → “Valid”, Date range → “Valid” |
| language |
| O |
| 0-1 |
| resource language (ISO-639-1, e.g. “en”) |
| resourceType |
| R |
| 0-1 |
| resource datasetType/datasetSubtype |
| resourceTypeGeneral |
| R |
| 1 |
| “Dataset” - controlled value (mandatory if resourceType is used) |
| alternateIdentifier |
| O |
| 0-n |
| GBIF Portal dataset page URL and IPT public resource page URL |
| alternateIdentifierType |
| O |
| 1 |
| “URL” - controlled value (mandatory if alternateIdentifier is used) |
| RelatedIdentifier |
| R |
| 0-n |
| previous resource DOIs |
| relatedIdentifierType |
| R |
| 1 |
| “DOI” - controlled value (mandatory if RelatedIdentifier is used) |
| relationType |
| R |
| 1 |
| “IsNewVersionOf” - controlled value (mandatory if RelatedIdentifier is used). Additional relationTypes that could be described include: bibliographic citations using 'cites' relationship, relationship to external data using 'isVariantFormOf' relationship, relationship to eml.xml using 'HasMetadata' relationship |
| relatedMetadataScheme |
| O |
| 0-1 |
| GBIF Metadata Profile (used with HasMetadataFor relation) |
| schemeURI |
| O |
| 0-1 |
| http://rs.gbif.org/schema/eml-gbif-profile/1.0.2/eml-gbif-profile.xsd (used with HasMetadataFor relation) |
| schemeType |
| O |
| 0-1 |
| XSD (used with HasMetadataFor relation) |
| Format |
| O |
| 0-n |
| “DwC-A” - free text value |
| Size |
| O |
| 0-n |
| resource’s number of records, or size of DwC-A in MB |
| Version |
| O |
| 0-1 |
| major\_version.minor\_version (used in conjunction with RelatedIdentifier to indicate information updates to resource) |
| rights |
| O |
| 0-n |
| resource’s IPR (complete title e.g. Creative Commons Attribution 3.0) |
| rightsURI |
| O |
| 0-1 |
| resource’s IPR’s URI (e.g. http://creativecommons.org/lincenses/by/3.0 |
| Description |
| R |
| 0-n |
| resource description, with descriptions in multiple languages specified using xml:lang attribute |
| descriptionType |
| R |
| 1 |
| “Abstract” - controlled value (mandatory if Description is used). Additional descriptions can be described for methods, with descriptionType “Methods” |
| geoLocationBox |
| R |
| 0-1 |
| resource bounding box (first pair is SW point, second pair is NE point, e.g. 41.090 -71.032 42.893 -68.211) |
| geoLocationPlace |
| R |
| 0-1 |
| resource geographic description, free text. |
