# Transcriptional expression profiling

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_7_1.png?raw=true" style="width:65%">
  <figcaption><b> </b></figcaption>  
</figure>

RNA-seq read alignment results provide information for assessing the expression levels of individual genes.
Furthermore, it is possible to obtain expression information for individual contigs or MAGs generated from de novo assembly results of the metagenome.
In some cases, for more systematic analysis, it may be necessary to categorize genes with similar functions or group genes involved in specific metabolic pathways to analyze their expression levels.
To accomplish this, annotation information for each CDS in functional databases is required.
The [eggNOG-mapper](https://github.com/eggnogdb/eggnog-mapper) can be used to easily obtain this information. eggNOG-mapper requires an input file in which the amino acid sequences of each gene are listed in a .faa file format.
When running with default options, eggNOG-mapper uses BLAST to find the most similar information for each gene's amino acid sequence, extracting data related to [COG(Clusters of Orthologous Groups)](https://www.ncbi.nlm.nih.gov/research/cog-project/), [KEGG(Kyoto Encyclopedia of Genes and Genomes)](https://www.genome.jp/kegg/), [CAZy(Carbohydrate-Active EnZymes)](http://www.cazy.org/), and [Pfam](http://pfam.xfam.org/).  

```bash
# download eggnog-mapper from https://github.com/eggnogdb/eggnog-mapper/releases/latest
$ tar -xvzf eggnog_mapper_(version).tar.gz
# download eggnog-mapper database
$ download_eggnog_data.py
# run eggnog-mapper
$ emapper.py (option) -i sample_MAG.prodigal.faa -o sample_MAG.eggnog.out
```

The resulting files include eggnog.out.hit, eggnog.out.annotation, and eggnog.out.seed_ortholog, with eggnog.out.annotation containing annotation information from various databases such as COG and KEGG.

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_7_2.png?raw=true" style="width:90%">
  <figcaption><b>Example of an announcement file among EGGNOG-mapper results</b></figcaption>  
</figure>

Using the COG information obtained from EGGNOG-mapper results, it is possible to predict the expression levels of each COG functional category across the entire metatranscriptome.  

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_7_3.png?raw=true" style="width:90%">
  <figcaption><b>Example of COG distribution</b></figcaption>  
</figure>

Additionally, the extracted COG or KEGG ORTHOLOGY information can be visualized using tools like KEGG mapper, IPATH3 [31], allowing for the exploration of the overall correlations among highly expressed genes. Depending on the options chosen, you can select a few genes with high count values, adjust line thickness based on count (i.e., expression level), or use different colors for each MAG, among other possibilities, to obtain diverse results.  

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_7_4.png?raw=true" style="width:70%">
  <figcaption><b> Example of iPATH3 results </b></figcaption>  
</figure>

