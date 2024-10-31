# Shotgun-metagenomics
## 1. FastQC
[FastQC](https://github.com/s-andrews/FastQC) can be run either on server or your own device. 

## BBduk
For [BBduk](https://jgi.doe.gov/data-and-tools/software-tools/bbtools/bb-tools-user-guide/bbduk-guide/), I have used Force-Trim Modulo, Adapter trimming, and Kmer filtering packages.

```
for force trim (run it in a loop)
#!/bin/bash
####### Reserve computing resources #############
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8
#SBATCH --time=24:00:00
#SBATCH --mem=200G
#SBATCH --partition=bigmem
####### Run your script #########################
module load bbmap/38.84 
bbduk.sh in1=/path/to/read1/fastq.gz in2=/path/to/read2/fastq.gz out1=/path/to/trimmed.fastq.gz out2=/path/to/trimmed.fastq.gz

```
