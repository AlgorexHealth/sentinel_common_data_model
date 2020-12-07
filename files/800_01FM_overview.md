# Overview and Description of the Common Data Model v8.0.0

## Sentinel

The primary goal of Sentinel is to build and operate a national public health surveillance system to monitor the safety of FDA-regulated medical products, including drugs, biologics, and devices. Sentinel is part of the Sentinel Initiative, the FDA’s response to a congressional mandate to create an active surveillance system using electronic health data.

The U.S. Food and Drug Administration's (FDA) Sentinel Initiative is a long-term effort to improve the FDA’s ability to identify and assess medical product safety issues. The Sentinel System is an active surveillance system that uses routine querying tools and pre-existing electronic healthcare data from multiple sources to monitor the safety of regulated medical products.

## Sentinel Common Data Model

The Sentinel Operations Center (SOC) coordinates the network of Sentinel Data Partners and leads development of the Sentinel Common Data Model (SCDM), a standard data structure that allows Data Partners to quickly execute distributed programs against local data. The SOC manages creation of the Sentinel Distributed Database (SDD) using the SCDM, and maintains complete documentation of the implementation and characteristics of the SDD. The SCDM was developed in accordance with the Mini-Sentinel Common Data Model Guiding Principles and was modeled after the Health Care Systems Research Network (formerly known as HMO Research Network) Virtual Data Warehouse.

The SCDM currently includes 16 tables that represent information for the data elements needed for Sentinel activities. Some tables are grouped into categories. Utilization tables (Encounter, Diagnosis, Procedure) are within the 4.0 group. Death and Cause of Death are within the 5.0 group. Laboratory Result and Vital Signs within the 6.0 group. Inpatient Pharmacy and Inpatient Transfusion are within the 7.0 group. Mother-Infant Linkage is within the 8.0 group. Prescribing is within the 9.0 group. Auxillary tables (Facility and Provider) are within the 10.0 group.

Several identifiers are used to link records across tables: a unique person identifier,`PatID`, a unique provider identifier, `ProviderID`, and a unique encounter identifier, `EncounterID`. Details of the 16 tables are provided in this document.

This data model is freely available to all.

* For more information about Sentinel visit the website at: [www.sentinelinitiative.org](https://www.sentinelinitiative.org/)
* For comments and suggestions, please email: [info@sentinelsystem.org](mailto:info@sentinelsystem.org?subject=Git SCDM 8.0.0)

[Navigate to SCDM Version 8.0.0. History of Modifications](800_3FM_history-of-modifications.md)

[Navigate to SCDM Version 8.0.0. Table of Contents](800_0FM_atoc_scdm.md)
