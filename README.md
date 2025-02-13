# Title

1. `ssh` into your CS VM

```ssh jba231@jba231.cs.uky.edu```

2.   `ssh` into Professor Farman's machine to determine where the `Po2` directory is located

```ssh ngs@10.163.183.71```

3. `logout` of the machine

4. `scp` the folder from Professor Farman's machine

```scp -r ngs@10.163.183.71:Desktop/Po2 ./myGenome```

5. Rename the samples to the following formats _sampleName_1.fq.gz_ and _sampleName_2.fq.gz_

```
mv Po2_CKDL240039120-1A_22HTV5LT4_L2_1.fq.gz Bm88503_1.fq.gz
mv Po2_CKDL240039120-1A_22HTV5LT4_L2_2.fq.gz Bm88503_2.fq.gz
```

6. Create HTML files to analyze using `fastqc` for each of the sequence reads

```fastqc Bm88503_1.fq.gz Bm88503_2.fq.gz```

7. `scp` the HTML files to local PC using

```scp -r jba231@jba231.cs.uky.edu:myGenome C:/Users/ssorp/Downloads```

8. View the HTML files to determine what kind of trimming we need to do

9. `cp` trimmomatic-0.38.jar from `~/sequences/` to `~/Po2/`

```cp trimmomatic-0.38.jar ~/myGenome/```

9. Trim the adaptor sequences from 
