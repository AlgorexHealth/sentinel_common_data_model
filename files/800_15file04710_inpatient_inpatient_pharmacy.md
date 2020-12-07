# SCDM: Inpatient Pharmacy Table Structure

**Description:** The SCDM Inpatient Pharmacy table contains data on inpatient drug administrations. It contains one record per unique combination of `PatID`, `NDC`, `RxADate`, `RxATime`, and `RxID`. Each record represents a unique inpatient pharmacy dispensing administration.

**Sort Order:** The Inpatient Pharmacy Table should be sorted by `PatID` and `RxADate`.

**Unique Row:** `PatID` and `RxID`.

| Variable Name | Variable Type and Length (Bytes) | Values | Status | Definition / Comments / Guideline | Example |
| --- | --- | --- | --- | --- |--- |
| `PatID`<sup>1</sup> | Num(#) | Unique patient identifier | Required | Arbitrary person&#45;level identifier. Used to link across tables. Use the fewest number of bytes necessary to hold all distinct values; see ["SAS Lengths" Reference Table](SAS_lengths_reference_table.md). | `123456789` |
| `EncounterID`<sup>2</sup> | Num(#) | Unique encounter identifier | Required | Arbitrary encounter&#45;level identifier. Used to link across the Encounter, Diagnosis, Procedure, Vital Signs, Mother&#45;Infant Linkage, Inpatient Pharmacy, Inpatient Transfusion, and Prescribing tables.Use the fewest number of bytes necessary to hold all distinct values; ["SAS Lengths" Reference Table](SAS_lengths_reference_table.md). | `98765432159753` |
| `NDC` | Char(11) | National Drug Code | Required | Please expunge any place holders (e.g., '\-' or extra digit) | `12345678910` |
| `RxID` | Num(#) | Unique Rx administration identifier | Required | Useful to map back to source data. Use the fewest number of bytes necessary to hold all distinct values. Use the fewest number of bytes necessary to hold all distinct values; ["SAS Lengths" Reference Table](SAS_lengths_reference_table.md). | |
| `RxADate` | Num(4) | SAS date value | Required | Rx Administration date | `12/1/2019` |
| `RxATime` | Num(4) | SAS time value HH:MM | Optional | Rx Administration time | `20:56` |
| `RxRoute` | Char(10) | Actual route description from source system | Optional | Actual / administered route. Standard list of allowable values under development. | `IV` |
| `RxDose` | Num(8) | Numeric digits with or without a decimal | Optional | Actual/administered dose. Intended to be analyzed in conjunction with the `RxUOM` (unit of measure) field and product strength data associated with the Drug Code (available from drug databases). Format captures maximum # of whole and decimal digits allowed by software technology for numeric data. | `100` |
| `RxUOM` | Char(10) | Actual unit of measure from source system | Optional | Actual/administered unit of measure. Intended to be analyzed in conjunction with the `RxDose` field and product strength data associated with the Drug Code (available from drug databases). Standard list of allowable values under development. | `ML` |

## NOTES:

1. `PatID` is a pseudoidentifier with a consistent crosswalk to the true identifier retained by the source Data Partner. For analytical data sets requiring patient-level data, only the pseudoidentifier is used to link across all information belonging to a patient.

2. The Encounter, Diagnosis, Procedure, Inpatient Transfusion, Inpatient Pharmacy, Vital Signs, Mother-Infant Linkage, Inpatient Pharmacy, Inpatient Transfusion, and Prescribing tables are linked by `PatID` and `EncounterID`.

[Return to SCDM Version 8.0.0 Table of Contents](800_00FM_atoc_scdm.md)
