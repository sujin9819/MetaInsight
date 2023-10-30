# Differential (transcriptional) expression analysis 

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_8_1.png?raw=true" style="width:90%">
  
</figure>


*다음과 같은 분석을 진행하기 위해서는 동일한 유전자세트를 가져야 함  
서로 다른 환경 조건의 메타전사체 데이터로부터 환경 조건에 따른 발현량 차이를 분석 할 수 있고, 각 환경 조건에서 up- or down- regulation 되는 유전자 정보를 확보할 수 있다.  
Alignment 결과로 생성된 count정보와 functional annotation locus tag를 이용해서 DESeq2 running을 진행한다. 그러나 DESeq2을 진행하기 위해서는 count정보와 각 샘플 정보(metadata) input파일이 필요하다. DEG 정보와 기타 시각화 과정에서 해당 metadata정보가 활용될 수 있다.


```bash
#Download FormatDESeqInput.py
$wget https://raw.githubusercontent.com/sujin9819/ngs/main/R_scripts/coverage.R
#make DESeq2 input file
$Rscript coverage.R –r $sample 
#sample 키워드에 해당하는 결과가 출력
```
`make design sheet(text파일 생성)`  
`File name: Design_Sheet.txt  `  
| Sample | Condition |
| --- | --- |
| cov1 | Control group |
| cov2 | Control group |
| cov3 | Experimental group |
| cov4 | Experimental group |
 
아래의 DESeq2 코드로는 각 유전자의 normalization된 count값과 그룹간 비교하여 나온 DESeq결과 값을 얻을 수 있다. Log2 Fold change >1또는 < -1이며, p-value < 0.05인 값들만 선정하여 각 환경에서의 발현 양 차이와 PCoA와 같은 각 RNA샘플에 따른 α-diversity등 샘플간의 유사성도 확인할 수 있으며, clustering 혹은 PCoA plot 등으로 시각화 가능하다.

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
  <figcaption><b>RunDESeq_flow.R 결과 파일 예시</b></figcaption>  
</figure>

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_8_3.png?raw=true" style="width:90%">
  <figcaption><b>RunDESeq_flow.R 결과 파일을 이용하여 얻을 수 있는 결과 예시</b></figcaption>  
</figure>

뿐만 아니라 normalization을 거친 count 정보, Log2 Fold change, p-value와 같은 DESeq2 결과 값들을 R의 다양한 패키지를 이용하여 heatmap, volcano plot등을 통해 발현량 대한 정보를 시각화 하는 것이 가능하다. 