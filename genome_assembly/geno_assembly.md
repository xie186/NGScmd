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
* Output:

Output directory can be assigned using `-C` papameter. 

## Scaffolding

Weblink: https://github.com/nsoranzo/sspace_basic

```
# Default: x=0 - do not extend contigs
SSPACE_Standard_v3.0.pl -l libraries.txt -s contigs.fasta -k 5 -a 0.7 -x 0 -p 1 -b default -T 20

```


## SEALER


```
abyss-sealer -b200G -k92 -k91 -k90 -k89 -k88 --print-flanks -j 20 -o L2 -S L1_scaffold.fa -v --mask R1.fq R2.fq

```

## MAKER 

Gene annotation 
An easy-to-use annotation pipeline designed for emerging model organism genomes

```
# MPI run
mpiexec -n 20 maker -fix_nucleotides maker_exe.ctl maker_opts.ctl maker_bopts.ctl
# Normal
maker -fix_nucleotides maker_exe.ctl maker_opts.ctl maker_bopts.ctl
```

This script `gff3_merge` will take a MAKER datastore index log file, extract all the relevant GFF3 files and combined GFF3 file.  The script can also
combine other correctly formated GFF3 files.  For this to work properly you need to be in the same directory as the datastore index.

```
#  -d The location of the MAKER datastore index log file.
#  -o Alternate base name for the output files.
#  -s Use STDOUT for output.
#  -g Only write MAKER gene models to the file, and ignore evidence.
#  -n Do not print fasta sequence in footer
#  -l Merge legacy annotation sets (ignores already having seen
#     features more than once for the same contig)
gff3_merge -g -n -l -d <The location of the MAKER datastore index log.> -o <Alternate base name for the output files.>
```


The script `fasta_merge` take a MAKER datastore index log file, extract all
the relevant fasta files and create fasta files with relevant
categories of sequence (i.e. transcript, protein, GeneMark protien,
etc.).  For this to work properly you need to be in the same directory
as the datastore index.

```
fasta_merge -d <The location of the MAKER datastore index log.> -o <Alternate base name for the output files.>
```



## 
perl orthomcl.pl --mode 1 --fa_files test1.fasta,test2,test3.fasta


## tRNA

```
tRNAscan-SE -d test.fasta
```


## rRNA

```
rnammer -S euk -gff out.gff -multi -f rRNA.fasta -h hmmreport -m ssu,lsu,tsu test.fasta

```
