## 메타유전체 분석 활용툴 
- Preprocessing of the sequencing reads : Kneaddata, minimap2, samtools
- Read-based profiling : HUMAnN 3.0, MetaPhlAn
- De novo assembly : MEGAHIT, Quast, hifiasm_meta, Bandage
- Taxonomic annotation : Kaiju
- Functional annotation : Prodigal, EggNOG
- Binning : MetaBAT2, BBmap, minimap2, samtools, CheckM
- Phylogenetic tree construction : GTDB-tk, PhyloPhlAn3

![메타유전체 분석 파이프라인](https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_4_1.png?raw=true)
> 메타유전체 분석 파이프라인

# Installation

### An introduction to Conda
메타 유전체 분석을 위해서는 다양한 분석 프로그램들을 설치해야 한다. 이때 프로그램들간의 충돌 또는 버전 의존성 문제가 발생할 수 있다.
예를 들면, 프로그램 A는 특정 버전의 프로그램 B에 의존하는데 프로그램 C의 경우 다른 버전의 프로그램 B에 의존 할 경우 초보자들이 프로그램 C를 설치하기는 상당히 많은 노력과 시간이 필요하게 된다.
이때 파이썬 패키지 및 환경 매니저 프로그램인 Conda를 이용하여 프로그램을 설치하면 이러한 특정 버전의 충돌 문제를 해결 할 수 있다.
본 SOP에 사용되는 분석 툴들은 Conda를 이용하여 설치하길 권장한다. 아래의 사이트는 Conda에 대한 공식문서 사이트이다.
[https://docs.conda.io/projects/conda/en/latest/user-guide/index.html]

### Making a new environment 
프로그램 간의 충돌이 발생하지 않도록 프로그램을 설치 할 때마다 새로운 Conda 환경을 만드는 것을 권장한다. 새로운 Conda 환경을 만드는 방법의 예시는 아래와 같다
```bash
# Create a new conda environment
$ conda create -n new-env 
```
`conda create` 라는 명령어를 입력 후 `-n` 을 사용하여 본인이 원하는 새 환경의 이름을 저장한다.
### Entering & exiting an environment
```bash
# Enter that environment
$ conda activate new-env
# Exit whatever conda environment we are running
$ conda deactivate
```

다음 표는 본 SOP에서 사용되는 프로그램들의 설치코드의 예시와 Anaconda 주소이다. create –n 다음의 환경이름은 사용자가 임의적으로 변경 가능하다. 

| 분석 툴 | 설치 코드 | ANACONDA 주소
| ------ | ------ | ------ |
| KNEDDATA | `conda create -n kneaddata -c bioconda kneaddata` | https://anaconda.org/bioconda/kneaddata |
| HUMANN3.0 | `conda create -n humann -c biobakery humann` | https://anaconda.org/biobakery/humann |
| METAPHLAN3.0 | `conda create –n metaphlan -c bioconda metaphlan` | https://anaconda.org/bioconda/metaphlan |
| MEGAHIT | `conda create –n MEGAHIT -c bioconda MEGAHIT` | https://anaconda.org/bioconda/MEGAHIT |
| QUAST | `conda create –n quast -c bioconda quast` | https://anaconda.org/bioconda/quast |
| KAIJU | `conda create –n kaiju -c bioconda kaiju` | https://anaconda.org/bioconda/kaiju |
| MINIMAP2 | `conda create –n minimap2 -c bioconda minimap2` | https://anaconda.org/bioconda/minimap2 |
| HIFIASM_META | `conda create –n hifiasm_meta -c bioconda hifiasm_meta` | https://anaconda.org/bioconda/hifiasm_meta |
| KRONA | `conda create –n krona -c bioconda krona` | https://anaconda.org/bioconda/krona |
| PRODIGAL | `conda create –n prodigal -c bioconda prodigal` | https://anaconda.org/bioconda/prodigal |
| EGGNOG | `conda create –n eggnog -c bioconda eggnog-mapper` | https://anaconda.org/bioconda/eggnog-mapper |
| METABAT2 | `conda create –n MetaBAT2 -c bioconda MetaBAT2` | https://anaconda.org/bioconda/MetaBAT2 |
| BBMAP | `conda create –n bbmap -c bioconda bbmap` | https://anaconda.org/bioconda/bbmap |
| SAMTOOLS | `conda create –n samtools -c bioconda samtools` | https://anaconda.org/bioconda/samtools |
| CHECKM | `conda create -n CheckM python=3.9`  
`conda activate CheckM`  
`conda install -c bioconda numpy matplotlib pysam` 
`conda install -c bioconda hmmer prodigal pplacer` 
`pip3 install CheckM-genome` | https://anaconda.org/bioconda/CheckM-genome |
| GTDB-TK | `conda create -n gtdbtk-2.1.1 -c conda-forge -c bioconda gtdbtk=2.1.1` | https://anaconda.org/bioconda/gtdbtk |
| PHYLOPHLAN3 | `conda create –n phylophlan -c bioconda phylophlan` | https://anaconda.org/bioconda/phylophlan |
