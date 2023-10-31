# Preprocessing of the sequencing reads

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_5_1.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>  
</figure>

## Short reads

For quality control of raw sequence data, two crucial steps are (1) removing low-quality bases and (2) eliminating artifacts such as barcodes, adaptors, and chimeras.
[KneadData](https://huttenhower.sph.harvard.edu/kneaddata) employs [Trimmomatic](http://www.usadellab.org/cms/index.php?page=trimmomatic) for quality filtering and trimming and Tandem Repeat Finder (TRF) for read preprocessing.
Additionally, it utilizes [Bowtie2](https://bowtie-bio.sourceforge.net/bowtie2/manual.shtml) for FastQC analysis and read alignment.
When using Trimmomatic, you can specify the minimum length of the sequence as a percentage of the input read with the `--trimmomatic-options='MINLEN:'` parameter.
```bash
# Downlodad host genome (ex.Human)
$ conda activate kneaddata
$ mkdir hostgenome
$ kneaddata_database --download human_genome bowtie2 hostgenome/
$ kneaddata --input1 input/seq1.fastq --input2 input/seq2.fastq --reference-db hostgenome/ --output kneaddataOutputPairedEnd --trimmomatic-options="MINLEN:90"  
$ conda deactivate
```
▶Example of KneadData output
<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_5_2.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>  
</figure>

▶Example of Output files
1. seq.kneaddata_human_genome_bowtie2_contam.fastq 
: Contaminant reads aligned to the human genome
2. seq.kneaddata.fastq 
: Reads not aligned to the human genome
3. seq.kneaddata.trimmed.fastq 
: trimmed reads
4. seq.kneaddata.log
: log file


## Long reads

The mapping methods typically employed for short reads are not well-suited for long reads.
Short reads are commonly mapped using the seed-and-extend method, which extends based on single base matches.
However, long reads require multiple consistent matches across the read for accurate alignment.
When seed-and-extend methods are applied to long reads, issues with extension and alignment accuracy can arise.
To address these challenges, alternative methods like seed-and-chain have been developed.

[minimap2](https://github.com/lh3/minimap2) is a versatile sequence mapping program that is effective for aligning and analyzing long reads such as PacBio and Oxford Nanopore technologies.
In this pipeline, we will use minimap2 for long read mapping.

```bash
$ conda install -c bioconda minimap2
$ conda activate minimap2
# General usage of minimap2
# minimap2 –ax map-hifi ref.fa query.fq > alignment.sam
$ minimap2 -ax map-hifi GCF_000001405.40_GRCh38.p14_genomic.fna N_008_HiFi.fastq.gz > N008.aln.sam
# Convert sam files to bam files
$ samtools view -Sb N008.aln.sam > N008.aln.bam 
# remove host genome aligned read
$ samtools view -bf 0x04 N008.aln.bam > N008.aln.unmapped.bam
# convert bam files to fastq
$ samtools bam2fq N008.aln.unmapped.bam > N008.aln.unmapped.fq
```