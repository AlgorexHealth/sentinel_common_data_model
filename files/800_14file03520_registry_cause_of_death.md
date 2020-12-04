# SCDM: Cause of Death Table Structure

Description: The SCDM Cause of Death Table can contain multiple COD records per `PatID`<sup>1</sup>. When legacy data have conflicting reports, please make a local determination as to which to use. There is typically a 1-2 year lag in death registry data.

Sort Order: The Cause of Death Table should be sorted by `PatID`.

Unique Row: `PatID`, `CodeType`, `COD`.

| Variable Name | Variable Type and Length (Bytes) | Values | Status | Definition / Comments / Guideline | Example |
| --- | --- | --- | --- | --- |--- |
| `PatID`<sup>2</sup> | Num(#) | Unique patient identifier | Required | Arbitrary person-level identifier. Used to link across tables. Use the fewest number of bytes necessary to hold all distinct values; see ["SAS Lengths" Reference Table](SCDM_draft_reference_tables_8.1.0_r2.xlsx). | `123456789` |
| `COD` | Char(8) | Diagnosis code | Required | Remove decimal points, site specific suffixes and prefixes. | `J180` |
| `CodeType` | Char(2) | `09` = ICD&#45;9<br>`10` = ICD&#45;10 | Cause of death code type. | `09` |
| `CauseType` | Char(1) | `C` = Contributory<br>`I` = Immediate / Primary<br>`O` = Other<br>`U` = Underlying | Cause of death type. There should be only one "Underlying" code for cause of death, per `PatID`. | `C` |
| `Source` | Char(1) | `L` = Other, locally defined<br> `N` = National Death  Registry<br> `S` = Death files from State/ Region/ Province<br> `T` = Tumor data | Required | Source of cause of death information. | `S` |
| `Confidence` | Char(1) | `E` = Excellent<br> `F` = Fair<br> `P` = Poor |Required | Confidence that the patient drawn from the Source data represents the actual patient (contrasts with Confidence in the Death table).  If uncertain, use `P` = Poor. | `E` |

## NOTES:

1. For efficiency, death data is captured in 2 tables:
    - **Death**: the record that characterizes the death date and source of that information,
    - **Cause of Death**: the cause(s) of death associated with the death record.

    These 2 tables are linked by `PatID`. All Cause of Death records have a matching `PatID` in the Death Table.

2. `PatID` is a pseudoidentifier with a consistent crosswalk to the true identifier retained by the source Data Partner. For analytical data sets requiring patient-level data, only the pseudoidentifier is used to link across all information belonging to a patient.

[Return to SCDM Version 8.0.0. Table of Contents](800_0FM_atoc_scdm.md)
