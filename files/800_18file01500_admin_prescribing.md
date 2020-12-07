# SCDM: Prescribing Table Structure

**Description:** The SCDM Prescribing Table contains one record per `PatID` and `PrescribingID`. This table should capture all uniquely recorded prescription orders, as unique combination of `PatID`, `OrderDate`, `Rx_CodeType`, `Rx`, and `RxRefills`.

**Sort Order:** The Prescribing Table should be sorted by `PatID` and `OrderDate`.

**Unique Row:** `PatID` and `PrescribingID`.

| Variable Name | Variable Type and Length (Bytes) | Values | Status | Definition / Comments / Guideline | Example |
| --- | --- | --- | --- | --- |--- |
| `PatID`<sup>1</sup> | Num(#) | Unique patient identifier | Required | Arbitrary person-level identifier. Used to link across tables. Use the fewest number of bytes necessary to hold all distinct values; see  ["SAS Lengths" Reference Table](SCDM_v8.0.0_reference_tables_v1.0.0). | `123456789` |
| `EncounterID`<sup>2</sup> | Num(#) | Unique encounter identifier | Optional | Arbitrary encounter-level identifier. Used to link across the Encounter, Diagnosis, Procedure, Vital Signs, Mother-Infant Linkage, Inpatient Pharmacy, Inpatient Transfusion, and Prescribing tables. Use the fewest number of bytes necessary to hold all distinct values; see ["SAS Lengths" Reference Table](SCDM_v8.0.0_reference_tables_v1.0.0). | `98765432159753` |
| `PrescribingID`<sup>2</sup> | Num(#) | Unique row identifier | Required | Arbitrary identifier for each unique Prescribing record. Does not need to be persistent across refreshes, and may be created by any method that achieve a unique identifier per row. Use the fewest number of bytes necessary to hold all distinct values; see ["SAS Lengths" Reference Table](SCDM_v8.0.0_reference_tables_v1.0.0). | `123456789012345` |
| `ProviderID` | Num(#)<sup>3</sup> | Unique provider identifier | Required | Provider code for the individual provider who prescribed the medication. The provider code is a pseudoidentifier with a consistent crosswalk to the real identifier and is the same set of pseudoidentifiers for `ProviderID` in other SCDM tables. If an individual provider can not be identified, populate the `ProviderID` value with special missing value of `.U`. Use the fewest number of bytes necessary to hold all distinct values; see ["SAS Lengths" Reference Table](SCDM_v8.0.0_reference_tables_v1.0.0). | `99218766` |
| `OrderDate` | Num(4) | Valid SAS dates | Required | Order date of the prescription by the provider | 2/16/2011 |
| `Rx_CodeType` | Char(2) | `ND` = National Drug Code (US)<br> `SN` = SNOMED CT (US)<br> `SK` = SNOMED CT (UK/CPRD)<br> `DM` = Dictionary of Medicines and Devices (UK)<br> `DI` = Drug Identification Number (CA)<br> `RN` = RxNorm (US)<br> `AT`= Anatomical Therapeutic Chemical Classification (DK)<br> `GP` = Generic Product Identifier<br> | Required | Code type of prescribed medication or medical device. This field combined with the `Rx` field should be used to capture any type of prescribed medication or medical device available in the source data. Other code types may be added as new terminologies are used. | `ND` |
| `Rx` | Char(#) | Drug Code | Required | Code representing a prescribed medication or medical device. Please expunge any place holders (e.g., ‘-‘ or extra digit). Use the fewest number of bytes to contain values for all values of `Rx_CodeType`. | `00006007431` |
| `RxAmt` | Num(4) | Positive integer values are expected. | Optional | Quantity ordered. | `90` |
| `RxSup` | Num(4) | Positive integer values are expected. | Optional | Number of days supply ordered, as specified by the prescription. | `90` |
| `RxSource` | Char(2) | `OD` = Order/EHR<br> `DR` = Derived<br> `UN` = Unknown<br> `OT` = Other<br> | Required | Source of the prescribing information. | `OD` |
| `RxRoute` | Char(25) | Fixed list; see ReferenceTables.RXRoute | Required |Route of medication delivery. | ORAL_TABLET |
| `RxDoseQuantity` | Num(8) | Values greater than zero | Required | Dose of a given medication, as ordered by the provider. | `120` |
| `RxDoseUnit` | Char(25) | Fixed list; see ReferenceTables.RxDoseUnit | Required | Units of measure associated with the dose of the medication (i.e., `RxDoseQuantity`) as ordered by the provider. | `ueq`
| `RxDoseForm` | Char(40) | Fixed list; see ReferenceTables.RxDoseForm | Optional | The unit associated with the quantity prescribed. This is equivalent to RxNorm Dose Form.  Only valuable if using RxNorm (`Rx_CodeType` = `RN`). Can be blank. |`PELLET` |
`RxFreqQuantity` | Num(4) | Number per unit in `RxFreqUnit`; integers expected |Required | Specified frequency of medication per unit of time. | `2` |
`RxFreqUnit` | Char(1) | `D` = Per day<br> `W` = Per week<br> `M` = Per month<br> `O` = Other | Required | Frequency unit of administration. | `D` |
`RxRefills` | Num(3) | 0 or positive integers | Required | Number of refills ordered (not including the original prescription). If no refills are ordered, the value should be zero. | `2`|
`RxPrnFlag`	| Char(1) | `Y` = Yes<br> `N` = No<br> `U` = Unknown | Required	| Flag to indicate that all or part of medication frequency instructions includes “as needed.” | `N` |
`RxDAW` | Char(1) | `Y` = Yes<br> `N` = No<br> `U` = Unknown<br> `O` = Other | Required	| Flag to indicate whether the provider indicated that the medication order was to be dispensed as written (DAW). | Y |

## NOTES:

1. `PatID` is a pseudoidentifier with a consistent crosswalk to the true identifier retained by the source Data Partner. For analytical data sets requiring patient-level data, only the pseudoidentifier is used to link across all information belonging to a patient.

2. The Encounter, Diagnosis, Procedure, Inpatient Transfusion, Inpatient Pharmacy, Vital Signs, Mother-Infant Linkage, Inpatient Pharmacy, Inpatient Transfusion, and Prescribing tables are linked by `PatID` and `EncounterID`.

3. If all `ProviderID` values are unknown (i.e., set to `.U`), use Num(3) for the length of the variable.

[Return to SCDM Version 8.0.0 Table of Contents](800_00FM_atoc_scdm.md)
