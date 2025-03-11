# MyGenome Project Steps

1. Create a GitHub repository and add a `README.md` file to it

2. [Download the sequence reads](DownloadReads.md) from Dr. Farman's computer

3. [Trim the sequence reads](TrimReads.md), if necessary

4. [Upload the Sequence Reads to the NCBI NIH Portal](UploadToNCBI.md)

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
