# Phylogenomic tree construction of the MAG
<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_11_1.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>  
</figure> 

There are various methods for performing taxonomic assignment after recovering multiple genomes from a metagenome.
Among these methods, the [GTDB database](https://gtdb.ecogenomic.org) and [GTDB-tk](https://ecogenomics.github.io/GTDBTk/index.html), which facilitates classification, are among the most commonly used.
GTDB is a database that compiles information about metagenome-assembled genomes (MAGs) recovered from diverse environmental samples based on data from RefSeq and GenBank.

GTDB-tk consists of multiple steps, including an identification step that utilizes Prodigal and HMMER, an alignment step for concatenating marker genes, and a classification step that involves comparison with the GTDB reference tree using the pplacer program and the maximum-likelihood placement technique.
Additionally, a single command, classify_wf, is available to combine these three steps into one streamlined process.


```bash
$ conda activate gtdbtk
# Download GTDB-Tk reference data & set the database PATH
$ wget https://data.gtdb.ecogenomic.org/releases/latest/auxillary_files/gtdbtk_v2_data.tar.gz
$ tar xvzf gtdbtk_v2_data.tar.gz
$ export GTDBTK_DATA_PATH=/path/to/unarchived/gtdbtk/release000
# run GTDB-tk (gene calling)
$ gtdbtk identify --genome_dir bins_dir/bin --out_dir /gtdbtk/identify --extension fa --cpus 2
# run GTDB-tk (align)
$ gtdbtk align --identify_dir /gtdbtk/identify --out_dir /gtdbtk/align --cpus 2
# run GTDB-tk (classify)
$ gtdbtk classify --genome_dir /gtdbtk/genomes --align_dir /gtdbtk/align --out_dir /gtdbtk/classify -x fa --cpus 2
$ conda deactivate
```

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_11_2.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>  
</figure>

Besides [GTDB-tk](https://ecogenomics.github.io/GTDBTk/index.html), another widely used program is [PhyloPhlAn](https://huttenhower.sph.harvard.edu/phylophlan). This program is known for its accuracy and speed.
It enables the characterization and construction of phylogenetic trees for microbial genomes and offers simple visualization options.  

```bash
$ conda activate phylophlan3
$ phylophlan_metagenomic -i bins_dir -o output_metagenomic --nproc 4 -n 1 -d SGB.Jan19 --verbose 2>&1
$ phylophlan_draw_metagenomic -i output_metagenomic.tsv -o output_heatmap --map bin2meta.tsv --top 20 --verbose 2>&1
$ conda deactivate
```
The `phylophlan_metagenomic` command in PhyloPhlAn 3.0 allows you to assign the closest species-level genome bins (SGBs) for each bin obtained from metagenome assembly analysis.
When using this command, you can adjust the number of CPU threads via the `-nproc` option.
Additionally, you can determine the number of SGBs to report for each input bin using the `-n` option, with a default value of 10.

This command generates three output files that list SGBs based on the average mash distance of the bins.
To visualize the output as a heatmap, you can utilize the `phylophlan_draw_metagenomic` command.
In this process, a mapping file for the bins entered in the `--map` option should be in `.tsv` file format.

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_11_3.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>  
</figure>
