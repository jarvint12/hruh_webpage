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
[here](https://gdc.cancer.gov/resources-tcga-users/tcga-code-tables/center-codes).

[Source and more information](https://docs.gdc.cancer.gov/Encyclopedia/pages/TCGA_Barcode/)  
[TCGA codes](https://gdc.cancer.gov/resources-tcga-users/tcga-code-tables)

## Access TCGA data
In this example we are interested in hematopoietic and reticuloendothelial systems data from TCGA program. We are interested cases where there is RNA-seq and WXS from the same sample, Primary Blood Derived Cancer - Peripheral Blood. We also want Solid tissue normal samples from those patients. We are only interested in BAM-files.

### 1. Go to the [GDC data portal](https://portal.gdc.cancer.gov/) and sign in

## 2. Filter data

### 2.1 In projects tab
In this case, we choose that primary site is hematopoietic and reticuloendothelial systems, program is TCGA, and experimental strategy is WXS. Then next to the keywords, we click "Open Query in Repository".

### 2.2 In Repository
Now, from the left, we choose Data format=bam. But we still want to specify, that we are only interested in solid tissue normal and Primary Blood Derived Cancer - Peripheral Blood samples. So next to the keywords we click "advanced search". There you can see examples how other search words have been written. We can write "and sample_type" and website proposes "sample.sample_type". Now we have written "and cases.samples.sample_type". Then add " in \[" and website proposes different sample types. Let us choose our sample types differentiated with comma. Now we have written " and cases.samples.sample_type in \["primary blood derived cancer - peripheral blood", "solid tissue normal"\]". Whole keyword should be
```bash
cases.primary_site in ["hematopoietic and reticuloendothelial systems"] and cases.project.program.name in ["TCGA"] and files.data_format in ["bam"] and files.experimental_strategy in ["WXS"] and cases.samples.sample_type in ["primary blood derived cancer - peripheral blood", "solid tissue normal"]
```
Now we can click "submit query".

### 2.3 Save set in Exploration
Under the keywords, click "View 149 cases in Exploration". There you can Save Case set. Let us name the case set "hemato_WXS". Now we can do the same with RNA-files, only difference is that in the first step we choose experimental strategy=RNA-Seq and in the second step we are not interested in solid tissue normal samples. You can save that case set with name "hemato_RNA". Saved sets you can find from top right corner, "Manage sets".

### 2.4 Filter sets in Analysis
Now you can go to "Analysis" tab and click "Select" in "Set Operations". Choose your two sets, "hemato_WXS" and "hemato_RNA", and click "Run". Now you can click the area where two sets overlap and click "Items saved" number on that row, which shows items in exploration. Again, you can save Case set.

## 3. View set in Repository and download Manifest and TSV files
Now you can view files of the set in Repository. From the left, choose bam-files and download Manifest file. This is a text file that contains all the necessary information about downloading. You should also download TSV files. From down of the page, choose "show 100 entries", and then, from every page download TSV.

## 4. Upload manifest and TSV files to the cluster.

## 5. Upload token_file.txt
From top right corner, click your username and Download token. Upload it to the cluster.

## 6. Download TCGA-data
```bash
/bioinformatics/tcga/gdc-client/gdc-client download -m path/to/manifestfile.txt -t path/to/token_file.txt -d path/to/wanted_directory
```
* -m path/to/manifestfile.txt = Path to the downloaded manifest file
* -t path/to/token_file.txt = Path to the downloaded token file
* -d path/to/wanted_directory = Path to directory you want files to be downloaded. Default is current directory

More optional commands can be found [here](https://docs.gdc.cancer.gov/Data_Transfer_Tool/PDF/Data_Transfer_Tool_UG.pdf) from page 16. 

## 7. Run gdc_filtering_tool.py
Now there should be directory for every file, containing bam, bai and log files. There could be multiple WXS tumor files, and we are only interested in the most recent one. We can filter wanted files with command
```bash
/bioinformatics/data/tcga/gdc_filtering_tool.py -r "path_to_repository_file1 path_to_repository_file2 path_to_repository_file3 path_to_repository_file4" -s path/to/source_directory -d /path/to/destination_directory
```
* -r "path_to_repository_file1 path_to_repository_file2 path_to_repository_file3 path_to_repository_file4" = Paths to all your repository files
* -s path/to/source_directory = Path to directory where you downloaded all TCGA files. Default is current directory.
* -d /path/to/destination_directory = Path to directory where you want all importan files. Default is current directory.

## 8. Aftermath
Now you should have all the important files in the given destination directory. There should also be a text file containing information of all bam-files sorted by patient number. And there should be a text file containing information about moved files.





