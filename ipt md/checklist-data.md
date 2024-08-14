# Checklist Data

Resources comprising a list of species belonging to some category (e.g. taxonomic, geographic, trait-based, red list, crop wild relative) and optionally with higher classification and/or additional traits associated with each species.  Examples of such datasets include global or regional taxonomic checklists, global or national red lists, catalogues of species included in undigitized collections, park checklists, etc. If sufficient information exists in the source dataset (or applies consistently to all species in the checklist), it is recommended that these datasets are presented as [Occurrence Data](occurrence-data.adoc). These datasets include the same basic descriptive information included under [Resource metadata](resource-metadata.adoc).

## How to transform your data into checklist data

![flow-cd](ipt2/flow-cd.png)

Ultimately your data needs to be transformed into a table structure using Darwin Core (DwC) term names as column names.

Try putting your data into the [Excel template](#templates), which includes all [required DwC fields](#Required DwC Fields) and [recommended DwC fields](#Recommended DwC Fields).

Alternatively if your data is stored in a [supported database](database-connection.adoc), you can write an SQL table (view) using DwC column names. Be careful to include all [required DwC fields](#Required DwC Fields) and add as many [recommended DwC fields](#Recommended DwC Fields) as possible.

For extra guidance, you can refer to the guide [Best Practices in Publishing Species Checklists](best-practices-checklists.adoc) and look at the [exemplar datasets](#Exemplar Datasets).

### Templates

[![Excel Template]({attachmentsdir}/downloads/checklist_ipt_template_v1.xlsx)(ipt2/excel-template2.png)]
[![Excel Template (with example data)]({attachmentsdir}/downloads/checklist_ipt_template_v1_example_data.xlsx)(ipt2/excel-template-data2.png)]

Populate it and upload it to the IPT. Try to augment it with as many [DwC terms](http://rs.tdwg.org/dwc/terms/) as you can. You can augment your core table with extra DwC columns, but only DwC terms from this {latest-dwc-taxon}[list].

### Required DwC fields

* [taxonID](https://dwc.tdwg.org/terms/#dwc:taxonID)
* [scientificName](https://dwc.tdwg.org/terms/#dwc:scientificName)
* [taxonRank](https://dwc.tdwg.org/terms/#dwc:taxonRank)

### Recommended DwC fields

* [kingdom](https://dwc.tdwg.org/terms/#dwc:kingdom) - and other higher taxonomy if possible
* [parentNameUsageID](https://dwc.tdwg.org/terms/#dwc:parentNameUsageID) - in situations where a taxonomy is meant to be published
* [acceptedNameUsageID](https://dwc.tdwg.org/terms/#dwc:acceptedNameUsageID) - in situations where a taxonomy is meant to be published

### Exemplar datasets

* [Database of Vascular Plants of Canada (VASCAN)](https://doi.org/10.5886/zw3aqw)

### FAQ

#### Q. *How do I add common names to a taxon record?*

**A.** Make a table of common names. The table must include a taxonID column. That way, each row can link to the (core) taxon record. You can augment your common names table with extra columns, but only using term names from this {latest-vernacularname}[list]. You can upload this table to the IPT, and map it to the {latest-vernacularname}[Vernacular Name extension].

#### Q. *How do I add the threat status of a species as defined by IUCN?*

**A.** Make a table of geographic distributions of a taxon. The table must include a taxonID column. That way, each row can link to the (core) taxon record. You can augment your geographic distributions table with extra columns such as the threat status, but only using term names from this {latest-species-distribution}[list]. You can upload this table to the IPT, and map it to the {latest-species-distribution}[Species Distribution extension].

#### Q. *Can I update the https://doi.org/10.15468/39omei[GBIF Backbone Taxonomy] with names from my checklist?*

**A.** Yes. To do so, you must publish your checklist, make it publicly available online under a GBIF-supported license (CC0, CC-BY, CC-BY-NC) and register it with GBIF. GBIF can then manually review it to determine if it is a suitable backbone source, e.g. by looking at how its names overlap with the backbone. Ideally the checklist will provide at least a minimal classification like a [kingdom](https://dwc.tdwg.org/terms/#dwc:kingdom) and [family](https://dwc.tdwg.org/terms/#dwc:family), be of high data quality meaning it has few name usage issues, include [scientificNameAuthorship](https://dwc.tdwg.org/terms/#dwc:scientificNameAuthorship) of names, supplying the [namePublishedIn](https://dwc.tdwg.org/terms/#dwc:namePublishedIn) reference, etc.
