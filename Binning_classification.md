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

