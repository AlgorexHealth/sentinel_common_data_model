# SCDM: Procedure Table Structure

Description: The SCDM Procedure Table contains one record per unique combination of `PatID`, `EncounterID`, `PX`, and `PX_CodeType`. This table should capture all uniquely recorded procedures for all encounters.

| Variable Name | Variable Type and Length (Bytes) | Values | Definition / Comments / Guideline | Example |
| --- | --- | --- | --- | --- |
| `PatID`<sup>1</sup> | Char (Site specific length) | Unique member identifier | Arbitrary person-level identifier. Used to link across tables. | `123456789012345` |
| `EncounterID`<sup>2</sup> | Char (Site specific length) | Unique encounter identifier | Arbitrary encounter-level identifier. Used to link across the Encounter, Diagnosis, Procedure, Vital Signs, Inpatient Pharmacy, & Inpatient Transfusion tables. | `123456789012345_12262005_99218766_IP` |
| `ADate` | Numeric (4) | SAS date | Encounter or admission date. | `12/26/2005` |
| `Provider` | Char (Site specific length) | Unique provider identifier | Provider code for the provider who is most responsible for this encounter. For encounters with multiple providers choose one so the encounter can be linked to the diagnosis and procedure tables. As with the `PatID`, the provider code is a pseudoidentifier with a consistent crosswalk to the real identifier. | `99218766` |
| `EncType` | Char (2) | `AV` = Ambulatory Visit | Includes visits at outpatient clinics, same day surgeries, urgent care visits, and other same-day ambulatory hospital encounters, but excludes emergency department encounters. | `IP` |
| | | `ED` = Emergency Department | Includes ED encounters that become inpatient stays (in which case inpatient stays would be a separate encounter). Excludes urgent care visits. ED claims should be pulled before hospitalization claims to ensure that ED with subsequent admission won't be rolled up in the hospital event. | |
| | | `IP` = Inpatient Hospital Stay | Includes all inpatient stays, same-day hospital discharges, hospital transfers, and acute hospital care where the discharge is after the admission date. | |
| | | `IS` = Non-Acute Institutional Stay | Includes hospice, skilled nursing facility (SNF), rehab center, nursing home, residential, overnight non-hospital dialysis and other non-hospital stays. | |
| | | `OA` = Other Ambulatory Visit | Includes other non overnight AV encounters such as hospice visits, home health visits, skilled nursing facility visits, other non-hospital visits, as well as telemedicine, telephone and email consultations. | |
| `PX` | Char (11) | Procedure code | Convert local codes to standard codes. | `76815` |
| `PX_CodeType` | Char (2) | `09` = ICD-9-CM<br>`10` = ICD-10-CM<br>`11` = ICD-11-CM<br>`C2` = CPT Category II<br>`C3` = CPT Category III<br>`C4` = CPT-4 (i.e., HCPCS Level I)<br>`H3` = HCPCS Level III<br>`HC` = HCPCS (i.e., HCPCS Level II)<br>`LC` = LOINC <br>`LO` = Local homegrown<br>`ND` = NDC<br>`OT` = Other <br>`RE` = Revenue | Procedure code type. | `C4` |
| `OrigPX` | Char (Site specific length) | Original procedure code from source table, if different. | Used if Data Partner has to map internal codes to standard codes. |

## NOTES:

1. `PatID` is a pseudoidentifier with a consistent crosswalk to the true identifier retained by the source Data Partner. For analytical data sets requiring patient-level data, only the pseudoidentifier is used to link across all information belonging to a patient.
   
2. For efficiency medical utilization data is captured in 3 tables:
    - **Encounter**: the encounter record that characterizes the outpatient visit or hospital stay
    - **Diagnosis**: the diagnosis code(s) associated with the encounter record
    - **Procedure**: the procedure code(s) associated with the encounter record

    These 3 tables and the Inpatient Pharmacy, Inpatient Transfusion, Vital Signs, and Mother-Infant Linkage tables are linked by `EncounterID`. All diagnoses and procedures for an encounter should have the same `EncounterID`. It is allowable to have "orphan" diagnosis or procedure records with `EncounterID`s that do not have a match in the Encounter table.

[Return to SCDM Version 7.1.0. Table of Contents](atoc_scdm.md) 