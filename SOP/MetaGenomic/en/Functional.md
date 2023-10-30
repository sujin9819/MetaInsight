# Functional annotation of contigs
<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_9_1.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>  
</figure>

After completing the taxonomic annotation of contigs, it is necessary to retrieve information about the open reading frame of the contigs to make a functional assignment.
Prodigal can predict protein-coding sequences of prokaryotes and can be used for metagenome analysis in addition to complete or draft genome analysis.

```bash
# run prodigal
$ conda activate prodigal
$ prodigal -i final.contigs.fa -p meta -a final.contigs.prodigal.faa -d final.contigs.prodigal.fna -f gff -o final.contigs.prodigal.gff 
$ conda deactivate
```

After gene prediction is completed, the contig file can be analyzed for functional annotation based on various databases, most commonly [KEGG](https://www.genome.jp/kegg/), [COG](https://www.ncbi.nlm.nih.gov/research/cog-project/), and [metaCyc](https://metacyc.org/) databases, and also specialized databases such as CAZyme [14] and ARDB [15] can be utilized.
One of the most widely used functional annotation programs is [eggNOG-mapper](https://github.com/eggnogdb/eggnog-mapper), which can perform fast functional annotation of novel sequences using the eggNOG database based on orthologs and phylogenies produced by the European Molecular Biology Laboratory (EMBL).
In addition to eggNOG-mapper, other tools that can be used are simple BLAST or programs such as [InterProScan](https://www.ebi.ac.uk/interpro/search/sequence/).

```bash
# run eggnog-mapper
$ conda activate eggnog
# download eggnog-mapper database
$ download_eggnog_data.py
# run eggnog-mapper
$ emapper.py -m diamond --cpu 5 -i final.contig.prodigal.faa -o eggnog.out
$ conda deactivate
```

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_9_2.png?raw=true" style="width:90%">
  <figcaption><b>Example of report.html </b></figcaption>  
</figure>

Besides the standalone version, eggNOG-mapper offers a [web-based analysis service](http://eggNOG-mapper.embl.de/) that can accommodate input of up to 100,000 proteins in FASTA format.

