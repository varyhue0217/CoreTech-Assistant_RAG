# Resource Metadata

Description and contact details for a biodiversity information resource where no digital data can currently be shared.  All other classes of GBIF data also include this basic information.  Such metadata may be a valuable tool for researchers to discover resources which are not yet available online.  This is also a useful way to assess the importance and value of non-digital resources for future digitization. GBIF ensures that every dataset is associated with a Digital Object Identifier (DOI) to facilitate citation.

## How to write resource metadata

![flow-rm](ipt2/flow-rm.png)

Ultimately your metadata needs to be transformed into an XML metadata document. The XML must conform to the GBIF Metadata Profile, which is based on the Ecological Metadata Language (EML).

No Excel template exists for resource metadata. Simply use the IPT’s built-in metadata editor to populate the metadata. The IPT makes sure it’s in the proper valid XML format.

Alternatively if your metadata is already in EML or Dublin Core, you can upload it in these formats to the IPT. Guidance on how to do that can be found [here](manage-resources.adoc#upload-a-metadata-file).

For extra guidance, you can look at the [Exemplar datasets](#exemplar-datasets).

### Template

No Excel template exists for resource metadata. Simply use the IPT’s built-in metadata editor to populate the metadata.

### Required metadata fields

* title
* description
* publishing organization
* type
* license
* contact(s)
* creator(s)
* metadata provider(s)

### Recommended metadata fields

* sampling methodology - in situations where data comes from a sampling event
* citation - to ensure your dataset gets cited the way you want

## Exemplar datasets

* Inter-Valley Soil Comparative Survey of the McMurdo Dry Valleys: [EML](https://ipt.biodiversity.aq/eml.do?r=ictar_ivscs&v=1.0) / [IPT homepage](https://ipt.biodiversity.aq/resource.do?r=ictar_ivscs)

## FAQ:

### Q. What should I do if my data cannot be made freely available?

**A.** You should publicize its existence by publishing metadata about it. You can indicate the data can be made available by request, to encourage future collaboration and meta-analysis.

### Q. How can I apply a license to my dataset?

**A.** Simply use the IPT’s built-in metadata editor following [these instructions](applying-license.adoc#dataset-level).

Alternatively if your metadata is already in EML you should assign the dataset a machine readable license before uploading it to the IPT following [these instructions](applying-license.adoc#supplementary-information).

### Q. Can I add a link to the dataset's related data paper?

**A.** Yes. To do so, add a citation to the data paper to the bibliographic citations list. Take special care to include the data paper’s DOI as part of the citation. It should be written as a linkable URL (e.g. https://doi.org/10.1038/sdata.2017.16). This will make it possible to discover the data paper when reading the resource metadata.

### Q. GBIF assigned my dataset a DOI - can I add this to my metadata?

**A.** Yes. To do so, add the GBIF DOI, written as a linkable URL (e.g. https://doi.org/10.15468/nc6rxy) in the following places:

* Citation DOI (remember to turn on citation [auto-generation](manage-resources.adoc#citations), to ensure your dataset’s citation complies with the [best-practice format](citation.adoc)).
* Alternate identifiers list

Note GBIF only assigns a DOI to a dataset during registration if no DOI was previously assigned to it.

Also note that using the GBIF DOI in the citation may mislead users, as it resolves to the GBIF dataset page - not the online dataset. A DOI is preferred to using a URL to the online dataset, however, because it guarantees persistent access.
