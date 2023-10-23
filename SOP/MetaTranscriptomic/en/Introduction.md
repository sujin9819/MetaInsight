# Next-Generation Sequencing (NGS)-based Microbiome Transcriptome Analysis SOP


## Metatranscriptome introduction

The term microbiome refers to the concept encompassing a community of microorganisms (microbiota) residing in a particular environment, along with their complete genetic information. Microbiome research traditionally involves the amplification and sequencing of conserved regions of marker genes, such as ribosomal genes, from environmental DNA using PCR, allowing for the identification of the types of microorganisms present in the environment. In contrast, microbiome research utilizes whole DNA sequence analysis, known as metagenome sequencing, which not only identifies the types of microorganisms present in the environment but also enables the exploration of the genetic diversity and functions possessed by these microorganisms. However, metagenomic (metagenome) data can inform about the presence or absence of specific species or genes but cannot determine whether they are active within the microbiome ecosystem, posing limitations.

![Metatranscriptomics overview](https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_0_1.png?raw=true)
> Multi-omics information-based microbiome functional analysis  

To investigate how microbial communities respond to environmental changes, metatranscriptome analysis has been initiated, and metatranscriptomic information will play a crucial role in understanding the ecology of the microbiome. Even before the advent of high-throughput DNA sequencing methods, research has been conducted to measure the expression levels of genes of interest using qPCR and to study the expression patterns of known transcripts from specific organisms using microarray technology. With the widespread adoption of Next-Generation Sequencing (NGS) technology, RNA sequencing (RNA-seq) has not only allowed for the measurement of the expression levels of known transcript targets but has also made it possible to obtain information on the entire transcriptome, including previously unknown transcripts and transcript variants, such as non-coding RNAs, in a specific environment. For these reasons, RNA-seq is increasingly prevalent in microbiome research and finds applications in various fields, including gene expression analysis, identification of highly active microbial community members, discovery of regulatory factors, investigation of microbial interactions, and studies on interactions with hosts.

Based on these requirements, RNA-seq is being increasingly utilized in microbiome research. In this Standard Operating Procedure (SOP), we aim to describe reference-guided metatranscriptome analysis and reference-independent metatranscriptome analysis methods based on mapping RNA-seq reads to de novo assembled contigs and metagenome-assembled genomes (MAGs) obtained from metagenomes.

![Metatranscriptomics overview](https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_0_2.png?raw=true)
> Reference-guided and reference-independent metatranscriptome analysis methods

Before diving into this comprehensive SOP, various tools that can be utilized for metatranscriptome analysis are introduced. In addition to the tools presented in this SOP, other tools listed in Table 1 or similar tools with similar purposes can be selectively applied at each step.

**Table 1. List of available RNA-seq analysis tools**
<table>
<thead>
  <tr>
    <th>1</th>
    <th>2</th>
    <th>3</th>
    <th>4</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="3"></td>
    <td>d</td>
    <td>d</td>
    <td>d</td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td>d</td>
  </tr>
  <tr>
    <td></td>
    <td>d</td>
    <td></td>
  </tr>
</tbody>
</table>