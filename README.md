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

5. Create HTML files to analyze using `fastqc` for each of the sequence reads

```fastqc Bm88503_1.fq.gz Bm88503_2.fq.gz```

6. `scp` the HTML files to local PC using

```scp -r jba231@jba231.cs.uky.edu:myGenome/*.html C:/Users/ssorp/Downloads```

7. View the HTML files to determine what kind of trimming to do

8. Set up a screen job to trim adaptor and low-quality reads from `Bm88503_1.fq.gz` and `Bm88503_2.fq.gz` using `trimmomatic-0.38.jar`

```screen java -jar ~/sequences/trimmomatic-0.38.jar PE -threads 2 -phred33 -trimlog Bm88503_errorLog.txt Bm88503_1.fq.gz Bm88503_2.fq.gz Bm88503_1_p.fq Bm88503_1_up.fq Bm88503_2_p.fq Bm88503_2_up.fq ILLUMINACLIP:../adaptors.fasta:2:30:10 SLIDINGWINDOW:20:20 MINLEN:120```

9. Create HTML files to analyze using `fastqc` for each of the sequence reads

```fastqc Bm88503_1_p.fq Bm88503_1_up.fq Bm88503_2_p.fq Bm88503_2_up.fq```

10. `scp` the HTML files to local PC using

```scp -r jba231@jba231.cs.uky.edu:myGenome/*.html C:/Users/ssorp/Downloads```

11. View the HTML files to determine if there is any more trimming to do. If there is, go back to step 7 and modify the `trimmomatic` command

12. `ssh` into the MCC VM

```ssh jba231@mcc.uky.edu```

13. If not already done, follow the directions to accept the terms and conditions to use the MCC VM

14. `mkdir` in Dr. Farman's CS 480 group project directory

```mkdir /project/farman_s25abt480/jba231```

15. `scp` the files from the CS VM into `/project/farman_s25abt480/jba231` on the MCC VM

```scp jba231@jba231.cs.uky.edu:~/myGenome/*_p.fq /project/farman_s25abt480/jba231```

16. Log in to the NCBI NIH portal

17. Initiate an entry in the class's online BioProject

18. Submit raw sequence datasets to NCBI Sequence Read Archive (SRA)
