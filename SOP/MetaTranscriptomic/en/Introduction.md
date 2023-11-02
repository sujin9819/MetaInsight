# Standard Operating Procedure for Next-Generation Sequencing (NGS)-Based Metatranscriptome Analysis

## Introduction to Metatranscriptome

The term microbiome refers to the concept encompassing a community of microorganisms (microbiota) residing in a particular environment, along with their complete genetic information. Microbiome research traditionally involves the amplification and sequencing of conserved regions of marker genes, such as ribosomal genes, from environmental DNA using PCR, allowing for the identification of the types of microorganisms present in the environment. In contrast, microbiome research utilizes whole DNA sequence analysis, known as metagenome sequencing, which not only identifies the types of microorganisms present in the environment but also enables the exploration of the genetic diversity and functions possessed by these microorganisms. However, metagenomic (metagenome) data can inform about the presence or absence of specific species or genes but cannot determine whether they are active within the microbiome ecosystem, posing limitations.

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_0_1.png?raw=true" style="width:90%">
  <figcaption><b> Multi-omics information-based microbiome functional analysis</b></figcaption>  
</figure>

To investigate how microbial communities respond to environmental changes, metatranscriptome analysis has been initiated, and metatranscriptomic information will play a crucial role in understanding the ecology of the microbiome. Even before the advent of high-throughput DNA sequencing methods, research has been conducted to measure the expression levels of genes of interest using qPCR and to study the expression patterns of known transcripts from specific organisms using microarray technology. With the widespread adoption of Next-Generation Sequencing (NGS) technology, RNA sequencing (RNA-seq) has not only allowed for the measurement of the expression levels of known transcript targets but has also made it possible to obtain information on the entire transcriptome, including previously unknown transcripts and transcript variants, such as non-coding RNAs, in a specific environment. For these reasons, RNA-seq is increasingly prevalent in microbiome research and finds applications in various fields, including gene expression analysis, identification of highly active microbial community members, discovery of regulatory factors, investigation of microbial interactions, and studies on interactions with hosts.

Based on these requirements, RNA-seq is being increasingly utilized in microbiome research. In this Standard Operating Procedure (SOP), we aim to describe reference-guided metatranscriptome analysis and reference-independent metatranscriptome analysis methods based on mapping RNA-seq reads to de novo assembled contigs and metagenome-assembled genomes (MAGs) obtained from metagenomes.

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_0_2.png?raw=true" style="width:65%">
  <figcaption><b>Reference-guided and reference-independent metatranscriptome analysis methods</b></figcaption>  
</figure>

Before diving into this comprehensive SOP, various tools that can be utilized for metatranscriptome analysis are introduced. In addition to the tools presented in this SOP, other tools listed in Table 1 or similar tools with similar purposes can be selectively applied at each step.

