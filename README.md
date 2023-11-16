# bioinformaticsclass_SAGseembly
Assemble a SAG for ENVS6492


# Outline of workflow
First will normalise reads (needed for WGA cells)
then assemble
then annotate using Prokka! 



# Step one. PREP READS FOR ASSEMBLY
input is a tar.gz for the class is a already interleaved file of pair end reads. This file already has had adapters removed from the data. 

# FROM BBTOOLS: 
https://jgi.doe.gov/data-and-tools/software-tools/bbtools/bb-tools-user-guide/usage-guide/

First use bbnorm to normalise reads to account for WGA
!Note- do not use bbnorm for long read data like nanopore! see manual 

usage: 
```{}
 bbnorm.sh in=AH-259-A01_pe.fastq.gz out=norm_AH259-A01.fastq target=100 min=2
```
*This will normalise reads to have an average 100x coverage, and minimum 2x coverage. Everything below 2x will be discarded. 

# ASSEMBLE GENOME USING SPADES




