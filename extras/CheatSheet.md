# Linux Cheat Sheet

Trim a file

```
java -jar path/to/trimmomatic-0.38.jar PE -threads 2 -phred33 -trimlog <LOGFILE>.txt <FORWARD>.fq <REVERSE>.fq <NEW_FORWARD_P>.fq <NEW_FORWARD_UP>.fq <NEW_REVERSE_P>.fq <NEW_REVERSE_UP>.fq ILLUMINACLIP:<ADAPTORS>.fasta:2:30:10 SLIDINGWINDOW:20:20 MINLEN:120
```

Read the number of sequences (reads) from a file

```
expr $(cat <FILE>.fq | wc -l) / 4
```

Read the number of bases from a file

```
awk 'NR % 4 == 2' <FILE>.fq | tr -d '\r\n' | wc -m
```

Upload file to ncbi using Aspera

```
.aspera/connect/bin/ascp -i ~/sequences/aspera.openssh -QT -l100m -k1 -d ~/myGenome/ subasp@upload.ncbi.nlm.nih.gov:uploads/jba231_uky.edu_<KEY>
```

Create an HTML file to visualize the fq analysis

```
fastqc <FILE1>.fq <FILE2>.fq etc...
```

Scp a file

```
scp <HOSTNAME_FROM>:<PATH_TO_FILE> <HOSTNAME_TO>:<PATH_TO_NEWFILE>
```

Create a new screen with a name

```
screen -S <NEW_NAME>
```

List all active screens

```
screen -ls
```

Attach to screen with name

```
screen -r <NAME>
```

Run velvet using a range of k-mer values

```
velvetoptimiser -s <MIN_K-MER_VALUE> -e <MAX_K-MER_VALUE> -x <K-MER_INCREMENT> -d <NEW_DIRECTORY> -f '-shortPaired -fastq.gz -separate <FORWARD>.fq <REVERSE>.fq' -t 1
```

Build `velveth` roadmaps

```
velveth <NEW_DIRECTORY> <K-MER_VALUE> -shortPaired -fastq -separate <FORWARD>.fq <REVERSE>.fq
```

Assemble via `velvetg`

```
velvetg <VELVETH_DIRECTORY>
```

Run commands from a file

```
source <FILE>
```

Commands that are put in `~/.bash_profile` are automatically run when connectiong via `ssh`
