# Finalize the Genome and Check its Completeness

Before we can begin BLASTing the genome to allow it to be checked against the genomes of other classmates, we need to polish the final version of our genome to standardize headers and remove short contigs before running BUSCO to get a quantitative assessment of our genome's completeness

1. `ssh` into the MCC VM

```ssh jba231@mcc.uky.edu```

2. Access your working directory in Dr. Farman's ABT 480 group project

```cd /project/farman_s25abt480/jba231```

3. Copy the SimpleFastaHeaders.pl perl script from /project/farman_s25abt480/SCRIPTs into your working directory

```cp ../SCRIPTs/SimpleFastaHeaders.pl .```

4. Use the script to rename the sequence headers to a standard format

```perl SimpleFastaHeaders.pl Bm88503.fasta Bm88503```

5. Copy the CullShortContigs.pl perl script from /project/farman_s25abt480/SCRIPTs into your working directory

```cp ../SCRIPTs/CullShortContigs.pl .```

6. Use the script to cull short contigs from the renamed genome assembly file

```perl CullShortContigs.pl Bm88503_nh.fasta```

7. Copy the SeqLen.pl perl script from /project/farman_s25abt480/SCRIPTs into your working directory

```cp ../SCRIPTs/SeqLen.pl .```

8. Enter the genome metrics into the class worksheet

9. Use the script to determine the final genome size after culling

```perl SeqLen.pl Bm88503_final.fasta```

10. Copy the BuscoSingularity.sh script into your working directory

```cp ../SLURM_SCRIPTS/BuscoSingularity.sh .```

11. Edit the BuscoSingularity.sh script to include your email address

12. Run BUSCO (2 hours)

```sbatch BuscoSingularity.sh Bm88503_final.fasta```
