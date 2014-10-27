WARNING: alien_index is in very preliminary stages.  The interface may change. It is quite simple though, and should work reliably. 

WARNING: the alien_index_blastdb.0.01.fasta file is 5.4 gigabytes when uncompressed. You will need close to 20 gigabytes of free space for the fasta file and the blast databases

alien_index
===========

identify potential non-animal transcripts or horizontally transferred genes in animal transcriptomes 

requires
========

alien_index BLAST database  
http://ryanlab.whitney.ufl.edu/downloads/alien_index/

algorithm
=========

algorithm is based on alogorithm described in the following:
  Gladyshev, Eugene A., Matthew Meselson, and Irina R. Arkhipova.
    "Massive horizontal gene transfer in bdelloid rotifers."
    science 320.5880 (2008): 1210-1213.

briefly: a transcriptome is BLASTed against proteomes from various metazoans and non-metazoans.  If the best hit is non-metazoan the e-value of the best hit is compared to the best metazoan hit and the difference is reported.  

Gladyshev et al (2008) was describing horizontally transferred genes. Here is the relevant quotation from the paper describing when a gene was reliably considered having a non-metazoan origin:

> We characterized the foreignness of such genes with an alien index (AI), 
> which measures by how many orders of magnitude the BLAST E-value for the
> best metazoan hit differs from that for the best nonmetazoan hit (Table 1
> and table S1) (19). We tested the AI validity by phylogenetic analyses of
> all CDS with AI > 0 yielding metazoan hits, excluding those with repetitive
> sequences. We found that AI ≥ 45, corresponding to a difference of ≥20 orders
> of magnitude between the best nonmetazoan and metazoan hits, was a good
> indicator of foreign origin, as judged by phylogenetic assignment to
> bacterial, plant, or fungal clades (Fig. 2 and fig. S2A). Genes with
> 0 < AI < 45 were designated indeterminate, because their phylogenetic
> analysis may or may not confidently support a foreign origin."

prerequisite
============

    BLAST+

usage
=====

these commands needs to be run only the first time you use the program

```bash
gzip -d alien_index_blastdb.0.01.fasta.gz

makeblastdb -dbtype prot -in alien_index_blastdb.0.01.fasta
```

these commands are run for a typical alien_index analysis

```bash
blastx -query YOURTRANSCRIPTOME.fasta -outfmt 6 -max_target_seqs 1000 \
  -seg yes -evalue 0.001 -db alien_index_blastdb.0.01.fasta \
  -out BLASTREPORT 2> blastx.err

./alien_index --blast=BLASTREPORT [--version] [--help]
```



