# How To Add a New Core

**⚠️ WARNING**\
This page contains configuration instructions for advanced IPT users only

The IPT always ships with 3 cores installed by default: taxon, occurrence, and event. Since IPT 2.1, there is the possibility to add custom cores to the IPT, which is useful for communities prototyping new data standards. In this way, their community can start trying to map their data to the new core, and iteratively refine its set of properties.

The 3 steps below explain how to

1. create your new core,
2. register it with GBIF, and
3. configure an IPT to use it.

## Instructions

1. **Write Core XML Definition**

   The core XML definition has to comply with the [GBIF Extension Schema](http://rs.gbif.org/schema/extension.xsd). It is easiest to simply adapt an existing core definition, such as the {latest-dwc-occurrence}[Darwin Core Occurrence Core]. Please note, the core definition must contain a property that serves as the record identifier (e.g. http://rs.tdwg.org/dwc/terms/occurrenceID for the Occurrence core, or http://rs.tdwg.org/dwc/terms/eventID for the Event Core. The process of creating a new non-core extension is exactly the same as for a core extension. The process of creating a new vocabulary (as a data type for a property within the core, or non-core extension) is different only in that the XML definition has to comply with the [GBIF Thesaurus Schema](http://rs.gbif.org/schema/thesaurus.xsd). Once again, it is easiest to adapt an existing vocabulary definition, such as the {latest-basis-of-record}[Darwin Core Type vocabulary].
2. **Register Core with GBIF**

   While the core definition is still undergoing changes, it gets registered into the GBIF Sandbox Registry. To register your core, make a pull request to the rs.gbif.org repository following [these instructions](https://github.com/gbif/rs.gbif.org/blob/master/versioning.md#how-to-create-a-new-version-of-an-extension-or-vocabulary-on-rsgbiforg). If it passes inspection, it will be merged in to https://rs.gbif.org/sandbox/core/, and included in the [Sandbox Registry’s list of extensions](https://gbrdsdev.gbif.org/registry/extensions.json). When the core definition has been finalized, meaning that its set of properties has been frozen, it will be hosted at https://rs.gbif.org/core/ and included in the [Live Registry’s list of extensions](https://gbrds.gbif.org/registry/extensions.json) The same process applies to registering non-core extensions and vocabularies.
3. **Configure IPT**

   To configure the IPT to use the {sandbox-material-sample}[Material Sample Core] for example, add the following 2 lines to `$IPT_DATA_DIR/config/ipt.properties`.

   **📌 NOTE**\
   be sure to escape any colons like above*

   ```
   ipt.core_rowTypes=http\://rs.tdwg.org/dwc/terms/MaterialSample
   ipt.core_idTerms=http\://rs.tdwg.org/dwc/terms/materialSampleID
   ```

   This configures the IPT to recognize all extensions with rowType http://rs.tdwg.org/dwc/terms/MaterialSample as core types, and to use http://rs.tdwg.org/dwc/terms/materialSampleID as its identifier term. Multiple cores can be specified, delimiting them with the pipe `|` character. The first entry of ipt.core_idTerms is the ID for the first entry of core_rowTypes, and so on. Lastly, save the ipt.properties file, restart Tomcat, and then [install the core](administration.adoc#install-extension). The core is now available to use in the IPT.
