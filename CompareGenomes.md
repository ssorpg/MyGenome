# Compare Class Genomes

Now that our genomes have been assembled, uploaded to NCBI, BLASTed, gene prediction has been run, and the genome has been verified to be valid, we can compare our genome to the otehrs in our class to etermine their similarity.

1. `ssh` into the MCC VM

```
ssh jba231@mcc.uky.edu
```

2. If not already done, [BLAST the genome](BLASTGenome.md)

3. Use head to look at the output file and count the number of columns in the blast output (there must be 7)

```
head ../CLASS_BLASTs/B71v2sh.Bm88503.BLAST
```

5. Copy the `CallVariants.sh` script from `farman_s25abt480/SLURM_SCRIPTS` into your personal directory

```
scp ../SLURM_SCRIPTS/CallVariants.sh .
```

7. Add your email address at the relevant spot

```
nano CallVariants.sh
```

8. Run the script as a SLURM job

```
sbatch CallVariants.sh path/to/MyGenome_BLAST
```

9. 
