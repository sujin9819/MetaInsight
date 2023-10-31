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
    <td>5' adaptor trimming 가능</td>
    <td>2011</td>
  </tr>
  <tr>
    <td><a href="https://github.com/FelixKrueger/TrimGalore">TrimGalore</a></td>
    <td>cutadapt기반의 trimming 프로그램<br>paired-end trimming가능</td>
    <td>2013</td>
  </tr>
  <tr>
    <td><a href="http://www.usadellab.org/cms/?page=trimmomatic">trimmomatic</a></td>
    <td>Paired-end trimming 가능</td>
    <td>2014</td>
  </tr>
  <tr>
    <td rowspan="5">Alignment</td>
    <td><a href="https://bowtie-bio.sourceforge.net/bowtie2/manual.shtml">bowtie2</a></td>
    <td>Short read mapping, local alignment, FM-index algorithm 사용</td>
    <td>2012</td>
  </tr>
  <tr>
    <td><a href="https://github.com/lh3/bwa">BWA</a></td>
    <td>Low-divergent sequences mapping, genome reference필요, BWT및 FM index algorithm 사용</td>
    <td>2009</td>
  </tr>
  <tr>
    <td><a href="https://daehwankimlab.github.io/hisat2/manual/">HiSat2</a></td>
    <td>Human 데이터 분석에 활용도가 높음. Human Leukocyte Antigen(HLA)타이핑 및 DNA 지문 채취 등에 이용, FM index 사용</td>
    <td>2019</td>
  </tr>
  <tr>
    <td><a href="https://github.com/alexdobin/STAR">STAR</a></td>
    <td><em>de novo</em> RNA-seq 문제 보완 및 long read mRNA mapping 가능</td>
    <td>2013</td>
  </tr>
  <tr>
    <td><a href="https://ccb.jhu.edu/software/tophat/manual.shtml">TopHat2</a></td>
    <td>bowtie 기반의 short read mapping</td>
    <td>2013</td>
  </tr>
  <tr>
    <td rowspan="6">DE analysis</td>
    <td><a href="https://cole-trapnell-lab.github.io/cufflinks/manual/">Cuffdiiff2</a></td>
    <td>cufflink 연계 tool. sam(bam)파일을 이용하여 gene, isoform 수준에서 발현 비교 </td>
    <td>2013</td>
  </tr>
  <tr>
    <td><a href="https://bioconductor.org/packages/release/bioc/html/DESeq2.html">DESeq2</a></td>
    <td>R package, shrinkage estimation 기법을 이용. RLE(Relative Log Expression) normalization 사용</td>
    <td>2014</td>
  </tr>
  <tr>
    <td><a href="https://bioconductor.org/packages/release/bioc/html/edgeR.html">EdgeR</a></td>
    <td>R package, input파일로 raw count값을 사용. TMM(Trimmed Mean M-values) normalization 사용</td>
    <td>2010</td>
  </tr>
  <tr>
    <td><a href="https://bioconductor.org/packages/release/bioc/html/limma.html">limma</a></td>
    <td>R package. 적은 수의 표본에 대해서 효과적이며 TMM normalization 사용</td>
    <td>2015</td>
  </tr>
  <tr>
    <td><a href="https://www.bioconductor.org/packages/release/bioc/html/NOISeq.html">NOISeq</a></td>
    <td>R package. 비모수적 접근 방식 및 RPKM/TMM/upper quartile normalization방식 사용</td>
    <td>2011</td>
  </tr>
  <tr>
    <td><a href="https://github.com/jefferys/SamSeq">SAMSeq</a></td>
    <td>R package. sam 파일을 input파일로 사용하는 gene-level DE분석. 전체 count의 mean값을 기준으로 normalization 진행</td>
    <td>2013</td>
  </tr>
  <tr>
    <td rowspan="3"><em>de novo</em> assembly</td>
    <td><a href="https://github.com/voutcn/megahit">megahit</a></td>
    <td>Single genome assembly, multiple libraries 가능</td>
    <td>2015</td>
  </tr>
  <tr>
    <td><a href="https://cab.spbu.ru/software/spades/">SPAdes</a></td>
    <td>RNA, virus RNA, plasmid등 다양한 종류의 data assembly가능. fastq, fasta파일 뿐만 아니라 bam파일 input가능</td>
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
    <td>메타유전체의 전체 서열 또는 메타전사체의 서열을 GenBank protein non-redundant database를 이용하여 분석</td>
    <td>2016</td>
  </tr>
  <tr>
    <td><a href="https://ccb.jhu.edu/software/kraken/MANUAL.html">kraken</a></td>
    <td>GenBank nucleotide non-redundant database를 이용하여 taxonomy 분석</td>
    <td>2014</td>
  </tr>
  <tr>
    <td><a href="https://huttenhower.sph.harvard.edu/metaphlan3/">MetaPhlAn</a></td>
    <td>종 수준에서 메타유전체 정보로부터 미생물 조성 분석. 자체적인 marker gene을 이용</td>
    <td>2012</td>
  </tr>
  <tr>
    <td><a href="https://www.onecodex.com/">onecodex</a></td>
    <td>Genome database와 targeted loci database를 이용한 web 기반 분석 도구</td>
    <td>2015</td>
  </tr>
  <tr>
    <td rowspan="4">Format transition</td>
    <td><a href="https://bedtools.readthedocs.io/en/latest/">BEDTools</a></td>
    <td>bam 또는 bed 파일을 이용하는 소프트웨어. Raw count값을 얻을 수 있지만 후보정이 필요</td>
    <td>2010</td>
  </tr>
  <tr>
    <td><a href="https://cole-trapnell-lab.github.io/cufflinks/manual/">Cufflink</a></td>
    <td>RNA-seq mapping결과(sam파일)를 assembly하고 abundance를 계산하는 도구로 FPKM값을 결과값으로 가짐</td>
    <td>2010</td>
  </tr>
  <tr>
    <td><a href="https://htseq.readthedocs.io/en/release_0.11.1/index.html">HTSeq</a></td>
    <td>Python package, gff정보를 이용한 read mapping 계산</td>
    <td>2015</td>
  </tr>
  <tr>
    <td><a href="https://www.htslib.org/">SAMTools</a></td>
    <td>sam 파일을 변환하거나 sorting하는 소프트웨어</td>
    <td>2009</td>
  </tr>
</tbody>
</table>