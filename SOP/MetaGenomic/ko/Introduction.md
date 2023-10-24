# NGS기반 마이크로바이옴 유전체 분석 SOP


## 메타유전체 (Metagenome) 개요

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_0_1.png?raw=true" style="width:90%">
  <figcaption><b>Metagenomics overview</b></figcaption>  
</figure>

메타유전체(metagenome)란 다양한 환경 시료(동물, 식물, 해양 등)에 존재하는 유전적 물질의 총체를 의미한다.
메타유전체 분석은 특정 환경 생태계에 존재하는 모든 생명체들의 유전적 정보를 추출하여 분석한다.
메타유전체 이전에, 미생물 유전체 분석은 배양가능한 미생물의 유전체만 분석이 가능하였다.
하지만 특정환경에 존재하는 미생물 들 중 배양가능한 미생물들은 극히 일부이기 때문에, 이러한 접근법은 일부 배양 가능한 미생물 중심의 편향된 정보를 갖게 한다.
하지만 메타유전체 분석을 통해서는 환경에 존재하는 유전체 총체에 대해 분석하기 때문에 특정 생태계에 대해 보다 정확한 전체적인 그림을 그릴 수 있게 된다.

시퀀싱 기술의 발전에 따라, 16S ribosomal DNA와 같은 유전체 특정 부분을 타겟 증폭하여 시퀀싱하는 amplicon 시퀀싱을 넘어서 수십억 개의 핵산 단편을 한꺼번에 시퀀싱해내는 whole meatgenome shotgun sequencing에 대한 연구자의 접근이 쉬워지고 그 연구 수요가 증가하였다.
Amplicon 시퀀싱 데이터의 경우, QIIME2를 이용한 스탠다드 분석 프로토콜 및 플랫폼이 존재하지만, WMS 분석에는 아직까진 표준 골든스탠다드 분석 SOP이 존재하지 않는다. 본 SOP에서는 다양한 분석 프로그램들 중 가장 보편적으로 사용되는 툴 중심으로 Whole genome seuqencing (WGS) 데이터를 분석하는 방법 및 흐름에 대하여 서술하려 한다.

