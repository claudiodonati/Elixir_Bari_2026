# Assembly, QC, Taxonomic classification and Functional annotation of MAGs

The tutorial is based on MetaShot (https://metashot.github.io/), a curated set of Docker images and Nextflow workflows for metagenomics and microbiome genomics. Metashot is based on nextflow (https://www.nextflow.io/) and singularity (https://docs.sylabs.io/guides/3.5/user-guide/introduction.html), which are the only two software the you will need to install on your machine. Nextflow provides the framework for portable workflow creation and execution, while Singularity is a container platform that allows to run containerized software without actually installing it. Compared to other tools, like Virtual Machines, it is much lighter and less resource intensive.

Please see nextflow installation instructions at https://docs.seqera.io/nextflow/install

1. Download Nextflow

```
curl -s https://get.nextflow.io | bash
```

2.  Make Nextflow executable:

```
chmod +x nextflow
```

3. Move nextflow into your path

```
mkdir -p $HOME/.local/bin/
mv nextflow $HOME/.local/bin/
export PATH="$PATH:$HOME/.local/bin".
```

4. Check if everything works correctly
   
```
nextflow info
```


- [Assembly, QC, Taxonomic classification and Functional annotation of MAGs](#assembly-qc-taxonomic-classification-and-functional-annotation-of-mags)
  - [First step: Assembly and Binning](#first-step-assembly-and-binning)
  - [Second step: Bin quality filtering and dereplication](#second-step-bin-quality-filtering-and-dereplication)
  - [Third step: Taxonomic assignment](#third-step-taxonomic-assignment)
  - [Fourth step: Functional annotation](#fourth-step-functional-annotation)




## First step: Assembly and Binning

This step uses the mag-illumina workflow (https://metashot.github.io/workflows/#mag-illumina). You will need to download the sequencing reads 

## Second step: Bin quality filtering and dereplication


## Third step: Taxonomic assignment

## Fourth step: Functional annotation

