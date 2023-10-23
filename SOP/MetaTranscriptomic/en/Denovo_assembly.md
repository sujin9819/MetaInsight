# Transcript _de novo_ assembly

In addition to the reference-guided approach, there is valuable information that can be obtained through a reference-independent analysis in metagenome analysis.
Performing de novo assembly using metatranscriptomic data allows for the extraction of (putative) transcriptional segment information.

The program used for assembly is called SPAdes, which supports various types of data, and the command options vary depending on the input data.
When working with metagenome data, metaSPAdes (or `--meta`) is used, while rnaSPAdes is employed for *de novo* assembly using RNA-seq reads. 
It's worth noting that SPAdes can be used for a wide range of input data types, including plasmid, metaplasmid, RNA virus data, and more.


```bash
#install SPAdes
$wget http://cab.spbu.ru/files/release3.15.3/SPAdes-3.15.3-Linux.tar.gz
$tar -xzf SPAdes-3.15.3-Linux.tar.gz
$cd SPAdes-3.15.3-Linux/bin/
#SPAdes running
#RNA single ends
$spades.py –-rna –s single_end_trimmed.fastq –o sample
#RNA paired ends
$spades.py –-rna –1 forward_trimmed.fastq -2 reverse_trimmed.fastq –o sample
```
