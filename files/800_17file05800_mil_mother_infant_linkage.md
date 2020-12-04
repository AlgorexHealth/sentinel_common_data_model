# SCDM: Mother-Infant Linkage Table Structure

**Description:** The SCDM Mother-Infant Linkage Table contains one record per `MPatID`, `CPatID`, and `ADate`. This table is created following identification of mothers (via evidence of live delivery by women aged 10-54 inclusive) and infants (via date of birth) in the Sentinel Distributed Database (SDD). The file may include:

1. Live birth deliveries (with `MPatID` and `ADate`) that were linked to an infant (`CPatID`);
2. Live birth deliveries (with `MPatID` and `ADate`) that were not linked to an infant (`CPatID`, `CBirth_Date`, `Sex`, and `CEnr_Start` will have missing values); and
3. Infants (with `CPatID`) who were not linked to a mother (`MPatID`, `MBirth_Date`, `Age`, `EncounterID`, `EncType`, `ADate`, `DDate`, `Birth_Type`, and `Birth_Type_Primes` will have missing values).

**Sort Order:** The Mother-Infant Linkage Table should be sorted by `MPatID`, `Adate`, and `CPatID`.

**Unique Row:** `MPatID`, `EncounterID`, `CPatID`.

| Variable Name | Variable Type and Length (Bytes) | Values | Status | Definition / Comments / Guideline | Example |
| --- | --- | --- | --- | --- |--- |
| `MPatID`<sup>1</sup> | Num(#) | Unique patient identifier | Required for mother | Arbitrary person-level identifier. Used to link across tables. Use the fewest number of bytes necessary to hold all distinct values; see ["SAS Lengths" Reference Table](SCDM_draft_reference_tables_8.1.0_r2.xlsx). Must match mother `PatID` value in all other SCDM tables. Blank for infant-only records. | `123456789` |
| `MBirth_Date` | Num(4) | SAS Date | Required for mother | Mother `Birth_Date` value from SCDM Demographic table.  Missing for infant-only records. | `12/5/1971` |
| `Age` | Num(3) | 10-54 inclusive | Required for mother | Mother's age as of `ADate`. Missing for infant-only records. | `32` |
|`EncounterID`<sup>2</sup> | Num(#) | Unique encounter identifier | Required for mother | Arbitrary encounter&#45;level identifier. Used to link across the Encounter, Diagnosis, Procedure, Vital Signs, Mother&#45;Infant Linkage, Inpatient Pharmacy, Inpatient Transfusion, and Prescribing tables. Use the fewest number of bytes necessary to hold all distinct values; see  ["SAS Lengths" Reference Table](SCDM_draft_reference_tables_8.1.0_r2.xlsx). `EncounterID` value from SCDM Encounter table, for mother’s delivery encounter. Missing for infant-only records. | `98765432159753` |
| `EncType`<sup>3</sup> | Char(2) | `AV` = Ambulatory Visit<br>`ED` = Emergency Department<br>`IP` = Inpatient Hospital Stay<br>`IS` = Non-Acute Institutional Stay<br>`OA` = Other Ambulatory Visit | Required for mother | `EncType` value from SCDM Encounter table, for mother's delivery encounter. Blank for infant-only records. | `IP` |
| `ADate` | Num(4) | SAS Date | Required for mother | `ADate` value from SCDM Encounter table, for mother's delivery encounter. Missing for infant-only records. | `12/24/2005` |
| `DDate` | Num(4) | SAS Date; may be null | Optional for mother | `DDate` value from SCDM Encounter table, for mother's delivery encounter. Missing for infant-only records. | `12/31/2005` |
| `CPatID` | Num(#) | Unique member identifier. | Required for infant | Arbitrary person-level identifier. Used to link across tables. Use the fewest number of bytes necessary to hold all distinct values; see ["SAS Lengths" Reference Table](SCDM_draft_reference_tables_8.1.0_r2.xlsx). Must match infant `PatID` value in all other SCDM tables. Missing for mother/delivery only records. | `12341234` |
| `CBirth_Date` | Num(4) | SAS Date | Required for infant | Infant `Birth_Date` value from SCDM Demographic table. Missing for mother/delivery-only records. | `1/2/2015` |
| `Sex` | Char(1) | `A` = Ambiguous<br>`F` = Female<br>`M` = Male<br>`U` = Unknown | Required for infant | Infant `Sex` value from SCDM Demographic table. Blank for mother/ delivery-only records. | `F` |
| `CEnr_Start` | Num(4) | SAS Date | Required for infant | Earliest `Enr_Start` from Enrollment table. Missing for mother/delivery-only records. | `1/1/2005` |
| `Birth_Type` | Num(3) | `0` = Unspecified # of live births<br>`1` = 1 live birth<br>`2` = 2 live births<br>`3` = 3 live births<br>`4` = 4 live births<br>`5` = 5 live births<br>`8` = Multiple live births, unspecified number<br>`9` = Conflicting code(s) for number of live births | Required for mother | Based upon ICD&#45;9&#45;CM/ICD&#45;10&#45;CM codes in the health plan data for the delivery admission. Missing for infant-only records. | `3` |
| `Birth_Type_Primes` | Num(8) | 2+ | Required for mother | Multiplication of all prime numbers assigned to all instances of `Birth_Type` found in delivery codes within the selected encounter, as follows:<br> Prime = Birth_Type<br> `2` = `Birth_Type` of 0<br> `3` = `Birth_Type` of 1<br> `5` = `Birth_Type` of 2 <br>`7` = `Birth_Type` of 3 <br> `11` = `Birth_Type` of 4 <br>`13` = `Birth_Type` of 5 <br>`17` = `Birth_Type` of 8<br> This provides a record of all values of `Birth_Type` for the selected encounter.  Missing for infant-only records. | `5` |
| `MatchMethod` | Char(2) | `BC` = Birth Certificate<br> `RE` = DP maintained birth registry<br> `SI` = health plan subscriber or family number<br> `LA` = exact or probabilistic last name and address match based upon health plan administrative data<br> `OT` = other<br> `N1` = No subscriber/ family IDs available for linkage<br> `N2` = No name/ address available for linkage<br> `N3` = Neither subscriber/ family IDs nor name/ address available for linkage<br> `NA` = no linkage made; any other reason | Required | Prioritized method of linkage for mother-infant match, or reason for unlinked record:<br> For linked records, prioritize so that only one method is listed: `RE` > `SI` > `LA` > `BC` > `OT`,<br>For cases where a mother/ delivery is not linked to an infant OR an infant is not linked to a mother/delivery, the value of this variable should be one of `N1`, `N2`, `N3`, or `NA` only. | `RE`|

## NOTES:

1. `PatID` is a pseudoidentifier with a consistent crosswalk to the true identifier retained by the source Data Partner. For analytical data sets requiring patient-level data, only the pseudoidentifier is used to link across all information belonging to a patient.

2. The Encounter, Diagnosis, Procedure, Inpatient Transfusion, Inpatient Pharmacy, Vital Signs, Mother-Infant Linkage, Inpatient Pharmacy, Inpatient Transfusion, and Prescribing tables are linked by `PatID` and `EncounterID`.

3. If more than 1 delivery encounter occur on the same `ADate`, then the `EncType` values are based on the encounter selected from the following hierarchy: `IP` > `ED` > `AV` > `IS` > `OA`.

[Return to SCDM Version 8.0.0. Table of Contents](800_0FM_atoc_scdm.md)
