# Prepare and Execute a Gene Prediction and Annotation Workflow

!description here!

1. ssh into the CS VM

```
ssh jba231@jba231.cs.uky.edu
```

2. Create a new screen to run our gene predictions

```
screen -S genes bash -l
```

3. Change to the `maker` directory under `~/genes`

```
cd ~/genes/maker
```

4. Create the MAKER configuration files

```
maker -CTL
```

5. Open `maker_opts.ctl` with a text editor and edit it as follows

```
genome=/home/jba231/genes/snap/Bm88503_final.fasta
model_org=
repeat_protein=
snaphmm=/home/jba231/genes/snap/Moryzae.hmm
augustus_species=magnaporthe_grisea
keep_preds=1
protein=/home/jba231/genes/maker/genbank/ncbi-protein-Magnaporthe_organism.fasta
```

6. Run MAKER (9 hours)

```
maker 2>&1 | tee maker.log
```

7. Confirm that MAKER ran successfully by checking the log file

```
cat Bm88503_final.maker.output/Bm88503_final_master_datastore_index.log
```

8. Merge everything together into one GFF file

```
gff3_merge -d Bm88503_final.maker.output/Bm88503_final_master_datastore_index.log -o Bm88503-annotations.gff
```
