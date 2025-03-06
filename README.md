# MyGenome Project Steps

1. Create a GitHub repository and add a `README.md` file to it

2. `ssh` into the CS VM

```ssh jba231@jba231.cs.uky.edu```

3. `scp` the folder from Dr. Farman's machine

```scp -r ngs@10.163.183.71:Desktop/Po2 ./myGenome```

4. Rename the samples to the following formats _sampleName_1.fq.gz_ and _sampleName_2.fq.gz_

```
mv Po2_CKDL240039120-1A_22HTV5LT4_L2_1.fq.gz Bm88503_1.fq.gz
mv Po2_CKDL240039120-1A_22HTV5LT4_L2_2.fq.gz Bm88503_2.fq.gz
```

5. Count the sequence reads in the forward and reverse directions

```
expr $(cat Bm88503_1.fq | wc -l) / 4
expr $(cat Bm88503_2.fq | wc -l) / 4
```

6. Create HTML files to analyze using `fastqc` for each of the sequence reads

```fastqc Bm88503_1.fq.gz Bm88503_2.fq.gz```

7. `scp` the HTML files to local PC using

```scp -r jba231@jba231.cs.uky.edu:myGenome/*.html C:/Users/ssorp/Downloads```

8. View the HTML files to determine what kind of trimming to do

9. Set up a screen job to trim adaptor and low-quality reads from `Bm88503_1.fq.gz` and `Bm88503_2.fq.gz` using `trimmomatic-0.38.jar`

```screen java -jar ~/sequences/trimmomatic-0.38.jar PE -threads 2 -phred33 -trimlog Bm88503_errorLog.txt Bm88503_1.fq.gz Bm88503_2.fq.gz Bm88503_1_p.fq Bm88503_1_up.fq Bm88503_2_p.fq Bm88503_2_up.fq ILLUMINACLIP:../adaptors.fasta:2:30:10 SLIDINGWINDOW:20:20 MINLEN:120```

10. Create HTML files to analyze using `fastqc` for each of the sequence reads

```fastqc Bm88503_1_p.fq Bm88503_1_up.fq Bm88503_2_p.fq Bm88503_2_up.fq```

11. `scp` the HTML files to local PC using

```scp -r jba231@jba231.cs.uky.edu:myGenome/*.html C:/Users/ssorp/Downloads```

12. View the HTML files to determine if there is any more trimming to do. If there is, go back to step 7 and modify the `trimmomatic` command

13. Log in to the NCBI NIH portal

14. Initiate an entry in the class's online BioProject

15. Download the Aspera Connect software using `wget`

```wget https://d3gcli72yxqn2z.cloudfront.net/downloads/connect/latest/bin/ibm-aspera-connect_4.2.13.820_linux_x86_64.tar.gz```

16. Uncompress the archive

```tar zxvf ibm-aspera-connect_4.2.8.540_linux_x86_64.tar.gz```

17. Install the software

```bash ibm-aspera-connect_4.2.8.540_linux_x86_64.sh```

18. Download the key file to local PC, upload to VM using `scp`

```scp aspera.openssh jba231@jba231.cs.uky.edu:~/sequences/```

19. Submit raw sequence datasets to NCBI Sequence Read Archive (SRA) using `aspera`

```.aspera/connect/bin/ascp -i ~/sequences/aspera.openssh -QT -l100m -k1 -d ~/myGenome/ subasp@upload.ncbi.nlm.nih.gov:uploads/jba231_uky.edu_FhPrmBCS```

20. `ssh` into the MCC VM

```ssh jba231@mcc.uky.edu```

21. If not already done, follow the directions to accept the terms and conditions to use the MCC VM

22. `mkdir` in Dr. Farman's CS 480 group project directory

```mkdir /project/farman_s25abt480/jba231```

23. `scp` the files from the CS VM into `/project/farman_s25abt480/jba231` on the MCC VM

```scp jba231@jba231.cs.uky.edu:~/myGenome/*_p.fq /project/farman_s25abt480/jba231```

24. Rename the `_p` files to `_paired`

```
mv Bm88503_1_p.fq Bm88503_1_paired.fq
mv Bm88503_2_p.fq Bm88503_2_paired.fq
```

25. Copy the velvetoptimiser script to your personal directory

```cp ../SLURM_SCRIPTS/velvetoptimiser_noclean.sh ~```

26. Use nano to add my email address to the mail-user line of the slurm script

```nano velvetoptimiser_noclean.sh```

Then edit the `main-user` line to read as follows `#SBATCH --mail-user farman@uky.edu,jba231@uky.edu`

27. Submit my assemblies to the SLURM queue

```sbatch velvetoptimiser_noclean.sh Bm88503 61 131 10```
