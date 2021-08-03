# SCDM: Encounter Table Structure

**Description:** The SCDM Encounter Table contains one record per `PatID` and `EncounterID`. Each encounter should have a single record in the SCDM Encounter Table. Each diagnosis and procedure recorded during the encounter should have a separate record in the Diagnosis or Procedure Tables. Rollback transactions and other adjustments should be processed before populating this table.<sup>1</sup> <br>• Conversion from Ambulatory or Emergency Visit (`ED`, `AV`, or `OA`) into Inpatient Hospital or Institutional Stay (`IP`, `IS`) through admission represents multiple encounters. The Ambulatory or Emergency Visit is one encounter, the Inpatient Hospital or Institutional Stay after admission is a second encounter.<br>• Transfer from one facility to another facility starts a new encounter at the new facility.<br>• If supported by Data Partner source data, multiple visits on the same day to the same facility, with no conversion from Ambulatory or Emergency Visit (`ED`, `AV`, or `OA`) into Inpatient Hospital or Institutional Stay (`IP`, `IS`) admission, should be created as distinct encounters and should include all diagnoses and procedures that were recorded during those separate visits, with distinct `ProviderID` values populated.  If source data cannot identify distinct multiple visits on the same day, then populate as a single encounter.

**Sort Order:** The Encounter Table should be sorted by `PatID` and `ADate`.

**Unique Row:** `PatID`, `EncounterID`.

