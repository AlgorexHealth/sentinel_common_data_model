# SCDM: Demographic Table Structure

**Description:** The SCDM Demographic Table contains one record per `PatID` with the most recent information on `Birth_Date`, `Sex`, `Race/Ethnicity`, and `PostalCode`.

**Sort Order:** The Demographic table should be sorted by `PatID`.

**Unique Row:** `PatID`.

| Variable Name | Variable Type and Length (Bytes) | Values | Status | Definition / Comments / Guideline | Example |
| --- | --- | --- | --- | --- |--- |
| `PatID`<sup>1</sup> | Num(#) | Unique patient identifier | Required | Arbitrary person-level identifier. Used to link across tables. Use the fewest number of bytes necessary to hold all distinct values; see ["SAS Lengths" Reference Table](SAS_lengths_reference_table.md). | `123456789` |
| `Birth_Date` | Num(4) | SAS date | Optional | Date of birth. | `12/5/1971` |
| `Sex` | Char(1) | `A` = Ambiguous (e.g., transgender/hermaphrodite)<br>`F` = Female<br>`M` = Male<br>`U` = Unknown | Required | Sex. | `F` |
| `Hispanic` | Char(1) | `N` = No<br>`Y` = Yes<br> `U` = Unknown | Required | A person of Cuban, Mexican, Puerto Rican, South or Central American, or other Spanish culture or origin, regardless of race. | `N` |
| `Race` | Char(1) | `0` = Unknown<br>`1` = American Indian or Alaska Native (A person having origins in any of the original peoples of North and South America (including Central America), and who maintains tribal affiliation or community attachment.<br>`2` = Asian (A person having origins in any of the original peoples of the Far East, Southeast Asia, or the Indian subcontinent including, for example, Cambodia, China, India, Japan, Korea, Malaysia, Pakistan, the Philippine Islands, Thailand, and Vietnam.)<br>`3` = Black or African American (A person having origins in any of the black racial groups of Africa.)<br>`4` = Native Hawaiian or Other Pacific Islander (A person having origins in any of the original peoples of Hawaii, Guam, Samoa, or other Pacific Islands.)<br>`5` = White (A person having origins in any of the original peoples of Europe, the Middle East, or North Africa.)<br>|Please use only one race value per patient.|Required| `2`
| `PostalCode` | Char(#) | Postal/region code |Optional| USA: First 5 digits of the ZIP code of the patient's most recent primary residence. (5 characters only)<br>Other: Complete postal code or region identifier. (variable length is dependent on code length) | `04090` |
| `PostalCode_Date` | Num(4) | SAS date |Optional| Earliest date that the `PostalCode` is believed to be continuously correct up until the end date of your source data for the ETL. Date will be updated/overwritten as postal code for a patient/member changes over time. | `12/12/2009` |

## NOTES:

1. `PatID` is a pseudoidentifier with a consistent crosswalk to the true identifier retained by the source Data Partner. For analytical data sets requiring patient-level data, only the pseudoidentifier is used to link across all information belonging to a patient.

[Return to SCDM Version 8.0.0 Table of Contents](800_00FM_atoc_scdm.md)
