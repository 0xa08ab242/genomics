# genomics
This repo is a place to keep some notes related to my personal efforts in getting more and better data from some whole genome sequence raw data files.  While more readily available tools (e.g. WGSExtract) and services (e.g. sequencing.com's EvE app) provide options for some analysis, these are insufficient for my purposes because:
- they do not utilize the latest reference files (both EGSExtract and EvE)
- they do not allow use of my raw data files (too big for sequencing.com)
- and/or do not output files in the format I need for analysis (WGSExtract)

At present, the steps hold to the following constraints:
- input raw files from test provider (Dante Labs for my current samples)
- use the latest reference human genome version and patch
- use the latest dbSNP build

The major steps of this pipeline from fastq to gvcf ready for analysis:
- prep reference fasta (generate indexes etc.)
- prep reference dbSNP build (CHROM rename, sort then index, etc.)
- align fastq to bam using reference fasta
- haplotyping of bam to produce intermediate vcf
- genotyping of intermediate vcf to produce final vcf (ready for analysis)

I had looked at doing raw conversions previously to lift-n-shift my old hg19 WGS results to hg38 to extract the y-dna for genealogy purposes.  However, I found a few readily available tools that could handle this, so I paused my DIY efforts.  I only picked the idea back up when someone close to me wanted the most current data possible for medical purposes, so I agreed to try to get them their dnSNP (and specifically the ClinVar) data from their WGS raw data before their next appointment with their physician.  For the approach, my inspiration was this blog post:
https://strahbg.com/?p=3356.
For the preliminary iterations of the pipeline, I used my own data.  I have multiple references using different reference fasta and dnSNP builds, and this gave me some basic quality control checks of the results.  These checks and some changes in the versions and availability of the reference files and tools led to changes in the steps.  While I am very grateful for the starting point this gave, here are a few changes I wanted or needed to make:
- use newer dbSNP for latest results
- add process to convert latest dnSNP from source to match reference fasta (to not have to restart that iteration)
- change the aligner to reduce errors in my files (i.e. a drop in read coverage)
- use different reference fasta (to remove the need for the dnSNP convert and sort to make it match the old fasta)
- adjust some performance variables (memory and/or threads)
- add/revise duration estimates for the various steps

Additional helpful URLs (aside from the manpages and reference documents for the tools used) included:
https://biology.stackexchange.com/questions/59493/how-to-convert-bwa-mem-output-to-bam-format-without-saving-sam-file
https://github.com/bwa-mem2/bwa-mem2
https://www.beholdgenealogy.com/blog/?p=3209
https://www.htslib.org/workflow/#mapping_to_variant
https://www.snpedia.com/index.php/VCF
