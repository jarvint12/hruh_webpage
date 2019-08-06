# Install R-packages

To install R packages, specify a path in the project directory:

```
package_library <- "/projects/fimm_ngs_mustjoki/scrnaseq/analysisR/packages/"
libpath <- .libPaths(package_library)

```

## Already built libraries, check if library you'd like is already installed

```
list.files("/projects/fimm_ngs_mustjoki/scrnaseq/analysisR/packages/")
list.files("/projects/hruh_flow/scrnaseq/analysisR/packages/")

```
## 1) Install from CRAN

```
install.packages("Seurat", repos = "http://cran.us.r-project.org")
```

## 2) Install from Github

```
install.packages("devtools", repos = "http://cran.us.r-project.org", lib = package_library)
devtools::install_github("ropenscilabs/umapr")

```

## 3) Install from Bioconductor

```
source("http://bioconductor.org/biocLite.R")
biocLite("scran", lib = package_library)

```

## 4) Install directly from source

```
chooseCRANmirror(ind = 64)
source("http://cf.10xgenomics.com/supp/cell-exp/rkit-install-2.0.0.R")

```

## 5) Install Seurat

Atlas don't have the latest hdf5r, too lazy to ask to update it so figured out to download a version that is independent of hdf5r. 

```
devtools::install_github("HenrikBengtsson/seurat", ref="feature/hdf5r-optional")

```



## Load the downloaded packages

```
library(scran, lib.loc = package_library)
message("Packages installed")

```