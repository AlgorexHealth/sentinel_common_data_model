# SCDM: Dispensing Table Structure

**Description:** The SCDM Outpatient Pharmacy Dispensing Table contains one record per unique outpatient pharmacy dispensing. Rollback transactions and other adjustments should be processed before populating this table.<sup>1,2</sup>

**Sort Order:** The Dispensing Table should be sorted by `PatID` and `RxDate`.

**Unique Row:** `PatID`, `RxDate`, `Rx_CodeType`, `Rx`, `ProviderID`.

| Variable Name | Variable Type and Length (Bytes) | Values | Status | Definition / Comments / Guideline | Example |
| --- | --- | --- | --- | --- |--- |
| `PatID`<sup>3</sup> | Num(#) | Unique patient identifier | Required | Arbitrary person-level identifier. Used to link across tables. Use the fewest number of bytes necessary to hold all distinct values; see ["SAS Lengths" Reference Table](SAS_lengths_reference_table.md). | `123456789` |
| `ProviderID` | Num(#)<sup>5</sup> | Unique provider identifier | Required | Identifier for the individual provider who prescribed the drug. As with the `PatID`, the provider identifier is a pseudoidentifier with a consistent crosswalk to the real identifier. If an individual provider/prescriber can not be identified, set to special missing value `.U`. This variable links to the Provider table. Use the fewest number of bytes necessary to hold all distinct values; see ["SAS Lengths" Reference Table](SAS_lengths_reference_table.md). | `12345` |
| `RxDate` | Num(4) | SAS date |Required |Dispensing date (as close as possible to date the person received the dispensing). | `11/29/2005` |
| `Rx` | Char(#) | Drug Code | Required | Code representing a prescribed medication or medical device. Please expunge any place holders (e.g., ‘-‘ or extra digit). Use the fewest number of bytes to contain values for all values of `Rx_CodeType`. | `00006007431` |
| `Rx_CodeType` | Char(2) | `ND` = National Drug Code (US)<br> `SN` = SNOMED CT (US)<br> `SK` = SNOMED CT (UK/CPRD)<br> `DM` = Dictionary of Medicines and Devices (UK)<br> `DI` = Drug Identification Number (CA)<br> `RN` = RxNorm (US)<br> `AT`= Anatomical Therapeutic Chemical Classification (DK)| Required | Code type of prescribed medication or medical device. This field combined with the `Rx` field should be used to capture any type of prescribed medication or medical device available in the source data. Other code types may be added as new terminologies are used. | `SK` |
| `RxSup`<sup>2</sup> | Num(4) | Days supply | Optional | Number of days that the medication supports based on the number of doses as reported by the pharmacist. This amount is typically found on the dispensings record. It should not be necessary to calculate this variable for use in the SCDM. Positive integer values are expected. | `30` |
| `RxAmt`<sup>2</sup> | Num(4) | Amount dispensed | Optional | Number of units (pills, tablets, vials) dispensed. Net amount per dispensing. This amount is typically found on the dispensings record. It should not be necessary to calculate this variable for use in the SCDM. Positive values are expected. | `60` |

## NOTES:

1. Medications distributed in other settings such as infusions given in medical practices or inpatient hospitals are captured in the utilization tables. Medication prescriptions (as opposed to dispensings) are captured in the Prescribing table within the SCDM.

2. Rollback transactions and other adjustments that are indicative of a dispensing being canceled or not picked up by the member should be processed before populating this table. This may be handled differently by Data Partners and may be affected by billing cycles.

3. `PatID` is a pseudoidentifier with a consistent crosswalk to the true identifier retained by the source Data Partner. For analytical data sets requiring patient-level data, only the pseudoidentifier is used to link across all information belonging to a patient.

4. `Rx_CodeType` includes options for values that are relevant to medication and medical device codes used in different international jurisdictions.

5. If all `ProviderID` values are unknown (i.e., set to `.U`), use Num(3) for the length of the variable.

[Return to SCDM Version 8.0.0 Table of Contents](800_00FM_atoc_scdm.md)
