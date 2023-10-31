# Reads-based profiling

Apart from eggNOG-mapper, you can also obtain information about metabolic pathways using [HUMAnN](https://huttenhower.sph.harvard.edu/humann/).

HUMAnN (HMP Unified Metabolic Analysis Network) is a software designed to profile microbial metabolism and molecular functions from metagenomic or metatranscriptomic sequence data.
It accepts various types of input files, including .fastq files from metagenomes or metatranscriptomes after host data removal and quality trimming, alignment result files (.sam or .bam), and gene information with count data in .tsv and .biom formats.
You can perform microbial community analysis and functional analysis within the community using pangenome databases such as MetaPhlAn and ChocoPhlAn. Additionally, you can acquire genome information and pathway details using UniRef, MetaCyc, and MinPath.

```bash
# download humann
$ conda create --name biobakery3 python=3.7
$ conda activate biobakery3
$ conda install humann –c biobakery3
# download database
$ humann_databases --download chocophlan full $INSTALL_LOCATION --update-config yes
$ humann_databases --download uniref uniref90_diamond $INSTALL_LOCATION --update-config yes
$ humann_databases --download utility_mapping full $INSTALL_LOCATION --update-config yes
# paired read concatenation
$ cat kneaddata.trimmed_paired_1.fastq kneaddata.trimmed_paired_2.fastq > kneaddata.trimmed.fastq
# running humann
$ humann --input sample_kneaddata_paired_1.fastq --output $OUTPUT_DIR
# humann result’s features
$ humann_join_tables -i $OUTPUT_DIR -o sample_pathcoverage.tsv –-file_name pathcoverage 
$ humann_barplot –-input sample_pathcoverage.tsv –-focal-feature $PATHWAY_NAME –-outfile sample_path
```
- The explanation related to HUMAnN installation and DB download is described once more.

When conducting HUMAnN analysis, you can obtain information about gene families and pathways.
Among them, you can use pathway information stored in the sample_pathabundance.tsv and sample_pathcoverage.tsv files to create bar plots, allowing you to visualize the proportion of microorganisms involved in specific pathways.
HUMAnN generates several files (e.g., bowtie results, diamond results), and you can use these for additional analyses.

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_11_2.png?raw=true" style="width:90%">
  <figcaption><b>Example of a barplot visualization result of path information derived from HUMAnN results</b></figcaption>  
</figure>
