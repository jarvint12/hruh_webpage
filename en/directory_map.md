## Storage systems

Several storage systems are connected to FIMM atlas

FIMM technology centre performs basic bioinformatics analyses as a part of the sequencing service. Outputs of these analyses are stored in various pipelines specific subfolder at /fs/vault/ and /fas/NGS/pipes/. Results within these pipeline specific folders are in turn organized by user groups. User groups that can include samples of relevance to group Mustjoki include those with patterns like: mustjoki, fhrb, hruh, heckman, kallioniemi, etc. Below list of some pipeline specific folders of importance to group Mustjoki. Please note that pipeline specific folders are read-only for most users.
 
 ```
/fs/vault/rnaseq2/	## RNA-seq analysis outputs by Kumar et al., 2017 RNA-seq data analysis pipeline
/fs/vault/rnaseq/	## RNA-seq analysis outputs by Nicoricci RNA-seq data analysis pipeline
/fas/NGS/pipes/FIMM-RNAseq/	## RNA-seq analysis outputs by Bishwa’s RNA-seq data analysis pipeline
/fs/vault/pipelines/	## 	Technology centre pipelines / software folder
/fs/vault/vcp/ ## 	DNA-seq QA and germline variant calling analysis outputs by Henrik Almusa’s VCP.
/fas/NGS/pipes/vcp/	## DNA-seq QA and germline variant calling analysis outputs by Henrik Almusa’s VCP.
/fs/vault/somatic/	## Somatic analysis outputs by Samuli’s (Eldfors) somatic variant calling pipeline
/fas/NGS/pipes/somatic/	## Somatic analysis outputs by Samuli’s (Eldfors) somatic variant calling pipeline
/fs/vault/bioinformatics	## Results of random bioinformatics analyses
/fas/NGS/pipes/cellranger/	## 	Results scRNA-seq data

/projects/hruh_flow_cytometry # (project directory for clinical flow cytometry data analysis)
/projects/crispr_cas9_screens # (project directory for CRISRP-Cas9 screen data analysis)

```

FIMM atlas has two folder spaces for project specific data at /project and /fs/projects. These include project folders that are mainly organized by user groups. Some folders of importance to group Mustjoki include /fs/projects/fimm_ngs_mustjoki/ and /projects/fimm_ngs_mustjoki/

FIMM atlas includes two group Mustjoki dedicated storages systems. All group Mustjoki users should be able to write to these folders. However, please note that these storages systems have a limited capacity and files should be removed once not needed anymore. General folders of importance include:

```
/csc/mustjoki/gatk/			## GATK analysis outputs
/csc/mustjoki/rnaseq/	## RNA-seq analysis outputs by Kumar et al., 2017 RNA-seq data analysis pipeline
/csc/mustjoki/pathogen_screen/ ## Microbe-screening analysis outputs by Ojala et al., 2021 analysis pipeilne
/csc/mustjoki/scrnaseq_vartrix ##	scRNA-seq somatic variant calls using Vartrix
/csc/mustjoki/vartrix/	## scRNA-seq somatic variant calls using Vartrix
/csc/mustjoki2/bioinformatics/	## Group Mustjoki shared pipelines / software
```


## Applications

```
/apps/statistics2/R-3.6.0/bin/ ## newest R
/csc/mustjoki/anaconda3/ ## anconda3

```
