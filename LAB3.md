# LAB3

1. Problem: Not many reads available for assembly                                  Solution: Use the unpaired reads to supplement
2. Problem: Per base sequence content is bad near the end of the fastq report      Solution: Trim the sequences
3. Problem: Sequence length is highly variable (35-251)                            Solution: Trim the sequences, set a MINLEN
4. Problem: Uneven distribution of nucleotides                                     Solution: I have no idea

Trimmomatic command

```screen java -jar trimmomatic-0.38.jar PE -threads 2 -phred33 -trimlog BcereusLogFile.txt Bcereus_S1_L001_R1_001.fastq.gz Bcereus_S1_L001_R2_001.fastq.gz Bcereus_S1_L001_R1_001_p.fq Bcereus_S1_L001_R1_001_up.fq Bcereus_S1_L001_R2_001_p.fq Bcereus_S1_L001_R2_001_up.fq ILLUMINACLIP:../adaptors.fasta:2:30:10 SLIDINGWINDOW:20:20 MINLEN:120```

