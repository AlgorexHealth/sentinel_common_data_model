# SCDM: Enrollment Table Structure

Description: The SCDM Enrollment Table has a start/stop structure that contains one record per continuous enrollment period. Members with medical coverage, drug coverage, or both should be included. A unique combination of PatID, Enr_Start, Enr_End, MedCov, DrugCov, and Chart identifies a unique record. A break in enrollment (of at least one day) or a change in either the medical or drug coverage variables should generate a new record.

| Variable | Description |
| --- | --- |
| `PatID` | Arbitrary person-level identifier. Used to link across tables. A new enrollment period generates a new record, but the same person should have the same PatID on subsequent records.<br><br>**Valid Values**: Unique member identifier<br><br>**Note 1**: `PatID` is a pseudoidentifier with a consistent crosswalk to the true identifier retained by the source Data Partner. For analytical data sets requiring patient-level data, only the pseudoidentifier is used to link across all information belonging to a patient.<br><br>**Format**: Char(Site Specific Length)<br>**Example**: `123456789012345` |
| `Enr_Start` | Date of the beginning of the enrollment period. If the exact date is unknown, use the first day of the month. `Enr_Start` should not be before January 1, 2000.<br><br>**Valid Values**: SAS Date<br><br>**Note 1**: Adjacent and overlapping enrollment periods with the same `PatID`, `Enr_Start`, `Enr_End`, `MedCov`, `DrugCov`, and `Chart` values should be collapsed. Enrollment periods separated by more than one day should not be bridged. For example, an `Enr_End` date of `1/31/2005` should be bridged with an `Enr_Start` date of `2/1/2005`, but should not be bridged with an `Enr_Start` date of `2/2/2005`.<br><br>**Format**: Numeric(4)<br>**Example**: `1/1/2005` |
| `Enr_End` | Date of the end of the enrollment period. If the exact date is unknown, use the last day of the month.<br><br>**Valid Values**: SAS Date<br><br>**Note 1**: Adjacent and overlapping enrollment periods with the same `PatID`, `Enr_Start`, `Enr_End`, `MedCov`, `DrugCov`, and `Chart` values should be collapsed. Enrollment periods separated by more than one day should not be bridged. For example, an `Enr_End` date of `1/31/2005` should be bridged with an `Enr_Start` date of `2/1/2005`, but should not be bridged with an `Enr_Start` date of `2/2/2005`.<br>**Note 2**: `Enr_End` should not be imputed using the date of death found in the Death table.<br><br>**Format**: Numeric(4)<br>Example:`12/31/2005` |
| `MedCov` | Mark as "Y" if the health plan has any responsibility for covering medical care for the member during this enrollment period (i.e., if you expect to observe medical care provided to this member during the enrollment period).<br><br>**Valid Values**: `Y` = Yes<br>`N` = No<br>`U` = Unknown<br><br>**Format**: Char(1)<br>Example:`Y` |
| `DrugCov` |  Mark as "Y" if the health plan has any responsibility for covering outpatient prescription drugs for the member during this enrollment period (i.e., if you expect to observe outpatient pharmacy dispensings for this member during this enrollment period).<br><br>**Valid Values**: `Y` = Yes<br>`N` = No<br>`U` = Unknown<br><br>**Format**: Char(1)<br>**Example**: `Y`|
| `Chart` | Chart abstraction flag to answer the question, "Are you able to request charts for this member?" This flag does not address chart availability. Mark as "Y" if there are no contractual restrictions between you and the member (or sponsor) that would prohibit you from requesting any chart for this member.<br><br>**Note 1**:<br><br>**Valid Values**: `Y` = Yes<br>`N` = No<br><br>**Format**: Char(1)<br>**Example**: `Y` |

| Variable Name | Variable Type and Length (Bytes) | Values | Definition / Comments / Guideline | Example |
| --- | --- | --- | --- | --- |
| `MedCov` | Char (1) |  |  | `Y` |
| `DrugCov` | Char (1) | `Y` = Yes<br> `N` = No<br> `U` = Unknown | | `Y` |
| `Chart`<sup>4</sup> | Char (1) | `Y` = Yes<br> `N` = No |  | `Y` |

## NOTES

1. .

2. 

3. 

4. "Chart variable aims to identify enrollment periods for which medical charts cannot be requested. Potential scenarios include:
    1. Charts cannot be requested for Medicare members (all enrollment periods for Medicare members should be assigned `Chart='N'`)
    2. Charts cannot be requested for administrative services only (ASO) populations (all ASO enrollment periods should be assigned `Chart='N'`)

    "If there is no definitive information indicating that medical charts cannot be requested for member enrollment period(s), records should be assigned `Chart = 'Y'`.
