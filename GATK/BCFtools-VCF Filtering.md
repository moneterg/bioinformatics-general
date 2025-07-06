# BCFtools and VCF Filtering

In this section, I'm using **bcftools version 1.9**.  
⚠️ Be aware that some tools and options may not be available in older versions.

Here, I'm selecting variant sites where **at least one sample** meets the criteria:  
`GQ >= 20` and `DP >= 8`

```bash
bcftools query -i'FMT/GQ >= 20 & FMT/DP >= 8' \
-f'%CHROM\t%POS[\t%SAMPLE\tGQ.%GQ\tDP.%DP]\n' \
X.vcf.gz \
>> W.txt
```

To count entries using `awk` and the number of fields (`NF`):
```bash
bcftools query -i'(FMT/GQ == ".")' -f'%CHROM\t%POS[\tGQ.%GQ]\n' \
X.vcf.gz | awk '{ print $1 "\t" $2 "\t" NF-2}' \
>> count-GQ-UNDEFINED.txt &
```
This will generate a tab-delimited table with the positions of the variants that match your criteria.

⚠️ Important: In bcftools, be careful with the use of & vs && and | vs ||, as they behave differently!

Useful links:
- http://samtools.github.io/bcftools/bcftools.html
- https://samtools.github.io/bcftools/howtos/filtering.html
