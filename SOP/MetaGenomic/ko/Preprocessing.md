# Preprocessing of the sequencing reads

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_5_1.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>  
</figure>

## Short reads

Raw sequence data의 quality control 작업을 위해서는 (1) low quality bases 제거, (2) Artifact 제거 (barcodes, adaptors, chimeras)가 이루어져야 한다.
[KneadData](https://huttenhower.sph.harvard.edu/kneaddata) 는 [Trimmomatic](http://www.usadellab.org/cms/index.php?page=trimmomatic) (quality filtering/trimming)과 Tandem Repeat Finder (TRF), 그리고 FastQC 와 read align을 위한 [Bowtie2](https://bowtie-bio.sourceforge.net/bowtie2/manual.shtml)를 사용하여 read preprocessing을 진행한다.
Trimmomatic 진행 시 `--trimmomatic-options="MINLEN:"`을 통해 서열길이의 최소길이를 input read의 percentage로 지정할 수 있다.

```bash
# Downlodad host genome (ex.Human)
$ conda activate kneaddata
$ mkdir hostgenome
$ kneaddata_database --download human_genome bowtie2 hostgenome/
$ kneaddata --input1 input/seq1.fastq --input2 input/seq2.fastq --reference-db hostgenome/ --output kneaddataOutputPairedEnd --trimmomatic-options="MINLEN:90"  
$ conda deactivate
```
▶kneaddata output예시
<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_5_2.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>  
</figure>

▶Output files 예시
1. seq.kneaddata_human_genome_bowtie2_contam.fastq 
: reference database에서 human genome에 align된 contaminant reads
2. seq.kneaddata.fastq 
: reference database에 align 되지 않은 reads
3. seq.kneaddata.trimmed.fastq 
: trimmed reads
4. seq.kneaddata.log
: log 파일

## Long reads

Short read에서 사용되는 mapping 방법은 long read에서는 적합하지 않다. Short read의 mapping에는 주로 seed-and-extend 방법을 통해 mapping이 이루어진다. Seed-and-extend 방법은 일반적으로 단일 base의 일치를 기반으로 확장(extend)하는데 long read 에서는 read 전체에서 여러 일관된 일치가 필요하기 때문에 long read에서의 seed-and-extend 방법의 적용은 연장과 정확성에 문제가 발생할 수 있다.
이러한 한계를 극복하기 위해 seed-and-chain과 같은 방법이 개발되었다.   
[minimap2](https://github.com/lh3/minimap2)는 다목적 시퀀스 mapping 프로그램으로서,  PacBio와 Oxford Nanopore technologies와 같은 긴 리드를 정렬하고 분석하는데 효과적이다. 본 파이프라인에서는 minimap2를 사용하여 long read mapping을 진행하고자 한다.

```bash
$ conda install -c bioconda minimap2
$ conda activate minimap2
# General usage of minimap2
# minimap2 –ax map-hifi ref.fa query.fq > alignment.sam
$ minimap2 -ax map-hifi GCF_000001405.40_GRCh38.p14_genomic.fna N_008_HiFi.fastq.gz > N008.aln.sam
# sam파일를 bam파일로 변환
$ samtools view -Sb N008.aln.sam > N008.aln.bam 
# host genome aligned read 제거
$ samtools view -bf 0x04 N008.aln.bam > N008.aln.unmapped.bam
# bam파일을 fastq파일로 변환

```