# Darwin Core Archives – How-to Guide

Version 2.2

![cover_art_cicindelinae](figures/cover_art_cicindelinae.png)

## Document Control

| Version | Description | Date of release | Author(s) |
| --- | --- | --- | --- |
| [1.0](http://links.gbif.org/gbif_dwc-a_how_to_guide_en_v1) | Content review and additions | April 2011 | David Remsen, Markus Döring |
| 2.0 | Transferred to wiki, major edits | 9 May 2017 | Kyle Braak |
| [2.1](https://github.com/gbif/ipt/wiki/DwCAHowToGuide) | Minor edits, updating links etc | 8 February 2021 | Matthew Blissett |
| [2.2](dwca-guide.adoc) | Conversion to AsciiDoc | 25 May 2021 | Matthew Blissett |

## Suggested citation

> GBIF (2021) Darwin Core Archives – How-to Guide, version 2.2. Copenhagen: GBIF Secretariat. https://ipt.gbif.org/manual/en/ipt/{page-version}/dwca-guide

_Cover art credit: Kim Wismann, Cicindelinae_

## What is Darwin Core Archive (DwC-A)?

Darwin Core Archive (DwC-A) is a biodiversity informatics data standard that makes use of the Darwin Core terms to produce a single, self contained dataset for sharing species-level (taxonomic), species-occurrence data, and sampling-event data. An archive is a set of text files, in standard comma- or tab-delimited format, with a simple descriptor file (called **meta.xml**) to inform others how the files are organized. The format is defined in the [Darwin Core Text Guidelines](https://dwc.tdwg.org/text/). **It is the preferred format for publishing data in the GBIF network.**

The central idea of an archive is that its data files are logically arranged in a star-like manner, with one core data file surrounded by any number of ‘extension’ data files. Core and extension files contain data records, one per line. Each extension record (or ‘extension file row’) points to a record in the core file; in this way, many extension records can exist for each single core record. This is sometimes referred to as a “star schema”.

![The components of a Darwin Core Archive.](figures/dwc-a_event.png)

Sharing entire datasets as DwC-As allows simple and efficient data transfer of the whole dataset.  (Earlier systems, such as [DiGIR](http://digir.sourceforge.net/) and [TAPIR](http://tdwg.github.io/tapir/docs/tdwg_tapir_specification_2010-05-05.html), required the GBIF system to make many thousands of requests to retrieve all data in a single dataset, and there was a risk of data being missed.)

The production of a DwC-A requires the use of stable identifiers for core records, but not for extensions. For any kind of shared data it is therefore necessary to have some sort of local record identifiers. It is good practice to maintain – with the original data – identifiers that are stable over time and are not being reused after the record is deleted. If possible, please provide globally unique identifiers (GUID) instead of local ones. Refer to [A Beginner’s Guide to Persistent Identifiers](http://links.gbif.org/persistent_identifiers_guide_en_v1.pdf) for more information about GUIDs. This identifier is referred to as the “core ID” in DwC-As and the specific Darwin Core term that it corresponds to is dependent on the data type being published.

### DwC-A Components

A DwC-A may consist of a single data file or multiple files, depending on the scope of the published data. The specific types of files that may be included in an archive are the following:

1. **A required core data file** consisting of a standard set of [Darwin Core terms](http://rs.tdwg.org/dwc/terms/). The data file is formatted as **fielded text**, where data records are expressed as rows of text, and data elements (columns) are separated with a standard delimiter such as a tab or comma (commonly referred to as CSV or [‘comma-separated value’ files](https://en.wikipedia.org/wiki/Comma-separated_values)). The first row of the data file may optionally contain data or represent a ‘header row’. In general, if a header row is included, it contains the names of the Darwin Core terms represented in the succeeding rows of data.
GBIF currently supports the following three biodiversity data types as the basis for a core data file:

   1. **Occurrence data** — The category of information pertaining to evidence of an occurrence in nature, in a collection, or in a dataset (specimen, observation, etc.). Core files of this type are used to share information about a specific instance of a taxon such as a specimen or observation. The required core ID is represented by **dwc:occurrenceID**. The definitive list of Occurrence terms can be found in the {latest-dwc-occurrence}[Occurrence (Core) Extension].
   2. **Checklist data** — The category of information pertaining to taxa or taxon concepts, such as species. Core files of this type are used to share annotated species checklists, taxonomic catalogues, and other information about taxa. The required core ID is represented by **dwc:taxonID**. The definitive list of core Taxon terms can be found in the {latest-dwc-taxon}[Taxon (Core) Extension].
   3. **Sampling-event data** — The category of information pertaining to a sampling event. Core files of this type are used to share information about ecological investigations that can be one-off studies or monitoring programmes that are usually quantitative, calibrated and follow certain protocols so that changes and trends of populations can be detected. The required core ID is represented by **dwc:eventID**. The definitive list of core Event terms can be found in the {latest-dwc-event}[Event (Core) Extension].

   ![A core data file is a simple](figures/core_data_file.png)
2. **Optional “extension” files** support the exchange of additional, described classes of data that relate to the core data type (Occurrence or Taxon). An extension record points to a record in the core data file. Extensions may apply only to Taxa or Occurrences or may apply to both. For example, the Vernacular Names extension (illustrated below) is an extension to the Taxon class, whereas an Images extension may be used in both. Extensions can be created and added to the GBIF Extension Repository following a consultation and development process with GBIF. The definitive list of supported Extensions can be found on the [GBIF Extension Repository](https://rs.gbif.org/extensions.html).

   ![An extension is linked to the core file via the common taxon ID](figures/extension_data_file.png)
3. A descriptor **metafile** describes how the files in your archive are organized. It describes the files in the archive and maps each data column to a corresponding standard Darwin Core or Extension term. The metafile is a relatively simple XML file format. GBIF provides an online tool for making this file but the format is simple enough that many data administrators will be able to generate it manually. These options are described in the Publishing Options section of this document.

   **📌 NOTE**\
   A metafile is **required** when an archive includes any extension files or if a single core data file uses non-standard column names in the first (header) row of data. A complete reference guide to this metafile is [available](gbif-metadata-profile.adoc).

   ![The metafile describes the file names and fields in the core and extension files](figures/meta_file.png)
4. Datasets require documentation. This is achieved in a DwC-A by including a **resource metadata document** that provides information about the dataset itself such as a description (abstract) of the dataset, the agents responsible for authorship, publication and documentation, bibliographic and citation information, collection methods and much more. GBIF currently supports a metadata profile based on the {eml-location}/index.html[Ecological Metadata Language] but other metadata standards exist and may be supported. The GBIF Metadata Profile’s XML Schema description can be found on the [GBIF Schema Repository](http://rs.gbif.org/schema/eml-gbif-profile/)

   ![A metadata document describes the complete dataset](figures/metadata_file.png)

   The entire collection of files (core data, extensions, metafile, and resource metadata) should be compressed into a single archive file. The supported compression formats are [ZIP](https://en.wikipedia.org/wiki/ZIP_(file_format)) and [TAR.GZ/TGZ](https://en.wikipedia.org/wiki/Tar_(file_format)).

   ![Text files are zipped into a single archive](figures/zipped_archive.png)

   This single, compressed file is the DwC-A file!

## DwC-A Data Publishing Solutions

There are a number of different options for generating a DwC-A.

To help select the most appropriate solution for creating your own archive, consider the following questions:

1. Have your data been digitized? (If yes, it is assumed that you can easily convert the data into CSV or Tab format).
2. Are your data stored in a relational database?
3. How many separate datasets (DwC-Archives) do you plan to publish?

[Publishing DwC-A using the IPT](#publishing-dwc-a-using-the-ipt) is most suitable when:

* Your data have been digitized already.
* Your data either are or are not already in a relational database
* You need to create/manage multiple archives.
* You would like to document datasets using the GBIF Metadata Profile.

[Publishing DwC-A using GBIF Spreadsheet Templates](#publishing-dwc-a-using-gbif-spreadsheet-templates) is most suitable when:

* Your data have not been digitized already.
* You already maintain data using spreadsheets.
* You need a simple solution to create/manage a limited number datasets
* You need extra guidance capturing and formatting the data

[Publishing DwC-A manually](#publishing-dwc-a-manually) is most suitable when:

* Your data have been digitized already.
* Your data may be in a relational database.
* You only need to create/manage a small number of archives, and/or you have the technical skills to automate/script the archive generation process.

A more detailed discussion of these three options follows.

### Publishing DwC-A using the IPT

**Assumption: Your data are already stored as a CSV/tab text file, or in one of the supported relational database management systems (MySQL, PostgreSQL, Microsoft SQL Server, Oracle, Sybase). Ideally, you are already using Darwin Core terms as column names, although this is not required.**

The [Integrated Publishing Toolkit (IPT)](index.adoc) is GBIF’s flagship tool for publishing DwC-As.

The simplest way to begin using the IPT is to request a free account on a [trusted data hosting centre](https://www.gbif.org/data-hosting-centres) allowing you to manage your own datasets and publish them through GBIF.org without the hassle of setting up and maintaining the IPT on your own server.

Otherwise if want to setup your own instance of the IPT the [Getting Started Guide](getting-started.adoc) is your entry point.

The IPT can be used to publish resource metadata, occurrence data, checklist data, and sampling-event data. The guide [How to publish biodiversity data through GBIF.org](how-to-publish.adoc) provides a simple set of instructions how to do so.

The IPT outputs a DwC-A during publishing and supports automatic registration in the GBIF network. See the [IPT User Manual](manage-resources.adoc#visibility) for further details.

### Publishing DwC-A using GBIF Spreadsheet Templates

**Assumption: The occurrence data, simple taxonomic data, or sampling-event data to be published are not yet captured in digital format OR a simple solution for creating a metadata document to describe a dataset is desired.**

GBIF provides a set of pre-configured Microsoft Excel spreadsheet files that serve as templates for capturing occurrence data, checklist data, and sampling-event data:

1. [Checklist data template](checklist-data.adoc#templates): suitable for basic species checklists
2. [Occurrence data template](occurrence-data.adoc#templates): suitable for occurrence data (specimen, observation)
3. [Sampling-event data template](sampling-event-data.adoc#templates): suitable for sampling-event data

Each template provides inline help and instructions in the worksheets.

To publish the data as a DwC-A, upload the templates to the IPT. Use the IPT’s built-in metadata editor to enter dataset metadata. The guide [How to publish biodiversity data through GBIF.org](how-to-publish.adoc) provides a simple set of instructions how to do so. If you require an account on an IPT, it is highly recommended that you request an account on a [trusted data hosting centre](https://www.gbif.org/data-hosting-centres) located in your country or community.

### Publishing DwC-A manually

**Assumption: Data is already in a CSV/Tab text file, or in one of the supported relational database management systems (MySQL, PostgreSQL, Microsoft SQL Server, Oracle, Sybase). The publisher does not wish to host an IPT instance but does have access to a web server.**

DwC-As can be created without installing any dedicated software. These instructions target data managers who are familiar with the dataset to be published and are comfortable working with their data management system.

Below is a set of instructions on how to manually create a DwC-Archive:

1. Unless the data are already stored in a CSV/Tab text file, the publisher needs to prepare a text file(s) from the source. If the data are stored in a database, generate an output of delimited text from the source database into an outfile. Most database management systems support this process; an example is given in the Annex to this guide, below, in the section “Outputting Data From a MySQL Database Into a Textfile”. As the metafile maps the columns of the text file to Darwin Core terms, it is not necessary to use Darwin Core terms as column header in the resultant text file, though it may help to reduce errors. A general recommendation is to produce a single core data file and a single file for each extension if the intention is to output data tied to an extension.
2. Create a Metafile: There are three different ways to generate the file:
   1. Create it manually by using an XML editor and using a sample metafile as a guiding example. A complete description of the metafile format can be found in the [Darwin Core Text Guide](http://rs.tdwg.org/dwc/terms/guides/text/index.htm).
   2. {blank}

      ![dwc-a_assistant](figures/dwc-a_assistant.png)

      Create it using the online application [Darwin Core Archive Assistant](http://tools.gbif.org/dwca-assistant/)  Simply select the fields of data to be published, provide some details about the files and save the resultant XML. This only needs to be done once unless the set of published fields changes at some later time.

      **⚠️ WARNING**\
      this tool is no longer supported by GBIF. Support for the Event core is missing. Publishers also need to manually add term dwc:taxonID to Taxon core and dwc:occurrenceID to Occurrence core, to ensure they are explicitly included.
3. Create a metadata file (eml.xml) that describes the data resource. Complete instructions on doing this are available in the [GBIF Extended Metadata Profile: How-To Guide](gbif-metadata-profile.adoc). It is best practice to include a metadata file and the simplest way to produce one is using the IPT’s built-in metadata editor.
4. Ensure the data files, the metafile (meta.xml) and metadata file (eml.xml) are in the same directory or folder. Compress the folder using one of the support compression formats. The result is a DwC-A.

**📌 NOTE**\
Metadata authored using IPT can be output as an RTF document, which can then be submitted as ‘Data Paper’ manuscript to Zookeys, PhytoKeys and BioRisks. See instructions to authors for ‘Data Paper’ submission to these journals.

## Validation of DwC-As

GBIF provides an online [DwC-Archive Validator](https://www.gbif.org/tools/data-validator) that performs the following checks:

* The metafile (meta.xml) is valid XML and complies with the [Darwin Core Text Guidelines](http://rs.tdwg.org/dwc/terms/guides/text/).
* The content complies with the known extensions and terms registered within the GBIF network. Note GBIF runs a production and a development registry that keeps track of extensions; the validator uses the production registry.
* The resource description file (eml.xml) is valid XML and complies with the GBIF Metadata Profile schema and the official EML schema.
* Referential integrity — that mapped ID terms in extension files reference existing core records.
* All core IDs are unique
* That no verbatim null values are found in the data. For example NULL or \N
* Taxonomy and locations pass typical GBIF interpretation processes (e.g. coordinates are within the specified country)

To use the validator:

1. Upload the DwC-A using the form provided in the Validator web page.
2. Validate
3. Review the response that and address any validation errors
4. Repeat the process until the file is successfully validated.
5. Contact the GBIF Help Desk if you get stuck (helpdesk@gbif.org).

## Registration of DwC-As with GBIF

An entry for the resource must be made in the GBIF Registry that enables the resource to be discoverable and accessible. Each new registration needs to be associated with a publishing organization that has been formally endorsed by a GBIF Participant Node manager. This is a simple quality control step required by the GBIF Participant Node Managers Committee.

Fortunately, the IPT and GBIF API support automatic registration for datasets. Otherwise if you are publishing DwC-As manually, initiate registration by sending an email to helpdesk@gbif.org with the following information:

1. Dataset title
2. Dataset description (copied from metadata file)
3. Publishing organization name (must be registered in GBIF, otherwise register it by filling in this [online questionnaire](https://www.gbif.org/become-a-publisher)).
4. Your relation to this organization
5. Dataset URL (publicly accessible address of zipped DwC-A)

You will receive a confirmation email, and a URL representing the resource entry in the Registry.

Advanced users can request permission to register datasets in bulk, by integrating the GBIF API into their existing systems.  A [basic example](https://github.com/gbif/registry/tree/master/registry-examples/src/test/scripts) is provided as a Linux (Bash) shell script; contact the Help Desk for more information.

## Annex: Preparing Your Data

### Required and recommended terms

The guide [How to publish biodiversity data through GBIF.org](how-to-publish.adoc) provides a set of required and recommended terms for each type of data:

1. Checklist data: [required terms](checklist-data.adoc#required-dwc-fields) / [recommended terms](checklist-data.adoc#recommended-dwc-fields)
2. Occurrence data: [required terms](occurrence-data.adoc#required-dwc-fields) / [recommended terms](occurrence-data.adoc#recommended-dwc-fields)
3. Sampling-event data: [required terms](sampling-event-data.adoc#required-dwc-fields) / [recommended terms](sampling-event-data.adoc#recommended-dwc-fields)
4. Resource metadata: [required terms](resource-metadata.adoc#required-dwc-fields) / [recommended terms](resource-metadata.adoc#recommended-dwc-fields)

### Character Encoding

Recommended best practice is to encode text (data) files using UTF-8.

The following tools for Linux, Mac and Windows can be used to convert character encodings of files:

* https://en.wikipedia.org/wiki/Iconv
* http://www.gnu.org/software/libiconv/
* http://gnuwin32.sourceforge.net/packages/libiconv.htm

Ex.: Convert character encodings from Windows-1252 to UTF-8 using [**iconv**](https://linux.die.net/man/1/iconv):

```shell
iconv -f CP1252 -t utf-8 example.txt > exampleUTF8.txt
```

### Data From a Database

It is easy to produce delimited text files from a database using the SQL commands. For MySQL, use the `SELECT INTO outfile` command. The encoding of the resulting file will depend on the server variables and collations used, and might need to be modified before the operation is done. Note that MySQL will export NULL values as `\N` by default. Use the IFNULL() function as shown in the following example to avoid this:

```sql
SELECT
  IFNULL(id, ''), IFNULL(scientific_name, ''), IFNULL(count,'')
  INTO outfile '/tmp/dwc.txt'
  FIELDS TERMINATED BY ','
  OPTIONALLY ENCLOSED BY '"'
  LINES TERMINATED BY '\n'
  FROM dwc;
```

Here are some other recommendations for generating data using SQL queries/functions:

* Concatenate or split strings as required, e.g. to construct the full scientific name string (watch out for autonyms)
* Format dates to conform to [ISO datetime format](https://en.wikipedia.org/wiki/ISO_8601) (1990-02-03, or 1990-02 if the day is unknown, 1990 if the month is also unknown, 1990-02-03/1990-02-28 to give a range).
* Create year/month/day by parsing native SQL date types
* Use a UNION to merge 2 or more tables, e.g. accepted taxa and synonyms, or specimen and observations

### DwC-A Examples

The guide [How to publish biodiversity data through GBIF.org](how-to-publish.adoc) provided a set of example DwC-As for each type of data:

1. Checklist data: [examplar datasets](checklist-data.adoc#exemplar-datasets)
2. Occurrence data: [examplar datasets](occurrence-data.adoc#exemplar-datasets)
3. Sampling-event data: [examplar datasets](sampling-event-data.adoc#exemplar-datasets)
4. Resource metadata: [examplar datasets](resource-metadata.adoc#exemplar-datasets)
