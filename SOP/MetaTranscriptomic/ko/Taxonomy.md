# Transcript taxonomy classification

메타유전체분석에서 taxonomy profiling이 이루어지는 것과 마찬가지로 메타전사체 데이터를 활용하여 read 혹은 contig 기반의 taxonomy assignment를 수행하면 환경에서active하게 발현하는 microorganism의 정보를 얻을 수 있다.  
메타유전체 SOP에서 소개된 Kaiju 툴을 활용한 방식이 아닌, 간단한 방법으로 taxonomy 분석이 가능한 [One codex](https://www.onecodex.com/) 웹서버를 소개하고자 한다.
One codex 사이트는fasta 파일이나 fastq 파일을 input 데이터로 결과를 도출할 수 있다. Taxonomy 분석에는 one codex에서 자체적으로 구축한 11만여개의 유전체 정보로 이루어진 자체 database 및 16S, 5S, 23S, gyrB, ITS 등의 targeted loci database가 사용된다. 

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_10_1.png?raw=true" style="width:75%">
  <figcaption><b>One codex reference database</b></figcaption>  
</figure>

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_10_2.png?raw=true" style="width:90%">
  <figcaption><b>One codex 웹서버를 활용한 taxonomy assignment 결과 예시</b></figcaption>  
</figure>

DNA 수준에서뿐만 아니라 RNA 정보에서의 taxonomy를 확인하여 비교한다. 메타유전체 정보가 있으면 참고용으로, 메타유전체 정보가 없는 경우 RNA 수준에서의 taxonomy를 확인 할 수 있다.
분석 결과 phylum부터 species에 이르는 각 taxonomy level에서의 군집 조성 및 이들의 read count비율을 포함한 정보까지 시각화가 가능하며, taxonomy 계층이 반영된 taxonomy chart또한 확인할 수 있다. 