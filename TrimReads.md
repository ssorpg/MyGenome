# Trimming Sequence Reads

1. ssh into the CS VM

```ssh jba231@jba231.cs.uky.edu```

2. Create HTML files to analyze using `fastqc` for each of the sequence reads

```fastqc Bm88503_1.fq.gz Bm88503_2.fq.gz```

3. `scp` the HTML files to local PC using

```scp -r jba231@jba231.cs.uky.edu:myGenome/*.html C:/Users/ssorp/Downloads```

4. View the HTML files to determine what kind of trimming to do

<h6>Pre-trim Sequence Quality Plot for Bm88503</h6>

![Pre_SequenceQuality.png](/images/Pre_SequenceQuality.png)

<h6>Pre-trim Adaptor Contamination for Bm88503</h6>

![Pre_Contamination.png](/images/Pre_Contamination.png)

6. Set up a screen job to trim adaptor and low-quality reads from `Bm88503_1.fq.gz` and `Bm88503_2.fq.gz` using `trimmomatic-0.38.jar`

```screen java -jar ~/sequences/trimmomatic-0.38.jar PE -threads 2 -phred33 -trimlog Bm88503_errorLog.txt Bm88503_1.fq.gz Bm88503_2.fq.gz Bm88503_1_p.fq Bm88503_1_up.fq Bm88503_2_p.fq Bm88503_2_up.fq ILLUMINACLIP:../adaptors.fasta:2:30:10 SLIDINGWINDOW:20:20 MINLEN:120```

6. Create HTML files to analyze using `fastqc` for each of the sequence reads

```fastqc Bm88503_1_p.fq Bm88503_1_up.fq Bm88503_2_p.fq Bm88503_2_up.fq```

7. `scp` the HTML files to local PC using

```scp -r jba231@jba231.cs.uky.edu:myGenome/*.html C:/Users/ssorp/Downloads```

7. View the HTML files to determine if there is any more trimming to do. If there is, go back to step 7 and modify the `trimmomatic` command

<h6>Post-trim Sequence Quality Plot for Bm88503</h6>

![Post_SequenceQuality.png](/images/Post_SequenceQuality.png)

<h6>Post-trim Adaptor Contamination for Bm88503</h6>

![Post_Contamination.png](/images/Post_Contamination.png)
