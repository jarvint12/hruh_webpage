# TCGA data

## TCGA filename barcode

TCGA file could be named for example TCGA-AB-2882-11A-01W-0732-08.
* TCGA = Project name
* AB = Tissue source site. AB means Acute Myeloid Leukemia sample from Washington University. More codes can be found
[here](https://gdc.cancer.gov/resources-tcga-users/tcga-code-tables/tissue-source-site-codes).
* 2882 = Study participant, this would be the 2882th participant in the AML study from Washington University. Could be any alphanumeric value.
* 11 = Sample type, 11 is solid tissue normal. More codes can be found
[here](https://gdc.cancer.gov/resources-tcga-users/tcga-code-tables/sample-type-codes). 01-09 are tumor types, 10-19 normal types and 
control samples are 20-29.
* A = Sample is split into vials, this indicates order of sample in a sequence of samples. A would be the first vial. 
Could be anything between A and Z.
* 01 = Vials are divided into portions. 01 is the first portion of sample. This can be 01-99.
* W = Analyte, DNA sample extracted from the portion. W would be Whole Genome Amplification (WGA) produced using Repli-G (Qiagen) DNA. 
List of letters are listed [here](https://gdc.cancer.gov/resources-tcga-users/tcga-code-tables/portion-analyte-codes)
* 0732 = Plate number. Analytes are distributed to plates (one or more), this one would be the 732th plate. 4-digit number.
* 08 = Center where the aliquot will go for analysis. 08 would be Broad Institute of MIT and Harvard. More center codes 
[here](https://gdc.cancer.gov/resources-tcga-users/tcga-code-tables/center-codes)

[Source and more information](https://docs.gdc.cancer.gov/Encyclopedia/pages/TCGA_Barcode/)  
[TCGA codes](https://gdc.cancer.gov/resources-tcga-users/tcga-code-tables)

## Access TCGA data
