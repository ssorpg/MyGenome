# BLAST Your Genome

1. `ssh` into the MCC VM

```ssh jba231@mcc.uky.edu```

2. Access your working directory in Dr. Farman's ABT 480 group project

```cd /project/farman_s25abt480/jba231```

3. Copy the final `.fasta` file into your CS VM `blast` directory

```scp Bm88503_final.fasta jba231@jba231.cs.uky.edu:~/blast/```

4. Log into your CS VM

```ssh jba231@jba231.cs.uky.edu```

5. Copy the `MoMitochondrion.fasta` file from Dr. Farman's machine to your `blast` directory

```scp ngs@10.163.183.71:Desktop/MoMitochondrion.fasta```

6. BLAST the `MoMitochondrion.fasta` sequence against your final genome assembly using output format 6 with specific column selections

```blastn -query MoMitochondrion.fasta -subject Bm88503_final.fasta -evalue 1e-50 -max_target_seqs 20000 -outfmt '6 qseqid sseqid slen length qstart qend sstart send btop' > B71v2sh.Bm88503.BLAST```

7. Export a list of contigs that mostly comprise mitochondrial sequences

```awk '$3/$4 > 0.9 {print $2 ",mitochondrion"}' B71v2sh.Bm88503.BLAST > Bm88503_mitochondrion.csv```

8. `ssh` into the MCC VM

```ssh jba231@mcc.uky.edu```

9. `cd` into your personal project directory

```cd /project/farman_s25abt480/jba231```

10. Copy the `B71v2sh_masked.fasta` genome from the `/project/farman_s25abt480/FASTA` directory into your personal project directory

```cp ../FASTA/B71v2sh_masked.fasta .```

11. BLAST your genome assembly against a repeat-masked version of the B71 reference genome

```singularity <???> blastn -query B71v2sh_masked.fasta -subject Bm88503_final.fasta -evalue 1e-50 -max_target_seqs 20000 -outfmt '6 qseqid sseqid qstart qend sstart send btop' -out B71v2sh.Bm88503.BLAST```
