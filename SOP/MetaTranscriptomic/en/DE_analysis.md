# Differential (transcriptional) expression analysis 

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_8_1.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>  
</figure>

*To perform the following analysis, you should have the same gene set.

By using metatranscriptomic data from different environmental conditions, you can analyze the differences in gene expression based on the specific environmental conditions and obtain information on which genes are up- or down-regulated in each condition. To achieve this, DESeq2 is run using count information generated from the alignment results and functional annotation locus tags.
However, for DESeq2 to work, you need count information and input files for each sample's metadata.
The metadata information can be used in DEG (Differentially Expressed Gene) analysis and various visualization steps.

```bash
#Download FormatDESeqInput.py
$wget https://raw.githubusercontent.com/sujin9819/ngs/main/R_scripts/coverage.R
#make DESeq2 input file
$Rscript coverage.R –r $sample 
#Outputs a result corresponding to the sample keyword
```
`make design sheet(text파일 생성)`  
`File name: Design_Sheet.txt  `  
| Sample | Condition |
| --- | --- |
| cov1 | Control group |
| cov2 | Control group |
| cov3 | Experimental group |
| cov4 | Experimental group |
 

The following DESeq2 code allows you to obtain normalized count values for each gene and DESeq results from comparisons between groups. Genes with a Log2 Fold Change > 1 or < -1 and a p-value < 0.05 are selected. This information enables you to assess differences in gene expression between different environments and explore the similarity between samples, such as PCoA and α-diversity based on each RNA sample. You can visualize this data through clustering, PCoA plots, and other visual representations.
```R
#install DESeq2 package
if (!requireNamespace("BiocManager", quietly = TRUE))
    install.packages("BiocManager")
BiocManager::install("DESeq2")
```

```bash
#DESeq2 running
#R script download
$wget https://raw.githubusercontent.com/sujin9819/ngs/main/R_scripts/RunDESeq_flow.R
$ Rscript RunDESeq_flow.R –i $sample.count –d Design_sheet.txt –o output_directory     
```

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_8_2.png?raw=true" style="width:90%">
  <figcaption><b>Example of output file using RunDESeq_flow.R</b></figcaption>  
</figure>

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_8_3.png?raw=true" style="width:90%">
  <figcaption><b>Example of results using RunDESeq_flow.R</b></figcaption>  
</figure>

Moreover, you can utilize R packages to visualize information related to gene expression, including normalized count data, Log2 Fold Change, and p-values, through visualizations like heatmaps and volcano plots.