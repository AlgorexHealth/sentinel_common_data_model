# SCDM: Inpatient Transfusion Table Structure

The SCDM Inpatient Transfusion table contains data on inpatient blood transfusion administrations. It contains one record per unique combination of PatID and TransID. Each record represents a unique inpatient pharmacy transfusion administration, as defined by unique value combinations of PatID / TransCode / TransCode_Type / TDate_Start / Ttime_Start.

| Variable Name | Variable Type and Length (Bytes) | Values | Definition / Comments / Guideline | Example |
|---|---|---|---|---|
| PatID<sup>1</sup> | Char (Site specific length) | Unique member identifier | Arbitrary person-level identifier. Used to link across tables. | `123456789012345` |
| EncounterID<sup>2</sup> | Char (Site specific length) | Unique encounter identifier | Arbitrary encounter-level identifier. Used to link across the Encounter, Diagnosis, Procedure, Vital Signs, Inpatient Pharmacy, & Inpatient Transfusion tables. | `123456789012345_12242005_99218766_IP` |
| TransID | Char (15) | Unique transfusion administration identifier | Retain b/c useful to map back to source data | `123456789012345` |
| TransCode | Char (15) | Code value for an infusion product | Must be paired with the correct TransCode_Type | `123451224200599` |
| TransCode_Type | Char(2) | `CD` = CODABAR<br>`IS` = ISBT | Transfusion product code type. This variable combined with the TransCode variable should be used to capture any type of Inpatient Infusion product in the source data. Other code types will be added as new terminologies are used. | `CD` |
| Orig_TransProd | Char (Site specific length) | Original product name/mneumonic | Name of product within Data Partner | `Thawed POOLED PLATELETS` |
| BloodType | Char(3) | `A`, `B`, `O`, `AB` (upper case) with RH factor (`+`, `-`, or null only) | Blood type and Rh factors, left-justified. Convert any text Rh factor to symbols (e.g., "pos" to "+", "negative" to "-"). Rh factor can be blank. | `AB+` |
| TDate_Start | Numeric (4) | SAS date value | Administration start date | `12/1/2005` |
| TTime_Start | Numeric (4) | SAS time value `HH:MM` | Administration start time. | `14:27` |
| TDate_End | Numeric (4) | SAS date value | Administration end date | `12/1/2005` |
| TTime_End | Numeric (4) | SAS time value `HH:MM` | Administration end time. | `20:56` |
| EncType | Char (2) | `ED` = Emergency Department | Includes ED encounters that become inpatient stays (in which case inpatient stays would be a separate encounter). Excludes urgent care visits. ED claims should be pulled before hospitalization claims to ensure that ED with subsequent admission won't be rolled up in the hospital event. | `IP` |
| | | `IP` = Inpatient Hospital Stay | Includes all inpatient stays, same-day hospital discharges, hospital transfers, and acute hospital care where the discharge is after the admission date. | |
| | | `IS` = Non-Acute Institutional Stay | Includes hospice, skilled nursing facility (SNF), rehab center, nursing home, residential, overnight non-hospital dialysis and other non-hospital stays. | |
| | | `OA` = Other Ambulatory Visit | Includes other non overnight AV encounters such as hospice visits, home health visits, skilled nursing facility visits, other non-hospital visits, as well as telemedicine, telephone and email consultations. |

# NOTES

1. PatID is a pseudoidentifier with a consistent crosswalk to the true identifier retained by the source Data Partner. For analytical data sets requiring patient-level data, only the pseudoidentifier is used to link across all information belonging to a patient.
2. The Encounter, Diagnosis, Procedure, Inpatient Transfusion, Inpatient Pharmacy, Vital Signs, and Mother-Infant Linkage tables are linked by EncounterID. All diagnoses and procedures for an encounter should have the same EncounterID.