# SCDM: Facility Table Structure

**Description:** The SCDM Facility Table contains one record per `FacilityID`. This table should capture all uniquely recorded facility identifiers in the Encounter table and the Laboratory Results (if populated) tables.<sup>1</sup>

**Sort Order:** The Facility Table should be sorted by `FacilityID`.

**Unique Row:** `FacilityID`.

| Variable Name | Variable Type and Length (Bytes) | Values | Status | Definition / Comments / Guideline | Example |
| --- | --- | --- | --- | --- |--- |
| `FacilityID`<sup>2</sup> | Num(#) | Servicing facility identifier | Required |Local facility pseudoidentifier that identifies hospital or clinic. Taken from facility claims. Used for chart abstraction and validation. | `12345678` |
| `Facility_Location` | Char(#) | Geographic location (postal/region  code) of servicing facility (not billing location) | Optional | Should be left blank if missing. | `04090` |

## NOTES

1. If ALL `FacilityID` values in the other tables are set to `.U`, then create a Facility table, that meets these requirements:

   - Only 1 row in the table
   - `FacilityID` has a length of Num(3)
   - `FacilityID` is set to `.U`
   - `Facility_Location` has a length of Char(1)
   - `Facility_Location` is set to " " (i.e., blank)

2. `FacilityID` links to the same-named variable in the Encounter and Laboratory Results table.

[Return to SCDM Version 8.0.0. Table of Contents](800_0FM_atoc_scdm.md)
