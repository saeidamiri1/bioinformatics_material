---
date: 2025-08-06
description: split‑pipe
categories:
  - Annotation
authors:
  - saeidamiri1
---

# Split‑pipe
split-pipe is a bioinformatics pipeline developed by [Parse Biosciences] used to process single-cell RNA sequencing data generated with their Split-Seq technology.

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
## Reference

