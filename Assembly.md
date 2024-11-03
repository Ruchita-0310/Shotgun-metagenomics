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
## 2. MetaSPAdes
[SPAdes](https://github.com/ablab/spades) is a versatile toolkit designed for assembly and analysis of sequencing data
```
mamba create -n spades
mamba activate spades
mamba install -c bioconda spades
####### Run your script #########################
mamba activate spades
cd /work/ebg_lab/eb/Ruchita_working/shotgun_data
# Define the array with your specific samples
samples=("Li49151-RS-Diatoms-4C" "Li49152-RS-PL4-30C" "Li49153-RS-PL4-NH4Cl-RT" 
         "Li49154-RS-GE7-RT" "Li49155-RS-GE2022-RT" "Li50127-RS-DL-1-RT")

# Define the main output directory
main_output_dir="./metaspades_assembly"

# Loop through each sample and run the spades.py command
for sample in "${samples[@]}"; do
    # Define the input files based on the sample name
    R1="${sample}_R1_001.fastq.gz"
    R2="${sample}_R2_001.fastq.gz"
    output_dir="$main_output_dir/${sample}_separate_unmerged"
    
    # Create the output directory if it doesn't exist
    mkdir -p "$output_dir"
    
    # Run the SPAdes command
    spades.py --meta -1 $R1 -2 $R2 -o $output_dir --threads 32
done
```
## 3. Kmer Coverage
[BBMap](https://jgi.doe.gov/data-and-tools/software-tools/bbtools/bb-tools-user-guide/bbmap-guide/)
```
####### Run your script #########################
module load bbmap/38.84
# Define an array of sample IDs to loop through
samples=("Li49151-RS-Diatoms-4C_S1"
         "Li49152-RS-PL4-30C_S2"
         "Li49153-RS-PL4-NH4Cl-RT_S3"
         "Li49154-RS-GE7-RT_S4"
         "Li49155-RS-GE2022-RT_S5"
         "Li50127-RS-DL-1-RT_S16")

# Loop through each sample
for sample in "${samples[@]}"; do
    kmercoverage.sh in=${sample}_R1_001.fastq.gz in2=${sample}_R2_001.fastq.gz \
    out=${sample}_kmer.fastq hist=${sample}_hist.txt
done

```
