![alt text](resources/logo.png)

<br> 
<br> 

# Sentinel Common Data Model (SCDM)  

#### Overview  
This repository contains documentation (data dictionary) for the Sentinel Common Data Model (SCDM), which is the standard data structure necessary for executing Sentinel's routine querying tools. Note that data must be in the form of SAS datasets in order to use these analytic programs.  

#### What is the SCDM?
The SCDM was developed by the Sentinel Operations Center (SOC) in accordance with the [Mini-Sentinel Common Data Model Guiding Principles](https://www.sentinelinitiative.org/sites/default/files/data/distributed-database/Mini-Sentinel_CommonDataModel_GuidingPrinciples_v1.0_0.pdf) and was originally modeled after the [Health Care Systems Research Network Virtual Data Warehouse (HCSRN/VDW)](http://www.hcsrn.org/en/Tools%20&%20Materials/VDW/). The SCDM includes various tables of data elements. Records are linked across tables by a unique person identifier, PatID. Details of the tables are provided in the latest SCDM document.  

#### How to Access the SCDM 
To translate data into the SCDM, navigate to the SCDM branch in this repository by using the drop down menu in the upper left-hand corner or click [this link](https://dev.sentinelsystem.org/projects/QA/repos/sentinel_common_data_model/browse?at=refs%2Fheads%2Fscdm) to access the documentation.   

For an example dataset in the SCDM format, please visit the Sentinel website to download [Medicare Claims Synthetic Public Use Files in Sentinel Common Data Model Format](https://www.sentinelinitiative.org/sentinel/surveillance-tools/software-toolkits/Medicare-SynPUFs-in-SCDM) files.

#### Getting Started
Follow the guidelines above for creating a SCDM/translating your data into SCDM.  

#### Additional Information
The Sentinel Operations Center has limited capacity to support use of our tools. However, we welcome feedback , comments, and suggestions pertaining to our documentation or tools. Email us [here](mailto:info@sentinelsystem.org?subject=Git).
