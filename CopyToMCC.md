# Copy Trimmed Sequence Reads to the MCC Supercomputer

1. `ssh` into the MCC VM

```ssh jba231@mcc.uky.edu```

2. If not already done, follow the directions to accept the terms and conditions to use the MCC VM

3. `mkdir` in Dr. Farman's CS 480 group project directory

```mkdir /project/farman_s25abt480/jba231```

4. `scp` the files from the CS VM into `/project/farman_s25abt480/jba231` on the MCC VM

```scp jba231@jba231.cs.uky.edu:~/myGenome/*_p.fq /project/farman_s25abt480/jba231```

5. Rename the `_p` files to `_paired`

```
mv Bm88503_1_p.fq Bm88503_1_paired.fq
mv Bm88503_2_p.fq Bm88503_2_paired.fq
```

6. Copy the velvetoptimiser script to your personal project directory

```cp ../SLURM_SCRIPTS/velvetoptimiser_noclean.sh .```

7. Use nano to add my email address to the mail-user line of the slurm script

```nano velvetoptimiser_noclean.sh```

Then edit the `main-user` line to read as follows `#SBATCH --mail-user farman@uky.edu,jba231@uky.edu`

8. Submit my assemblies to the SLURM queue, first with 10 step-size and then with 2

```
sbatch velvetoptimiser_noclean.sh Bm88503 61 131 10
sbatch velvetoptimiser_noclean.sh Bm88503 61 131 2
```
