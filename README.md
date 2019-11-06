# CUL_OpenRefine2Hyacinth_JSON
JSON task lists for use by Columbia University Libraries in reformatting digital collections metadata for ingest into the Hyacinth system.
These JSON files should be opened in Sublime or another basic text editor, and the contents pasted into the Undo/Redo tab in OpenRefine

Here is a breadkdown of the files:
- **PDCD_conversion_2019-10-03.json**: for a typical sheet received from PDCD, this will rename the columns and add some constant data needed by most materials being uploaded to Hyacinth
- **item-asset-split_2019-10-03.json**: Add a column named NewItemFlag to your datasheet, and mark the first asset for a given item with an "x"; this script will create the item-asset structure required by the Hyacinth data model.  Item-only fields will be moved into an item row, asset-only fields retained in the asset row, and data for fields that can appear in both item and asset rows will be duplicated.  As such, you may want to adjust the script based on the data you are working with--in many cases metadata does not need to be at both item and asset levels, even if this is allowed by the data model
- **pre-recon.json**: use after enhancing the sheet with any name, subject, form, and/or genre access points, as well as name relator terms, language, use/reproduction, and location data.
  - Use the following syntaxt conventions: 
    - Keep names and roles in synch, e.g. name1;name2  should match roles as such: name1_role1–role2;name2_role1–role2 – the scripts assume that the values in these columns line up correctly
    - If a name has multiple associated roles, separate each role with two dashes e.g. name1_role1–role2;
    - (NOTE: Ryan has drafted a new version of the script in which the names and roles can be entered into the same column, using this syntax: name1|name1_role1--name1_role2;name2|name2_role1–name2_role2) (this script is being tested in October 2019, and documentation will be updated once this has been finalized)
    - Separate all distinct access points with a semicolon ;  DO NOT put any spaces before or after the semicolon (Ryan will adjust the scripts to remove leading/trailing whitespace so that this will not be an issue)
    - Because of the limitations of using the GREL-JSON scripting format (no looping is possible), the script presumes the following:
      - Access points addressed by the scripts (all EXCEPT roles: names, subjects, languages, and forms) are capped at 10 values per item
      - Roles are capped at 3 roles per item
  - Reconciliation is run against: LC/NAF via VIAF (name, subject-name, subject-geographic, subject-title), FAST (subject-topic, genre), MARC relators (name-role), MARC languages (language), Hyacinth Form (form), Hyacinth location (Location), Hyacinth Rights (use-reproduction)
  - Currently there are some dependencies for MARC languages, Hyacinth Rights, and Hyacinth Form, available in the **Dependencies** directory
- **post-recon.json**: this will split up fields with multiple values, e.g. name-1, name-2, and keep them in sync with their reconciliation data and item-asset structure
- **column-sort_2019-10-03.json**: this will sort the columns; note that any custom columns will be deleted by this task list; edit the JSON if you need to add in custom columns
- **Older versions** of the JSON files will be put into the Older versions directory
- **Test/Beta versions** will be in the Beta directory

