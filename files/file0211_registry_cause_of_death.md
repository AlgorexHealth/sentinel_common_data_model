# SCDM: Cause of Death Table Structure

Description: The SCDM Cause of Death Table contains one record per unique combination of `PatID` and `COD`.<sup>1</sup> When legacy data have conflicting reports, please make a local determination as to which to use. There is typically a 1-2 year lag in death registry data.

| Variable Name | Variable Type and Length (Bytes) | Values | Definition / Comments / Guideline | Example |
| --- | --- | --- | --- | --- |
| `PatID`<sup>2<sup> | Char (Site specific length) | Unique member identifier | Arbitrary person-level identifier. Used to link across tables. | `123456789012345` |
| `COD` | Char (8) | Diagnosis code | Cause of death code. Please include the decimal point in ICD codes (if any). | `J18.0` |
| `CodeType` | Char (2) | `09` = ICD-9<br>`10` = ICD-10 | Cause of death code type. | `09` |
| `CauseType` | Char (1) | `C` = Contributory<br>`I` = Immediate / Primary<br>`O` = Other<br>`U` = Underlying | Cause of death type. There should be only one underlying cause of death. | `C` |
| `Source` | Char (1) | `L` = Other, locally defined<br>`N` = National Death Index<br>`S` = State Death files<br>`T` = Tumor data | Source of cause of death information. | `S` |
| `Confidence` | Char (1) | `E` = Excellent<br>`F` = Fair<br>`P` = Poor | Confidence in the accuracy of the cause of death based on source, match, number of reporting sources, discrepancies, etc. | `E` |

## NOTES:

1. For efficiency death data is captured in 2 tables:
    - **Death**: the record that characterizes the death date and source of that information
    - **Cause of Death**: the cause(s) of death associated with the death record

    These 2 tables are linked by `PatID`. All Cause of Death records have a matching `PatID` in the Death Table.

2. `PatID` is a pseudoidentifier with a consistent crosswalk to the true identifier retained by the source Data Partner. For analytical data sets requiring patient-level data, only the pseudoidentifier is used to link across all information belonging to a patient.

[Return to Table of Contents](atoc_scdm.md) 