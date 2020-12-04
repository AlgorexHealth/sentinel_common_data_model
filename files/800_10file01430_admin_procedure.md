# SCDM: Procedure Table Structure

**Description:** The SCDM Procedure Table contains one record per unique combination of `PatID`, `EncounterID`, `Px_CodeType`, `Px`, and `ProviderID`. This table should capture all uniquely recorded procedures for all encounters, per provider.

**Sort Order:** The Procedure Table should be sorted by `PatID` and `ADate`.

**Unique Row:** `PatID`, `EncounterID`, `Px_CodeType`, `Px`, `ProviderID`.

| Variable Name | Variable Type and Length (Bytes) | Values | Status | Definition / Comments / Guideline | Example |
| --- | --- | --- | --- | --- |--- |
| `PatID`<sup>1</sup> | Num(#) | Unique patient identifier | Required | Arbitrary person-level identifier. Used to link across tables. Use the fewest number of bytes necessary to hold all distinct values; see "SAS Lengths" Reference Table. | `123456789` |
| `EncounterID`<sup>2</sup> | Num(#) | Unique encounter identifier | Required | Arbitrary encounter-level identifier. Used to link across the Encounter, Diagnosis, Procedure, Vital Signs, Mother-Infant Linkage, Inpatient Pharmacy, Inpatient Transfusion, and Prescribing tables. Use the fewest number of bytes necessary to hold all distinct values; see ["SAS Lengths" Reference Table](SCDM_draft_reference_tables_8.1.0_r2.xlsx). | `98765432159753` |
| `ADate` | Num(4) | SAS date | Required | Encounter or admission date; Value must match `ADate` in the Encounter table for the same `PatID`/ `EncounterID` combination. | `12/24/2019` |
| `ProviderID` | Num(#)<sup>4</sup> | Unique provider identifier | Required | Identifier for the individual provider who made the diagnosis. As with the `PatID`, the `ProviderID` identifier is a pseudoidentifier with a consistent crosswalk to the real identifier. If an individual provider cannot be identified, populate the `ProviderID` value with special missing value of `.U`. This variable links to the Provider table. Use the fewest number of bytes necessary to hold all distinct values; see ["SAS Lengths" Reference Table](SCDM_draft_reference_tables_8.1.0_r2.xlsx). | `99218766` |
| `EncType` | Char(2) | `AV` = Ambulatory Visit (Includes visits at outpatient clinics, same day surgeries, urgent care visits, and other same-day ambulatory hospital encounters, but excludes Emergency Department encounters. Transfer from AV facility to an ED facility starts a new encounter at the new facility.)<br> `ED` = Emergency Department (Includes ED encounters that become inpatient stays through hospital admission. In this scenario, ED is one encounter, Inpatient Hospital Stay after admission from the ED is a second encounter. ED data should be identified before hospitalization data to ensure that ED with subsequent admission won't be rolled up in the hospital event. Transfer from one ED facility to another ED facility starts a new encounter at the new facility. Excludes urgent care visits.)<br> `IP` = Inpatient Hospital Stay (Includes all inpatient stays, same-day hospital discharges, hospital transfers, and other acute hospital care where the discharge is after the admission date. Transfer from one facility to another starts a new encounter at the new facility.)<br>`IS` = Non-Acute Institutional Stay (Includes hospice, skilled nursing facility (SNF), rehab center, nursing home, residential, overnight non-hospital dialysis and other non-hospital stays. Transfer from one facility to another starts a new encounter at the new facility.)<br>`OA` = Other Ambulatory Visit (Includes other non-overnight `AV` encounters such as hospice visits, home health visits, skilled nursing facility visits, other non-hospital visits, as well as telemedicine, telephone and email consultations.) | Required | Encounter Type |`IP` |
| `PX` | Char(#) | Procedure code | Required | Remove decimal points, site specific suffixes and prefixes. Other codes should be listed as recorded in the source data. Convert local codes to standard codes. Use the fewest number of bytes to contain values for all values of `Px_CodeType`. | `76815` |
| `PX_CodeType` | Char(2) | `09` = ICD&#45;9&#45;CM<br>`10` = ICD&#45;10&#45;CM<br>`11` = ICD&#45;11&#45;CM<br>`C2` = CPT Category II<br>`C3` = CPT Category III<br>`C4` = CPT&#45;4 (i.e., HCPCS Level I)<br>`CP` = Canadian Classification of Diagnostic, Therapeutic, and Surgical Procedures (CCP)<br>`CX` = Canadian Classification of Health Interventions (CCI)<br>`H3` = HCPCS Level III<br>`HC` = HCPCS (i.e., HCPCS Level II)<br>`LC` = LOINC <br>`LO` = Local homegrown<br>`ND` = NDC<br>`OT` = Other <br>`RE` = Revenue<br>`SK` = SNOMED CT (UK/CPRD)| Required | Procedure code type. | `C4` |
| `OrigPX` | Char(#) | Original procedure code from source table, if different. | Optional | Used if Data Partner has to map internal codes to standard codes. | |

## NOTES

1. `PatID` is a pseudoidentifier with a consistent crosswalk to the true identifier retained by the source Data Partner. For analytical data sets requiring patient-level data, only the pseudoidentifier is used to link across all information belonging to a patient.

2. For efficiency medical utilization data is captured in 3 tables:
    - **Encounter**: the encounter record that characterizes the outpatient visit or hospital stay
    - **Diagnosis**: the diagnosis code(s) associated with the encounter record
    - **Procedure**: the procedure code(s) associated with the encounter record

    All diagnoses and procedures for an encounter should have the same EncounterID. It is allowable to have "orphan" diagnosis or procedure records with EncounterIDs that do not have a match in the Encounter table.

    The Encounter, Diagnosis, Procedure, Inpatient Transfusion, Inpatient Pharmacy, Vital Signs, Mother-Infant Linkage, Inpatient Pharmacy, Inpatient Transfusion, and Prescribing tables are linked by `PatID` and `EncounterID`.

3. If all `ProviderID` values are unknown (i.e., set to `.U`), use Num(3) for the length of the variable.

[Return to SCDM Version 8.0.0. Table of Contents](800_0FM_atoc_scdm.md)
