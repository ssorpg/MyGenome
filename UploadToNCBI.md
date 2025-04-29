# Upload Reads to the NCBI NIH Portal

After trimming the sequence reads, we need to create a BioSample in the class BioProject, and link the SRA to it with uploaded sequence reads so that the reads are organized and automatically published at a specified date.

1. Log in to the NCBI NIH portal

2. Initiate an entry in the class's online BioProject

3. ssh into the CS VM

```
ssh jba231@jba231.cs.uky.edu
```

4. Download the Aspera Connect software using `wget`

```
wget https://d3gcli72yxqn2z.cloudfront.net/downloads/connect/latest/bin/ibm-aspera-connect_4.2.13.820_linux_x86_64.tar.gz
```

5. Uncompress the archive

```
tar zxvf ibm-aspera-connect_4.2.8.540_linux_x86_64.tar.gz
```

6. Install the software

```
bash ibm-aspera-connect_4.2.8.540_linux_x86_64.sh
```

7. Download the key file to local PC, then upload to VM using `scp`

```
scp aspera.openssh jba231@jba231.cs.uky.edu:~/sequences/
```

8. Submit raw sequence datasets to NCBI Sequence Read Archive (SRA) using `aspera`

```
.aspera/connect/bin/ascp -i ~/sequences/aspera.openssh -QT -l100m -k1 -d ~/myGenome/ subasp@upload.ncbi.nlm.nih.gov:uploads/jba231_uky.edu_FhPrmBCS
```

9. Record your SRA accession number
    a. SRR32334450
