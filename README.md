# AutomatedFlatFileCreation
Project to automate, simplify, enhance and speed up Text File creation using SQL server and SSIS

Reason: Text file exports are a common request from many different clients.  Each client has their own particular required format.  SSIS can create many formats, but often there are 
    subtleties in the request which are problematic for SSIS, or in some cases cannot be done at all.  Additionally, subsequent requested changes to the extract require not only 
	changes to the code, but to the SSIS package itself.  In
	
Purpose: This project provides a solution where everything is done in SQL server.  If formatting changes are needed they are done in the procedure that gathers the data.  New fields
    are added automatically, and once the SSIS package is created it never needs to be touched.  SSIS package is a simple Execute and ForEach loop that creates the file(s).
	
Details - SP Pull:
    1) Table(s) (can be temporary) are created with fields in the format of the required extract.
		a) Field Names match what is required by the extract.
		    i) All extract fields will be of type varchar, nvarchar, char or nchar
		    ii) Field sizes will match what is required in the export.
			iii) Flat file extracts should use char or nchar.
		b) Identity and linking fields used for reference and table population
			i) Identity fields used for linking and gathering data, but not needed in the file will be prefixed with "ZZ_" as part of the field name
			ii) Identity fields that need to be in the export, but are not of the appropriate type will be added as "ZZ_" fields, with a computed field used for the extract.
	2) User creates code to populate the extract tables.
	3) Canned code is added that will read the table(s) and create the text lines for extract; which is inserted into an ordered table as a BLOB.
	    a) 
