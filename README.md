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

6. Count the sequence reads in the forward and reverse directions

```expr $(cat Bm88503_1.fq | wc -l) / 4```

7. Create HTML files to analyze using `fastqc` for each of the sequence reads

```fastqc Bm88503_1.fq.gz Bm88503_2.fq.gz```

8. `scp` the HTML files to local PC using

```scp -r jba231@jba231.cs.uky.edu:myGenome/*.html C:/Users/ssorp/Downloads```

9. View the HTML files to determine what kind of trimming to do

10. Set up a screen job to trim adaptor and low-quality reads from `Bm88503_1.fq.gz` and `Bm88503_2.fq.gz` using `trimmomatic-0.38.jar`

```screen java -jar ~/sequences/trimmomatic-0.38.jar PE -threads 2 -phred33 -trimlog Bm88503_errorLog.txt Bm88503_1.fq.gz Bm88503_2.fq.gz Bm88503_1_p.fq Bm88503_1_up.fq Bm88503_2_p.fq Bm88503_2_up.fq ILLUMINACLIP:../adaptors.fasta:2:30:10 SLIDINGWINDOW:20:20 MINLEN:120```

11. Create HTML files to analyze using `fastqc` for each of the sequence reads

```fastqc Bm88503_1_p.fq Bm88503_1_up.fq Bm88503_2_p.fq Bm88503_2_up.fq```

12. `scp` the HTML files to local PC using

```scp -r jba231@jba231.cs.uky.edu:myGenome/*.html C:/Users/ssorp/Downloads```

13. View the HTML files to determine if there is any more trimming to do. If there is, go back to step 7 and modify the `trimmomatic` command

14. Log in to the NCBI NIH portal

15. Initiate an entry in the class's online BioProject

16. Download the Aspera Connect software using `wget`

```wget https://d3gcli72yxqn2z.cloudfront.net/downloads/connect/latest/bin/ibm-aspera-connect_4.2.13.820_linux_x86_64.tar.gz```

17. Uncompress the archive

```tar zxvf ibm-aspera-connect_4.2.8.540_linux_x86_64.tar.gz```

18. Install the software

```bash ibm-aspera-connect_4.2.8.540_linux_x86_64.sh```

19. Download the key file to local PC, upload to VM using `scp`

```scp aspera.openssh jba231@jba231.cs.uky.edu:~/sequences/```

20. Submit raw sequence datasets to NCBI Sequence Read Archive (SRA) using `aspera`

```.aspera/connect/bin/ascp -i ~/sequences/aspera.openssh -QT -l100m -k1 -d ~/myGenome/ subasp@upload.ncbi.nlm.nih.gov:uploads/jba231_uky.edu_FhPrmBCS```

21. `ssh` into the MCC VM

```ssh jba231@mcc.uky.edu```

22. If not already done, follow the directions to accept the terms and conditions to use the MCC VM

23. `mkdir` in Dr. Farman's CS 480 group project directory

```mkdir /project/farman_s25abt480/jba231```

24. `scp` the files from the CS VM into `/project/farman_s25abt480/jba231` on the MCC VM

```scp jba231@jba231.cs.uky.edu:~/myGenome/*_p.fq /project/farman_s25abt480/jba231```
