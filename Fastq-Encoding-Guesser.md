### Fastq Encoding guesser notes

### 🔍 Reference
- Based on information from: [BioStars discussion thread](https://www.biostars.org/p/63225/)

head -n 40 file.fastq | awk '{if(NR%4==0) printf("%s",$0);}' |  od -A n -t u1 | awk 'BEGIN{min=100;max=0;}{for(i=1;i<=NF;i++) {if($i>max) max=$i; if($i<min) min=$i;}}END{if(max<=74 && min<59) print "Phred+33"; else if(max>73 && min>=64) print "Phred+64"; else if(min>=59 && min<64 && max>73) print "Solexa+64"; else print "Unknown score encoding\!";}'

### 🧪 Quick Check via Command Line
To inspect the encoding type from a compressed FASTQ file:

```bash
zcat SRR1015405_1.fastq.gz | head -n 40 | awk ... (command above)
```

⚠️ Note: This approach raised an error due to differences between _1 and _2 files.

✅ Recommended Method
Use one of the two available scripts:
- guess-encoding.py 
Here: https://github.com/brentp/bio-playground/tree/master/reads-utils
- fastq_detect.pl

I used fastq_detect.pl, and it worked successfully.

🧰 Perl Script Details
fastq_detect.pl is a Perl script designed to diagnose the Phred score type from FASTQ data, written by Stephane Plaisance and Joachim Jacob.
I couldn’t find their GitHub repository, so if you have that information, please let me know so I can add the link here.

It can handle both raw and compressed inputs and matches the score code against known formats.
You can optionally limit the number of lines processed:
# Use the first 1000 records
fastq_detect.pl fastq.file 1000
