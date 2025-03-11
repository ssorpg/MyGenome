# MyGenome Project Steps

1. Create a GitHub repository and add a `README.md` file to it

2. [Download the sequence reads](DownloadReads.md) from Dr. Farman's computer

3. [Trim the sequence reads](TrimReads.md), if necessary

4. Log in to the NCBI NIH portal

5. Initiate an entry in the class's online BioProject

6. Download the Aspera Connect software using `wget`

```wget https://d3gcli72yxqn2z.cloudfront.net/downloads/connect/latest/bin/ibm-aspera-connect_4.2.13.820_linux_x86_64.tar.gz```

7. Uncompress the archive

```tar zxvf ibm-aspera-connect_4.2.8.540_linux_x86_64.tar.gz```

8. Install the software

```bash ibm-aspera-connect_4.2.8.540_linux_x86_64.sh```

9. Download the key file to local PC, upload to VM using `scp`

```scp aspera.openssh jba231@jba231.cs.uky.edu:~/sequences/```

10. Submit raw sequence datasets to NCBI Sequence Read Archive (SRA) using `aspera`

```.aspera/connect/bin/ascp -i ~/sequences/aspera.openssh -QT -l100m -k1 -d ~/myGenome/ subasp@upload.ncbi.nlm.nih.gov:uploads/jba231_uky.edu_FhPrmBCS```

11. `ssh` into the MCC VM

```ssh jba231@mcc.uky.edu```

12. If not already done, follow the directions to accept the terms and conditions to use the MCC VM

13. `mkdir` in Dr. Farman's CS 480 group project directory

```mkdir /project/farman_s25abt480/jba231```

14. `scp` the files from the CS VM into `/project/farman_s25abt480/jba231` on the MCC VM

```scp jba231@jba231.cs.uky.edu:~/myGenome/*_p.fq /project/farman_s25abt480/jba231```

15. Rename the `_p` files to `_paired`

```
mv Bm88503_1_p.fq Bm88503_1_paired.fq
mv Bm88503_2_p.fq Bm88503_2_paired.fq
```

16. Copy the velvetoptimiser script to your personal directory

```cp ../SLURM_SCRIPTS/velvetoptimiser_noclean.sh ~```

17. Use nano to add my email address to the mail-user line of the slurm script

```nano velvetoptimiser_noclean.sh```

Then edit the `main-user` line to read as follows `#SBATCH --mail-user farman@uky.edu,jba231@uky.edu`

18. Submit my assemblies to the SLURM queue

```sbatch velvetoptimiser_noclean.sh Bm88503 61 131 10```
