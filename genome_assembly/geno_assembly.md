# Command lines used for genome assembly


## Read trimming

Weblink: https://github.com/FelixKrueger/TrimGalore

```
trim_galore --paired --quality 30 --length 50 --fastqc --nextera test_R1.fq test_R2.fq
```

Output files:

```
test_R2_val_2_fastqc.html
test_R2_val_2_fastqc.zip
test_R1_val_1_fastqc.html
test_R1_val_1_fastqc.zip
test_R2.fq_trimming_report.txt
test_R1_val_1.fq
test_R2_val_2.fq
test_R1.fq_trimming_report.txt
```

## ABYSS

```
abyss-pe k=104 name=cotton v=-v lib='pea peb' mp='mpc mpd'  \
pea='readA_1.fastq readA_2.fastq' \
peb='readB_1.fastq readB_2.fastq' \
mpc='readC_1.fastq readC_2.fastq' \
mpd='readD_1.fastq readD_2.fastq'
```

## Scaffolding

Weblink: https://github.com/nsoranzo/sspace_basic

```
SSPACE_Standard_v3.0.pl -l lib.txt -s contig.fa -k 5 -a 0.7 -x 1 -p 1 -b x1 -T 19

```


