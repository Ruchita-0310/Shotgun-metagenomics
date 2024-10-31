# Assembly
## 1. Megahit
[Megathit](https://github.com/voutcn/megahit) is an ultra-fast and memory-efficient NGS assembler
Run it in a loop
```
####### Run your script #########################
cd /work/ebg_lab/eb/Ruchita_working/shotgun_data
module load megahit/1.2.9

# Decompress R1 and R2 files for all samples
gunzip *_clean_R1.fastq.gz
gunzip *_clean_R2.fastq.gz

# List of specific sample names without extensions
samples=("Li49151-RS-Diatoms-4C_S1" "Li49152-RS-PL4-30C_S2" "Li49153-RS-PL4-NH4Cl-RT_S3" "Li49154-RS-GE7-RT_S4" "Li49155-RS-GE2022-RT_S5" "Li50127-RS-DL-1-RT_S16")

# Loop through each sample and run megahit
for SAMPLE in "${samples[@]}"
do
    megahit -1 ${SAMPLE}_clean_R1.fastq -2 ${SAMPLE}_clean_R2.fastq -o ./megahit_assembly/seperate/${SAMPLE}_output -t 32
done
```
