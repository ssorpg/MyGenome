# BLAST Your Genome

After BUSCO has run, we can now BLAST our genome against a repeat-masked version of the B71 reference genome. This will allow us to compare genomes across classmates, and to confirm that our genome fits within the 40kb (mb?) length requirement on NCBI.

1. `ssh` into the MCC VM

```
ssh jba231@mcc.uky.edu
```

2. Access your working directory in Dr. Farman's ABT 480 group project

```
cd /project/farman_s25abt480/jba231
```

3. Copy the final `.fasta` file into your CS VM `blast` directory

```
scp Bm88503_final.fasta jba231@jba231.cs.uky.edu:~/blast/
```

4. Log into your CS VM

```
ssh jba231@jba231.cs.uky.edu
```

5. Copy the `MoMitochondrion.fasta` file from Dr. Farman's machine to your `blast` directory

```
scp ngs@10.163.183.71:Desktop/MoMitochondrion.fasta
```

6. BLAST the `MoMitochondrion.fasta` sequence against your final genome assembly using output format 6 with specific column selections

```
blastn -query MoMitochondrion.fasta -subject Bm88503_final.fasta -evalue 1e-50 -max_target_seqs 20000 -outfmt '6 qseqid sseqid slen length qstart qend sstart send btop' > B71v2sh.Bm88503.BLAST
```

7. Export a list of contigs that mostly comprise mitochondrial sequences

```
awk '$3/$4 > 0.9 {print $2 ",mitochondrion"}' B71v2sh.Bm88503.BLAST > Bm88503_mitochondrion.csv
```

8. `ssh` into the MCC VM

```
ssh jba231@mcc.uky.edu
```

9. `cd` into your personal project directory

```
cd /project/farman_s25abt480/jba231
```

10. Copy the `B71v2sh_masked.fasta` genome from the `/project/farman_s25abt480/FASTA` directory into your personal project directory

```
cp ../FASTA/B71v2sh_masked.fasta .
```

11. BLAST your genome assembly against a repeat-masked version of the B71 reference genome

```
singularity run --app blast2120 /share/singularity/data/ccs/conda/amd-conda1-centos8.sinf blastn -query B71v2sh_masked.fasta -subject Bm88503_final.fasta -evalue 1e-50 -max_target_seqs 20000 -outfmt '6 qseqid sseqid qstart qend sstart send btop' -out B71v2sh.Bm88503.BLAST
```

12. Create a new folder `MyGenome_BLAST` and copy the BLAST results into it

```
mkdir MyGenome_BLAST
cp B71v2sh.Bm88503.BLAST MyGenome_BLAST/
```

12. Copy the BLAST results into the `CLASS_BLASTS` folder

```
cp B71v2sh.Bm88503.BLAST ../CLASS_BLASTs/
```

13. BLAST your genome assembly against `MoMitochondrion.fasta`

```
singularity run --app blast2120 /share/singularity/data/ccs/conda/amd-conda1-centos8.sinf blastn -query MoMitochondrion.fasta -subject Bm88503_final.fasta -evalue 1e-50 -max_target_seqs 20000 -outfmt '6 qseqid sseqid qstart qend sstart send btop' -out MoMitochondrion.Bm88503.BLAST
```

14. Record the total length of the contigs that match the mitochondrial sequences  
    a. The following command outputs 40,118, or ~40kb

```
awk '{len = ($6 > $5) ? $6 - $5 + 1 : $5 - $6 + 1; sum += len} END {print sum}' MoMitochondrion.Bm88503.BLAST
```
