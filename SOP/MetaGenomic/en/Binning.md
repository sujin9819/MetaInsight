# Binning
<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_10_1.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>  
</figure>


In metagenome analysis, binning is the process of grouping contigs based on specific criteria, primarily relying on sequence composition and coverage data.
By utilizing a binning program to cluster contigs, it becomes possible to reconstruct complete microbial genomes.
In addition to [MetaBAT2](https://bitbucket.org/berkeleylab/metabat/src/master/) we used, other widely used binning programs are [MaxBin 2.0](https://sourceforge.net/projects/maxbin/) and [CONCOCT](https://github.com/BinPro/CONCOCT). 

To perform binning using MetaBAT2, a sam file with coverage information is required.
For short reads data, this can be obtained by using the BBmap script to map the trimmed sequence to the template of the assembled contigs.
For long read data, minimap2 is used instead of bbmap to map reads to contig.

```bash
# calculate coverage information from short reads assembly
$ conda activate bbmap
$ bbmap.sh in=trimmed.reads_1.fastq in2=trimmed.reads_2.fastq covstats=covstats.txt out=MEGAHIT.sam threads=3 ref=/MEGAHIT_result/final.contigs.fa
$ conda deactivate 

# generate bam file from sam file
$ conda activate samtools
$ samtools view -bS -o MEGAHIT.bam MEGAHIT.sam -@ 5
# sort the bam file
$ samtools sort MEGAHIT.bam –o MEGAHIT.sorted.bam -@ 5
$ conda deactivate 
```

```bash
# calculate coverage information  from long reads assembly
$ conda activate minimap2
# align host read-filtered read file(N008.aln.unamapped.fq) to assembled contig file(N_008_HiFi.p_ctg.fa)
$ minimap2 -ax map-hifi N_008_HiFi.p_ctg.fa N008.aln.unmapped.fq > N_008_HiFi.p_ctg_mapped.sam
$ conda deactivate 

# generate bam file from sam file
$ conda activate samtools
$ samtools view -bS -o N_008_HiFi.p_ctg_mapped.bam N_008_HiFi.p_ctg_mapped.sam -@ 5
# sort the bam file
$ samtools sort N_008_HiFi.p_ctg_mapped.bam -o 
```

Compress and index the formed sam file and convert it to a binary bam file.

When the bam file with coverage information is ready, use the jgi_summarize_bam_contig_depth script provided by MetaBAT2 to generate the final depth.txt file and then perform binning with the assembled contigs. 

```bash
$ conda activate MetaBAT2
# generate depth file from bam file
$ jgi_summarize_bam_contig_depths --outputDepth jgi.depth.txt MEGAHIT.sorted.bam
# run MetaBAT2
$ MetaBAT2 -i final.contigs.fa -a jgi.depth.txt -o bins_dir/bin
$ conda deactivate 
```

After the completion of binning using MetaBAT2, the quality of the bins is assessed using [CheckM](https://github.com/Ecogenomics/CheckM).
CheckM is a program designed to gauge the quality of genomes recovered from isolates, single cells, or metagenomes.
The program furnishes information about phylogenetic lineage, genetic characteristics (such as GC contents and coding density), contamination, completeness, and strain heterogeneity.
It accomplishes this by analyzing single-copy genes within the genome.

```bash
$ conda activate CheckM
# download CheckM database from https://data.ace.uq.edu.au/public/CheckM_databases/
$ export CHECKM_DATA_PATH=/path/to/my_CheckM_data
# run CheckM
$ CheckM lineage_wf –x fa bins_dir bins_CheckM
```
It displays the marker lineage and the number of marker genes in the generated bin, along with the completeness, contamination, and strain heterogeneity of the constructed genome in the last three columns.

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_10_2.png?raw=true" style="width:90%">
  <figcaption><b>Example of CheckM result</b></figcaption>  
</figure>