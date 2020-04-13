# SCDM: Vital Signs Table Structure

Description: The SCDM Vital Signs Table contains one record per result/entry.

| Variable Name | Variable Type and Length (Bytes) | Values | Definition / Comments / Guideline | Example |
|---|---|---|---|---|
| PatID<sup>1</sup> | Char (Site specific length) | Unique member identifier | Arbitrary person-level identifier. Used to link across tables. | `123456789012345` |
| EncounterID<sup>2</sup> | Char (Site specific length) | Unique encounter identifier | Arbitrary encounter-level identifier. Used to link across the Encounter, Diagnosis, Procedure, Vital Signs, Inpatient Pharmacy, & Inpatient Transfusion tables. | `123456789012345_12242005_99218766_IP` |
| Measure_Date<sup>2</sup> | Numeric (4) | SAS date | Date the vital signs were measured. | `12/1/2005` |
| Measure_Time | Numeric (4) | SAS time | Time associated with the vital signs record. This may be the time an actual blood pressure measurement was taken or it may be a check-in time from encounter. | |
| HT | Numeric (8) | Height (in inches) | `####.##` = If HT can be represented in inches. Only populated if height was taken on this date. If missing, leave blank. | `60.50` |
| WT | Numeric (8) | Weight (in lbs) | `####.##` = If WT can be represented in pounds. Only populated if weight was taken on this date. If missing, leave blank. | `170.25` |
| Diastolic | Numeric (4) | Diastolic blood pressure | `###` = If Diastolic can be represented in mmHg. Only populated if diastolic blood pressure was taken on this date. If missing, leave blank. | `70` |
| Systolic | Numeric (4) | Systolic blood pressure | `###` = If Systolic can be represented in mmHg. Only populated if systolic blood pressure was taken on this date. If missing, leave blank. | `120` |
| BP_Type | Char (1) | `E` = Extended<br>`M` = Multiple<br>`O` = Orthostatic<br>`R` = Rooming | Type of blood pressure taken. | `E` |
| Position | Char (1) | `1` = Sitting<br>`2` = Standing<br>`3` = Supine | Position for orthostatic blood pressure. If unknown, leave blank. | `1` |
| Tobacco | Numeric (3) | `1` = Current user<br>`2` = Never<br>`3` = Quit/former user<br>`4` = Passive<br>`5` = Environmental exposure<br>`6` = Not asked<br>`7` = Conflicting | Tobacco status as of the visit date. Unknown values should be left blank. The "Not asked" value should be used only when it is a valid response from your system (e.g. this is a valid value for EPIC). The "Conflicting" value should be used when you receive tobacco information from multiple sources that disagree. | `3` |
| Tobacco_Type | Numeric (3) | `1` = Cigarettes only<br>`2` = Other tobacco only<br>`3` = Cigarettes and other tobacco<br>`4` = None  | Type of tobacco used. Unknown values should be left blank. | `4` |

## NOTES

1. PatID is a pseudoidentifier with a consistent crosswalk to the true identifier retained by the source Data Partner. For analytical data sets requiring patient-level data, only the pseudoidentifier is used to link across all information belonging to a patient.
2. The Encounter, Diagnosis, Procedure, Inpatient Transfusion, Inpatient Pharmacy, Vital Signs, and Mother-Infant Linkage tables are linked by EncounterID. All diagnoses & procedures for an encounter should have the same EncounterID.