![alt text](resources/logo.png)

<br> 
<br> 

# Sentinel Common Data Model (SCDM)<br>  

### Overview<br>  
The Sentinel Common Data Model (SCDM) represents the standard data structure that allows for rapid implementation of standard queries across the Sentinel Distributed Database (SDD). [<b>Sentinel routine querying tools</b>](https://dev.sentinelsystem.org/projects/AD/repos/qrp/browse) are designed to run against data transformed into the Sentinel Common Data Model format.

Sentinel routine querying tools are SAS® programs. This means the SCDM-formatted data must be in the form of SAS datasets in order to use these analytic programs.

### What is the SCDM?<br>
The SCDM was developed by the Sentinel Operations Center (SOC) in accordance with the [<b>Mini-Sentinel Common Data Model Guiding Principles</b>](https://www.sentinelinitiative.org/sites/default/files/data/distributed-database/Mini-Sentinel_CommonDataModel_GuidingPrinciples_v1.0_0.pdf) and was originally modeled after the [<b>Health Care Systems Research Network Virtual Data Warehouse (HCSRN/VDW)</b>](http://www.hcsrn.org/en/Tools%20&%20Materials/VDW/). 

The SCDM includes various tables of data elements. Records are linked across tables by a unique person identifier, `PatID`. 

### The following versions of the SCDM are available<br>
[<b>SCDM Version 7.1.0</b>](https://dev.sentinelsystem.org/projects/SCDM/repos/sentinel_common_data_model/browse?at=SCDM7.1.0)<br>
Date: 7/18/20<br>
Updated Laboratory Result Table to add new allowable values to several existing variables in order to include new Covid-19 diagnostic test results.<br> 

### Getting Started<br>
To begin translating your data into the SCDM format, see the SCDM versions available at the link(s) above.

### Additional Resources <br>
For an example dataset in the SCDM format, please visit the Sentinel website to download [<b>Medicare Claims Synthetic Public Use Files in Sentinel Common Data Model Format</b>](https://www.sentinelinitiative.org/sentinel/surveillance-tools/software-toolkits/Medicare-SynPUFs-in-SCDM) files.

### Additional Information <br>
The Sentinel Operations Center has limited capacity to support use of our tools. However, we welcome feedback, comments, and suggestions pertaining to our documentation or tools. Email us [<b>here</b>](mailto:info@sentinelsystem.org?subject=Git).  

[<b>Navigate back to the Sentinel Initiative SCDM web page</b>](https://www.sentinelinitiative.org/sentinel/data/distributed-database-common-data-model/sentinel-common-data-model)
