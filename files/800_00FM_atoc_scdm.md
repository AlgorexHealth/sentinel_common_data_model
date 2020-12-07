# List of Tables

| Table Name | Source | Description |
|---|---|---|
|1. [Enrollment](800_05file01100_admin_enrollment.md) | Created by Data Partners using Data Partner data. | The SCDM Enrollment Table has a start/stop structure that contains one record per continuous enrollment period. Members with medical coverage, drug coverage, or both should be included. A unique combination of `PatID`, `Enr_Start`, `Enr_End`, `MedCov`, `DrugCov`, and `Chart` identifies a unique record. A break in enrollment (of at least one day) or a change in either the medical or drug coverage variables should generate a new record. |
|2. [Demographic](800_06file01200_admin_demographic.md) | Created by Data Partners using Data Partner data. | The SCDM Demographic Table contains one record per `PatID` with the most recent information on `Birth_Date`, `Sex`, `Race/Ethnicity`, and `PostalCode`. |
|3. [Dispensing](800_07file01300_admin_dispensing.md) | Created by Data Partners using Data Partner data. | The SCDM Outpatient Pharmacy Dispensing Table contains one record per unique outpatient pharmacy dispensing. Rollback transactions and other adjustments should be processed before populating this table. |
|4.1. [Encounter](800_08file01410_admin_encounter.md) | Created by Data Partners using Data Partner data. | The SCDM Encounter Table contains one record per `PatID` and `EncounterID`. Each encounter should have a single record in the SCDM Encounter Table. Each diagnosis and procedure recorded during the encounter should have a separate record in the Diagnosis or Procedure Tables. Rollback transactions and other adjustments should be processed before populating this table.<sup>1</sup> <br>• Conversion from Ambulatory or Emergency Visit (`ED`, `AV`, or `OA`) into Inpatient Hospital or Institutional Stay (`IP`, `IS`) through admission represents multiple encounters. The Ambulatory or Emergency Visit is one encounter, the Inpatient Hospital or Institutional Stay after admission is a second encounter.<br>• Transfer from one facility to another facility starts a new encounter at the new facility.<br>• If supported by Data Partner source data, multiple visits on the same day to the same facility, with no conversion from Ambulatory or Emergency Visit (`ED`, `AV`, or `OA`) into Inpatient Hospital or Institutional Stay (`IP`, `IS`) admission, should be created as distinct encounters and should include all diagnoses and procedures that were recorded during those separate visits, with distinct `ProviderID` values populated.  If source data cannot identify distinct multiple visits on the same day, then populate as a single encounter. |
|4.2. [Diagnosis](800_09file01420_admin_diagnosis.md) | Created by Data Partners using Data Partner data. | The SCDM Diagnosis Table contains one record per unique combination of `PatID`, `EncounterID`, `DX_CodeType`, `DX`, and `ProviderID`. This table should capture all uniquely recorded diagnoses for all encounters, per provider. |
|4.3. [Procedure](800_10file01430_admin_procedure.md) | Created by Data Partners using Data Partner data. | The SCDM Procedure Table contains one record per unique combination of `PatID`, `EncounterID`, `Px_CodeType`, `Px`, and `ProviderID`. This table should capture all uniquely recorded procedures for all encounters, per provider. |
|5.1. [Death](800_13file03510_registry_death.md) | Created by selected Data Partners. | The SCDM Death Table contains one record per `PatID`. When legacy data have conflicting reports, please make a local determination as to which to use. There is typically a 1-2 year lag in death registry data. |
|5.2. [Cause of Death](800_14file03520_registry_cause_of_death.md) | Created by selected Data Partners. | The SCDM Cause of Death Table can contain multiple COD records per `PatID`<sup>1</sup>. When legacy data have conflicting reports, please make a local determination as to which to use. There is typically a 1-2 year lag in death registry data. |
|6.1. [Laboratory Result](800_11file02610_clinical_lab_result.md) | Created by selected Data Partners. | The SCDM Laboratory Result Table contains one record per result/entry. Include only resulted lab tests.<sup>1</sup> Data Partners are strongly encouraged to review the comprehensive [Sentinel Common Data Model Laboratory Result Table Documentation](https://www.sentinelinitiative.org/sites/default/files/data/distributed-database/Sentinel_Common-Data-Model_Laboratory-Result-Table-Documentation_0.pdf) for details on how to populate each variable. |
|6.2. [Vital Signs](800_12file02620_clinical_vital_signs.md) | Created by selected Data Partners. | The SCDM Vital Signs Table contains one record per result/entry. |
|7.1. [Inpatient Pharmacy](800_15file04710_inpatient_inpatient_pharmacy.md) | Created by selected Data Partners. | The SCDM Inpatient Pharmacy table contains data on inpatient drug administrations. It contains one record per unique combination of `PatID`, `NDC`, `RxADate`, `RxATime`, and `RxID`. Each record represents a unique inpatient pharmacy dispensing administration. |
|7.2. [Inpatient Transfusion](800_16file04720_inpatient_inpatient_transfusion.md) | Created by selected Data Partners. | The SCDM Inpatient Transfusion table contains data on inpatient blood transfusion administrations. It contains one record per unique combination of `PatID` and `TransID`. Each record represents a unique inpatient pharmacy transfusion administration, as defined by unique value combinations of `PatID`/ `TransCode`/ `TransCode_Type`/ `TDate_Start`/ `Ttime_Start`. |
|8. [Mother&#8209;Infant Linkage](800_17file05800_mil_mother_infant_linkage.md) | Created by selected Data Partners. | The SCDM Mother-Infant Linkage Table contains one record per `MPatID`, `CPatID`, and `ADate`. This table is created following identification of mothers (via evidence of live delivery by women aged 10-54 inclusive) and infants (via date of birth) in the Sentinel Distributed Database (SDD). The file may include: <ol><li> Live birth deliveries (with `MPatID` and `ADate`) that were linked to a child (`CPatID`);</li><li>Live birth deliveries (with `MPatID` and `ADate`) that were not linked to a child (`CPatID`, `CBirth_Date`, `Sex`, and `CEnr_Start` will have missing values); and</li><li>Infants (with `CPatID`) who were not linked to a mother (`MPatID`, `MBirth_Date`, `Age`, `EncounterID`, `EncType`, `ADate`, `DDate`, `Birth_Type`, and `Birth_Type_Primes` will have missing values).</li></ol> |
|9. [Prescribing](800_18file01500_admin_prescribing.md) | Created by selected Data Partners. | The SCDM Prescribing Table contains one record per `PatID` and `PrescribingID`. This table should capture all uniquely recorded prescription orders, as unique combination of `PatID`, `OrderDate`, `Rx_CodeType`, `Rx`, and `RxRefills`. |
|10.1. [Facility](800_19file061010_ref_facility.md) | Created by selected Data Partners. | The SCDM Facility Table contains one record per `FacilityID`. This table should capture all uniquely recorded facility identifiers in the Encounter table and the Laboratory Results (if populated) tables. |
|10.2. [Provider](800_20file061020_ref_provider.md) | Created by selected Data Partners. | The SCDM Provider Table contains one record per `ProviderID`. This table should capture all uniquely recorded individual provider identifiers in the Dispensing, Diagnosis, Procedure, and Prescribing (if populated) tables. |


[Return to Overview](800_01FM_overview.md) 

[Navigate to SCDM Version 8.0.0. History of Modifications](800_03FM_history-of-modifications.md)
