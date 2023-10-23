# Transcript taxonomy classification

In metatranscriptome analysis, just as taxonomy profiling is conducted in metagenome analysis, performing taxonomy assignment based on reads or contigs allows us to obtain information about microorganisms actively expressing themselves in the environment.  
In addition to the approach using the Kaiju tool, which is introduced in the metagenome SOP, there's a simple method for taxonomy analysis available through the [One Codex](https://www.onecodex.com/) web server.
The One Codex website accepts fasta or fastq files as input data and provides results accordingly.
For taxonomy analysis, One Codex employs its own database containing over 110,000 genomes and targeted loci databases such as 16S, 5S, 23S, gyrB, ITS, and more.  

![one codex reference database](https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_10_1.png?raw=true)
> one codex refernce database 

![one codex results](https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_10_2.png?raw=true)
> example of taxonomy assignment results using the One Codex web server.

You can compare taxonomy information not only at the DNA level but also from RNA data.
If you have metagenomic information, it can be used for reference. In cases where metagenomic information is unavailable, you can verify taxonomy at the RNA level.
The analysis results allow for visualization of cluster composition and read count ratios at each taxonomy level, from phylum to species. Additionally, a taxonomy chart reflecting hierarchical taxonomy levels is available for examination.
