# SCDM: Inpatient Pharmacy Table Structure

Description: The SCDM Inpatient Pharmacy table contains data on inpatient drug administrations. It contains one record per unique combination of `PatID`, `NDC`, `RxADate`, `RxATime`, and `RxID`. Each record represents a unique inpatient pharmacy dispensing administration.

| Variable Name | Variable Type and Length (Bytes) | Values | Definition / Comments / Guideline | Example |
|---|---|---|---|---|
| `PatID`<sup>1</sup> | Char (Site specific length) | Unique member identifier | Arbitrary person-level identifier. Used to link across tables. | `123456789012345` |
| `EncounterID`<sup>2</sup> | Char (Site specific length) | Unique encounter identifier | Arbitrary encounter-level identifier. Used to link across the Encounter, Diagnosis, Procedure, Vital Signs, Inpatient Pharmacy, & Inpatient Transfusion tables. | `123456789012345_12242005_99218766_IP` |
| `NDC` | Char (11) | National Drug Code | Please expunge any place holders (e.g., '\-' or extra digit) | `12345678910` |
| `RxID` | Char (15) | Unique Rx administration identifier | Useful to map back to source data | |
| `RxADate` | Numeric (4) | SAS date value | Rx Administration date | `12/1/2005` |
| `RxATime` | Numeric (4) | SAS time value `HH:MM` | Rx Administration time | `20:56` |
| `RxRoute` | Char (10) | Text | Actual / administered route. Standard list of allowable values under development. | `IV` |
| `RxDose` | Num (8) | Numeric digits with or without a decimal | Actual / administered dose. Intended to be analyzed in conjunction with the `RxUOM` (unit of measure) field and product strength data associated with the NDC (available from drug databases). Format captures maximum # of whole and decimal digits allowed by software technology for numeric data. | `100` |
| `RxUOM` | Char (10) | Text | Actual / administered unit of measure. Intended to be analyzed in conjunction with the `RxDose` field and product strength data associated with the NDC (available from drug databases). Standard list of allowable values under development. | `ML` |

## NOTES:

1. `PatID` is a pseudoidentifier with a consistent crosswalk to the true identifier retained by the source Data Partner. For analytical data sets requiring patient-level data, only the pseudoidentifier is used to link across all information belonging to a patient.

2. The Encounter, Diagnosis, Procedure, Inpatient Transfusion, Inpatient Pharmacy, Vital Signs, and Mother-Infant Linkage tables are linked by `EncounterID`. All diagnoses and procedures for an encounter should have the same `EncounterID`.

[Return to SCDM Version 7.1.0. Table of Contents](atoc_scdm.md) 