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
checkm2 predict -t 30 -x fa --input ./ --output-directory ./CheckM2
```
# Gene Prediction
## MetaErg
```
####### Run your script #########################
\time  singularity exec --bind /work/ebg_lab/referenceDatabases/metaerg_db_V214:/databases --bind /work/ebg_lab/eb/Ruchita_working/shotgun_data/megahit_assembly/DL1_assembly/metabat/erg:/data  --writable /work/ebg_lab/software/metaerg-v2.5.2/sandbox_metaerg_2.5.8/ metaerg --database_dir /databases --contig_file /data --file_extension .fa
```

