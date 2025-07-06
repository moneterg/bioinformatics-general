# Downloading FASTQ files directly from SRA

To download reads from the SRA database directly in `fastq.gz` format:

```bash
nohup nice -n 19 fastq-dump --gzip --split-3 -v SRRX > nohupSRRX.txt &
```
Arguments:

`--gzip`: compresses the FASTQ files as .fastq.gz

`--split-3`: for paired-end data, creates R1, R2, and an unpaired file (if applicable); for single-end data, creates a single file with all reads.

`-v`: verbose mode, shows details of the process on the screen

`SRRX`: the SRA run accession you want to download

📌 Note: The `--outdir` wasn't neccessary as the default behavior is to place the output files in the current working directory. So, run this command in your target dir.

