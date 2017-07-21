

```
#Download databases
/group/bioinfo/apps/apps/Trinotate-3.0.1/admin/Build_Trinotate_Boilerplate_SQLite_db.pl Trinotate


module load bioinfo blast
blastp -query test.fa -db uniprot_sprot.pep -num_threads 8 -max_target_seqs 1 -outfmt 6 > blastp.outfmt6

#BLASTx
#blastx -query test.fa -db uniprot_sprot.pep -num_threads 8 -max_target_seqs 1 -outfmt 6 > blastx.outfmt6

#BLASTp
blastp -query PvSporo.transdecoder.pep -db uniprot_sprot.pep -num_threads 8 -max_target_seqs 1 -outfmt 6 > blastp.outfmt6

#Run HMMER
hmmscan --cpu 8 --domtblout PFAM_Trinotate_Pv.out Pfam-A.hmm PvSporo.fasta.transdecoder.pep > pfam_PvSporo.log

#Run Signalp
signalp -f short -n signalp_PvSporo.out PvSporo.fasta.transdecoder.pep

#Run tmHMM
tmhmm --short PvSporo.fasta.transdecoder.pep>PvSporo_tmhmm.out

#Run RNAMMER
/group/bioinfo/apps/apps/Trinotate-3.0.1/util/rnammer_support/RnammerTranscriptome.pl --transcriptome PvSporo.fasta --path_to_rnammer /group/bioinfo/apps/apps/rnammer-1.2/rnammer

#Initial import
init --gene_trans_map PvSporo.fasta.gene_trans_map --transcript_fasta PvSporo.fasta --transdecoder_pep PvSporo.fasta.transdecoder.pep

#Load results to the database
Trinotate Trinotate.sqlite LOAD_swissprot_blastp blastp.outfmt6
Trinotate Trinotate.sqlite LOAD_swissprot_blastx blastx.outfmt6
Trinotate Trinotate.sqlite LOAD_pfam PFAM_Trinotate_Pv.out
Trinotate Trinotate.sqlite LOAD_tmhmm PvSporo_tmhmm.out
Trinotate Trinotate.sqlite LOAD_signalp signalp_PvSporo.out
Trinotate Trinotate.sqlite LOAD_rnammer PvSporo.fasta.rnammer.gff

#Export report
Trinotate Trinotate.sqlite report -E 0.0000000001 > PvSporo_report.xls
```



Reference:

https://github.com/trinityrnaseq/trinityrnaseq/wiki/Running-GOSeq
https://github.com/trinityrnaseq/BernWorkshop2016/wiki/Day_2_FunctionalAnnotation


