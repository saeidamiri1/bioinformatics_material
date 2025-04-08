---
date: 2025-04-07
description: Hail
categories:
  - Annotation
authors:
  - saeidamiri1
---

# VEP
To use the Ensembl Variant Effect Predictor [VEP](https://useast.ensembl.org/info/docs/tools/vep/script/index.html) in Beluga, follow the steps outlined below:

<!-- more -->

## Step to run VEP in Beluga
###  VCF 
Specify the path of the VCF file as below:

```
VCF=./scratch/temp.vcf.gz
```
###  Output 
To save the output in the same directory as the VCF file, include the following in the job file. Otherwise, specify the output path in the OUTPUT parameter.
```
OUTPUT=${OUTPUT:-${VCF/.vcf/.annotated_vep.vcf}}
```

### Reference  
You need to specify the reference and data root folders. Add the following lines to the job file:

```
FASTA=/cvmfs/ref.mugqic/genomes/species/Homo_sapiens.GRCh38/genome/Homo_sapiens.GRCh38.fa
DIR_CACHE=/lustre03/project/6004655/COMMUN/data/VEP
DIR_PLUGINS=${DIR_CACHE}/Plugins
```

### Custom annotation
VEP can integrate custom annotation from standard format files into your results by using the --custom flag

In th emain code, we will use CLINVAR_VCF and CLINVAR_FIELDS. 



VEP can incorporate custom annotations from standard format files into your results using the --custom flag [see reference](https://useast.ensembl.org/info/docs/tools/vep/script/vep_custom.html).
In the main code, we will utilize CLINVAR_VCF and CLINVAR_FIELDS.

```
CLINVAR_VCF=${DIR_CACHE}/clinvar/clinvar_20240407.GRCh38.vcf.gz
CLINVAR_FIELDS="ALLELEID,CLNDN,CLNREVSTAT,CLNSIG,CLNSIGCONF"
```

### Plugins
VEP has several to extend, filter and manipulate the VEP output.
[see reference](https://useast.ensembl.org/info/docs/tools/vep/script/vep_plugins.html), for instance 
the follwoing  are  CADD_SNV,CADD_INDEL,REVEL_DATA,ALPHAMISSENSE_DATA,SPLICEAI_SNV,SPLICEAI_INDEL,UTRANNOTATOR_DATA,PLI_DATA. 

```
CADD_SNV=${DIR_PLUGINS}/CADD/GRCh38/gnomad.genomes.r3.0.snv.tsv.gz
CADD_INDEL=${DIR_PLUGINS}/CADD/GRCh38/gnomad.genomes.r3.0.indel.tsv.gz
REVEL_DATA=${DIR_PLUGINS}/REVEL/new_tabbed_revel_grch38.tsv.gz
ALPHAMISSENSE_DATA=${DIR_PLUGINS}/AlphaMissense/AlphaMissense_hg38.tsv.gz
SPLICEAI_SNV=${DIR_PLUGINS}/SpliceAI/spliceai_scores.raw.snv.hg38.vcf.gz
SPLICEAI_INDEL=${DIR_PLUGINS}/SpliceAI/spliceai_scores.raw.indel.hg38.vcf.gz
UTRANNOTATOR_DATA=${DIR_PLUGINS}/UTRAnnotator/uORF_5UTR_GRCh38_PUBLIC.txt
PLI_DATA=${DIR_PLUGINS}/pLI/pLI_values.txt
```


### Main vep command
Here is the VEP code that generates the annotation file, provided you correctly define the paths for the VCF file, annotations, and plugins.

```
vep -i ${VCF} \
  --fork 4 \
  --show_ref_allele \
  --xref_refseq \
  --af_gnomade \
  --af_gnomadg \
  --af \
  --assembly GRCh38 \
  --fasta ${FASTA} \
  --cache \
  --dir_cache ${DIR_CACHE} \
  --cache_version 111 \
  --dir_plugins ${DIR_PLUGINS} \
  --buffer_size 20000 \
  --offline \
  --force_overwrite \
  --vcf \
  --compress_output bgzip \
  --symbol \
  --hgvs \
  --hgvsg \
  --pick_allele \
  --variant_class \
  --domains \
  --sift s \
  --polyphen s \
  --regulatory \
  --custom ${CLINVAR_VCF},ClinVar,vcf,exact,0,${CLINVAR_FIELDS} \
  --plugin CADD,${CADD_SNV},${CADD_INDEL} \
  --plugin REVEL,${REVEL_DATA} \
  --plugin AlphaMissense,file=${ALPHAMISSENSE_DATA} \
  --plugin SpliceAI,snv=${SPLICEAI_SNV},indel=${SPLICEAI_INDEL} \
  --plugin NMD \
  --plugin UTRAnnotator,file=${UTRANNOTATOR_DATA} \
  --plugin pLI,${PLI_DATA} \
  -o ${OUTPUT}
```

### Main vep command
If you need to perform segregation after running VEP, consider using [segpy](https://neurobioinfo.github.io/segpy/latest/). 

## Whole CODE

```
VCF=./scratch/temp.vcf.gz
OUTPUT=${OUTPUT:-${VCF/.vcf/.annotated_vep.vcf}}


# reference and data root folders
FASTA=/cvmfs/ref.mugqic/genomes/species/Homo_sapiens.GRCh38/genome/Homo_sapiens.GRCh38.fa
DIR_CACHE=/lustre03/project/6004655/COMMUN/data/VEP
DIR_PLUGINS=${DIR_CACHE}/Plugins
# custom anno files and fields
CLINVAR_VCF=${DIR_CACHE}/clinvar/clinvar_20240407.GRCh38.vcf.gz
CLINVAR_FIELDS="ALLELEID,CLNDN,CLNREVSTAT,CLNSIG,CLNSIGCONF"
# plugin data files
CADD_SNV=${DIR_PLUGINS}/CADD/GRCh38/gnomad.genomes.r3.0.snv.tsv.gz
CADD_INDEL=${DIR_PLUGINS}/CADD/GRCh38/gnomad.genomes.r3.0.indel.tsv.gz
REVEL_DATA=${DIR_PLUGINS}/REVEL/new_tabbed_revel_grch38.tsv.gz
ALPHAMISSENSE_DATA=${DIR_PLUGINS}/AlphaMissense/AlphaMissense_hg38.tsv.gz
SPLICEAI_SNV=${DIR_PLUGINS}/SpliceAI/spliceai_scores.raw.snv.hg38.vcf.gz
SPLICEAI_INDEL=${DIR_PLUGINS}/SpliceAI/spliceai_scores.raw.indel.hg38.vcf.gz
UTRANNOTATOR_DATA=${DIR_PLUGINS}/UTRAnnotator/uORF_5UTR_GRCh38_PUBLIC.txt
PLI_DATA=${DIR_PLUGINS}/pLI/pLI_values.txt

# main vep command
vep -i ${VCF} \
  --fork 4 \
  --show_ref_allele \
  --xref_refseq \
  --af_gnomade \
  --af_gnomadg \
  --af \
  --assembly GRCh38 \
  --fasta ${FASTA} \
  --cache \
  --dir_cache ${DIR_CACHE} \
  --cache_version 111 \
  --dir_plugins ${DIR_PLUGINS} \
  --buffer_size 20000 \
  --offline \
  --force_overwrite \
  --vcf \
  --compress_output bgzip \
  --symbol \
  --hgvs \
  --hgvsg \
  --pick_allele \
  --variant_class \
  --domains \
  --sift s \
  --polyphen s \
  --regulatory \
  --custom ${CLINVAR_VCF},ClinVar,vcf,exact,0,${CLINVAR_FIELDS} \
  --plugin CADD,${CADD_SNV},${CADD_INDEL} \
  --plugin REVEL,${REVEL_DATA} \
  --plugin AlphaMissense,file=${ALPHAMISSENSE_DATA} \
  --plugin SpliceAI,snv=${SPLICEAI_SNV},indel=${SPLICEAI_INDEL} \
  --plugin NMD \
  --plugin UTRAnnotator,file=${UTRANNOTATOR_DATA} \
  --plugin pLI,${PLI_DATA} \
  -o ${OUTPUT}

```

## How use individual plugin
If you want to use an individual plug-in, visit the [Ensembl plug-in](https://useast.ensembl.org/info/docs/tools/vep/script/vep_plugins.html), download the desired plug-in, and add its path to your command. For example, to use CADD v1.7:


```
mkdir -p ~/scratch/CADD/GRCh38
cd  ~/scratch/CADD/GRCh38
wget https://krishna.gs.washington.edu/download/CADD/v1.7/GRCh38/whole_genome_SNVs.tsv.gz
wget https://krishna.gs.washington.edu/download/CADD/v1.7/GRCh38/whole_genome_SNVs.tsv.gz.tbi
wget https://krishna.gs.washington.edu/download/CADD/v1.7/GRCh38/gnomad.genomes.r4.0.indel.tsv.gz
wget https://krishna.gs.washington.edu/download/CADD/v1.7/GRCh38/gnomad.genomes.r4.0.indel.tsv.gz.tbi
```

Redefind the path: 

```
CADD_SNV=~/scratch/CADD/GRCh38/whole_genome_SNVs.tsv.gz
CADD_INDEL=~/scratch/CADD/GRCh38/gnomad.genomes.r4.0.indel.tsv.gz
```

Then run main vep command. 

## Reference
https://useast.ensembl.org/info/docs/tools/vep/script/index.html
https://useast.ensembl.org/info/docs/tools/vep/script/vep_tutorial.html
https://hpc.nih.gov/apps/VEP.html

