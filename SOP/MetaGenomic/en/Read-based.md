# Read-based profiling 

The methods for analyzing preprocessed reads can be categorized into two main approaches: read-based profiling and assembly-based profiling.
Read-based profiling involves taxonomic and functional profiling without the need for assembly, primarily relying on k-mer matching.
This approach is particularly useful for analyzing low-depth samples that are challenging to assemble. It offers the advantage of faster analysis completion.

[HUMAnN 3.0](https://huttenhower.sph.harvard.edu/humann/), for instance, utilizes the MetaPhlAn program for pre-taxonomic profiling.
It then employs a translated search to examine unmapped reads, facilitating further analysis and quantification of gene families and pathways across the entire pangenomes.

```bash
# download database
$ conda activate humann
$ humann_databases --download chocophlan full /database/humann
$ humann_databases --download uniref uniref90_diamond /database/humann
# concatenate all reads into a single FASTAQ file
$ cat kneaddata.trimmed.1.fastq kneaddata.trimmed.2.fastq > kneaddata.trimmed.fastq
# run human 3.0
$ humann3 --input kneaddata.trimmed.fastq --output humann3_out/ --nucleotide-database /database/humann/chocophlan/ --protein-database /database/humann/uniref/
```

▶Example of output files
1. HUMAnN 3.0_genefamilies.tsv  
: Gene family abundance, calculated as reads per kilobase (RPK) value. If the taxonomy assignment is successful, the contribution value is assigned to each microorganism and divided. Gene families are presented in the first column with the UniRef90 identifier, separated by '|' or labeled as 'UniRef90_unknown' if no identifier is available.

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_6_1.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>  
</figure>

2. HUMAnN 3.0_pathabundance.tsv  
: Represents the pathway abundance of each sample and is calculated as an RPK value, the same as the gene family result. It is divided according to the contribution of each microorganism. 

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_6_2.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>  
</figure>

To compare gene families across samples with different sequencing depths, normalization can be performed by obtaining relative abundance numbers (relab) or counts per million (CPM), which is the copy number of a gene divided by one million reads.
This can be done by specifying cpm or relab in the `--units` option of the `Human_renorm_table` command.

```bash
# Normalization 
$ humann_renorm_table --input Trimmed_paired_merged_genefamilies.tsv --output Trimmed_paired_merged_genefamilies_relab.tsv --units cpm
```

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_6_3.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>  
</figure>

After normalization, UniRef gene families can be grouped into reaction units in the default database, MetaCyc, and abundances can be reconstructed. 

```bash
# Generate barplot for specific pathway
$ humann_barplot --input Trimmed_paired_merged_genefamilies_relab.tsv --output plot1.png --focal-feature 2-ISOPROPYLMALATESYN-RXN
# Generate sorted barplot by total sum of abundances
$ humann_barplot --input Trimmed_paired_merged_genefamilies_relab.tsv --output plot2_sorted.png --focal-feature 2-ISOPROPYLMALATESYN-RXN -–sort sum 
# Generate sorted barplot by bray-curtis distance and facetted by genera
$ humann_barplot --input Trimmed_paired_merged_genefamilies_relab.tsv --output plot3_sorted_facetted.png --focal-feature COA-PWY -–sort braycurtis –-as-genera –-remove-zeros
```
After grouping by reaction, you can plot specific reactions, sort bar graphs based on the sum of their total abundance, sort bar graphs based on their Bayesian distance, or facet by genera.

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_6_4.png?raw=true" style="width:90%">
  <figcaption><b>Bar plot for METSYN_PWY (plot1.png)</b></figcaption>  
</figure>
  
<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_6_5.png?raw=true" style="width:90%">
  <figcaption><b>Sorted bar plot for METSYN_PWY (plot1_sorted.png)</b></figcaption>  
</figure>
  
<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_6_6.png?raw=true" style="width:90%">
  <figcaption><b>Sorted and facetted bar plot for COA-PWY</b></figcaption>  
</figure>
