# SCDM: Provider Table Structure

**Description:** The SCDM Provider Table contains one record per `ProviderID`. This table should capture all uniquely recorded individual provider identifiers in the Dispensing, Diagnosis, Procedure, and Prescribing (if populated) tables.<sup>1</sup>

**Sort Order:** The Provider Table should be sorted by `ProviderID`.

**Unique Row:** `ProviderID`.

| Variable Name | Variable Type and Length (Bytes) | Values | Status | Definition / Comments / Guideline | Example |
| --- | --- | --- | --- | --- |--- |
| `ProviderID`<sup>2</sup> | Num(#) | Unique provider identifier | Required |Identifier for the individual provider who wrote a prescription in the Prescribing table, was identified in a row in the Dispensing table, made a diagnosis in the Diagnosis table, or performed a procedure or service in the Procedure table. As with the `PatID`, the provider identifier is a pseudoidentifier with a consistent crosswalk to the real identifier. Use the fewest number of bytes necessary to hold all distinct values; see ["SAS Lengths" Reference Table](SAS_lengths_reference_table.md). | `99218766` |
| `Specialty`<sup>3</sup> | Char(#)	| Provider specialty | Required | Code indicating the medical specialty of the Provider. See  [Reference Tables](SCDM_v8.0.0_reference_tables_v1.0.0.xlsx). If an individual provider has more than one specialty, select the specialty under which the provider practices most often. Data Partners are requested to map to the most specific description possible. That is, Map to a 10&#45;character Taxonomy Code if possible; otherwise use a 2&#45;character specialty code. Length of either 2 or 10 per row, aligning with `Specialty_CodeType`. Use `99` for unknown or undefined individual provider specialty. | `45` or `207X00000X` |
| `Specialty_CodeType`	| Char(1) | `2` = 2&#45;character code<br> `0` = 10&#45;character code" | Required | `2` = a 2&#45;character code as found in the "PVD.specialty" Table within the [Reference Tables](SCDM_v8.0.0_reference_tables_v1.0.0.xlsx).<br> `0` = a 10&#45;character code as found in the Specialty_Codes table. | `2` |


## NOTES

1. If ALL `ProviderID` values in the other tables are set to `.U`, then create a Provider table, that meets these requirements:

   - Only 1 row in the table
   - `ProviderID` has a length of Num(3)
   - `ProviderID` is set to `.U`
   - `Specialty` has a length of Char(2)
   - `Specialty` is set to `99`
   - `Specialty_CodeType` is set to `2`

1. `ProviderID` links to the same-named variable in the Dispensing, Diagnosis, Procedure, and if populated, the Prescribing tables.
   
2. CMS Provider Taxonomy & Specialty Codes: Use only those values found in "PVD.specialty" Table, located within the [Reference Tables](SCDM_v8.0.0_reference_tables_v1.0.0.xlsx).  These are a subset from the [CMS Taxonomy Crosswalk.](https://www.cms.gov/Medicare/Provider-Enrollment-and-Certification/MedicareProviderSupEnroll/Downloads/TaxonomyCrosswalk.pdf)

[Return to SCDM Version 8.0.0 Table of Contents](800_00FM_atoc_scdm.md)
