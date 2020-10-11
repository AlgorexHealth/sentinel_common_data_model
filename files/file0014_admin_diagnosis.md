# SCDM: Diagnosis Table Structure

Description: The SCDM Diagnosis Table contains one record per unique combination of `PatID`, `EncounterID`, `DX`, and `DX_CodeType`. This table should capture all uniquely recorded diagnoses for all encounters.

| Variable Name | Variable Type and Length (Bytes) | Values | Definition / Comments / Guideline | Example |
| --- | --- | --- | --- | --- |
| `PatID`<sup>1</sup> | Char (Site specific length) | Unique member identifier | Arbitrary person-level identifier. Used to link across tables. | `123456789012345` |
| `EncounterID`<sup>2</sup> | Char (Site specific length) | Unique encounter identifier | Arbitrary encounter-level identifier. Used to link across the Encounter, Diagnosis, Procedure, Vital Signs, Inpatient Pharmacy, & Inpatient Transfusion tables. | `123456789012345_12242005_99218766_IP` |
| `ADate` | Numeric (4) | SAS date | Encounter or admission date. | `12/24/2005` |
| `Provider` | Char (Site specific length) | Unique provider identifier | Provider code for the provider who is most responsible for this encounter. For encounters with multiple providers choose one so the encounter can be linked to the diagnosis and procedure tables. As with the `PatID`, the provider code is a pseudoidentifier with a consistent crosswalk to the real identifier. | `99218766` |
| `EncType` | Char (2) | `AV` = Ambulatory Visit | Includes visits at outpatient clinics, same day surgeries, urgent care visits, and other same-day ambulatory hospital encounters, but excludes emergency department encounters. | `IP` |
| | | `ED` = Emergency Department | Includes ED encounters that become inpatient stays (in which case inpatient stays would be a separate encounter). Excludes urgent care visits. ED claims should be pulled before hospitalization claims to ensure that ED with subsequent admission won't be rolled up in the hospital event. | |
| | | `IP` = Inpatient Hospital Stay | Includes all inpatient stays, same-day hospital discharges, hospital transfers, and acute hospital care where the discharge is after the admission date. | |
| | | `IS` = Non-Acute Institutional Stay | Includes hospice, skilled nursing facility (SNF), rehab center, nursing home, residential, overnight non-hospital dialysis and other non-hospital stays. | |
| | | `OA` = Other Ambulatory Visit | Includes other non overnight AV encounters such as hospice visits, home health visits, skilled nursing facility visits, other non-hospital visits, as well as telemedicine, telephone and email consultations. | |
| `DX`<sup>3</sup> | Char (18) | Diagnosis code | For ICD codes this variable can include decimal points or not. Remove site specific suffixes and prefixes. Other codes should be listed as recorded in the source data. | `761.5` |
| `Dx_Codetype`<sup>4</sup> | Char (2) | `09` = ICD-9-CM<br>`10` = ICD-10-CM<br>`11` = ICD-11-CM<br>`SM` = SNOMED CT<br>`OT` = Other | Diagnosis code type. This field combined with the `DX` field should be used to capture any type of diagnosis or clinical concept available in the source data. We provide values for ICD and SNOMED code types. Other code types will be added as new terminologies are used. | `09` |
| `OrigDX` | Char (Site specific length) | Original diagnosis from source table, if different | Used if Data Partner has to map internal codes to standard codes. | |
| `PDX` | Char (1) | `P` = Principal<br>`S` = Secondary<br/>`X` = Unable to Classify | Principal discharge diagnosis flag. Relevant only on `IP` and `IS` encounters. For `ED`, `AV`, and `OA` encounter types, mark as missing. One principal diagnosis is expected, although in some instances more than one diagnosis may be flagged as principal | `P` |
| `PAdmit`<sup>5</sup> | Char (1) | `N` = No<br>`Y` = Yes<br>`U` = Unknown or unable to determine<br>`X` = Unreported/not used | Indicates whether the diagnosis code is indicative of a condition present at admission. | `Y` |


## NOTES:

1. `PatID` is a pseudoidentifier with a consistent crosswalk to the true identifier retained by the source Data Partner. For analytical data sets requiring patient-level data, only the pseudoidentifier is used to link across all information belonging to a patient.

2. For efficiency medical utilization data is captured in 3 tables:
    - **Encounter**: the encounter record that characterizes the outpatient visit or hospital stay
    - **Diagnosis**: the diagnosis code(s) associated with the encounter record
    - **Procedure**: the procedure code(s) associated with the encounter record

    These 3 tables and the Inpatient Pharmacy, Inpatient Transfusion, Vital Signs, and Mother-Infant Linkage tables are linked by `EncounterID`. All diagnoses and procedures for an encounter should have the same `EncounterID`. It is allowable to have "orphan" diagnosis or procedure records with `EncounterIDs` that do not have a match in the Encounter table.

3. For ICD codes, some Data Partners will have a decimal point in the `DX` variable and others will not. We recommend that users of the data strip the decimal point during data analyses.

4. For those who collect SNOMED CT codes as part of routine care, those codes can be stored in this table, using the `SM` `DX_CodeType`

5. Sentinel Data Partners receive individual guidance for populating the `PAdmit` field.

[Return to SCDM Version 7.1.0. Table of Contents](atoc_scdm.md) 