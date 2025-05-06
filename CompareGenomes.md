# Compare Class Genomes

Now that our genomes have been assembled, uploaded to NCBI, BLASTed, gene prediction has been run, and the genome has been verified to be valid, we can compare our genome to the others in our class to determine their similarity.

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
cp ../SLURM_SCRIPTS/CallVariants.sh .
```

7. Add your email address at the relevant spot

```
nano CallVariants.sh
```

8. Run the script as a SLURM job  
   a. Results will be written to a directory named Bm88503_SNPs  
   b. A summary of the total number of variants (SNPs) identified will be in the SNP_counts_out_Bm88503 file

```
sbatch CallVariants.sh Bm88503_BLAST
```

9. Copy the B71v2sh_v_Bm88503_out file into the CLASS_SNPS directory (/project/farman_s25abt480/CLASS_SNPs)

```
cp Bm88503_SNPs/B71v2sh_v_Bm88503_out  ../CLASS_SNPs
```

10. We are now ready to compare all of our genomes against one another
