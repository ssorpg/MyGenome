# LAB3

1. Problem: Not many reads available for assembly                                  Solution: Use the unpaired reads to supplement
2. Problem: Per base sequence content is bad near the end of the fastq report      Solution: Trim the sequences
3. Problem: Sequence length is highly variable (35-251)                            Solution: Trim the sequences, set a MINLEN
4. Problem: Uneven distribution of nucleotides                                     Solution: I have no idea

Trimmomatic command

```screen java -jar trimmomatic-0.38.jar PE -threads 2 -phred33 -trimlog BcereusLogFile.txt Bcereus_S1_L001_R1_001.fastq.gz Bcereus_S1_L001_R2_001.fastq.gz Bcereus_S1_L001_R1_001_p.fq Bcereus_S1_L001_R1_001_up.fq Bcereus_S1_L001_R2_001_p.fq Bcereus_S1_L001_R2_001_up.fq ILLUMINACLIP:../adaptors.fasta:2:30:10 SLIDINGWINDOW:20:20 MINLEN:120```

- Suggested k-mer length for B. cereus: 95
- Suggested k-mer length for fungal: 137
- Suggested k-mer length for human: 99

# Steps

Create a Velvet screen

```screen -S velvet```

Attach to Velvet screen

```screen -r velvet```

Detatch from Velvet screen

```CTRL+A then CTRL+D```

Build `velveth` roadmaps

```velveth Bcereus_velvet1 95 -shortPaired -fastq -separate Bcereus_S1_L001_R1_001_p.fq Bcereus_S1_L001_R2_001_p.fq```

Assemble via `velvetg`

```velvetg Bcereus_velvet1/```

- Genome size (total): 5,534,174
- Number of scaffolds (nodes): 6,738
- Longest scaffold (max): 36,962
- N50 value: 5,291

Run velvet using a range of k-mer values

```velvetoptimiser -s 121 -e 201 -x 10 -d Bcereus_velvet_optimal -f '-shortPaired -fastq.gz -separate Bcereus_S1_L001_R1_001.fastq.gz Bcereus_S1_L001_R2_001.fastq.gz' -t 1```

- Genome size (total bases in contigs): 5,402,802
- Number of scaffolds (contigs)*: 85
- Longest scaffold: 488,605
- N50: 161,935
