# Ribosome profiling

[plotVisualRibo.R](https://github.com/bhattlab/bhattlab_workflows/tree/master/metariboseq) 스크립트를 활용하여 .bam 파일과 메타유전체 분석 결과 얻은 결과 fasta파일을 input 파일로 활용하여  결과를 얻을 수 있다. (Linux 환경 권장) 

```R
#install RiboseqR
if (!requireNamespace("BiocManager", quietly = TRUE))
    install.packages("BiocManager")
BiocManager::install("RiboseqR")
```
```bash
#ribo-seq running
#file download in https://github.com/bhattlab/bhattlab_workflows/tree/master/metariboseq
$ Rscript plotVisualRibo.R final.contigs.fa sample_metariboseq.bam
```
결과적으로 allFSshift.pdf, histogram.pdf, plotCDS(28/31/35}filt.pdf의 5종류의 파일이 생성되고, 그 중 allFSshift.pdf 결과를 통해 codon의 주기성에 대한 frame정보를 및 각 frame의 비율을 확인 할 수 있다.

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaProteomic/img/P_7_1.png?raw=true" style="width:90%">
  <figcaption><b>plotVisualRibo.R 결과 파일 중 allFSshift.pdf 파일 예시</b></figcaption>  
</figure>

위 그림에서 (allFSshift.pdf의 파일 예시) x축은 footprint(size)를, y축은 reads 개수를 나타낸다.
각 CDS에서 유전자 염기서열이 codon이 되는 주기성을 예측하기위한 지표로 사용된다.
어떤 frame으로 묶이는지 여부에 따른 ribosome-bound mRNA의 footprint를 capture정도를 확인 가능하다.
이러한 주기성에 대한 결과 값은 미생물 종마다 다른 양상을 보인다고 알려져 있다. 

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaProteomic/img/P_7_2.png?raw=true" style="width:90%">
  <figcaption><b>plotVisualRibo.R 결과 파일 중 hisogram.pdf(왼쪽)와 plotCDSfilt.pdf(오른쪽) 파일 예시</b></figcaption>  
</figure>  

Histogram.pdf 결과는 reads의 길이와 alignment 되는 비율을 나타낸 그래프로, 특정 길이의 reads가 많이 존재하는지의 여부와 얼마만큼의 비율로 존재하는지 확인이 가능하다.
plotCDSfilt.pdf파일들은 ribosome이 결합하는 크기(footprint size)인 28, 31, 35 일 때 각각 3개의 pdf파일이 결과로 나오며 RNA-seq결과와 다르게 ribo-seq결과는 start 코돈과 stop 코돈에 강한 signal을 보인다.
이는 ribosome이 mRNA를 단백질로 합성할 때의 특징과 관련이 있다.
리보솜이 mRNA를 인식하여 번역을 준비하는 단계와 번역이 끝나고 stop codon에 위치하게 되는 시간이 긴 편으로 start와 stop에 강한 signal을 보이게 된다. 

이러한 정보들을 이용하여 ribosome-bound mRNA의 count값을 얻을 수 있다.
이 count값을 얻어 번역 당시에 ribosome의 위치 정보와 그 위치에 있는 비율에 대해 얻을 수 있다. 그리고 이러한 ribosome 정보를 이용하여 단백질의 합성과 관련된 정보를 직간접적으로 얻을 수 있다.
그러나 ribosome-bound mRNA의 정보만으로 분석하기보다는 transcriptome 정보와 상호 보완하면서 분석 하는 것이 더 좋은 결과를 도출할 수 있다. 


<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaProteomic/img/P_7_3.png?raw=true" style="width:90%">
  <figcaption><b>Predicted translation efficiency</b></figcaption>  
</figure>
