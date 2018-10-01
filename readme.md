![alt text](resources/logo.png)
# Sentinel Common Data Model (SCDM)  

#### What is this?  
This repository contains documentation (data dictionary) for the Sentinel Common Data Model (SCDM), which is the standard data structure necessary for executing Sentinel's analytic programs.  

If you are looking for an example dataset in the SCDM format, please visit the Sentinel website to download [Medicare Claims Synthetic Public Use Files in Sentinel Common Data Model Format](https://www.sentinelinitiative.org/sentinel/surveillance-tools/software-toolkits/Medicare-SynPUFs-in-SCDM) files.

#### What is the SCDM?  
The Sentinel Operations Center (SOC) coordinates the network of Sentinel Data Partners and leads development of the Sentinel Common Data Model (SCDM), a standard data structure that allows Data Partners to quickly execute distributed programs against local data. The SOC Data Core manages creation of the Sentinel Distributed Database (SDD) using the SCDM, and maintains complete documentation of the implementation and characteristics of the SDD. The SDD refers to the data held and maintained by the Data Partners in the SCDM format.  

The SCDM was developed in accordance with the Mini-Sentinel Common Data Model Guiding Principles and was originally modeled after the Health Care Systems Research Network Virtual Data Warehouse (HCSRN/VDW). The SCDM includes tables that represent information for the data elements needed for Sentinel activities. Records are linked across tables by a unique person identifier, PatID. Details of the tables are provided in the latest SCDM document.  

#### What you do  
Follow these guidelines for creating a SCDM/translating your data into SCDM
 

We acknowledge that the structure and content of data sources differs, thus Sentinel does not provide specific instructions on how to convert data to SCDM format. While Sentinel does not directly support use of our tools, we welcome feedback, comments, and suggestions pertaining to our documentation or the CIDA tool. Email us [here](mailto:info@sentinelsystem.org?subject=Git).