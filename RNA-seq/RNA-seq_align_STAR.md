## Create index

```
STAR --runThreadN 10 --runMode genomeGenerate --genomeDir ./ --genomeFastaFiles test.fasta
```

## Alignment

```
STAR  --runThreadN 3 --runMode alignReads --outSAMattrIHstart 0 --outFilterIntronMotifs RemoveNoncanonical --genomeDir ../../data/references/ara/STAR_index/ --readFilesIn /psc/base/zhujiankang/sharedata/pscngs/JKZ0182/2198/JKZ0182_2198_mRNA170302_S170303_R1.fq.gz /psc/base/zhujiankang/sharedata/pscngs/JKZ0182/2198/JKZ0182_2198_mRNA170302_S170303_R2.fq.gz --twopassMode Basic --outFileNamePrefix  WT-CON1 --outSAMtype BAM SortedByCoordinate --readFilesCommand zcat --sjdbGTFfile ../../data/references/ara/TAIR10_GFF3_genes_chr.gtf 
```
