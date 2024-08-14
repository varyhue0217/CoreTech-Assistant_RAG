# Sampling Event Data

## Introduction

Resources which present evidence not only of the occurrence of a species at a particular place and time, but also sufficient detail to assess community composition for a broader taxonomic group or relative abundance of species at multiple times and places.  Such datasets derive from standardized protocols for measuring and observing biodiversity.  Examples include vegetation transects, standardized bird census data, eco-genomic samples, etc. These add to Occurrence Data by indicating what protocol was followed, which occurrence records derive from a sampling event following the protocol, and ideally the relative abundance (by a suitable numerical measure) of species recorded in the sample.  These additional elements can support better comparison of the data from different times and places (where the same protocol is indicated) and may in some cases enable researchers to infer the absence of particular species from particular sites. These datasets include the same basic descriptive information included under [Resource metadata](resource-metadata.adoc) and the same standard elements as in [Occurrence Data](occurrence-data.adoc).

## How to transform your data into sampling event data

![flow-sed](ipt2/flow-sed.png)

Ultimately your data needs to be transformed into two tables using Darwin Core (DwC) term names as column names: one table of sampling events and another table of species occurrences derived from (associated to) each sampling event.

Try putting your data into the [Excel template](#templates), which includes two sheets: one for sampling events and another for associated species occurrences.

Alternatively, if your data is stored in a [supported database](database-connection.adoc), you can write two SQL tables (views) using DwC column names: one for sampling events and another for associated species occurrences.

Each sampling event record should include all [required DwC fields](occurrence-data.adoc#required-dwc-fields) and as many [recommended DwC fields](occurrence-data.adoc#recommended-dwc-fields) as possible. You can augment your table with extra DwC columns, but only DwC terms from this {latest-dwc-event}[list].

Similarly, each species occurrence record should include all [required DwC fields](occurrence-data.adoc#required-dwc-fields) and as many [recommended DwC fields](occurrence-data.adoc#recommended-dwc-fields) as possible. You can augment your table with extra DwC columns, but only DwC terms from this {latest-dwc-occurrence}[list]. Some DwC terms will be redundant meaning they are added to both sampling event and species occurrence records. As a general rule, try not to add redundant terms with the same values. It is fine if they have different values though, for example, if you wanted to define a location of an event and then define more specific locations for individual occurrences. Otherwise, when the location of individual occurrences isn’t supplied, its location gets inherited from the event.

For extra guidance, you can refer to the guide [Best Practices in Publishing Sampling-event data](best-practices-sampling-event-data.adoc) and look at the [template populated with example data](#templates) or the list of [exemplar datasets](#exemplar-datasets).

### Templates

[![Excel Template]({attachmentsdir}/downloads/event_ipt_template_v2.xlsx)(ipt2/excel-template2.png)]
[![Excel Template (with example data)]({attachmentsdir}/downloads/event_ipt_template_v2_example_data.xlsx)(ipt2/excel-template-data2.png)]

Populate it and upload it to the IPT.

### Required DwC fields

* [eventID](https://dwc.tdwg.org/terms/#dwc:eventID) - also required for associated occurrence data (to link them together)
* [eventDate](https://dwc.tdwg.org/terms/#dwc:eventDate)
* [samplingProtocol](https://dwc.tdwg.org/terms/#dwc:samplingProtocol)

### Recommended DwC fields

* [sampleSizeValue](https://dwc.tdwg.org/terms/#dwc:sampleSizeValue) & [sampleSizeUnit](https://dwc.tdwg.org/terms/#dwc:sampleSizeUnit)
* [parentEventID](https://dwc.tdwg.org/terms/#dwc:parentEventID) - in situations where the event is part of an event series
* [samplingEffort](https://dwc.tdwg.org/terms/#dwc:samplingEffort) - to provide evidence of rigour of sampling event
* [locationID](https://dwc.tdwg.org/terms/#dwc:locationID) - in situations where the plot/transect being sampled has a unique identifier
* [decimalLatitude](https://dwc.tdwg.org/terms/#dwc:decimalLatitude) & [decimalLongitude](https://dwc.tdwg.org/terms/#dwc:decimalLongitude) & [geodeticDatum](https://dwc.tdwg.org/terms/#dwc:geodeticDatum) - to provide a specific point location
* [footprintWKT](https://dwc.tdwg.org/terms/#dwc:footprintWKT) & [footprintSRS](https://dwc.tdwg.org/terms/#dwc:footprintSRS) - to provide a specific shape location
* [countryCode](https://dwc.tdwg.org/terms/#dwc:countryCode)
* [occurrenceStatus](https://dwc.tdwg.org/terms/#dwc:occurrenceStatus) - only for associated occurrence data to record presence/absence data.

### Exemplar datasets

* [Israeli Butterfly Monitoring Scheme (BMS-IL)](http://cloud.gbif.org/eubon/resource?r=butterflies-monitoring-scheme-il)
* [Dutch Vegetation Database (LVD)](http://cloud.gbif.org/eubon/resource?r=lvd)
* [Lepidurus arcticus survey Northeast Greenland 2013](http://gbif.vm.ntnu.no/ipt/resource?r=lepidurus-arcticus-survey_northeast-greenland_2013)
* [Insects from light trap (1992–2009), rooftop Zoological Museum, Copenhagen](http://danbif.au.dk/ipt/resource?r=rooftop)

### FAQ

#### Q. How do I indicate that a sampling event was part of a time series?

**A.** All sampling events at the same location must share the same [locationID](https://dwc.tdwg.org/terms/#dwc:locationID).

#### Q. How do I publish a hierarchy of events (recursive data type) using parentEventID?

**A.** The classic example is sub-sampling of a larger plot. To group all (child) sub-sampling events under the (parent) sampling event, the parentEventID of all sub-sampling events must be set to the eventID of the (parent) sampling event. To be valid, all parentEventIDs must reference eventIDs of records defined in the same dataset. Otherwise, the parentEventID must be a globally unique identifier (e.g. DOI, HTTP URI, etc) that resolves to an event record described elsewhere. Ideally, all (child) sub-sampling events share the same date and location as the (parent) event it references.

#### Q. How do I publish absence data?

**A.** **Step 1**: Make species absences explicit by adding a species occurrence record for each species that could have been observed at the time and place of sampling, but was not observed, by setting the following fields:

Mandatory:

* [occurrenceStatus](https://dwc.tdwg.org/terms/#dwc:occurrenceStatus)=[absent]({latest-occurrence-status})

Optional (provide one or both):

* [individualCount](https://dwc.tdwg.org/terms/#dwc:individualCount)="0"
* [organismQuantity](https://dwc.tdwg.org/terms/#dwc:organismQuantity) and [organismQuantityType](https://dwc.tdwg.org/terms/#dwc:organismQuantityType) pair: "0", "individuals"

Alternatively, include sampling event records even if the sampling yielded no derived species occurrences. This allows species absences to be inferred. This [example sampling event dataset from Norway](https://gbif.vm.ntnu.no/ipt/resource?r=lepidurus-arcticus-survey_northeast-greenland_2013) ([also on GBIF.org](https://www.gbif.org/occurrence/search?dataset_key=78360224-5493-45fd-a9a0-c336557f09c3)) demonstrates how this looks.

**Step 2**: Define the taxonomic scope of all sampling events included in the dataset, it is recommended to publish a timestamped checklist together with the sampling event dataset, which represents the species composition that could be observed at the time and place of sampling given the sampling protocol (and/or the taxonomic coverage of the study and the expertise of the personnel carrying out identification). This would allow for accurate presence/absence data to be recorded. In addition to the normal (expected) species composition, the checklist could include invasive (unexpected) species. For taxonomic and biogeographical/ecological reasons, however, this checklist would exist solely within the context of the sampling event dataset.

Instructions on how to create a checklist can be found [here](checklist-data.adoc). Detailed metadata should be included with the checklist describing a) the people who performed the identifications and their taxonomic expertise and b) how it was decided that these species were detectable & identifiable at the time and place of sampling.

To link the checklist to the sampling event dataset, add the checklist to the dataset metadata in the [External links](manage-resources.adoc#external-links) section.
