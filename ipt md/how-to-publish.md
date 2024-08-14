# How to publish biodiversity data through GBIF.org

GBIF supports publication, discovery and use of four classes of data:

* [Resource metadata](resource-metadata.adoc)
* [Checklist Data](checklist-data.adoc)
* [Occurrence Data](occurrence-data.adoc)
* [Sampling Event Data](sampling-event-data.adoc)

At the simplest, GBIF enables sharing information describing a biodiversity data resource – even when no further digital information is currently available from the resource. Other data classes support an increasingly richer and wider range of information on species, their distributions and abundance.

Data publishers are strongly encouraged to share their data using the richest appropriate data class. This maximizes the usefulness of the data for users.

To give yourself an introduction to how the IPT can be used to publish biodiversity data through GBIF.org, it’s highly recommended watching this concise 25 minute live demo below:

**How to publish biodiversity data through GBIF.org using the IPT**

video::eDH9IoTrMVE[youtube,width=100%]

## Prerequisites

1. You require an account on a GBIF Integrated Publishing Toolkit (IPT) to publish your data.
   * Hint: it is highly recommended that you save yourself time and money by requesting an account on an IPT located at a [data hosting centre](https://www.gbif.org/data-hosting-centres) in your country or community.
   * Hint: you could install and maintain your own IPT instance if you have technical skills and capacity to maintain it online near 100% of the time.
   * Hint: if no data hosting centre exists in your country, and you or your organization don’t have the technical skills and capacity to host an IPT, you can contact the GBIF Help Desk &lt;helpdesk@gbif.org> for assistance.
2. Assuming that you would like to register your dataset with GBIF and make it globally discoverable via [GBIF.org](https://www.gbif.org), your dataset must be affiliated with an organization that is registered with GBIF.
   * Hint: to register your organization with GBIF, start by completing [this online questionnaire](https://www.gbif.org/become-a-publisher). The registration process can take days, so in parallel you can proceed to publish your data.
   * Hint: if you aren’t affiliated with any organization, you can contact the GBIF Help Desk &lt;helpdesk@gbif.org> for assistance. In the meantime, you can proceed to publish your data.

## Instructions

To publish your data, follow the 7 steps below.

![flow-all](ipt2/flow-all.png)

1. Select the class of biodiversity data you have from this list:
   * [Resource metadata](resource-metadata.adoc)
   * [Checklist Data](checklist-data.adoc)
   * [Occurrence Data](occurrence-data.adoc)
   * [Sampling Event Data](sampling-event-data.adoc)
2. Transform your data into a table structure, using Darwin Core (DwC) terms as column names
   * Hint: try using an Excel template to structure your data, and understand what DwC terms are required and recommended (Excel templates for each dataset class are available in the above links - see the previous point)
   * Hint: it is possible to use data stored in a [supported database](database-connection.adoc)
3. Upload your data to the IPT
   * Hint: refer to other sections of this manual for additional guidance, such as the [Manage Resources Menu](manage-resources.adoc) section.
4. Map the data (e.g. [Checklist Data](checklist-data.adoc) gets mapped to the {latest-dwc-taxon}[Taxon Core], [Occurrence Data](occurrence-data.adoc) gets mapped to the {latest-dwc-occurrence}[Occurrence Core], [Sampling Event Data](sampling-event-data.adoc) gets mapped to the {latest-dwc-event}[Event Core]).
5. Fill in resource metadata using the IPT’s metadata editor
6. Publish the dataset (make it freely and openly available worldwide)
7. Register the dataset with GBIF.

   **📌 NOTE**\
   Your organization must be registered with GBIF (see prerequisite 2 above) and added to your IPT by the IPT administrator. Otherwise, the organization will not be available to choose from in the IPT.
