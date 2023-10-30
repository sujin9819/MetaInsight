# Taxonomic annotation of contigs
<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_8_1.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>  
</figure> 

Taxonomic profiling of metagenome datasets can be categorized into three main methods. (1) DNA-to-DNA, (2) DNA-to-protein, and (3) DNA-to-marker genes.
The commonly used method (1) is similar to BLASTn and uses a genomic database, while (2) is similar to BLASTx and requires a protein database. 

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_8_2.png?raw=true" style="width:90%">
  <figcaption><b>>Comparison of the taxonomic classification tools ; <a href="https://doi.org/10.1016/j.cell.2019.07.010">[ref]</a></b></figcaption>  
</figure>

Each program has its advantages and disadvantages. DNA-to-DNA methods are known for their speed and low memory consumption, but they are generally less sensitive than DNA-to-protein methods.
Conversely, DNA-to-protein methods tend to be slower and more resource-intensive in terms of memory and CPU usage.
However, their advantage lies in their sensitivity and accuracy since they are based on amino acid sequences.
The choice of the best program depends on the nature of the data you are analyzing and your database.
Kaiju is one of the representative DNA-to-protein programs, utilizing the NCBI taxonomy and protein reference database for the classification of microorganisms and viruses.

To run the [Kaiju](https://bioinformatics-centre.github.io/kaiju/) program, you need to download databases, and the duration of this process may vary based on your computer's performance.
The table below lists the available databases.

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_8_3.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>  
</figure>

```bash
# creating the reference database and index from NCBI nr database
$ conda activate kaiju
$ kaiju-makedb -s nr
```
Files generated after the Makedb command : `Kaiju_db_nr.fmi`, `nodes.dmp`, `names.dmp`


```bash
$ kaiju -t nodes.dmp -f nr/kaiju_db_nr.fmi -i MEGAHIT_result/final.contigs.fa -o kaiju.out -z 15
$ kaiju2krona -t nodes.dmp -n names.dmp -i kaiju.out -o kaiju.out.krona
$ conda deactivate
$ conda activate krona
$ ktImportText -o kaiju.out.html kaiju.out.krona
$ conda deactivate
$ conda activate kaiju
$ kaiju2table -t nodes.dmp -n names.dmp -r genus -o kaiju_summary.tsv kaiju.out -l superkingdom,phylum,class,order,family,genus,species
$ kaiju-addTaxonNames -t nodes.dmp -n names.dmp -i kaiju.out -o kaiju.names.out
$ conda deactivate
```

Three options (`-t`, `-f`, and `-i`) are required to run the kaiju program.
The `-t` option requires nodes.dmp, the `-f` option requires kaiju_db_nr.fmi, and the `-i` option requires assembled contig file(final.contigs.fa).
The `-o` option sets the name of kaiju's output file, and the `-z` option allows you to adjust the number of CPU threads.
To visualize the results of kaiju's analysis, convert the kaiju.out file into an input file for the Krona program with the `kaiju2krona` command.
After that, you can activate the Krona program and get the visualization result file in html format through the `ktImportText` command.
The results of Kaiju's analysis can also be downloaded as a `tsv` file using the `kaiju2table` command, with the option `-i` to specify the rank of the taxon.

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_8_4.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>  
</figure>
