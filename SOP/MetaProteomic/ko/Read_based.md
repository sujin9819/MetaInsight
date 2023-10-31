# Reads-based profiling

eggNOG-mapper 외에도 [HUMAnN](https://huttenhower.sph.harvard.edu/humann/)을 이용하여 metabolic pathway에 대한 정보를 얻을 수 있다.
HUMAnN(HMP Unified Metabolic Analysis Network)은 메타유전체 또는 메타전사체 서열 정보로부터 미생물의 대사경로 및 분자 기능을 프로파일링하는 소프트웨어이다.
Input파일로는 다양한 종류의 파일을 이용할 수 있다. 메타유전체나 메타 전사체 데이터를 host 데이터 제거 및 quality trimming을 진행한 후의 .fastq 파일, alignment 결과 파일인 .sam 또는 .bam 파일, 그리고 유전자 정보와 count 정보가 담긴 .tsv, .biom 파일을 input파일로 사용할 수 있다.
MetaPhlAn 및 ChocoPhlAn 등의 pangenome 데이터 베이스를 통해 미생물 군집 분석과 군집 내 미생물의 기능 분석을 진행할 수 있다.
또한 UniRef, MetaCyc, MinPath를 사용하여 유전체 정보와 pathway에 대한 정보를 얻을 수 있다.

```bash
# download humann
$ conda create --name biobakery3 python=3.7
$ conda activate biobakery3
$ conda install humann –c biobakery3
# download database
$ humann_databases --download chocophlan full $INSTALL_LOCATION --update-config yes
$ humann_databases --download uniref uniref90_diamond $INSTALL_LOCATION --update-config yes
$ humann_databases --download utility_mapping full $INSTALL_LOCATION --update-config yes
# paired read concatenation
$ cat kneaddata.trimmed_paired_1.fastq kneaddata.trimmed_paired_2.fastq > kneaddata.trimmed.fastq
# running humann
$ humann --input sample_kneaddata_paired_1.fastq --output $OUTPUT_DIR
# humann result’s features
$ humann_join_tables -i $OUTPUT_DIR -o sample_pathcoverage.tsv –-file_name pathcoverage 
$ humann_barplot –-input sample_pathcoverage.tsv –-focal-feature $PATHWAY_NAME –-outfile sample_path
```
- HUMAnN 설치와 DB 다운로드와 관련된 설명을 한 번 더 서술하였음.

HUMAnN 분석을 진행하게 되면 gene family정보와 pathway정보를 얻을 수 있다.
이 중 sample_pathabaundace.tsv와 sample_pathcoverage.tsv 파일에 담긴 pathway정보를 이용하여 barplot을 그려, 특정 pathway에 관여하는 미생물 비율을 확인할 수 있다.
HUMAnN분석으로 얻어진 여러 파일(bowtie결과, diamond결과 등)을 이용하여 추가적인 분석 역시 가능하다.

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaProteomic/img/P_10_1.png?raw=true" style="width:90%">
  <figcaption><b>HUMAnN 결과로 도출된pathway 정보의 barplot 시각화 결과 예시</b></figcaption>  
</figure>
