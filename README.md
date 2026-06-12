# Assembly, QC, Taxonomic classification and Functional annotation of MAGs

- [Assembly, QC, Taxonomic classification and Functional annotation of MAGs](#assembly-qc-taxonomic-classification-and-functional-annotation-of-mags)
  - [First step: Assembly and Binning](#first-step-assembly-and-binning)


## First step: Assembly and Binning

This step uses the mag-illumina workflow (https://metashot.github.io/workflows/#mag-illumina). The workflow is based on nextflow (https://www.nextflow.io/) and singularity (https://docs.sylabs.io/guides/3.5/user-guide/introduction.html), which are the only two software the you will need to install on your machine. Nextflow provides the framework for portable workflow creation and execution, while Singularity is a container platform that allows to run containerized software without actually installing it. Compared to other tools, like Virtual Machines, it is much lighter and less resource intensive.