| Variable Name | Variable Type and Length (Bytes) | Values | Status | Definition / Comments / Guideline | Example |
| --- | --- | --- | --- | --- |--- |
| `PatID`<sup>2</sup> | Num(#) | Unique patient identifier | Required | Arbitrary person-level identifier. Used to link across tables. Use the fewest number of bytes necessary to hold all distinct values; see ["SAS Lengths" Reference Table](SAS_lengths_reference_table.md). | `123456789` |
| `EncounterID`<sup>3</sup> | Num(#) | Unique encounter identifier | Required | Arbitrary encounter-level identifier. Used to link across the Encounter, Diagnosis, Procedure, Vital Signs, Mother-Infant Linkage, Inpatient Pharmacy, Inpatient Transfusion, and Prescribing tables. Use the fewest number of bytes necessary to hold all distinct values; see ["SAS Lengths" Reference Table](SAS_lengths_reference_table.md). | `98765432159753` |
| `ADate` | Num(4) | SAS date |  Required |Encounter or admission date. | `12/24/2019` |
| `DDate` | Num(4) | Valid Values: <ul><li>SAS Date</li><li>`.S`: Special Missing</li><li>`.`: Missing</li></ul> | Conditional on `EncType` value | Discharge date. Should be populated for all Inpatient Hospital Stay (`IP`) and Non-Acute Institutional Stay (`IS`) encounter types. May be populated for Emergency Department (`ED`) encounter types. Should be missing for ambulatory visit (`AV` or `OA`) encounter types. For patients still in facility (`IP` or `IS`) use special missing value of `.S`. | `12/31/2019` |
| `EncType` | Char(2) | `AV` = Ambulatory Visit (Includes visits at outpatient clinics, same day surgeries, urgent care visits, and other same-day ambulatory hospital encounters, but excludes Emergency Department encounters. Transfer from AV facility to an ED facility starts a new encounter at the new facility.)<br> `ED` = Emergency Department (Includes ED encounters that become inpatient stays through hospital admission. In this scenario, ED is one encounter, Inpatient Hospital Stay after admission from the ED is a second encounter. ED data should be identified before hospitalization data to ensure that ED with subsequent admission won't be rolled up in the hospital event. Transfer from one ED facility to another ED facility starts a new encounter at the new facility. Excludes urgent care visits.)<br> `IP` = Inpatient Hospital Stay (Includes all inpatient stays, same-day hospital discharges, hospital transfers, and other acute hospital care where the discharge is after the admission date. Transfer from one facility to another starts a new encounter at the new facility.)<br>`IS` = Non-Acute Institutional Stay (Includes hospice, skilled nursing facility (SNF), rehab center, nursing home, residential, overnight non-hospital dialysis and other non-hospital stays. Transfer from one facility to another starts a new encounter at the new facility.)<br>`OA` = Other Ambulatory Visit (Includes other non-overnight `AV` encounters such as hospice visits, home health visits, skilled nursing facility visits, other non-hospital visits, as well as telemedicine, telephone and email consultations.) | Required | Encounter Type |`IP` |
| `FacilityID` | Num(#)<sup>4</sup> | Servicing provider identifier | Required | Local facility pseudoidentifier that identifies hospital or clinic in which the encounter occurred. There must be only one facility per encounter. Used for chart abstraction and validation. This variable links to the Facility table. If unavailable, set to special missing value `.U`.Use the fewest number of bytes necessary to hold all distinct values; see ["SAS Lengths" Reference Table](SAS_lengths_reference_table.md). | `45678` |
| `Discharge_ Disposition` | Char(1) | `A` = Discharged alive<br>`E` = Expired<br>`S` = Still in facility<br>`U` = Unknown | Conditional on `EncType` value | Should be populated for Inpatient Hospital Stay (`IP`) and Non-Acute Institutional Stay (`IS`) encounter types. May be populated for Emergency Department (`ED`) encounter types. Should be missing for ambulatory visit (`AV` or `OA`) encounter types. | `A` |
| `Discharge_Status` <sup>5</sup> | Char(2) | `AF` = Adult Foster Home<br>`AL` = Assisted Living Facility<br>`AM` = Against Medical Advice<br>`AW` = Absent without leave<br>`EX` = Expired<br>`HH` = Home Health<br>`HO` = Home / Self Care<br>`HS` = Hospice<br>`IP` = Other Acute Inpatient Hospital<br>`NH` = Nursing Home (Includes Intermediate Care Facility (ICF))<br>`OT` = Other<br>`RH` = Rehabilitation Facility<br>`RS` = Residential Facility<br>`SH` = Still In Facility<br>`SN` = Skilled Nursing Facility<br>`UN` = Unknown | Conditional on `EncType` value | Should be populated for Inpatient Hospital Stay (`IP`) and Non-Acute Institutional Stay (`IS`) encounter types. May be populated for Emergency Department (`ED`) encounter types. Should be missing for ambulatory visit (`AV` or `OA`) encounter types. | `SN` |
| `DRG` | Char(3) | 3&#45;digit Diagnosis Related Group | Conditional on `EncType` value | Diagnosis Related Group. Should be populated for `IP` and `IS` encounter types. May be populated for `ED` encounter types. Can be missing for `IP`, `IS`, `ED`. Should be missing for `AV` or `OA` encounters. Use leading zeroes for codes less than 100. | `372` |
| `DRG_Type` | Char(1) | `1` = CMS&#45;DRG (old system)<br>`2` = MS&#45;DRG (current system) | Conditional on `EncType` value | DRG code version. MS-DRG (current system) began on 10/1/2007. Should be missing for `AV` or `OA` encounters.  Can be missing for `IP`, `IS`, `ED`. | `1` |
| `Admitting_Source` | Char(2) | `AF` = Adult Foster Home<br>`AL` = Assisted Living Facility<br>`AV` = Ambulatory Visit<br>`ED` = Emergency Department<br>`HH` = Home Health<br>`HO` = Home / Self Care<br>`HS` = Hospice<br>`IP` = Other Acute Inpatient Hospital<br>`NH` = Nursing Home (Includes ICF)<br>`OT` = Other<br>`RH` = Rehabilitation Facility<br>`RS` = Residential Facility<br>`SN` = Skilled Nursing Facility<br>`UN` = Unknown<br> | Conditional on `EncType` value | Should be populated for Inpatient Hospital Stay (`IP`) and Non-Acute Institutional Stay (`IS`) encounter types. May be populated for Emergency Department (`ED`) encounter types. Should be missing for ambulatory visit (`AV` or `OA`) encounter types. | `HH` |

## NOTES:

1. Rollback transactions and other adjustments should be processed before populating this table. This may be handled differently by Data Partners and may be affected by billing cycles.
Encounters for a patient to the same facility but with different individual providers should be set as distinct encounters.<br><br>The definition of a unique row in the Encounter table (i.e., `PatID`/ `EncounterID`) may be satisfied while multiple rows may have the same `PatID`/ `ADate` / `FacilityID` / `EncType`. Uniqueness of encounters can be verified by linking to the `ProviderID` values in the Diagnosis and Procedure tables.<br><br>For claims-based source systems:<br>

- Multiple claims that reflect a single encounter should be rolled into a single encounter, such as an inpatient hospitalization that generates multiple claims from the facility.
- Transfers from one hospitalization to another should have each facility's hospitalization set as a single encounter.
- Claims with visits on multiple dates should have each date established as a separate encounter, such as multiple outpatient visits to the same individual provider all billed on a single claim.

2. `PatID` is a pseudoidentifier with a consistent crosswalk to the true identifier retained by the source Data Partner. For analytical data sets requiring patient-level data, only the pseudoidentifier is used to link across all information belonging to a patient.

3. For efficiency, medical utilization data is captured in 3 tables:
    - **Encounter**: the encounter record that characterizes the outpatient visit or hospital stay
    - **Diagnosis**: the diagnosis or other clinical code(s) associated with the encounter record
    - **Procedure**: the procedure code(s) associated with the encounter record.

    All diagnoses and procedures for an encounter should have the same `EncounterID`. It is allowable to have "orphan" diagnosis or procedure records with `EncounterID`s that do not have a match in the Encounter table.<br><br>The Encounter, Diagnosis, Procedure, Inpatient Transfusion, Inpatient Pharmacy, Vital Signs, Mother-Infant Linkage, Inpatient Pharmacy, Inpatient Transfusion, and Prescribing tables are linked by `PatID` and `EncounterID`.

4. If all `FacilityID` values are unknown (i.e., set to `.U`), use Num(3) for the length of the variable.

5. Guidance regarding `Discharge_Status` is attached in the [Discharge Status Code Guidance document](DischargeStatusCodeGuidance_Public_0204213p.xlsx)

[Return to SCDM Version 8.0.0 Table of Contents](800_00FM_atoc_scdm.md)