**Table 1. List of available RNA-seq analysis tools**
<table>
<thead>
  <tr>
    <th>Category</th>
    <th>Tools</th>
    <th>Description</th>
    <th>Year</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="3">Trimming</td>
    <td><a href="https://cutadapt.readthedocs.io/en/stable/">cutadapt</a></td>
    <td>5' adaptor trimming</td>
    <td>2011</td>
  </tr>
  <tr>
    <td><a href="https://github.com/FelixKrueger/TrimGalore">TrimGalore</a></td>
    <td>Wrapper around Cutadapt and FastQC<br>paired-end trimming</td>
    <td>2013</td>
  </tr>
  <tr>
    <td><a href="http://www.usadellab.org/cms/?page=trimmomatic">trimmomatic</a></td>
    <td>Paired-end trimming</td>
    <td>2014</td>
  </tr>
  <tr>
    <td rowspan="5">Alignment</td>
    <td><a href="https://bowtie-bio.sourceforge.net/bowtie2/manual.shtml">bowtie2</a></td>
    <td>Short read mapping, local alignment, use FM-index algorithm</td>
    <td>2012</td>
  </tr>
  <tr>
    <td><a href="https://github.com/lh3/bwa">BWA</a></td>
    <td>Low-divergent sequences mapping, need genome reference, use BWT and FM index algorithm</td>
    <td>2009</td>
  </tr>
  <tr>
    <td><a href="https://daehwankimlab.github.io/hisat2/manual/">HiSat2</a></td>
    <td>Highly useful for human data analysis. Utilized in tasks like Human Leukocyte Antigen (HLA) typing and DNA fingerprinting. Use the FM index.</td>
    <td>2019</td>
  </tr>
  <tr>
    <td><a href="https://github.com/alexdobin/STAR">STAR</a></td>
    <td>Improve <em>de novo</em> RNA-seq analysis and allow for the mapping of long-read mRNA data.</td>
    <td>2013</td>
  </tr>
  <tr>
    <td><a href="https://ccb.jhu.edu/software/tophat/manual.shtml">TopHat2</a></td>
    <td>Bowtie-based short read mapping</td>
    <td>2013</td>
  </tr>
  <tr>
    <td rowspan="6">DE analysis</td>
    <td><a href="https://cole-trapnell-lab.github.io/cufflinks/manual/">Cuffdiiff2</a></td>
    <td>cufflink-associated tool. utilize sam(bam)file to compare gene and isoform expression </td>
    <td>2013</td>
  </tr>
  <tr>
    <td><a href="https://bioconductor.org/packages/release/bioc/html/DESeq2.html">DESeq2</a></td>
    <td>R package, employ shrinkage estimation techniques and utilizes RLE (Relative Log Expression) normalization.</td>
    <td>2014</td>
  </tr>
  <tr>
    <td><a href="https://bioconductor.org/packages/release/bioc/html/edgeR.html">EdgeR</a></td>
    <td>R package, Use raw count value as input file. TMM(Trimmed Mean M-values) normalization »ç¿ë</td>
    <td>2010</td>
  </tr>
  <tr>
    <td><a href="https://bioconductor.org/packages/release/bioc/html/limma.html">limma</a></td>
    <td>R package. Effective for a small number of samples, using TMM normalization</td>
    <td>2015</td>
  </tr>
  <tr>
    <td><a href="https://www.bioconductor.org/packages/release/bioc/html/NOISeq.html">NOISeq</a></td>
    <td>R package. Using a nonparametric approach and an RPKM/TMM/uppartile normalization approach</td>
    <td>2011</td>
  </tr>
  <tr>
    <td><a href="https://github.com/jefferys/SamSeq">SAMSeq</a></td>
    <td>R package. Gene-level DE analysis using sam file as input file. Normalization based on the mean value of the total count</td>
    <td>2013</td>
  </tr>
  <tr>
    <td rowspan="3"><em>de novo</em> assembly</td>
    <td><a href="https://github.com/voutcn/megahit">megahit</a></td>
    <td>Single genome assembly, Multiple library analysis is possible</td>
    <td>2015</td>
  </tr>
  <tr>
    <td><a href="https://cab.spbu.ru/software/spades/">SPAdes</a></td>
    <td>Various types of data, such as RNA, virus RNA, plasmid, etc., can be assembled. Not only fastq, fasta files but also bam files can be inputted</td>
    <td>2012</td>
  </tr>
  <tr>
    <td><a href="https://github.com/trinityrnaseq/trinityrnaseq/wiki">trinity</a></td>
    <td>Transcriptome assembler</td>
    <td>2011</td>
  </tr>
  <tr>
    <td rowspan="4">Taxonomy assignment</td>
    <td><a href="https://bioinformatics-centre.github.io/kaiju/">kaiju</a></td>
    <td>Analyze the entire sequence of the meta-genome or the sequence of the meta-transcript using the GenBank protein-redundant database</td>
    <td>2016</td>
  </tr>
  <tr>
    <td><a href="https://ccb.jhu.edu/software/kraken/MANUAL.html">kraken</a></td>
    <td>Tazonomy analysis using GenBank nucleotide non-redundant database</td>
    <td>2014</td>
  </tr>
  <tr>
    <td><a href="https://huttenhower.sph.harvard.edu/metaphlan3/">MetaPhlAn</a></td>
    <td>Analysis of microbial composition from meta-genetic information at species level. Use your own marker genes</td>
    <td>2012</td>
  </tr>
  <tr>
    <td><a href="https://www.onecodex.com/">onecodex</a></td>
    <td>Web-based analysis tool using Genome database and targeted loci database</td>
    <td>2015</td>
  </tr>
  <tr>
    <td rowspan="4">Format transition</td>
    <td><a href="https://bedtools.readthedocs.io/en/latest/">BEDTools</a></td>
    <td>Software using bam or bed files. Raw count value can be obtained, but a candidate is required</td>
    <td>2010</td>
  </tr>
  <tr>
    <td><a href="https://cole-trapnell-lab.github.io/cufflinks/manual/">Cufflink</a></td>
    <td>Tool that assembles RNA-seq mapping results (sam file) and calculates an unbalance haved FPKM value as result</td>
    <td>2010</td>
  </tr>
  <tr>
    <td><a href="https://htseq.readthedocs.io/en/release_0.11.1/index.html">HTSeq</a></td>
    <td>Python package, calculation of read mapping using gff information</td>
    <td>2015</td>
  </tr>
  <tr>
    <td><a href="https://www.htslib.org/">SAMTools</a></td>
    <td>Software that converts or sorts sam files</td>
    <td>2009</td>
  </tr>
</tbody>
</table>