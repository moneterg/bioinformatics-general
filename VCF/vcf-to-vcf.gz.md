# Converting VCF to VCF.gz

### To compress and index a VCF file, first install **htslib**:  
🔗 [HTSlib Download](http://www.htslib.org/download/)

Then run the following commands:

```bash
/path/to/tabix/bgzip myvcf.vcf
/path/to/tabix/tabix -p vcf myvcf.vcf.gz
```
