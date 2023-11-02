# *De novo* assembly
<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_7_1.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>  
</figure>

## Short reads 
Read-based profiling offers a rapid overview of the metagenome but is limited by the presence of a significant number of unmapped reads.
To overcome this limitation, de novo assembly is employed using assemblers to extend overlapping reads into contigs or scaffolds.
This approach enables in-depth profiling of genomic components and the discovery of previously unknown sequences since it is a database-independent process.

Currently, various assemblers are available. Some assemblers are specifically designed for the efficient assembly of short reads.
Among the most widely utilized assemblers, [MEGAHIT](https://github.com/voutcn/megahit) and [metaSPAdes](https://cab.spbu.ru/software/meta-spades/) stand out.
metaSPAdes is particularly renowned for its performance with high-depth samples. However, it demands a substantial amount of memory, even for small-sized metagenome data.
MEGAHIT shows competitive assembly quality and efficient memory usage compared to metaSPAdes. [&#91;ref&#93;](https://doi.org/10.1038/s41596-020-00480-3).

MEGAHIT employs k-mers, and the size of these k-mers can be adjusted based on the sample's complexity using the `--k-min` and `--k-max` options.
When dealing with high-depth samples, it is advisable to select a relatively larger k-mer size (typically 25-31) to prevent excessive complexity in the de Bruijn graph.
Conversely, for low-depth samples where the assembly isn't functioning optimally, you can enhance assembly efficiency by employing the `--no-mercy` option.
For paired-end reads, make sure to specify the forward and reverse read filenames separately using `-1` and `-2.` For single reads, use the `-r` option.
The maximum memory allocated for de Bruijn graph construction can be set using the `-m` option and the total system memory can be adjusted within the range of 0-1.
The default value is typically set to 0.9. The `-t` option allows you to define the number of CPU threads, with a minimum requirement of 2.
By default, the software automatically calculates the available CPU threads and utilizes them collectively.

```bash
# run MEGAHIT 
$ conda activate MEGAHIT
$ MEGAHIT -1 kneaddata.trimmed.1.fastq  -2 kneaddata.trimmed.2.fastq  -m 0.5  -t 12 -o MEGAHIT_result
$ conda deactivate
```

##Lond reads assembly

```bash
# run hifiasm_meta 
$ conda activate hifiam_meta
$ hifiasm_meta -o N14.asm -t 60 N14.aln.unmapped.fq > N14.log
$ conda deactivate
# .gfa 파일을 .fa 파일로 변환
$ awk '/^S/{print ">"$2;print $3}' test.p_ctg.gfa > test.p_ctg.fa
```

`.gfa` stands for graphical fragment assembly, a file format designed to store graph-based assembly information.
It contains data about the graph generated during the assembly process.
The structure of the graph file is akin to a de Bruijn graph, illustrating the connectivity of nodes and edges.
These graphs depict the interactions among overlapping DNA sequences, aiding in the assembly process.

When running [Hifiasm-meta](https://github.com/lh3/hifiasm-meta), the output files are as follows.


__1. Raw unitig graph: asm.r_utg*.gfa__  
This file contains the raw unitig graph generated during the assembly process. The raw unitig graph is the initial graph for assembly, which organizes nodes and edges based on overlapping sequence information.
__2. Cleaned unitig graph: asm.p_utg*.gfa__  
This file contains preprocessed cleaned unitig graphs. Preprocessing refers to the process of removing errors from the raw unitig graph and improving its accuracy.
__3. Contig graph: asm.p_ctg*.gfa, asm.a_ctg*.gfa__  
This file contains the contig graph. The file asm.p_ctg*.gfa means primary contig and asm.a_ctg*.gfa means alternate contig.


* Unitig  
A unitig, which stands for unique sequence, is a unit of overlapping DNA sequences that is the result of an intermediate step in assembly. Each unitig consists of one or more DNA sequences and contains overlapping parts. The assembly process generates a raw unitig graph. This raw unitig graph may contain some errors. The subsequent processing removes the errors from the raw unitig graph and generates a cleaned unitig graph.

## Contig check
Long read assembly results can be visualized using a bandage plot, which is a tool for representing complex assembly results, including De Bruijn graphs or overlap graphs.
Long read assemblies often yield intricate graphs, and the bandage plot is a good option for visualizing these graphs.

It provides the following information.


To generate bandage plots, you can use Bandage, a Bioinformatics Application for Navigating De novo Assembly Graphs Easily. Bandage is available for download at http://rrwick.github.io/Bandage/.


After running the Bandage program, load the *p_ctg.gfa file from File > Load graph at the top. Once the file is loaded, click Draw graph in Graph drawing to display the graph.


<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_7_2.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>  
</figure>

After assembly, check the assembly result and quality using [QUAST](https://github.com/ablab/quast)(Quality assessment tool) to know the information of the produced contigs.

```bash
# calculate assembly statistics
$ conda activate quast
$ quast.py MEGAHIT_result/final.contigs.fa -o MEGAHIT_quast
$ conda deactivate
```

 
<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_7_3.png?raw=true" style="width:90%">
  <figcaption><b>Example of report.html </b></figcaption>  
</figure>

**contigs: Number of contigs produced after assembly**
- Largest contig: The length of the longest contig among the contigs produced after assembly
- Total length: Total number of bases of contigs generated after assembly
- N50: Length of the contig with the top 50% length among the contigs generated after assembly
- N75: Length of the contig with the top 75% length among the contigs generated after assembly
- L50: Number of contigs with the length of N50 among the contigs generated after assembly
- L75: Number of contigs with the length of N75 among the contigs generated after assembly
- Mismatches # N's: Number of uncalled bases that were not assembled
- Mismatches # N's per 100kbp: Number of uncalled bases per 100000 bases

The left Graph shows cumulative length as the contig index increases and the right graph shows GC contents of contigs 
<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_7_4.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>  
</figure>
