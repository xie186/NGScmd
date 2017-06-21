

```
module load java
module load bioinfo
module load rsem
module load trinity
module load bowtie2
module load tophat
module list

rsem-generate-ngvector ../blat_chl_mt/Trinity_contigs_witho_chloroplast.fasta Trinity_RSEM

rsem-generate-data-matrix MA1_rsem/MA1_rsem.genes.results MA2_rsem/MA2_rsem.genes.results MA3_rsem/MA3_rsem.genes.results PA1_rsem/PA1_rsem.genes.results PA2_rsem/PA2_rsem.genes.results PA3_rsem/PA3_rsem.genes.results > MAPA_rsem.counts.matrix

rsem-run-ebseq --ngvector Trinity_RSEM.ngvec MAPA_rsem.counts.matrix 3,3 MAPA_ebseq.out

rsem-control-fdr --soft-threshold MAPA_ebseq.out 0.05 MAPA_DGE_0.05.txt

rsem-control-fdr MAPA_ebseq.out 0.05 MAPA_ebseq_DGE_0.05_default.txt

rsem-control-fdr MAPA_ebseq.out 0.01 MAPA_ebseq_DGE_0.01.txt
#There are 36 genes/transcripts reported at FDR = 0.01.

rsem-control-fdr MAPA_ebseq.out 0.05 MAPA_ebseq_DGE_0.05.txt
#There are 46 genes/transcripts reported at FDR = 0.05.

```
