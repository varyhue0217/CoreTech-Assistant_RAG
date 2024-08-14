# Occurrence Data

## Introduction
Resources which present evidence of the occurrence of a species at a particular place and normally on a specified date.  These datasets expand on most Checklist Data because they contribute to mapping the historical or current distribution of a species. At the most basic, such datasets may provide only general locality information (even limited to a country identifier).  Ideally they also include coordinates and a coordinate precision to support fine scale mapping.  In many cases, these datasets may separately record multiple individuals of the same species. Examples of such datasets include databases of specimens in natural history collections, citizen science observations, data from species atlas projects, etc.  If sufficient information exists in the source dataset (or applies consistently to all occurrences in the dataset), it is recommended that these datasets are presented as [Sampling Event Data](sampling-event-data.adoc).  These datasets include the same basic descriptive information included under [Resource metadata](resource-metadata.adoc).

## How to transform your data into occurrence data

![flow-od](ipt2/flow-od.png)

Ultimately your data needs to be transformed into a table structure using Darwin Core (DwC) term names as column names.

Try putting your data into the [Excel template](#templates), which includes all [required DwC fields](#Required DwC Fields) and [recommended DwC fields](#Recommended DwC Fields).

Alternatively if your data is stored in a [supported database](database-connection.adoc), you can write an SQL table (view) using DwC column names. Be careful to include all [required DwC fields](#Required DwC Fields) and add as many [recommended DwC fields](#Recommended DwC Fields) as possible.

For extra guidance, you can look at the [exemplar datasets](#exemplar-datasets).

You can augment your table with extra DwC columns, but only DwC terms from this {latest-dwc-occurrence}[list].

### Templates

[![Excel Template]({attachmentsdir}/downloads/occurrence_ipt_template_v2.xlsx)(ipt2/excel-template2.png)]
[![Excel Template (with example data)]({attachmentsdir}/downloads/occurrence_ipt_template_v2_example_data.xlsx)(ipt2/excel-template-data2.png)]

Populate it and upload it to the IPT. Try to augment it with as many [DwC terms](http://rs.tdwg.org/dwc/terms/) as you can.

### Required DwC fields

* [occurrenceID](https://dwc.tdwg.org/terms/#dwc:occurrenceID)
* [basisOfRecord](https://dwc.tdwg.org/terms/#dwc:basisOfRecord)
* [scientificName](https://dwc.tdwg.org/terms/#dwc:scientificName)
* [eventDate](https://dwc.tdwg.org/terms/#dwc:eventDate)

### Recommended DwC fields

* [taxonRank](https://dwc.tdwg.org/terms/#dwc:taxonRank) - to substantiate scientificName
* [kingdom](https://dwc.tdwg.org/terms/#dwc:kingdom) - and other higher taxonomy if possible
* [decimalLatitude](https://dwc.tdwg.org/terms/#dwc:decimalLatitude) & [decimalLongitude](https://dwc.tdwg.org/terms/#dwc:decimalLongitude) & [geodeticDatum](https://dwc.tdwg.org/terms/#dwc:geodeticDatum) - to provide a specific point location
* [countryCode](https://dwc.tdwg.org/terms/#dwc:countryCode)
* [individualCount](https://dwc.tdwg.org/terms/#dwc:individualCount) / [organismQuantity](https://dwc.tdwg.org/terms/#dwc:organismQuantity) & [organismQuantityType](https://dwc.tdwg.org/terms/#dwc:organismQuantityType) - to record the quantity of a species occurrence

### Exemplar datasets

* [CUMV Amphibian Collection (Arctos)](http://ipt.vertnet.org:8080/ipt/resource.do?r=cumv_amph)

### FAQ

#### Q. How do I indicate a species was absent?

**A.** Set [occurrenceStatus](https://dwc.tdwg.org/terms/#dwc:occurrenceStatus)=["absent"]({latest-occurrence-status}). In addition, [individualCount](https://dwc.tdwg.org/terms/#dwc:individualCount) and [organismQuantity](https://dwc.tdwg.org/terms/#dwc:organismQuantity) should be equal to 0.

#### Q. How can I generalize sensitive species occurrence data?

**A.** How you generalize sensitive species data (e.g. restrict the resolution of the data) depends on the species' category of sensitivity. Where there is low risk of perverse outcomes, unrestricted publication of sensitive species data remains appropriate. Note it is the responsibility of the publisher to protect sensitive species occurrence data. For guidance, please refer to this [best-practice guide](https://www.gbif.org/resource/80512). You could refer to this [recent essay in Science](http://science.sciencemag.org/content/356/6340/800), which presents a simplified assessment scheme that can be used to help assess the risks from publishing sensitive species data.

When generalizing data you should try not to reduce the value of the data for analysis, and make users aware how and why the original record was modified using the Darwin Core term [informationWithheld](https://dwc.tdwg.org/terms/#dwc:informationWithheld).

As indicated in the [best-practice guide](http://www.gbif.org/resource/80512), you should also publish a checklist of the sensitive species being generalized. For each species you should explain:

* the rationale for inclusion in the list
* the geographic coverage of sensitivity
* its sensitivity category
* the date to review its sensitivity

This will help alert other data custodians that these species are regarded as potentially sensitive in a certain area and that they should take the sensitivity into account when publishing the results of their analyses, etc.

##### Helpful formulas for generalizing point location

The following formula obscures a latitude/longitude point by a factor of 5000m. Note pointX and pointY must be provided in 'length in meters' and TRUNC truncates the number to an integer by removing the decimal part:

```
pointX = TRUNC(pointX / 5000) * 5000
pointY = TRUNC(pointY / 5000) * 5000
```
