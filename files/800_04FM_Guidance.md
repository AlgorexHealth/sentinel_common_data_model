
# General Guidance

 Information provided here is general guidance that affects multiple tables and/or variables in the model. 

|#|Issue|Guidance|
|-----|--------|--------|
|(1)|Data inclusion rules|The Sentinel Operations Center endeavors to have Data Partners include all of their source data in each ETL database.  Please discuss with SOC any potential deviations from including all of your source data.|
|(2)|Table names|While there are distinct table names in this model, Data Partners can name their actual SAS datasets whatever name is useful to them.  Table names also can vary across ETLs. It is through use of Common Components that actual table names are identified for Sentinel queries.|
|(3)|Within ETL model & rules|All of the information in this model documentation, is applicable to any distinct ETL/refresh. Any considerations about data relationships across ETLs is outside of the scope of this document. If there are requirements for relationships of data across ETLs (e.g., consistency of `PatID`s), that will be communicated separately by the Sentinel Operations Center.|
|(4)|Sort order|New as of the 8.0.0. model is a requirement for the sort order of each table. This is promulgated to obtain execution efficiences for queries.|
|(5)|Unique row definition|New as of the 8.0.0. model is an explicit definition of a unique row, for most tables.  If defined, no duplicate rows are permitted.|
|(6)|Required, Conditional, Optional|New as of the 8.0.0. model is a Status column, per table description, that indicates the rules for populating each variable.|
|(7)|Dates are SAS dates|All date variables are SAS dates, consisting of integers, using a numeric length=4.  Formatting of date variables is optional per Data Partner preference.|
|(8)|Times are SAS times|All time variables are SAS times, consisting of integers between 0 and 86400, using a numeric length=4. Formatting of time variables is optional per Data Partner preference.|
|(9)|"#" lengths|The use of "#" when defining variable lengths is to indicate that this can vary across Data Partners and/or across ETLs.|
|(10)|Numeric type for ID variables|All ID variables (whose names end with "ID") must be numeric integers and must utilize the fewest number of bytes to precisely represent all values. The Sentinel Operations Center has made this change towards the goal of improving execution efficiency. A recommended process for populating ID variables is provided in the Notes below this table<sup>1</sup>.|
|(11)|Linking to source data|Data Partners are required to maintain mechanisms for linking back to their source data for purposes of: QA checking, potential chart review, and detailed investigations. SOC expects that the most suitable mechanism are cross-walk tables, although the ultimate mechanism is up to the Data Partner. Note that only the tables named in this model documentation will be eligible for querying.|
|(12)|Same lengths of same variable names|All variables that exist in more than one table must have an identical length for that variable.  This includes all ID variables (i.e., `PatID`, `EncounterID`, `FacilityID`, `ProviderID`), `Px` (Procedure and Laboratory Result tables, if the latter is populated), and `Rx` (Dispensing and Prescribing tables, if the latter is populated).|
|(13)|`FacilityID` is unknown|The `FacilityID` variable appears in the Encounter and Laboratory Results tables.  If an individual facility cannot be determined, use the special missing value of `.U` to populate this variable.|
|(14)|`ProviderID` is unknown|The `ProviderID` variable appears in the Dispensing, Diagnosis, Procedure, and Prescribing tables.  If an individual provider cannot be determined, use the special missing value of `.U` to populate this variable.|
|(15)|Character values|Values for character variables should have no leading spaces; i.e., left-justified.|
|(16)|Table Guidance|Each table contains definitions for individual tables and associated guidance for defining the contents of variables and rows.|
|(17)|Dispensing and Prescribing table values|The Dispensing and Prescribing tables contain values appropriate to International colleagues. Data Partners, please use the values appropriate for your SCDM:<br>`ND` = National Drug Code (US)<br>`SN` = SNOMED CT (US)<br>`SK` = SNOMED CT (UK)<br>`DM` = Dictionary of Medicines and Devices (UK)<br>`DI` = Drug Identification Number (CA)<br>`RN` = RxNorm (US)<br>`AT`= Anatomical Therapeutic Chemical Classification (DK)<br>`GP`= Generic Product Identifier (US); for Prescribing table only|
|(18)|All `FacilityID` and/or all `ProviderID` values are unknown|See first footnote in Facility and Provider tables and footnotes for the `FacilityID` and `ProviderID` variables, for "Num(#)", in these tables: Dispensing, Encounter, Diagnosis, Procedure, Laboratory Results, and Prescribing.|

## NOTES

1. The following is a recommended process for populating ID variables:

- Determine the count for the number of distinct values required (e.g., For `PatID`, count up the number of unique patients within the ETL).
- In any ID variable, there is no need for sequencing of all values. That is, gaps are allowed between numeric values.
- Using the Reference Tables "SAS&#45;Lengths" tab, set the numeric length for the ID variable to the minimum length required to represent the count of distinct values, or the highest value, whichever is greater.
There will be at least 2 QA checks for all ID variables:
  1) The highest value found correctly fits within the numeric length established for the variable (e.g., if the highest value found is 98765, then a length of 4 has been set for the variable).
  2) The numeric length is the minimum necessary to contain all values (e.g., if the highest value found is 1589753, then a length of no more than 4 has been set for the variable).|

[Return to Overview](800_1FM_overview.md)

[Navigate to SCDM Version 8.0.0. Table of Contents](800_0FM_atoc_scdm.md)
