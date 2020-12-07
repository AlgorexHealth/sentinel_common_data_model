# SCDM: Enrollment Table Structure

**Description:** The SCDM Enrollment Table has a start/stop structure that contains one record per continuous enrollment period. Patients with medical coverage, drug coverage, or both should be included. A unique combination of `PatID`, `Enr_Start`, `Enr_End`, `MedCov`, `DrugCov`, and `Chart` identifies a unique record. A break in enrollment (of at least one day) or a change in either the medical or drug coverage variables should generate a new record.

**Sort Order:** The Enrollment Table should be sorted by `PatID`, `Enr_Start`, `Enr_End`, `MedCov`, `DrugCov`, `Chart`.

**Unique Row:** `PatID`, `Enr_Start`, `Enr_End`, `MedCov`, `DrugCov`, `Chart`.

| Variable Name | Variable Type and Length (Bytes) | Values | Status | Definition / Comments / Guideline | Example |
| --- | --- | --- | --- | --- |--- |
| `PatID`<sup>1</sup> | Num(#) | Unique patient identifier| Required | Arbitrary person-level identifier. Used to link across tables. A new enrollment period generates a new record, but the same person should have the same PatID on subsequent records. Use the fewest number of bytes necessary to hold all distinct values; see ["SAS Lengths" Reference Table](SAS_lengths_reference_table.md).| `123456789` |
| `Enr_Start`<sup>2</sup> | Num(4) | SAS date | Required | Date of the beginning of the enrollment period. If the exact date is unknown, use the first day of the month. `Enr_Start` should not be before January 1, 2000. | `1/1/2019` |
| `Enr_End`<sup>2,3</sup> | Num(4) | SAS date | Required | Date of the end of the enrollment period. If the exact date is unknown, use the last day of the month. | `12/31/2019` |
| `MedCov` | Char(1) | `Y` = Yes<br> `N` = No<br> `U` = Unknown<br> `A` = Ambulatory Only | Required | Mark as `Y` if the health plan has any responsibility for covering medical care for the member during this enrollment period (i.e., if you expect to observe medical care provided to this member during the enrollment period). Mark as `A` if only ambulatory visit coverage is provided.| `Y` |
| `DrugCov` | Char(1) | `Y` = Yes<br> `N` = No<br> `U` = Unknown | Required | Mark as `Y` if the health plan has any responsibility for covering outpatient prescription drugs for the member during this enrollment period (i.e., if you expect to observe outpatient pharmacy dispensings for this member during this enrollment period). | `Y` |
| `Chart`<sup>4</sup> | Char(1) | `Y` = Yes<br> `N` = No | Required |Chart abstraction flag to answer the question, "Are you able to request charts for this member?" This flag does not address chart availability. Mark as `Y` if there are no contractual restrictions between you and the member (or sponsor) that would prohibit you from requesting any chart for this member. | `Y` |

## NOTES:

1. `PatID` is a pseudoidentifier with a consistent crosswalk to the true identifier retained by the source Data Partner. For analytical data sets requiring patient-level data, only the pseudoidentifier is used to link across all information belonging to a patient.

2. Adjacent and overlapping enrollment periods with the same `PatID`, `Enr_Start`, `Enr_End`, `MedCov`, `DrugCov`, and `Chart` values should be collapsed. Enrollment periods separated by more than one day should not be bridged. For example, an `Enr_End` date of `1/31/201` should be bridged with an `Enr_Start` date of `2/1/2019`, but should not be bridged with an `Enr_Start` date of `2/2/2019`.

3. `Enr_End` should not be imputed using the date of death found in the Death table.

4. `Chart` variable aims to identify enrollment periods for which medical charts cannot be requested. Potential scenarios include:
    1. Charts cannot be requested for Medicare members (all enrollment periods for Medicare members should be assigned `Chart`=`N`)
    2. Charts cannot be requested for administrative services only (ASO) populations (all ASO enrollment periods should be assigned `Chart`=`N`)

    If there is no definitive information indicating that medical charts cannot be requested for member enrollment period(s), records should be assigned `Chart`=`Y`.

[Return to SCDM Version 8.0.0 Table of Contents](800_00FM_atoc_scdm.md)
