# Exported Data Model

When someone wants to publish artifacts that use curated terminology, the first step is to run a scripted export process that transforms a subset of the corpus from the [internal data model](internal-data-model.md) to another structure so that that is optimally suited for the publication tools of choice. This new structure will contain de-normalized data, combining terms and their definitions to make them easier to render. Such a structure could take the form of a glossary or dictionary from which the publication tools can draw whatever they need to do the actual publishing. Typically, it would contain metadata and [adjusted some hyperlinks](#hyperlink-adjustment).

From this, it follows that there may be multiple exported data models. In order to get started, we specify what we currently think is needed to create an export script that, after having run on the (entire) corpus, produces a collection of markdown files that is ready to be futher processed/transformed by a publication tool like MkDocs, SpecUp, or Docusaurus. This means that a single folder is created within which a copy of every exported file will be placed (the files thus being siblings in that folder). They are named according to their associated [term ID](term-record.md#naming). Their internal structure is as follows:

## Term-related fields

All fields from the associated [term record](term-record.md) appear exactly as they did in the internal data model, except that [hyperlinks are adjusted](#hyperlink-adjustment).

## Concept-related fields

Most fields from the associated [concept record](concept-record.md) appear exactly as they did in the internal data model, except that [hyperlinks are adjusted](#hyperlink-adjustment). The execption is the [Concept ID field](concept-record.md#concept-id), which is suppressed.

## Generated fields

The following fields are automatically added to each exported file by the export algorithm:

* Tags U: The union of the Tags field and the Concept Tags field.
* Tags I: the intersection of the Tags field and the Concept Tags field.
* Hovertext: The first sentence of the Definition field.
* Contributors: A list of all github handles that have submitted content for this record.
* Synonyms: A list of [local hyperlinks](hyperlinks.md#local-links) to other terms that share the same definition.
* Term commit: The latest commit hash of the term record.
* Term version: How many unique versions of the term record exists.
* Concept commit: The latest commit hash of the concept record.
* Concept version: How many unique versions of the concept record exists.
* Export date: The UTC ISO 8601 timestamp when the export was created.

## Images
TODO: Are externally referenced images downloaded?

## Macros
TODO: Should we expand macros? For example, validate hyperlinks to confirm that they are still valid, and then update references in the way they sometimes show up in bibliographies: "retrieved &lt;date&gt;"?.

## Hyperlink Adjustment
* [Local links](hyperlinks.md#local-links) that are now part of the record are removed (if they don't have a fragment)
* [Local links](hyperlinks.md#local-links) that are not part of the current record are converted to refer to a sibling file.
* [Cross-scope links](hyperlinks.md#cross-scope-links) are converted to fully qualified links.

## Errors
TODO: How are errors handled?
