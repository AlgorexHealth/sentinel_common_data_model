

# SCDM v8.0.0: Model Change Goals, Rationales, and Detailed Table Changes

Up-versioning the Sentinel Common Data Model to v8.0.0. included substantial modifications in the service of the following goals: (1) Increasing data capture, (2) Improving organizational precision for some data, and (3) Improving run-time efficiencies for data reading and manipulation.
Additional details and rationale are below.

|Goal of Change|Rationale|
|--------|--------|
|(1) Increase data capture.|
|Add Prescribing Table|Satisfy FDA requirement to better understand prescribing patterns which may affect medical product safety and use, particularly in the relationship of prescribing and actual dispensing.|
|In the Dispensing Table, add variable `Rx_CodeType` and replace variable `NDC` with variable `Rx`|Enable the SCDM to be used internationally with code types other than the National Drug Codes (NDC).|
|In the Diagnosis and Procedures Tables, add values for `Dx_CodeType` and for `Px_CodeType`|Enable the SCDM to be used internationally with additional code types.|
|(2) Improve organizational precision for some data.|
|In the Encounter Table, remove variables `Provider` and `Facility_Location`. In Diagnosis and Procedure Tables, modify definition of `Provider` variable. Added tables Facility and Provider. Enabled `Specialty_Codes` as a reference table to be used by Data Partners in this model, for populating the Provider table.|Improve precision in identifying facilities, providers, and specialists for purposes of chart selection.|
|(3) Improve run-time efficiencies for data reading and manipulation.|
|In all tables, set a required sort order.|Enable distributed code to take advantage of uniform sorting of rows in all SCDM tables.|
|Set all identification variables (e.g., `PatID`) to numeric data type.|Using the fewest number of bytes to hold distinct values results in less data being transferred between computer storage and computer memory, enabling increased query performance.|
|Name all identification variables with a suffix of "ID".|Uniformity in variable naming.|
|In the Dispensing, Diagnosis, Procedure and Inpatient Transfusion tables, enable the `Rx`, `Dx`, `Px`, and `Orig_Trans_Prod` variable lengths to be variable by Data Partners' ETLs, as the minimal length necessary to contain values.|Using the fewest number of bytes to hold distinct values results in less data being transferred between computer storage and computer memory, enabling increased query performance.|


|Detailed Table Changes from Version 7.1.0|Change|
|--------|--------|
|All tables|`PatID`, `EncounterID`, `ProviderID`, and `FacilityID`, are set to numeric data type with as short a variable length as needed to capture all values; all identification variables end with "ID".|
|Enrollment|Added value for `MedCov`|
|Demographic|Changed `ZipCode` and `ZipCode_Date` to `PostalCode` and `PostalCode_Date` to accommodate international collaborators|
|Dispensing|Add `ProviderID` variable; Replace National Drug Codes (`NDC` variable) with `Rx_CodeType` and `Rx` variables|
|Encounter|Remove `Provider` and `Facility_Location`; Clarify definition of Encounter table row; Add value to `Ddate`, `Discharge_Status`, and `Discharge_Disposition`|
|Diagnosis|Modify definition of `Provider`; Add values for `Dx_CodeType`; Render variable length for `Dx` DP/ETL specific.|
|Procedure|Modify definition of `Provider`; Add values for `Px_CodeType`; Render variable length for `Px` DP/ETL specific.|
|Death|Enhanced labels for `Source`; Values did not change|
|Cause of Death|Enhanced labels for `Source`; Values did not change|
|Laboratory Result| Addition of `LabID`|
|Vital Signs|`Diastolic` and `Systolic` both changed to Num(3); `Tobacco` and `Tobacco_Type` both changed to Char(1);
|Inpatient Pharmacy|No changes except as noted above|
|Inpatient Transfusion|Render variable length for `Orig_Trans_Prod` DP/ETL specific.|
|Mother-Infant Linkage|No changes except as noted above.|
|Prescribing|New table.|
|Facility|New table.|
|Provider|New table.|
|PRM Survey|New table.|
|PRM Response|New table.|


[Return to Overview](810_overview.md) 

[Navigate to SCDM Version 8.1.0. Table of Contents](atoc_scdm810.md)