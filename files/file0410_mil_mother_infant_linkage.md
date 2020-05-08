# SCDM: Mother-Infant Linkage Table Structure

The SCDM Mother-Infant Linkage Table contains one record per MPatID, CPatID, and ADate. This table is created following identification of mothers (via evidence of live delivery by women aged 10-54 inclusive) and infants (via date of birth) in the Sentinel Distributed Database (SDD). The file may include:

1. Live birth deliveries (with MPatID and ADate) that were linked to a child (CPatID);
2. Live birth deliveries (with MPatID and ADate) that were not linked to a child (CPatID, CBirth_Date, Sex, and CEnr_Start will have missing values); and
3. Children (with CPatID) who were not linked to a mother (MPatID, MBirth_Date, Age, EncounterID, EncType, ADate, DDate, Birth_Type, and Birth_Type_Primes will have missing values).

| Variable Name | Variable Type and Length (Bytes) | Values | Definition / Comments / Guideline | Example |
| --- | --- | --- | --- | --- |
| MPatID<sup>1</sup> | Char(Site specific length) | Unique member identifier. Text string; left justified. | Arbitrary person-level identifier. Used to link across tables. Length is DP specific. Must match mom "PatID" value in all other SCDM tables.Blank for child-only records. | `123456789012345` |
| MBirth_Date | Numeric(4) | SAS Date | Mother Birth_Date value from SCDM Demographic table.  Blank for child-only records. | `12/5/1971` |
| Age | Numeric(3) | 10-54 inclusive | Mother's age as of ADate.Blank for child-only records. | `32` |
| EncounterID<sup>2</sup> | Char(Site specific length) | Unique encounter identifier. | EncounterID value from SCDM Encounter table, for mother's delivery encounter.Blank for child-only records. | `123456789012345_12242005_99218766_IP` |
| EncType<sup>2</sup> | Char(2) | `AV` = Ambulatory Visit<br>`ED` = Emergency Department<br>`IP` = Inpatient Hospital Stay<br>`IS` = Non-Acute Institutional Stay<br>`OA` = Other Ambulatory Visit | EncType value from SCDM Encounter table, for mother's delivery encounter.Blank for child-only records. | `IP` |
| ADate | Numeric(4) | SAS Date | ADate value from SCDM Encounter table, for mother's delivery encounter.Blank for child-only records. | `12/24/200`5 |
| DDate | Numeric(4) | SAS Date; may be null | DDate value from SCDM Encounter table, for mother's delivery encounter.Blank for child-only records. | `12/31/2005` |
| CPatID | Char(Site specific length) | Unique member identifier. Text string; left justified. | Arbitrary person-level identifier. Used to link across tables. Length is DP specific. Must match child "PatID" value in all other SCDM tables.Blank for mother/delivery-only records. | `12341234` |
| CBirth_Date | Numeric(4) | SAS Date | Child Birth_Date value from SCDM Demographic table.Blank for mother/delivery-only records. | `1/2/2015` |
| Sex | Char(1) | `A` = Ambiguous (e.g., transgender/hermaphrodite)<br>`F` = Female<br>`M` = Male<br>`U` = Unknown | Child Sex value from SCDM Demographic table.Blank for mother/delivery-only records. | `F` |
| CEnr_Start | Numeric(4) | SAS Date | Earliest Enr_Start from Enrollment table.Blank for mother/delivery-only records. | `1/1/2005` |
| Birth_Type | Numeric(3) | `0` = Unspecified # of live births<br>`1` = 1 live birth<br>`2` = 2 live births<br>`3` = 3 live births<br>`4` = 4 live births<br>`5` = 5 live births<br>`8` = Multiple live births, unspecified number<br>`9` = Conflicting code(s) for number of live births | Based upon ICD-9-CM/ICD-10-CM codes in the health plan data for the delivery admission.Blank for child-only records. | `3` |
| Birth_Type_Primes | Numeric(8) | `2` = Birth_Type of 0<br>`3` = Birth_Type of 1<br>`5` = Birth_Type of 2<br>`7` = Birth_Type of 3<br>`11` = Birth_Type of 4<br>`13` = Birth_Type of 5<br>`17` = Birth_Type of 8 | Multiplication of all prime numbers assigned to all Birth_Types found in delivery codes within the selected encounter.  This provides a record of all values of Birth_Type for the selected encounter.Missing/null for child-only records. | `5` |
| MatchMethod | Char(2) | `BC` = Birth Certificate<br>`RE` = DP maintained birth registry<br>`SI` = health plan subscriber or family number<br>`LA` = exact or probabilistic last name and address match based upon health plan administrative data<br>`OT` = other<br> | Prioritized method of linkage for mom-baby match, or reason for unlinked record.For linked records, prioritize so that only one method is listed:RE > SI > LA > BC > OT | `RE` |
|  |  | `N1` = No subscriber/family IDs available for linkage<br>`N2` = No name/address available for linkage<br>`N3` = Neither subscriber/family IDs nor name/address available for linkage<br>`NA` = no linkage made; any other reason | Prioritized method of linkage for mom-baby match, or reason for unlinked record.For cases where a mother/delivery is not linked to a child OR a child is not linked to a mother/delivery, the value of this variable should be one of N1, N2, N3, or NA only | `N2` |

## NOTES

1. PatID is a pseudoidentifier with a consistent crosswalk to the true identifier retained by the source Data Partner. For analytical data sets requiring patient-level data, only the pseudoidentifier is used to link across all information belonging to a patient.
2. The Encounter, Diagnosis, Procedure, Inpatient Transfusion, Inpatient Pharmacy, Vital Signs, and Mother-Infant Linkage tables are linked by EncounterID. All diagnoses and procedures for an encounter should have the same EncounterID. If more than 1 delivery encounter occur on the same ADate, then the values are based on the encounter selected from the following hierarchy: IP > ED > AV > IS > OA
