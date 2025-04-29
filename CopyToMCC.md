# Copy Trimmed Sequence Reads to the MCC Supercomputer

Assembling a real world genome takes a lot of computing power. By uploading our sequence reads to the MCC Supercomputer and leveraging the power of parallel processing to optimize our assembly, we can quickly and efficient generate our full genome.

1. `ssh` into the MCC VM

```
ssh jba231@mcc.uky.edu
```

2. If not already done, follow the directions to accept the terms and conditions to use the MCC VM

3. `mkdir` in Dr. Farman's ABT 480 group project directory

```
mkdir /project/farman_s25abt480/jba231
```

4. `scp` the files from the CS VM into `/project/farman_s25abt480/jba231` on the MCC VM

```
scp jba231@jba231.cs.uky.edu:~/myGenome/*_p.fq /project/farman_s25abt480/jba231
```

5. Rename the `_p` files to `_paired`

```
mv Bm88503_1_p.fq Bm88503_1_paired.fq
mv Bm88503_2_p.fq Bm88503_2_paired.fq
```

6. Copy the velvetoptimiser script to your personal project directory

```
cp ../SLURM_SCRIPTS/velvetoptimiser_noclean.sh .
```

7. Use nano to add your email address to the mail-user line of the slurm script

```
nano velvetoptimiser_noclean.sh
```

Then edit the `main-user` line to read as follows `#SBATCH --mail-user farman@uky.edu,jba231@uky.edu`

8. Submit my assemblies to the SLURM queue, first with 10 step-size (40 minutes) and then with 2 (15 minutes)

```
sbatch velvetoptimiser_noclean.sh Bm88503 61 131 10
sbatch velvetoptimiser_noclean.sh Bm88503 89 103 2
```

9. Once the assemblies have been completed, view the optimizer output files to find the genome size, number of contigs, and n50 for both step size 10 and step size 2 optimizations
<ol>
    <ol>
      <li>
          Step size 10
          <ol>
              <li>Genome size: 41,111,799</li>
              <li>Number of contigs: 2,855</li>
              <li>N50: 106,972</li>
          </ol>
      </li>
      <li>
          Step size 2
          <ol>
              <li>Genome size: 40,947,956</li>
              <li>Number of contigs: 2,082</li>
              <li>N50: 108,656</li>
          </ol>
      </li>
    </ol>
</ol> 
