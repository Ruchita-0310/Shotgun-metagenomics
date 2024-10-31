# Shotgun-metagenomics
## 1. FastQC
[FastQC](https://github.com/s-andrews/FastQC) can be run either on server or your own device. 

## 2. BBduk
For [BBduk](https://jgi.doe.gov/data-and-tools/software-tools/bbtools/bb-tools-user-guide/bbduk-guide/), I have used Force-Trim Modulo, Adapter trimming, Kmer filtering, and Quality trimming apackages.

for force trim (run it in a loop)
```
####### Run your script #########################
module load bbmap/38.84 
# Define an array of sample prefixes (e.g., "Li49151-RS-Diatoms-4C_S1")
samples=("Li49151-RS-Diatoms-4C_S1" "Li49152-RS-PL4-30C_S2" "Li49153-RS-PL4-NH4Cl-RT_S3" "Li49154-RS-GE7-RT_S4" "Li49155-RS-GE2022-RT_S5" "Li50127-RS-DL-1-RT_S16")

# Base directory for input and output files
base_dir="/work/ebg_lab/eb/Ruchita_working/shotgun_data"

# Loop through each sample and run bbduk.sh with the correct file paths
for sample in "${samples[@]}"
do
    bbduk.sh \
        in1="${base_dir}/${sample}_R1_001.fastq.gz" \
        in2="${base_dir}/${sample}_R2_001.fastq.gz" \
        out1="${base_dir}/${sample}_R1_trimmed.fastq.gz" \
        out2="${base_dir}/${sample}_R2_trimmed.fastq.gz"
done
```
for  adapter trimming (run it in a loop)
```
####### Run your script #########################
module load bbmap/38.84

cd /work/ebg_lab/eb/Ruchita_working/shotgun_data
samples=("Li49151-RS-Diatoms-4C_S1" "Li49152-RS-PL4-30C_S2" "Li49153-RS-PL4-NH4Cl-RT_S3" "Li49154-RS-GE7-RT_S4" "Li49155-RS-GE2022-RT_S5" "Li50127-RS-DL-1-RT_S16")

# Loop through each sample and run bbduk.sh with the correct file paths
for sample in "${samples[@]}"
do
    bbduk.sh \
        in1=${sample}_R1_001.fastq.gz \
        in2=${sample}_R2_001.fastq.gz \
        out1=${sample}_clip_R1.fastq.gz \
        out2=${sample}_clip_R2.fastq.gz \
        tbo tpe k=23 mink=11 hdist=1 ktrim=r t=32
done
```
for kmer filter (run it in a loop)
```
####### Run your script #########################
module load bbmap/38.84

cd /work/ebg_lab/eb/Ruchita_working/shotgun_data
# Define an array of sample prefixes (e.g., "Li49151-RS-Diatoms-4C_S1")
samples=("Li49151-RS-Diatoms-4C_S1" "Li49152-RS-PL4-30C_S2" "Li49153-RS-PL4-NH4Cl-RT_S3" "Li49154-RS-GE7-RT_S4" "Li49155-RS-GE2022-RT_S5" "Li50127-RS-DL-1-RT_S16")

# Loop through each sample and run bbduk.sh with the correct file paths
for sample in "${samples[@]}"
do
    bbduk.sh \
        in1=${sample}_clip_R1.fastq.gz \
        in2=${sample}_clip_R2.fastq.gz \
        out1=${sample}_unmatched_R1.fastq.gz \
        out2=${sample}_unmatched_R2.fastq.gz \
        outm1=${sample}_matched_R1.fastq.gz \
        outm2=${sample}_matched_R2.fastq.gz \
        ref=/work/ebg_lab/software/bbmap/v38.84/resources/phix174_ill.ref.fa.gz \
        k=31 hdist=1 t=32
done
```
for Quality trimming (run it in a loop)
```
####### Run your script #########################
module load bbmap/38.84

cd /work/ebg_lab/eb/Ruchita_working/shotgun_data
# Define an array of sample prefixes
samples=("Li49151-RS-Diatoms-4C_S1" "Li49152-RS-PL4-30C_S2" "Li49153-RS-PL4-NH4Cl-RT_S3" "Li49154-RS-GE7-RT_S4" "Li49155-RS-GE2022-RT_S5" "Li50127-RS-DL-1-RT_S16")

# Loop through each sample and run bbduk.sh for both R1 and R2 files
for sample in "${samples[@]}"
do
    bbduk.sh in=${sample}_R1_001.fastq.gz out=${sample}_clean_R1.fastq.gz qtrim=rl trimq=15 minlength=30 t=32
    bbduk.sh in=${sample}_R2_001.fastq.gz out=${sample}_clean_R2.fastq.gz qtrim=rl trimq=15 minlength=30 t=32
done
```
