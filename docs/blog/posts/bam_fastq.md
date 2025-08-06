---
date: 2025-02-04
authors:
  - saeidamiri1
description: Bam to Fastq
categories:
  - Bioinfo
authors:
  - saeidamiri1
---

# Does the BAM file contain all the necessary information to regenerate the original FASTQ files?
If you'd like to specify the human genome reference, run the following command:
<!-- more -->


It depends on a few things that you'll need to answer:
- Can you use the bam files to re-generate the fastq files? If so, then bam is good enough
  - Are the bam files "lossless", i.e. if any of the primary reads (i.e. Not flagged as secondary reads) are hard-clipped, then you can't recreate the original fastq.
     - Non-primary reads will include the sam flag not primary alignment (0x100) or the sam flag supplementary alignment (0x800).
     - Hard-clipped reads will include a "H" in the read's CIGAR string
     -  You can try the command `samtools view -F 2304 your_bam_file.bam | awk '$6 ~ /H/'|wc -l`
       1.1  The "-F 2304" excludes any reads that are either not-primary or supplementary
       1.2 the awk command looks for the "H" in the CIGAR string, i.e. the 6th bam column
       1.3 If this command returns a number > 0, then you'll know your bam isn't "lossless", so you need fastq
  - Do the bam files contain unmapped reads as well? If they don't then you can't recreate the original fastq
- Do the bam files take up less space than the fastq files?

If the answer to both questions is "yes", then you should use fastq. If the answer to either is "no", then use bam
