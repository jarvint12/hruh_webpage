# Submitting jobs to the job queue (adapted from Matti Kankainen)

Use the job queue for all longer running computations.

#### 1. Create your script e.g.  
```bash
/projects/fimm_ngs_mustjoki/tcr/run.sh 
```
#### 2. Edit permissions to your script to be able to run it
```bash
chmod +x run.sh 
```
#### 3. Submit job to queue

```bash
grun.py -n xyz -q highmem.q -c "/projects/fimm_ngs_mustjoki/tcr/run.sh"
```

* -n xyz = xyz is a prefix for error and stdout files and the name for the run in the queue
* -c ”pathtoscript” = path to your script to be submitted to the queue
* -q highmem.q = queue where the job is submitted

After the run has started, three files will appear to the directory you started the run in: 

* xyz.OU 	STDOUT of the program you are running, if not directed to other file by the program
* xyz.ER	error report of the program you are running, if not directed to other file by the program
* xyz.job		run start command
		

If you need to run several jobs, e.g. same script for 4 different datasets, create 4 scripts and start them separately. If your task takes long, it is useful to break it into multiple parts (if possible) to be run in parallel so that it will finish sooner.

```bash
grun.py -n xyz1 -q highmem.q -c "/projects/fimm_ngs_mustjoki/tcr/run1.sh"
grun.py -n xyz2 -q highmem.q -c "/projects/fimm_ngs_mustjoki/tcr/run2.sh"
grun.py -n xyz3 -q highmem.q -c "/projects/fimm_ngs_mustjoki/tcr/run3.sh"
grun.py -n xyz4 -q highmem.q -c "/projects/fimm_ngs_mustjoki/tcr/run4.sh"
```
If you need more memory, use –q hugemem.q


#### 4. To check if the status of your job, use 

```bash
qstat
```
In qstat output:

* job-ID 	= ID of your job, can be used to terminate the job
* prior	= 0.5 for all
* name	= the job name you specified
* user	= you
* state	= r (running), Eqw (error, job will not start), q (queued)
 
6. If you made a mistake and want to terminate the process

```bash
qdel JOBID
```
E.g. qdel 1205638


## Running R scripts in job queue

Running R scripts in job queue

#### 1.	Make an R script e.g. 

```bash
/projects/fimm_ngs_mustjoki/tcr/analysis.R
```

#### 2.	Make a bash script e.g. “run_R.sh” containing the following:

```R
/apps/statistics2/R-3.5.1/bin/R --no-save < /projects/fimm_ngs_mustjoki/tcr/analysis.R >& messages.err
```

messages.err will contain the error, warning etc. messages from R.

#### 3.	Submit the bash script to queue as above.

##### To install R packages, specify a path in the project directory and save it into libpath variable:

```R
package_library <- "path/to/packages"
libpath <- .libPaths(package_library)
 
source("http://bioconductor.org/biocLite.R")
biocLite("scran", lib = package_library)
biocLite("scater", lib = package_library)
```

Or from CRAN: 
```R
install.packages(“igraph”, repos = "http://cran.us.r-project.org")
```

To use the installed packages, specify the path when loading library:

```R
library(DNAcopy, lib.loc =  package_library)
```

