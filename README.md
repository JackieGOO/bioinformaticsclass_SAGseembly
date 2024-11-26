# bioinformaticsclass_SAGseembly
Assemble a SAG for ENVS6492
Editting to show the 2024 class version control 

# Outline of workflow
First will normalise reads (needed for WGA cells)
then assemble
then annotate using Prokka! 



# Step one: Prep reads for assembly
input is a tar.gz for the class is a already interleaved file of pair end reads. This file already has had adapters removed from the data. 

BBTOOLS
https://jgi.doe.gov/data-and-tools/software-tools/bbtools/bb-tools-user-guide/usage-guide/

1. First use bbnorm to normalise reads to account for WGA
!Note- do not use bbnorm for long read data like nanopore! see manual 

usage: 
```{}
 bbnorm.sh in=AH-259-A01_pe.fastq.gz out=norm_AH259-A01.fastq target=100 min=2
```
*This will normalise reads to have an average 100x coverage, and minimum 2x coverage. Everything below 2x will be discarded. 

# Assemble genome using Spades

Spades manual: https://cab.spbu.ru/files/release3.12.0/manual.html#sec3.1

```{}
spades.py --sc --pe1-12 norm_AH259-A01.fastq -o ASSEMBLED_AH259-A01 
```

--sc specifies single cell data that has been amplified. --pe-1-12 specifies it is an interleaved paired end read file, we use the normalised reads as our input. -o specificies output folder.


Now go into your folder. Lets take the scaffolds file and annotate it using prokka 


# Annotate using Prokka 
**Note - this is the porkka installation that finally worked for me - I had to uninstall several other packages prior to this fix: https://github.com/tseemann/prokka/issues/615
Manual for Prokka found here: https://github.com/tseemann/prokka

```{}
prokka --outdir ~/Prokka_AH-259-A01 --prefix AH259-A01 ~/ASSEMBLED_AH259-A01/scaffolds.fasta --force
```
prokka calls the tool, outdir specifies the out directory --prefix sets the prefix of file names then locaiton of file ot annotate. --force allows overwriting of existing files ( optional)






