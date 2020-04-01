# SCDM: Death Table Structure

Description: The SCDM Death Table contains one record per `PatID`<sup>1</sup>. When legacy data have conflicting reports, please make a local determination as to which to use. There is typically a 1-2 year lag in death registry data.

| Variable Name | Variable Type and Length (Bytes) | Values | Definition / Comments / Guideline | Example |
|--|--|--|--|--|
|`PatID`<sup>2</sup>|Char (Site specific length)| Unique member identifier|Arbitrary person-level identifier. Used to link across tables.|`123456789012345`|
|`DeathDt`| Numeric (4) | SAS date | Date of death. |`1/1/2006`|
|`DtImpute`|Char (1)| `B` = Both month and day imputed<br>`D` = Day imputed<br>`M` = Month imputed<br>`N` = Not imputed | When `DeathDt` is imputed, this variable indicates which parts of the date were imputed.|`N`|
|`Source`| Char (1)| `L` = Other, locally defined<br>`N` = National Death Index<br>`S` = State Death files<br>`T` = Tumor data | Source of death information.|`S`|
|`Confidence`| Char (1)|`E` = Excellent<br>F = Fair<br>P = Poor| Confidence that the patient drawn from the Source data represents the actual patient (contrasts with Confidence in the Cause of Death table). |`E`|

## NOTES

1. For efficiency death data is captured in 2 tables:
    - Death: the record that characterizes the death date and source of that information
    - Cause of Death: the cause(s) of death associated with the death record
    These 2 tables are linked by `PatID`. All Cause of Death records have a matching `PatID` in the Death Table.

2. `PatID` is a pseudoidentifier with a consistent crosswalk to the true identifier retained by the source Data Partner. For analytical data sets requiring patient-level data, only the pseudoidentifier is used to link across all information belonging to a patient.
