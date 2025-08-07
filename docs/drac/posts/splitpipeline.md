---
date: 2025-08-07
description: split‑pipe
categories:
  - Annotation
authors:
  - saeidamiri1
---

# Split‑pipe
`split-pipe` a bioinformatics pipeline developed by [Parse Biosciences] for processing single-cell RNA sequencing data generated using their Split-Seq technology. The pipeline takes raw FASTQ files and produces processed data in the form of a cell-by-gene count matrix, which can be used as input for popular open-source analysis tools such as Scanpy and Seurat. It enables streamlined and efficient processing of sequencing results from start to finish.

<!-- more -->

## Step to run in Rorqual
###  Pipeline.0.9.6

First load the module

```
module load StdEnv/2023
PYTHONENV0=/lustre09/project/6004655/COMMON/soft2/packages/splitpipe/ParseBiosciences-Pipeline.0.9.6p/venv
export PYTHONPATH=$PYTHONENV0/lib/python3.10/site-packages:$PYTHONPATH
source $PYTHONENV0/bin/activate
```

Now you should have access to it 
```
split-pipe --help
usage: split-pipe [-h] [-m MODE] [-k KIT] [-p PARFILE] [-f FQ1] [--fq2 FQ2] [--genome_dir GENOME_DIR] [-o OUTPUT_DIR] [--sample SAMPLE_NAME [WELLS ...]] [--samp_list SAMP_LIST]
                  [--samp_sltab SAMP_SLTAB] [--no_allwell] [--genome_name [GENOME_NAME ...]] [--genes [GENES ...]] [--fasta [FASTA ...]] [--sublibraries [SUBLIBRARIES ...]]
                  [--sublib_list SUBLIB_LIST] [--tscp_use TSCP_USE] [--tscp_min TSCP_MIN] [--tscp_max TSCP_MAX] [--cell_use CELL_USE] [--cell_est CELL_EST] [--cell_xf CELL_XF]
                  [--cell_min CELL_MIN] [--cell_max CELL_MAX] [--save_anndata] [--save_figs] [--kit_list] [--bc_list] [--bc_round_set ROUND NAME] [--rseed RSEED] [--nthreads NTHREADS]
                  [--keep_going] [--reuse] [--keep_temps] [--one_step] [--clear_env_files] [--dryrun] [-e] [-V]
```

###  Pipeline.1.0.5
First load the module

```
module load StdEnv/2023
PYTHONENV0=/lustre09/project/6004655/COMMON/soft2/packages/splitpipe/ParseBiosciences-Pipeline.1.0.5p/venv
export PYTHONPATH=$PYTHONENV0/lib/python3.10/site-packages:$PYTHONPATH
source $PYTHONENV0/bin/activate
```

Now you should have access to it 
```
split-pipe --help
usage: split-pipe [-h] [-m MODE] [-k KIT] [-p PARFILE] [-f FQ1] [--fq2 FQ2] [--genome_dir GENOME_DIR] [-o OUTPUT_DIR] [--sample SAMPLE_NAME [WELLS ...]] [--samp_list SAMP_LIST]
                  [--samp_sltab SAMP_SLTAB] [--no_allwell] [--genome_name [GENOME_NAME ...]] [--genes [GENES ...]] [--fasta [FASTA ...]] [--sublibraries [SUBLIBRARIES ...]]
                  [--sublib_list SUBLIB_LIST] [--tscp_use TSCP_USE] [--tscp_min TSCP_MIN] [--tscp_max TSCP_MAX] [--cell_use CELL_USE] [--cell_est CELL_EST] [--cell_xf CELL_XF]
                  [--cell_min CELL_MIN] [--cell_max CELL_MAX] [--save_anndata] [--save_figs] [--kit_list] [--bc_list] [--bc_round_set ROUND NAME] [--rseed RSEED] [--nthreads NTHREADS]
                  [--keep_going] [--reuse] [--keep_temps] [--one_step] [--clear_env_files] [--dryrun] [-e] [-V]
```


###  Pipeline.1.6.0
First load the module

```
module load StdEnv/2023
module load python/3.13.2
module load  rust/1.85.0
PYTHONENV0=/lustre09/project/6004655/COMMON/soft2/packages/splitpipe/ParseBiosciences-Pipeline.1.6.0/venv
export PYTHONPATH=$PYTHONENV0/lib/python3.13/site-packages:$PYTHONPATH
source $PYTHONENV0/bin/activate
```

Now you should have access to it 

```
split-pipe --help
usage: split-pipe [-h] [-m MODE] [-c CHEMISTRY] [-k KIT] [-p PARFILE] [--run_name RUN_NAME] [-f [FQ1 ...]] [--fq2 [FQ2 ...]] [-o OUTPUT_DIR] [-g GENOME_DIR] [--parent_dir PARENT_DIR] [--targeted_list TARGETED_LIST] [--sample SAMPLE_NAME WELLS] [--samp_list SAMP_LIST] [--samp_sltab SAMP_SLTAB]
                  [--yes_allwell] [--no_allsample] [--genome_name [GENOME_NAME ...]] [--genes [GENES ...]] [--fasta [FASTA ...]] [--gfasta GENOME_NAME FASTA] [--mkref_validate] [--sublibraries [SUBLIBRARIES ...]] [--sublib_list SUBLIB_LIST] [--sublib_pref SUBLIB_PREF] [--sublib_suff SUBLIB_SUFF]
                  [--cell_list CELL_LIST] [--crispr] [--crsp_guides CRSP_GUIDES] [--crsp_read_thresh CRSP_READ_THRESH] [--crsp_tscp_thresh CRSP_TSCP_THRESH] [--crsp_use_star] [--immune_check] [--bcr_analysis] [--tcr_analysis] [--immune_genome IMMUNE_GENOME] [--use_imgt_db]
                  [--immune_read_thresh IMMUNE_READ_THRESH] [--save_anndata] [--kit_list [KIT_LIST]] [--chem_list] [--bc_list] [--sample_bc_rounds SAMPLE_BC_ROUNDS] [--rseed RSEED] [--nthreads NTHREADS] [--no_keep_going] [--no_fq_name_check] [--agg_sum_transpose] [--keep_temps] [--one_step]
                  [--until_step UNTIL_STEP] [--star_extra_args STAR_EXTRA_ARGS] [--clear_runproc] [--start_timeout START_TIMEOUT] [--chem_score_skip] [--kit_score_skip] [--dryrun] [-e] [-V]

SplitPipe data processing pipeline v1.6.0
```

## Reference

