# Title

1. `ssh` into Professor Farman's machine to determine where the `Po2` directory is located

```ssh ngs@10.163.183.71```

2. `scp` the folder from Professor Farman's machine

```scp -r ngs@10.163.183.71:Desktop/Po2 ./Po2```

3. Create HTML files to analyze using `fastqc` for each of the sequence reads

```fastqc Po2_CKDL240039120-1A_22HTV5LT4_L2_1.fq.gz Po2_CKDL240039120-1A_22HTV5LT4_L2_2.fq.gz```

4. `scp` the HTML files to local PC using

```scp -r jba231@jba231.cs.uky.edu:Po2 C:/Users/ssorp/Downloads```

5. View the HTML files to determine what kind of trimming we need to do

6. `cp` trimmomatic-0.38.jar from `~/sequences/` to `~/Po2/`

```cp trimmomatic-0.38.jar ~/Po2/```

8. Trim the adaptor sequences from 
