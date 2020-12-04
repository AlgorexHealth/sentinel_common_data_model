# SCDM: Vital Signs Table Structure

**Description:** The SCDM Vital Signs Table contains one record per result/entry.

**Sort Order:** The Vital Signs Table should be sorted by `PatID` and `Measure_Date`.

**Unique Row:** No definition for this table.

| Variable Name | Variable Type and Length (Bytes) | Values | Definition / Comments / Guideline | Example |
|---|---|---|---|---|
| `PatID`<sup>1</sup>| Num(#) | Unique patient identifier | Required | Arbitrary person-level identifier. Used to link across tables. Use the fewest number of bytes necessary to hold all distinct values; see ["SAS Lengths" Reference Table](SCDM_draft_reference_tables_8.1.0_r2.xlsx). | `123456789` |
| `EncounterID`<sup>2</sup> | Num(#) | Unique encounter identifier | Optional | Arbitrary encounter-level identifier. Used to link acronss the Encounter, Diagnosis, Procedure, Vital Signs, Mother-Infant Linkage, Inpatient Pharmacy, Inpatient Transfusion, and Prescribing tables. Use the fewest number of bytes necessary to hold all distinct values; see ["SAS Lengths" Reference Table](SCDM_draft_reference_tables_8.1.0_r2.xlsx). | `98765432159753` |
| `Measure_Date`| Num(4) | SAS date | Required | Date the vital signs were measured. | `12/1/2019` |
| `Measure_Time` | Num(4) | SAS time value HH:MM | Optional | Time associated with the vital signs record. This may be the time an actual blood pressure measurement was taken or it may be a check-in time from encounter. | `10:33` |
| `HT` | Num(8) | Number gt 0 | Optional | Height (in inches). `####.##` = If `HT` can be represented in inches. Only populated if height was taken on this date. If missing, leave blank. | `60.50` |
| `WT` | Num(8) | Number gt 0 | Optional | Weight (in lbs). `####.##` = If `WT` can be represented in pounds. Only populated if weight was taken on this date. If missing, leave blank. | `170.25` |
| `Diastolic` | Num(4) | Integer ge 0 | Optional | Diastolic blood pressure. `###` = If `Diastolic` can be represented in mmHg. Only populated if diastolic blood pressure was taken on this date. If missing, leave blank. | `70` |
| `Systolic` | Num(4) | Integer ge 0 | Optional | Systolic blood pressure. `###` = If `Systolic` can be represented in mmHg. Only populated if systolic blood pressure was taken on this date. If missing, leave blank. | `120` |
| `BP_Type` | Char(1) | `E` = Extended<br> `M` = Multiple<br> `O` = Orthostatic<br> `R` = Rooming | Optional | Type of blood pressure taken. | `E` |
| `Position` | Char(1) | `1` = Sitting<br> `2` = Standing<br> `3` = Supine | Optional | Position for orthostatic blood pressure. If unknown, leave blank. | `1` |
| `Tobacco` | Num(3) | `1` = Current user<br> `2` = Never<br> `3` = Quit/former user<br> `4` = Passive<br> `5` = Environmental exposure<br> `6` = Not asked<br> `7` = Conflicting | Optional | Tobacco status as of the visit date. Unknown values should be left blank. The "Not asked" value should be used only when it is a valid response from your system (e.g. this is a valid value for EPIC). The "Conflicting" value should be used when you receive tobacco information from multiple sources that disagree. | `3` |
| `Tobacco_Type` | Num(3) | `1` = Cigarettes only<br> `2` = Other tobacco only<br> `3` = Cigarettes and other tobacco<br> `4` = None  | Optional | Type of tobacco used. Unknown values should be left blank. | `4` |

## NOTES:

1. `PatID` is a pseudoidentifier with a consistent crosswalk to the true identifier retained by the source Data Partner. For analytical data sets requiring patient-level data, only the pseudoidentifier is used to link across all information belonging to a patient.

2. The Encounter, Diagnosis, Procedure, Inpatient Transfusion, Inpatient Pharmacy, Vital Signs, Mother-Infant Linkage, Inpatient Pharmacy, Inpatient Transfusion, and Prescribing tables are linked by `PatID` and `EncounterID`.

[Return to SCDM Version 8.0.0. Table of Contents](800_0FM_atoc_scdm.md)
