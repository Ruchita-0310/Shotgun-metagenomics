# Binning from Megahit assembly
## MetaBAT2
```
####### Run your script #########################
module load miniconda3/metabat2  
metabat2 -i final.contigs.fa.gz -o ./metabat_bins 
```
# Classification
## GTDB-Tk 
```
####### Run your script #########################
conda activate gtdbtk-2.3.2
gtdbtk classify_wf --genome_dir ./ --out_dir gtdb_class --skip_ani_screen --extension fa
```
# Completeness of bins
## CheckM2
```
####### Run your script #########################
conda activate checkm2
checkm2 predict -t 30 -x fa --input ./ --output-directory ./CheckM2
```
# Gene Annotation
## MetaErg
```
####### Run your script #########################
\time  singularity exec --bind /path/to/reference/database/metaerg_db_V214:/databases --bind /path/to/your/bins:/data  --writable sandbox_metaerg_2.5.8/ metaerg --database_dir /databases --contig_file /data --file_extension .fa
```
# FastANI
```
Download GCA_007692715.1 from NCBI - this is the reference genome
Query genome is Nodosilinea bin with 100% completeness
module load  miniconda3/fastani
fastANI -q metabat_bins.15.fa -r GCA_007692715.1_ASM769271v1_genomic.fna -o output.txt
```
Ouput file: ANI estimate between metabat_bins.15.fa and GCA_007692715.1_ASM769271v1_genomic.fna is 98.5423. Out of the total 2371 sequence fragments from metabat_bins.15.fa, 1132 were aligned as orthologous matches
