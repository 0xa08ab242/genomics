# genomics
This repo is a place to keep some notes related to my personal efforts in getting more and better data from some whole genome sequence raw data files.  While more readily available tools (e.g. WGSExtract) and services (e.g. sequencing.com's EvE app) provide options for some analysis, these are insufficient for my purposes because:
- they does not utilize the latest reference files (both EGSExtract and EvE)
- they does not allow use of my raw data files (too big for sequencing.com)
- and/or does not output files in the format I need for analysis (WGSextract)

At present, these pertain specifically to the following:
- input raw files from test provider (Dante Labs for my current samples)
- use the latest reference files (currently hg38 patch 13 from 2021)
- use the latest dbSNP (build 155)

The major steps of this pipeline from fastq to gvcf ready for analysis:
- prep reference fasta (generate indexes etc.)
- prep reference dbSNP build (CHROM rename, sort then index, etc.)
- align fastq to bam using reference fasta
- haplotyping of bam to produce intermediate vcf
- genotyping of intermediate vcf to produce final vcf (ready for analysis)

My inspiration for attempting this myself was this blog:
https://strahbg.com/?p=3356.  While I am very grateful for the starting point this gave, I found some of the steps needed revisions. A few changes I wanted or needed to make were:
- use newer reference files (both fasta and dbSNP)
- add how to convert latest dnSNP from source to match aligner
- change the aligner to reduce errors in my files (i.e. a drop in read coverage)
- adjust some performance variables (memory and/or threads)
- add/revise duration estimates for the various steps
