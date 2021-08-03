
# Overview and Description of the Sentinel Common Data Model (SCDM) v8.0.0 Enhancements

Up-versioning the Sentinel Common Data Model to v8.0.0 included substantial modifications in the service of the following goals: (1) Increasing capture of data, (2) Improving precision in organization of some of the data, and (3) Improving run-time efficiencies for data reading and manipulation.
Additional rationale and detailed table changes from the prior version are provided below.

|Goal of v8.0.0 Enhancements|Rationale|
|--------|--------|
|(1) Increase capture of data.|
|Add Prescribing Table|Satisfy FDA requirement to better understand prescribing patterns which may affect medical product safety and use, particularly in the relationship of prescribing and actual dispensing.|
|In the Dispensing Table, add variable `Rx_CodeType` and replace variable `NDC` with variable `Rx`|Enable the SCDM to be used internationally with code types other than the National Drug Codes (NDC).|
|In the Diagnosis and Procedures Tables, add values for `Dx_CodeType` and for `Px_CodeType`|Enable the SCDM to be used internationally with additional code types.|
|(2)  Improve precision in organization of some of the data.|
|In the Encounter Table, remove variables `Provider` and `Facility_Location`. In Diagnosis and Procedure Tables, modify definition of `Provider` variable. Added tables Facility and Provider. Enabled `Specialty_Codes` as a reference table to be used by Data Partners in this model, for populating the Provider table.|Improve precision in identifying facilities, providers, and specialists for purposes of chart selection.|
|(3) Improve run-time efficiencies for data reading and manipulation.|
|In all tables, set a required sort order.|Enable distributed code to take advantage of uniform sorting of rows in all SCDM tables.|
|Set all identification variables (e.g., `PatID`) to numeric data type.|Using the fewest number of bytes to hold distinct values results in less data being transferred between computer storage and computer memory, enabling increased query performance.|
|Name all identification variables with a suffix of "ID".|Uniformity in variable naming.|
|In the Dispensing, Diagnosis, Procedure and Inpatient Transfusion tables, enable the `Rx`, `Dx`, `Px`, and `Orig_Trans_Prod` variable lengths to be variable by Data Partners' ETLs, as the minimal length necessary to contain values.|Using the fewest number of bytes to hold distinct values results in less data being transferred between computer storage and computer memory, enabling increased query performance.|



|Detailed Table Changes from Version 7.1.0 to v8.0.0|Change|
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
|Laboratory Result| Addition of `LabID`. Valid values for 3 variables (MS_Test_Name, MS_Test_Sub_Category, and Specimen_Source) have been removed from this document, and included as a reference table.|
|Vital Signs|`Diastolic` and `Systolic` both changed to Num(3); `Tobacco` and `Tobacco_Type` both changed to Char(1);
|Inpatient Pharmacy|No changes except as noted above|
|Inpatient Transfusion|Render variable length for `Orig_Trans_Prod` DP/ETL specific.|
|Mother-Infant Linkage|No changes except as noted above.|
|Prescribing|New table.|
|Facility|New table.|
|Provider|New table.|

[Return to Overview](800_01FM_overview.md)

[Return to History of Modifications](800_03FM_history-of-modifications.md)

[Navigate to SCDM Version 8.0.0 Table of Contents](800_00FM_atoc_scdm.md)
