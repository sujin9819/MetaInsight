# Transcriptional expression profiling

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_7_1.png?raw=true" style="width:65%">
  <figcaption><b> </b></figcaption>  
</figure>


RNA-seq read alignment결과 count 정보를 이용하여 각 유전자의 발현량을 확인할 수 있다.
더 나아가 각 유전자뿐만 아니라 메타유전체 결과 얻어진 de novo assembly로 생성된 개별 contig 또는 개별 MAG의 발현 정보를 얻는 것도 가능하다.
그리고, 좀 더 체계적인 분석을 위하여 경우에 따라서는 비슷한 기능을 가진 유전자들을 카테고리 별로 분류하거나 혹은 특정 대사경로(metabolic pathway)에 관여하는 유전자들을 묶어서 그들의 발현량을 분석해야 할 필요성이 존재한다.
이를 위해서는 functional database에 대한 각 CDS들의 annotation정보가 필요한데, [eggNOG-mapper](https://github.com/eggnogdb/eggnog-mapper)를 활용하면 이러한 정보를 수월하게 얻을 수 있다.
eggNOG-mapper는 input 파일로 각 유전자의 아미노산 서열이 나열되어진 `.faa` 파일이 요구되며, default option으로 running 하였을 때 각 유전자의 아미노산 서열을 blast하여 가장 유사한 [COG(Clusters of Orthologous Groups)](https://www.ncbi.nlm.nih.gov/research/cog-project/), [KEGG(Kyoto Encyclopedia of Genes and Genomes)](https://www.genome.jp/kegg/), [CAZy(Carbohydrate-Active EnZymes)](http://www.cazy.org/), [Pfam](http://pfam.xfam.org/)정보를 도출한다.

```bash
# download eggnog-mapper from https://github.com/eggnogdb/eggnog-mapper/releases/latest
$ tar -xvzf eggnog_mapper_(version).tar.gz
# download eggnog-mapper database
$ download_eggnog_data.py
# run eggnog-mapper
$ emapper.py (option) -i sample_MAG.prodigal.faa -o sample_MAG.eggnog.out
```
결과 파일로는 eggnog.out.hit, eggnog.out.annotation, eggnog.out.seed_ortholog이 생성되며, 이 중 eggnog.out.annotation 파일이 COG, KEGG등 다양한 database의 annotation정보를 담고있다. 

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_7_2.png?raw=true" style="width:90%">
  <figcaption><b>EGGNOG-mapper 결과 중 annotation 파일 예시</b></figcaption>  
</figure>


EGGNOG-mapper결과로 도출된 COG정보를 활용하여, 전체 메타전사체에서 각 COG functional category의 발현 정도를 예측 가능하다. 

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_7_3.png?raw=true" style="width:90%">
  <figcaption><b>COG 분포에 대한 예시</b></figcaption>  
</figure>


또한 도출된 COG 혹은 KEGG ORTHOLOGY 정보를 KEGG mapper, [IPATH3](https://pathways.embl.de/)등의 툴을 활용하여 시각화가 가능하며, 발현량이 높은 유전자의 전체적인 상관관계를 유추 할 수 있다. 간단히 count값이 높은 유전자 몇 개만 선택해서 하거나 count값, 즉 발현량에 따라 선 굵기를 설정하거나 MAG별로 다른 색으로 표시하는 등 옵션에 따라 다양한 결과를 얻을 수 있다. 

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_7_4.png?raw=true" style="width:70%">
  <figcaption><b> iPATH3 결과 예시</b></figcaption>  
</figure>

