# 메타전사체 분석 활용툴
■ Sequencing reads trimming
- FastQC, cutadapt, trimGalore
■ 메타유전체 서열에 read 정렬
- Bowtie2[4]
■ 정렬된 정보를 다른형태의 파일로 변경 (file format: sam to cov)
- SamTools, bedtools
■ Functional annotation
- eggNOG-mapper
■ Visualization
-iPATH3, KEGG-mapper, IGV
■ R package
-DESeq2, ggplot2, pheatmap

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_4_1.png?raw=true" style="width:90%">
  <figcaption><b>Metatranscriptome 분석 파이프라인</b></figcaption>  
</figure>

# Installation
분석 파이프라인 진행에 앞서 사용하는 프로그램 설치에 대해서 먼저 설명하겠다.
## conda 설치
콘다는 가상의 환경으로 프로그램 설치 및 독립적으로 관리가 가능하다는 장점이 존재한다.
프로그램 충돌과 관련된 문제를 비교적 줄일 수 있기 때문에 콘다 설치 가능 프로그램의 경우 콘다에 설치하는 것을 추천한다. 

```bash
# 사용할 conda 환경 설정하기기(이름 및 파이썬은 사용자가 설정)
$ conda create --name NGS python=3.7
# conda 환경 활성화
$ conda activate NGS
# conda 환경에 사용할 프로그램 설치
$ conda install cutadapt				#cutadapt install
$ conda install humann –c biobakery3		#humann install
# download database
$ humann_databases --download chocophlan full $INSTALL_LOCATION --update-config yes
$ humann_databases --download uniref uniref90_diamond $INSTALL_LOCATION --update-config yes
$ humann_databases --download utility_mapping full $INSTALL_LOCATION --update-config yes
$ conda install bowtie2				#bowtie2 install
$ make
```

## 프로그램 설치
가상환경에 설치하여 독립적으로 관리가 가능한 콘다가 있는 반면 일부 프로그램은 여전히 직접 설치를 진행해야한다.
따로 프로그램을 설치한 일부 프로그램의 경우, 프로그램 및 데이터베이스를 따로 bash_profile파일을 편집하여 $PATH를 추가 설정할 필요가 있다.

```bash
# 설치 폴더 생성 및 지정
$ mkdir program
$ cd program
# SAMtools install
$ tar -xvf samtools.zip
$ cd samtools
$ ./configure -prefix==/where/to/install
$ make
$ make install
# install prodigal
$ cd prodigal/
$ make install
#install bedtools
$ tar -zxvf bedtools-2.29.1.tar.gz
$ cd bedtools2
# download eggnog-mapper from https://github.com/eggnogdb/eggnog-mapper/releases/latest
$ tar -xvzf eggnog_mapper_(version).tar.gz
# download eggnog-mapper database
$ download_eggnog_data.py
#install SPAdes
$wget http://cab.spbu.ru/files/release3.15.3/SPAdes-3.15.3-Linux.tar.gz
$tar -xzf SPAdes-3.15.3-Linux.tar.gz
$cd SPAdes-3.15.3-Linux/bin/
```