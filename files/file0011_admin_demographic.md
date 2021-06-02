# SCDM: Demographic Table Structure

Description: The SCDM Demographic Table contains one record per `PatID` with the most recent information on `Birth_Date`, `Sex`, `Race/Ethnicity`, and `Zip Code`.

| Variable Name | Variable Type and Length (Bytes) | Values | Definition / Comments / Guideline | Example |
| --- | --- | --- | --- | --- |
| `PatID`<sup>1</sup> | Char (Site specific length) | Unique member identifier | Arbitrary person-level identifier. Used to link across tables. | `123456789012345` |
| `Birth_Date` | Numeric (4) | SAS date | Date of birth. | `12/5/1971` |
| `Sex` | Char (1) | `A` = Ambiguous (e.g., transgender)<br>`F` = Female<br>`M` = Male<br>`U` = Unknown | Sex. | `F` |
| `Hispanic` | Char (1) | `N` = No<br>`Y` = Yes<br> `U` = Unknown | A person of Cuban, Mexican, Puerto Rican, South or Central American, or other Spanish culture or origin, regardless of race. | `N` |
| `Race` | Char (1) | `0` = Unknown | Please use only one race value per member.<br> | `2` |
| | | `1` = American Indian or Alaska Native | A person having origins in any of the original peoples of North and South America (including Central America), and who maintains tribal affiliation or community attachment. | |
| | | `2` = Asian | A person having origins in any of the original peoples of the Far East, Southeast Asia, or the Indian subcontinent including, for example, Cambodia, China, India, Japan, Korea, Malaysia, Pakistan, the Philippine Islands, Thailand, and Vietnam. | |
| | | `3` = Black or African American | A person having origins in any of the black racial groups of Africa. | |
| | | `4` = Native Hawaiian or Other Pacific Islander | A person having origins in any of the original peoples of Hawaii, Guam, Samoa, or other Pacific Islands. | |
| | | `5` = White | A person having origins in any of the original peoples of Europe, the Middle East, or North Africa. | |
| `Zip` | Char (5) | Zip code | First 5 digits of the ZIP code of the member's most recent primary residence. | `04090` |
| `Zip_Date` | Numeric (4) | SAS date | Earliest date that the ZIP code is believed to be valid. Date will be updated/overwritten as ZIP code changes over time. | `12/12/2009` |

## NOTES:

1. `PatID` is a pseudoidentifier with a consistent crosswalk to the true identifier retained by the source Data Partner. For analytical data sets requiring patient-level data, only the pseudoidentifier is used to link across all information belonging to a patient.

[Return to SCDM Version 7.1.0. Table of Contents](atoc_scdm.md)

