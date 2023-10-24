# NGS기반 마이크로바이옴 단백체 분석 SOP

## 메타단백체(Metaproteome) 개요

전사체 및 단백체 분석으로 실제 미생물이 생태계에 미치는 생물학적인 요소에 대한 더 정확한 정보를 얻을 수 있으며, 마이크로바이옴 연구에서도 메타전사체와 메타단백체 정보 역시 군집을 이루는 미생물군의 정확한 기능 분석에 도움을 준다.
메타전사체 정보가 환경 내 유전자의 발현과 활성에 대한 정보를 제공해준다면, 메타단백체 정보는 단백질의 발현 및 조절 정보를 포함하므로 메타전사체 정보와는 다르게 나타난다.
질량분석기를 이용한 메타단백체 분석의 경우 미생물 군집에서 단백체를 추출한 후, liquid chromatograph(LC)를 이용하여 단백질을 분리하고 tandem mass spectrometry를 이용하여 각 단백질들이 무엇인지 검출하는 과정을 거친다.
보다 개선된 단백질 특정화를 위해서 고성능의 mass spectrometry를 활용 및 정교한 단백질 분리를 위한 chromatography 방법 개발 등이 시도되고 있지만, 기존의 질량분석기를 이용한 메타단백체 분석의 경우 마이크로바이옴 샘플에서 일부분만이 프로파일링이 가능하며 특히 저분자 단백질은 고분자 단백질에 비해 확인될 가능성이 낮은 한계점을 가지며, 분석 빈도 또한 메타전사체 분석 건수와 비교하면 매우 낮은 편이다. 

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaProteomic/img/P_0_1.png?raw=true" style="width:90%">
  <figcaption><b>멀티오믹스 정보기반 마이크로바이옴 기능 분석</b></figcaption>  
</figure>

## Ribo-sequencing

Ribo-seq은 시퀀싱 기술을 응용하여 단백체를 분석하는 기술로서, 클로람페니콜을 처리하여 세포 상태를 고정시키고 MNase를 통해 ribosome으로 보호되지 않은 DNA와 RNA를 제거한 후 단백질 생합성 중인 mRNA 서열을 시퀀싱하는 방법이다.
이는 기존의 질량분석기 기반 기술의 낮은 throughput, yield, 제한된 정확도의 데이터베이스가 가지고 있는 문제점을 해결하고자 시도되었다.
Ribo-seq 기술은 2009년 Science지에 처음 보고 되었으며 ribosome 프로파일링을 통하여 yeast에서 영양이 풍부한 상태와 고갈된 상태에서 단백질 합성이 달라지는 양상을 확인한 바 있다[2].
Ribo-seq은 이용한 단백체 분석은 합성되고 있는 단백질을 암호화하고 있는 유전자 정보를 확인하여 단백질 합성을 정량화 할 수 있으며, 메타 단백체 분석에서도 분변 샘플에 대해 RNALater에 얼려서 보관되고 있는 분변에 대해 ribo-Seq을 통하여 충분히 신뢰할만한 메타 단백체 분석 결과를 얻을 수 있음이 보고 되었다[3].

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaProteomic/img/P_0_2.jpg?raw=true" style="width:90%">
  <figcaption><b>MetaRibo-seq을 포함한 마이크로바이옴 분석 workflow</b></figcaption>  
</figure>

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaProteomic/img/P_0_3.jpg?raw=true" style="width:90%">
  <figcaption><b>Ribosome profiling workflow</b></figcaption>  
</figure>