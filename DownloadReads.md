# Download Reads of Genome from Dr. Farman's Computer

To download the raw sequence reads, we need to log in to our VM, copy the reads from Dr. Farman's computer, and rename the files for easier identification.

1. ssh into the CS VM

```ssh jba231@jba231.cs.uky.edu```

2. scp the folder from Dr. Farman's machine

```scp -r ngs@10.163.183.71:Desktop/Po2 ./myGenome```

3. Rename the samples to the following formats sampleName_1.fq.gz and sampleName_2.fq.gz

```
mv Po2_CKDL240039120-1A_22HTV5LT4_L2_1.fq.gz Bm88503_1.fq.gz
mv Po2_CKDL240039120-1A_22HTV5LT4_L2_2.fq.gz Bm88503_2.fq.gz
```

4. Count the sequence reads in the forward and reverse directions

```
expr $(cat Bm88503_1.fq | wc -l) / 4
expr $(cat Bm88503_2.fq | wc -l) / 4
```
