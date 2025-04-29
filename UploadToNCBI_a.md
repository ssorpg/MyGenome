# Upload Assembly to the NCBI NIH Portal

Our genome has been assembled so we now need to upload it to NCBI. We've uploaded our raw reads to NCBI using Aspera, but this time we can upload them manually by uploading the file directly using the NCBI upload UI.

1. Download the assembled genome from the MCC using `scp`

```
scp jba@mcc.uky.edu:/project/farman_s25abt480/jba231/Bm88503_final.fasta ./Bm88503.fasta
```

2. Log in to the NCBI NIH portal

3. Initiate an entry in the class's online BioProject

4. Complete the entry following [Dr. Farman's instructions](data/FarmanNCBI.png)

5. If the submission is returned with NCBI having detected adaptor contamination, clean the reads and resubmit  
    a. NCBI will return a version of the genome where it has removed any adaptor contamination it found at the start and end of each contig  
    b. Therefore, only the contamination found in the middle of each genome will need to be removed  
    c. It can be removed by splitting the contig at the location of the contamination and removing the offending reads
