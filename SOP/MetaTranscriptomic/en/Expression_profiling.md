# Transcriptional expression profiling

![pipeline](https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_7_1.png?raw=true)


RNA-seq read alignment results provide information for assessing the expression levels of individual genes.
Furthermore, it is possible to obtain expression information for individual contigs or MAGs generated from de novo assembly results of the metagenome.
In some cases, for more systematic analysis, it may be necessary to categorize genes with similar functions or group genes involved in specific metabolic pathways to analyze their expression levels.
To accomplish this, annotation information for each CDS in functional databases is required.
The eggNOG-mapper [26] can be used to easily obtain this information. eggNOG-mapper requires an input file in which the amino acid sequences of each gene are listed in a .faa file format.
When running with default options, eggNOG-mapper uses BLAST to find the most similar information for each gene's amino acid sequence, extracting data related to COG (Clusters of Orthologous Groups) [27], KEGG (Kyoto Encyclopedia of Genes and Genomes) [28], CAZy (Carbohydrate-Active EnZymes) [29], and Pfam [30].  

```bash
# download eggnog-mapper from https://github.com/eggnogdb/eggnog-mapper/releases/latest
$ tar -xvzf eggnog_mapper_(version).tar.gz
# download eggnog-mapper database
$ download_eggnog_data.py
# run eggnog-mapper
$ emapper.py (option) -i sample_MAG.prodigal.faa -o sample_MAG.eggnog.out
```

The resulting files include eggnog.out.hit, eggnog.out.annotation, and eggnog.out.seed_ortholog, with eggnog.out.annotation containing annotation information from various databases such as COG and KEGG.

![eggnog](https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_7_2.png?raw=true)
> Example of an announcement file among EGGNOG-mapper results  

Using the COG information obtained from EGGNOG-mapper results, it is possible to predict the expression levels of each COG functional category across the entire metatranscriptome.  

![COG](https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_7_3.png?raw=true)
> Example of COG distribution  

Additionally, the extracted COG or KEGG ORTHOLOGY information can be visualized using tools like KEGG mapper, IPATH3 [31], allowing for the exploration of the overall correlations among highly expressed genes. Depending on the options chosen, you can select a few genes with high count values, adjust line thickness based on count (i.e., expression level), or use different colors for each MAG, among other possibilities, to obtain diverse results.  

![ipath](https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_7_4.png?raw=true)
> Example of iPATH3 results 

