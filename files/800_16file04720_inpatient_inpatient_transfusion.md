# SCDM: Inpatient Transfusion Table Structure

**Description:** The SCDM Inpatient Transfusion table contains data on inpatient blood transfusion administrations. It contains one record per unique combination of `PatID` and `TransID`. Each record represents a unique inpatient pharmacy transfusion administration, as defined by unique value combinations of `PatID`/ `TransCode`/ `TransCode_Type`/ `TDate_Start`/ `Ttime_Start`.

**Sort Order:** The Inpatient Transfusion Table should be sorted by `PatID` and `TDate_Start`.

**Unique Row:** `PatID` and `TransID`.

| Variable Name | Variable Type and Length (Bytes) | Values | Status | Definition / Comments / Guideline | Example |
| --- | --- | --- | --- | --- |--- |
| `PatID`<sup>1</sup> | Num(#) | Unique patient identifier | Required | Arbitrary person&#45;level identifier. Used to link across tables. Use the fewest number of bytes necessary to hold all distinct values; see ["SAS Lengths" Reference Table](SAS_lengths_reference_table.md). | `123456789` |
| `EncounterID`<sup>2</sup> | Num(#) | Unique encounter identifier | Required | Arbitrary encounter&#45;level identifier. Used to link across the Encounter, Diagnosis, Procedure, Vital Signs, Mother&#45;Infant Linkage, Inpatient Pharmacy, Inpatient Transfusion, and Prescribing tables. Use the fewest number of bytes necessary to hold all distinct values; see  ["SAS Lengths" Reference Table](SAS_lengths_reference_table.md). | `98765432159753` |
| `TransID` | Char(15) | Unique transfusion administration identifier | Required | Retain because useful to map back to source data | `123456789012345` |
| `TransCode` | Char (15) | Code value for an infusion product | Required | Must be paired with the correct `TransCode_Type` | `123451224200599` |
| `TransCode_Type` | Char(2) | `CD` = CODABAR<br>`IS` = ISBT | Required | Transfusion product code type. This variable combined with the `TransCode` variable should be used to capture any type of Inpatient Infusion product in the source data. Other code types will be added as new terminologies are used. | `CD` |
| `Orig_TransProd` | Char(#) | Original product name/ mnemonic | Optional | Name of product within Data Partner. Site-specific length. | `Thawed POOLED PLATELETS` |
| `BloodType` | Char(3) | `A`, `B`, `O`, `AB` (upper case) with Rh factor (`+`, `-`, or null only) or `UN` = Unknown | Required | Blood type and Rh factors, without leading spaces. Convert any text Rh factor to symbols (e.g., “pos” to “+”, “negative” to “-“). Rh factor can be blank. | `AB+` |
| `TDate_Start` | Num(4) | SAS date value | Required | Administration start date. | `12/1/2015` |
| `TTime_Start` | Num(4) | SAS time value HH:MM | Optional | Administration start time. | `14:27` |
| `TDate_End` | Num(4) | SAS date value | Optional | Administration end date. | `12/1/2015` |
| `TTime_End` | Num(4) | SAS time value HH:MM | Optional | Administration end time. | `20:56` |
| `EncType` | Char(2) | `ED` = Emergency Department (Includes ED encounters that become inpatient stays through hospital admission. In this scenario, `ED` is one encounter, Inpatient Hospital Stay after admission from the ED is a second encounter. ED data should be identified before hospitalization data to ensure that ED with subsequent admission won't be rolled up in the hospital event. Transfer from one ED facility to another ED facility starts a new encounter at the new facility. Excludes urgent care visits.)<br> `IP` = Inpatient Hospital Stay (Includes all inpatient stays, same-day hospital discharges, and other acute hospital care where the discharge is after the admission date. Transfer from one facility to another facility starts a new encounter at the new facility.)<br>`IS` = Non-Acute Institutional Stay (Includes hospice, skilled nursing facility (SNF), rehab center, nursing home, residential, overnight non-hospital dialysis and other non-hospital stays. Transfer from one facility to another facility starts a new encounter at the new facility.)<br>`OA` = Other Ambulatory Visit (Includes other non-overnight `AV` encounters such as hospice visits, home health visits, skilled nursing facility visits, other non-hospital visits, as well as telemedicine, telephone and email consultations.) | Optional | Encounter Type |`IP` |

## NOTES:

1. `PatID` is a pseudoidentifier with a consistent crosswalk to the true identifier retained by the source Data Partner. For analytical data sets requiring patient-level data, only the pseudoidentifier is used to link across all information belonging to a patient.

2. The Encounter, Diagnosis, Procedure, Inpatient Transfusion, Inpatient Pharmacy, Vital Signs, Mother-Infant Linkage, Inpatient Pharmacy, Inpatient Transfusion, and Prescribing tables are linked by `PatID` and `EncounterID`.

[Return to SCDM Version 8.0.0 Table of Contents](800_00FM_atoc_scdm.md)
