# CUL_OpenRefine2Hyacinth_JSON
JSON task lists for use by Columbia University Libraries in reformatting digital collections metadata for ingest into the Hyacinth system.
These JSON files should be opened in Sublime or another basic text editor, and the contents pasted into the Undo/Redo tab in OpenRefine

Here is a breadkdown of the files:
- **PDCD_conversion_2019-10-03.json**: for a typical sheet received from PDCD, this will rename the columns and add some constant data needed by most materials being uploaded to Hyacinth
- **item-asset-split_2020-02-25.json**: Using the Hyacinth Column Headings data dictionary on the Columbia University Libraries wiki as a specification, this json task list will take a flat input dataset and make it fit into the hierarchical digital asset data model deployed in Hyacinth, CUL's digital asset management system.  Full instructions are on the CUL wiki; in short, the first column in the dataset needs to be \_identifiers-1, the row containing the first file in a digital object should be marked "item" in the column \_digital_object_type.string_key and all "items" need to have an identifier; subsequent files in a digital object should be marked as "asset" in the column \_digital_object_type.string_key and need to have a blank value in the column \_identifiers-1.  All column headers should match those in the Hyacinth Column Headings data dictionary.  If the column header isn't specified in the Hyacinth Column Headings data dictionary, the data will not be processed and remain "as-is."
- **pre-recon_2020-02-27.json**: runs reconciliation tasks on culture, form, genre, language, location, name, name-role, subjects, and use/reproduction. **Before running, be sure to have the FAST reconciliation service running!** Use the following syntax conventions: 
  - In general, enter each type of access point into a single column, with individual terms separated by a semicolon
  - Note that each type of subject should be in a separate column: subject-geographic, subject-name, subject-title, subject-topic
  - Enter names and roles into the same column, using this syntax: name1--role1--role2;name2--role1--role2
  - Because of the limitations of using the GREL-JSON scripting format (no looping is possible), the script presumes the following:
  - Roles are capped at 3 roles per item
  - Reconciliation is run against: LC/NAF via VIAF (name, subject-name, subject-geographic, subject-title), FAST (subject-topic, genre), MARC relators (name-role), MARC languages (language), Hyacinth Form (form), Hyacinth location (Location), Hyacinth Rights (use-reproduction)
  - Currently there are some dependencies for MARC languages, Hyacinth Rights, and Hyacinth Form, available in the **Dependencies** directory
- **post-recon.json**: this will split up fields with multiple values, e.g. name-1, name-2, and keep them in sync with their reconciliation data and item-asset structure
- **column-sort_2019-10-03.json**: this will sort the columns; note that any custom columns will be deleted by this task list; edit the JSON if you need to add in custom columns
- **Older versions** of the JSON files will be put into the Older versions directory
- **Test/Beta versions** will be in the Beta directory
- **Test datasets** are in the TestDatasets directory

