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

nextflow requires a site specific configuration file. We provide a generic configuration file that works if you have Singularity installed and you are working on a HPC cluster running SGE. 

```
cp /data/course_backup/.../nf-machina-low.conf .
```

Let's look at the config file

```
>more nf-machina-low.conf

##### Use singularity instead of docker ########
docker.enabled = false

singularity.enabled = true
singularity.autoMounts = true

### Use SGE ###########
process.executor = 'sge'
process.penv = 'smp'

### cluster specific options ###
process.clusterOptions = '-S /bin/bash -p -1000 -q gpu.q,global.q,hram.q

executor.queueSize = 10000
```

the file contains three blocks: the first tells nextflow to use singularity instead of docker. Singularity is preferred in a HPC environment because it does not require root privileges. The second block tells nextflow to use Sun Grid Engine as a scheduler. If your cluster uses other schedulers, e.g. slurm, you will need to adjust this block. The third block adds system specific options that you would use if submitting by hand.


- [Assembly, QC, Taxonomic classification and Functional annotation of MAGs](#assembly-qc-taxonomic-classification-and-functional-annotation-of-mags)
  - [First step: Assembly and Binning](#first-step-assembly-and-binning)
  - [Second step: Bin quality filtering and dereplication](#second-step-bin-quality-filtering-and-dereplication)
  - [Third step: Taxonomic assignment](#third-step-taxonomic-assignment)
  - [Fourth step: Functional annotation](#fourth-step-functional-annotation)




## First step: Assembly and Binning

This step uses the mag-illumina workflow (https://metashot.github.io/workflows/#mag-illumina). You will need to download the sequencing reads 

```
mkdir fastq
cp /data/course_backup/.../*.fastq fastq
```

## Second step: Bin quality filtering and dereplication


## Third step: Taxonomic assignment

## Fourth step: Functional annotation

