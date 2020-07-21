# TCGA data

## TCGA filename barcode

TCGA file could be named for example TCGA-AB-2882-11A-01W-0732-08.
* TCGA = Project name
* AB = Tissue source site. AB means Acute Myeloid Leukemia sample from Washington University. More codes can be found [here](https://gdc.cancer.gov/resources-tcga-users/tcga-code-tables/tissue-source-site-codes).
* 2882 = Study participant, this would be the 2882th participant in the AML study from Washington University. Could be any alphanumeric value.
* 11 = Sample type, 11 is solid tissue normal. More codes can be found [here](https://gdc.cancer.gov/resources-tcga-users/tcga-code-tables/sample-type-codes). 01-09 are tumor types, 10-19 normal types and control samples are 20-29.
* A = Sample is split into vials, this indicates order of sample in a sequence of samples. A would be the first vial. Could be anything between A and Z.
* 01 = Vials are divided into portions. 01 is the first portion of sample. This can be 01-99.
* W = Analyte, DNA sample extracted from the portion. W would be Whole Genome Amplification (WGA) produced using Repli-G (Qiagen) DNA. List of letters are listed [here](https://gdc.cancer.gov/resources-tcga-users/tcga-code-tables/portion-analyte-codes)
* 0732 = Plate number. Analytes are distributed to plates (one or more), this one would be the 732th plate. 4-digit number.
* 08 = Center where the aliquot will go for analysis. 08 would be Broad Institute of MIT and Harvard. More center codes [here](https://gdc.cancer.gov/resources-tcga-users/tcga-code-tables/center-codes).

[Source and more information](https://docs.gdc.cancer.gov/Encyclopedia/pages/TCGA_Barcode/)  
[TCGA codes](https://gdc.cancer.gov/resources-tcga-users/tcga-code-tables)

## Access TCGA data
In this example we are interested in hematopoietic and reticuloendothelial systems data from TCGA program. We are interested cases where there is RNA-seq and WXS from the same sample, Primary Blood Derived Cancer - Peripheral Blood. We also want Solid tissue normal samples from those patients. We are only interested in BAM-files.

## 1. Go to the [GDC data portal](https://portal.gdc.cancer.gov/) and sign in

## 2. Filter data

### 2.1 In projects tab
In this case, we choose that primary site is hematopoietic and reticuloendothelial systems, program is TCGA, and experimental strategy is WXS. Then next to the keywords, we click "Open Query in Repository".

### 2.2 In Repository
We still want to specify, that we are only interested in solid tissue normal and Primary Blood Derived Cancer - Peripheral Blood samples. So next to the keywords we click "advanced search". There you can see examples how other search words have been written. We can write "and sample_type" and website proposes "sample.sample_type". Now we have written "and cases.samples.sample_type". Then add " in \[" and website proposes different sample types. Let us choose our sample types differentiated with comma. Now we have written " and cases.samples.sample_type in \["primary blood derived cancer - peripheral blood", "solid tissue normal"\]". Whole keyword should be
```bash
cases.primary_site in ["hematopoietic and reticuloendothelial systems"] and cases.project.program.name in ["TCGA"] and files.data_format in ["bam"] and files.experimental_strategy in ["WXS"] and cases.samples.sample_type in ["primary blood derived cancer - peripheral blood", "solid tissue normal"]
```
Now we can click "submit query".

### 2.3 Save set in Exploration
Under the keywords, click "View 149 cases in Exploration". There you can Save Case set. Let us name the case set "hemato_WXS". Now we can do the same with RNA-files, only difference is that in the first step we choose experimental strategy=RNA-Seq and in the second step we are not interested in solid tissue normal samples. You can save that case set with name "hemato_RNA". Saved sets you can find from top right corner, "Manage sets".

### 2.4 Filter sets in Analysis
Now you can go to "Analysis" tab and click "Select" in "Set Operations". Choose your two sets, "hemato_WXS" and "hemato_RNA", and click "Run". Now you can click the area where two sets overlap and click "Items saved" number on that row, which shows items in exploration. Again, you can save Case set.

## 3. View set in Repository, choose bam files and add all files to cart 
First, make sure your cart (upper right corner) is empty. Now you can view files of the set in Repository. From the left, choose bam-file. Add all files to cart.

## 4. Go to your cart, download Metadata and Manifest text files

## 5. Upload manifest and metadata files to the cluster.

## 6. Upload token_file.txt
From top right corner, click your username and Download token if you already have not. Upload it to the cluster.

## 7. Run manifest_editing.py in cluster
Program needs manifest and metadata files as arguments. It creates new_manifest.txt and important_info_of_metadata_files.txt. If you download TCGA-data with original manifest file, you will get a lot of useless files, because one patient may contain multiple WXS Tumor and WXS solid normal files. Program chooses the newest ones. It also makes sure that all the downloaded samples have RNA-seq and WXS tumor files from the same sample, as well as solid tissue normal file.

## 8. Download TCGA-data
```bash
/bioinformatics/tcga/gdc-client/gdc-client download -m path/to/new_manifest.txt -t path/to/token_file.txt -d path/to/wanted_directory
```
* -m path/to/new_manifest.txt = Path to the manifest file created by manifest_editing.py
* -t path/to/token_file.txt = Path to the downloaded token file
* -d path/to/wanted_directory = Path to directory you want files to be downloaded. Default is current directory

More optional commands can be found [here](https://docs.gdc.cancer.gov/Data_Transfer_Tool/PDF/Data_Transfer_Tool_UG.pdf) from page 16. 

## 9. Aftermath
Now you should have all the important files in the given destination directory (or current directory). Every file has its own directory containing the bam file, bai file and log files.
