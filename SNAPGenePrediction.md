# Gene Prediction on MyGenome With SNAP

1. `ssh` into the MCC VM

```
ssh jba231@mcc.uky.edu
```

2. Access your working directory in Dr. Farman's ABT 480 group project

```
cd /project/farman_s25abt480/jba231
```

3. Create a new screen to run our gene predictions

```
screen -S genes bash -l
```

4. Change to the `snap` directory under `~/genes`

```
cd ~/genes/snap
```

5. Download the B71ref2.fasta genome and B71Ref2_a0.3.gff3 annotation file from the Farman Mac Desktop to the current directory

```
scp ngs@10.163.183.71:Desktop/B71ref2* .
```

6. Append the genome fasta sequence to the end of the gff3

```
echo '##FASTA' | cat B71Ref2_a0.3.gff3 - B71Ref2.fasta > B71Ref2.gff3
```

7. Convert the MAKER annotations to ZFF for SNAP

```
maker2zff B71Ref2.gff3
```

8. Extract the genome regions containing unique genes using the `-categorize` subcommand

```
fathom genome.ann genome.dna -categorize 1000
```

9. Use the `-export` subcommand to extract the genome, transcript, and protein sequences from these genes

```
fathom uni.ann uni.dna -export 1000 -plus
```

10. Train the HMM using the Forge tool

```
forge export.ann export.dna
```

11. Condense everything into a single file for use with runs of SNAP

```
hmm-assembler.pl Moryzae . > Moryzae.hmm
```

12. Run SNAP

```
snap-hmm Moryzae.hmm Bm88503_final.fasta > Bm88503-snap.zff
```

13. It is also possible to generate a GFF file in the older GFF2 format

```
snap-hmm Moryzae.hmm Bm88503_final.fasta -gff > Bm88503-snap.gff2
```
