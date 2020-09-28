# SCDM: Dispensing Table Structure

Description: The SCDM Outpatient Pharmacy Dispensing Table contains one record per unique combination of `PatID`, `NDC`, and `RxDate`. Each record represents an outpatient pharmacy dispensing. Rollback transactions and other adjustments should be processed before populating this table.<sup>1,2</sup>

| Variable Name | Variable Type and Length (Bytes) | Values | Definition / Comments / Guideline | Example |
| --- | --- | --- | --- | --- |
| `PatID`<sup>3</sup> | Char (Site specific length) | Unique member identifier | Arbitrary person-level identifier. Used to link across tables. | `123456789012345` |
| `RxDate` | Numeric (4) | SAS date | Dispensing date (as close as possible to date the person received the dispensing). | `11/29/2005` |
| `NDC` | Char (11) | National Drug Code | Please expunge any place holders (e.g., '-' or extra digit). | `00006007431` |
| `RxSup`<sup>2</sup> | Numeric (4) | Days supply | Number of days that the medication supports based on the number of doses as reported by the pharmacist. This amount is typically found on the dispensings record. It should not be necessary to calculate this variable for use in the SCDM. Positive integer values are expected. | `30` |
| `RxAmt`<sup>2</sup> | Numeric (4) | Amount dispensed | Number of units (pills, tablets, vials) dispensed. Net amount per NDC per dispensing. This amount is typically found on the dispensings record. It should not be necessary to calculate this variable for use in the SCDM. Positive values are expected. | `60` |

## NOTES:

1. Medications distributed in other settings such as infusions given in medical practices or inpatient hospitals are captured in the utilization tables. Medication prescriptions (as opposed to dispensings) are not currently captured in the SCDM.

2. Rollback transactions and other adjustments that are indicative of a dispensing being canceled or not picked up by the member should be processed before populating this table. This may be handled differently by Data Partners and may be affected by billing cycles.

3. `PatID` is a pseudoidentifier with a consistent crosswalk to the true identifier retained by the source Data Partner. For analytical data sets requiring patient-level data, only the pseudoidentifier is used to link across all information belonging to a patient.

[Return to Table of Contents](atoc_scdm.md) 