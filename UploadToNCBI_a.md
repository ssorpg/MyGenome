# Upload Assembly to the NCBI NIH Portal

After trimming the sequence reads, we need to create a BioSample in the class BioProject, and link the SRA to it with uploaded sequence reads so that the reads are organized and automatically published at a specified date.

1. Download the assembled genome from the MCC using `scp`

```
scp jba@mcc.uky.edu:/project/farman_s25abt480/jba231/Bm88503_final.fasta ./Bm88503.fasta
```

2. Log in to the NCBI NIH portal

3. Initiate an entry in the class's online BioProject

4. Complete the entry following [Dr. Farman's instructions](images/FarmanNCBI.png)
