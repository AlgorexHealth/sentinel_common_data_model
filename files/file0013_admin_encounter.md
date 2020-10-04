# SCDM: Encounter Table Structure

Description: The SCDM Encounter Table contains one record per `PatID` and `EncounterID`. Each encounter should have a single record in the SCDM Encounter Table. Each diagnosis and procedure recorded during the encounter should have a separate record in the Diagnosis or Procedure Tables. Multiple visits to the same provider on the same day should be considered one encounter and should include all diagnoses and procedures that were recorded during those visits. Visits to different providers on the same day, such as a physician appointment that leads to a hospitalization, should be considered multiple encounters. Rollback transactions and other adjustments should be processed before populating this table.<sup>1</sup>

| Variable Name | Variable Type and Length (Bytes) | Values | Definition / Comments / Guideline | Example |
| --- | --- | --- | --- | --- |
| `PatID`<sup>2</sup> | Char (Site specific length) | Unique member identifier | Arbitrary person-level identifier. Used to link across tables. | `123456789012345` |
| `EncounterID`<sup>3</sup> | Char (Site specific length) | Unique encounter identifier | Arbitrary encounter-level identifier. Used to link across the Encounter, Diagnosis, Procedure, Vital Signs, Inpatient Pharmacy, & Inpatient Transfusion tables. | `123456789012345_12242005_99218766_IP` |
| `ADate` | Numeric (4) | SAS date | Encounter or admission date. | `12/24/2005` |
| `DDate` | Numeric (4) | SAS date | Discharge date. Should be populated for all Inpatient Hospital Stay (`IP`) and Non-Acute Institutional Stay (`IS`) encounter types. May be populated for Emergency Department (`ED`) encounter types. Should be missing for ambulatory visit (`AV` or `OA`) encounter types. | `12/31/2005` |
| `Provider`<sup>4</sup> | Char (Site specific length) | Unique provider identifier | Provider code for the provider who is most responsible for this encounter. For encounters with multiple providers choose **one** so the encounter can be linked to the diagnosis and procedure tables. As with the PatID, the provider code is a pseudoidentifier with a consistent crosswalk to the real identifier. | `99218766` |
| `Facility_Location` | Char (3) | Geographic location (3 digit zip code) | Should be left blank if missing. | `902` |
| `EncType` | Char (2) | `AV` = Ambulatory Visit | Includes visits at outpatient clinics, same day surgeries, urgent care visits, and other same-day ambulatory hospital encounters, but excludes emergency department encounters. | `IP` |
| | | `ED` = Emergency Department | Includes Emergency Department encounters that become inpatient stays (in which case inpatient stays would be a separate encounter). Excludes urgent care visits. Emergency Department claims should be pulled before hospitalization claims to ensure that `ED` with subsequent admission won't be rolled up in the hospital event. | |
| | | `IP` = Inpatient Hospital Stay | Includes all inpatient stays, same-day hospital discharges, hospital transfers, and acute hospital care where the discharge is after the admission date. | |
| | | `IS` = Non-Acute Institutional Stay | Includes hospice, skilled nursing facility (SNF), rehab center, nursing home, residential, overnight non-hospital dialysis and other non-hospital stays. | |
| | | `OA` = Other Ambulatory Visit | Includes other non overnight AV encounters such as hospice visits, home health visits, skilled nursing facility visits, other non-hospital visits, as well as telemedicine, telephone and email consultations. |
| `Facility_Code` | Char (Site specific length) | Servicing provider identifier | Local facility code that identifies hospital or clinic. Taken from facility claims. Used for chart abstraction and validation. | `FC12345678` |
| `Discharge_ Disposition` | Char (1) | `A` = Discharged alive<br>`E` = Expired<br>`U` = Unknown | Should be populated for Inpatient Hospital Stay (`IP`) and Non-Acute Institutional Stay (`IS`) encounter types. May be populated for Emergency Department (`ED`) encounter types. Should be missing for ambulatory visit (`AV` or `OA`) encounter types. | `A` |
| `Discharge_Status` | Char (2) | `AF` = Adult Foster Home<br>`AL` = Assisted Living Facility<br>`AM` = Against Medical Advice<br>`AW` = Absent without leave<br>`EX` = Expired<br>`HH` = Home Health<br>`HO` = Home / Self Care<br>`HS` = Hospice<br>`IP` = Other Acute Inpatient Hospital<br>`NH` = Nursing Home (Includes ICF)<br>`OT` = Other<br>`RH` = Rehabilitation Facility<br>`RS` = Residential Facility<br>`SH` = Still In Hospital<br>`SN` = Skilled Nursing Facility<br>`UN` = Unknown | Should be populated for Inpatient Hospital Stay (`IP`) and Non-Acute Institutional Stay (`IS`) encounter types. May be populated for Emergency Department (`ED`) encounter types. Should be missing for ambulatory visit (`AV` or `OA`) encounter types. | `SN` |
| `DRG` | Char (3) | 3-digit Diagnosis Related Group | Diagnosis Related Group. Should be populated for `IP` and `IS` encounter types. May be populated for `ED` encounter types. Should be missing for `AV` or `OA` encounters. Use leading zeroes for codes less than 100. | `372` |
| `DRG_Type` | Char (1) | `1` = CMS-DRG (old system)<br>`2` = MS-DRG (current system) | DRG code version. MS-DRG (current system) began on 10/1/2007. Should be populated for `IP` and `IS` encounter types. May be populated for `ED` encounter types. Should be missing for `AV` or `OA` encounters. | `1` |
| `Admitting_Source` | Char (2) | `AF` = Adult Foster Home<br>`AL` = Assisted Living Facility<br>`AV` = Ambulatory Visit<br>`ED` = Emergency Department<br>`HH` = Home Health<br>`HO` = Home / Self Care<br>`HS` = Hospice<br>`IP` = Other Acute Inpatient Hospital<br>`NH` = Nursing Home (Includes ICF)<br>`OT` = Other<br>`RH` = Rehabilitation Facility<br>`RS` = Residential Facility<br>`SN` = Skilled Nursing Facility<br>`UN` = Unknown<br> | Should be populated for Inpatient Hospital Stay (`IP`) and Non-Acute Institutional Stay (`IS`) encounter types. May be populated for Emergency Department (`ED`) encounter types. Should be missing for ambulatory visit (`AV` or `OA`) encounter types. | `HH` |

## NOTES:

1. Rollback transactions and other adjustments should be processed before populating this table. This may be handled differently by Data Partners and may be affected by billing cycles.

2. `PatID` is a pseudoidentifier with a consistent crosswalk to the true identifier retained by the source Data Partner. For analytical data sets requiring patient-level data, only the pseudoidentifier is used to link across all information belonging to a patient.

3. Medical utilization data is captured in 3 tables:
    - **Encounter**: the encounter record that characterizes the outpatient visit or hospital stay
    - **Diagnosis**: the diagnosis or other clinical code(s) associated with the encounter record
    - **Procedure**: the procedure code(s) associated with the encounter record.

    These 3 tables and the Inpatient Pharmacy, Inpatient Transfusion, Vital Signs, and Mother-Infant Linkage tables are linked by `EncounterID`. All diagnoses and procedures for an encounter should have the same `EncounterID`. It is allowable to have "orphan" diagnosis or procedure records with `EncounterID`s that do not have a match in the Encounter table.

4. The `Provider` variable must be consistent within a health plan. An inpatient stay must only have one `Provider`, even if multiple providers performed procedures.

[Return to Table of Contents](atoc_scdm.md) 