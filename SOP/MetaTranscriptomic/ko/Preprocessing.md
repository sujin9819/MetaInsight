# Preprocessing of the sequencing reads

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_5_1.png?raw=true" style="width:90%">
  <figcaption><b>Sequencing reads의 preprocessing 과정</b></figcaption>  
</figure>

Raw sequence data를 분석에 이용하기 위해서는 low quality base의 제거와 adaptor를 제거하는 과정이 필요하다.
이 과정을 거친 sequence data는 sequence quality가 향상되어mapping rate가 증가하게 된다. Kneaddata 프로그램을 활용하면 Illumina 플랫폼 기반 시퀀싱에 활용된 adaptor 서열과 host genome의 서열을 쉽게 제거할 수 있다.

```bash
#host RNA removal and trimming
$ kneaddata --input sample_1.fastq.gz --input sample_2.fastq.gz --reference-db hg37dec_v0.1 --output ./1.Trim/sample --trimmomatic /where/to/Trimmomatic-0.36/ --trimmomatic-options="MINLEN:90" 
#--trimmomatic option; trimmomatic 설치 위치 지정
```

FastQC 프로그램을 이용하여 preprocessing전 후 sequence read의 quality를 비교하여 trimming결과를 확인할 수 있다.
FastQC는 종합적인 fastq파일의 정보와 per base sequence quality와 per sequence QC content, per sequence quality score, sequence length distribution 등 trimming 결과를 다양한 parameter로 나타내준다.

```bash
#FastQC running(java script)
$./fastqc
#java에서 fastq파일 선택하여 확인가능
```

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_5_2.png?raw=true" style="width:90%">
  <figcaption><b>FastQC로 raw sequence의 quality check 결과 예시</b></figcaption>  
</figure>