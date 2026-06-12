# Assembly, QC, Taxonomic classification and Functional annotation of MAGs

- [Assembly, QC, Taxonomic classification and Functional annotation of MAGs](#assembly-qc-taxonomic-classification-and-functional-annotation-of-mags)
  - [First step: Assembly and Binning](#first-step-assembly-and-binning)
  - [Second step: Bin quality filtering and dereplication](#second-step-bin-quality-filtering-and-dereplication)
  - [Third step: Taxonomic assignment](#third-step-taxonomic-assignment)
  - [Fourth step: Functional annotation](#fourth-step-functional-annotation)


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



## First step: Assembly and Binning

This step uses the mag-illumina workflow (https://metashot.github.io/workflows/#mag-illumina). You will need to download the sequencing reads 

```
mkdir fastq
cp /data/course_backup/.../*.fastq fastq
```

then run the workflow (do not do it, it would take several hours)

```
nextflow run metashot/mag-illumina \
 -r 2.2.0 \ ## version of the workflow
--assembler "megahit" \ ## use megahit as assembler
--reads '../fastq/*_R{1,2}.fastq.gz' \
--outdir "results" \ ## put the results here
-c nf-machina-low.conf \ ## use this configuration file
-with-report report.html \ ##produce an html report
-resume ##resume in case you start from a previous run
```

Running the workflow will produce two directories, namely "work" where all teh intermediate syeps are stored, and "results", where you will find the results of the run. "works" is needed only if you want to restart/rerun your workflow with different parameters, you can delete it if you are done.
Now lets look at the results. 

```
ls results/
bins  clean_reads_stats  metabat2  qc  raw_reads_stats  scaffolds  stats_scaffolds.tsv  unbinned
```

these directories contain the main output of the workflow. In particular:

scaffolds: scaffolds for each input sample;  
bins: genome bins;  
unbinned: unbinned contigs;  
stats_scaffolds.tsv: scaffold statistics. 

```
more results/stats_scaffolds.tsv
n_scaffolds	n_contigs	scaf_bp	contig_bp	gap_pct	scaf_N50	scaf_L50	ctg_N50	ctg_L50	scaf_N90	scaf_L90	ctg_N90	ctg_L90	scaf_max	ctg_max	scaf_n_gt50K	scaf_pct_gt50K	gc_avg	gc_std	filename
723443	723443	583269202	583269202	0.000	99194	960	99194	960	538340	353	538340	353	1283613	1283613	313	6.349	0.54500	0.11001	/nfs2/donatic/projects/Scuola_Bari/mag/work/17/b05c9d5e911502be97ed6e220a5971/Sample1.fa
284336	284336	399692155	399692155	0.000	14250	3452	14250	3452	175329	460	175329	460	1132101	1132101	681	19.894	0.59955	0.10263	/nfs2/donatic/projects/Scuola_Bari/mag/work/8a/cec91c719e0665e665564d6a8ca5aa/Sample2.fa
998958	998958	776929726	776929726	0.000	151465	949	151465	949	736223	347	736223	347	608239	608239	230	2.741	0.47109	0.11882	/nfs2/donatic/projects/Scuola_Bari/mag/work/4e/70206b5a198e8937253aef5b5c5dd1/Sample3.fa
```


## Second step: Bin quality filtering and dereplication


## Third step: Taxonomic assignment

## Fourth step: Functional annotation

