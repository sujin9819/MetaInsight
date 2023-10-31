# Preprocessing of the sequencing reads

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_5_1.png?raw=true" style="width:90%">
  <figcaption><b>Preprocessing of sequencing reads</b></figcaption>  
</figure>

To utilize raw sequence data for analysis, it's necessary to go through a process of removing low-quality bases and eliminating adaptors. This process results in enhanced sequence quality and an increased mapping rate.
The Kneaddata program makes it easy to remove adaptor sequences used in Illumina platform-based sequencing and host genome sequences.

```bash
#host RNA removal and trimming
$ kneaddata --input sample_1.fastq.gz --input sample_2.fastq.gz --reference-db hg37dec_v0.1 --output ./1.Trim/sample --trimmomatic /where/to/Trimmomatic-0.36/ --trimmomatic-options="MINLEN:90" 
#--trimmomatic option; trimmomatic path
```

You can use the FastQC program to compare the quality of sequence reads before and after preprocessing, allowing you to verify the trimming results. FastQC provides comprehensive information about the fastq files, including parameters such as per base sequence quality, per sequence QC content, per sequence quality score, sequence length distribution, and more, to assess the outcomes of trimming.

```bash
#FastQC running(java script)
$./fastqc
#check fastq file with java
```

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_5_2.png?raw=true" style="width:90%">
  <figcaption><b>Example of quality check results of raw sequence with FastQC</b></figcaption>  
</figure>
