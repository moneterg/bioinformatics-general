# Counting Bases in FASTQ and FASTA Files

#### Counting bases in a FASTQ file line by line:

Using Perl:

```bash
cat file.fastq | perl -ne '$s=<>;<>;<>;chomp($s);print length($s)."\n";'
```
Or using `awk`:

```bash
awk '{if(NR%4==2) print length($1)}' file.fastq
```

Note: This awk command assumes a standard FASTQ format where each read and its quality scores are represented in 4 lines.
The lines used to calculate the length are: 2, 6, 10, 14, ... (lines where the remainder when divided by 4 is 2).

To calculate the **total number of bases in the entire FASTQ file**:
```bash
awk 'BEGIN{sum=0;} {if(NR%4==2){sum+=length($0);}} END{print sum;}' file.fastq
```
Useful link:
- https://www.biostars.org/p/78043/

#### Counting bases in each sequence of a MULTIFASTA file:
```bash
awk '/^>/ {if (seqlen){print seqlen}; print; seqlen=0; next;} {seqlen += length($0)} END{print seqlen}' file.fasta
```
Useful links:
- https://github.com/ECBSU/oneliners
