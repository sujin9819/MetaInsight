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

![Metatranscriptomics overview](https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_4_1.png?raw=true)
> Metatranscriptomics 분석 파이프라인

# Installation
Before proceeding with the analysis pipeline, let me first explain the program installation process.
## Install conda environment
Conda offers the advantage of creating virtual environments, allowing for independent program installations and management. This feature is particularly valuable as it significantly reduces the risk of program conflicts. Therefore, it is recommended to install Conda-compatible programs via Conda.

```bash
# set up conda environment (name and python version are set by user)
$ conda create --name NGS python=3.7
# active conda environment
$ conda activate NGS
# install program for conda 
$ conda install cutadapt				#cutadapt install
$ conda install humann –c biobakery3		#humann install
# download database
$ humann_databases --download chocophlan full $INSTALL_LOCATION --update-config yes
$ humann_databases --download uniref uniref90_diamond $INSTALL_LOCATION --update-config yes
$ humann_databases --download utility_mapping full $INSTALL_LOCATION --update-config yes
$ conda install bowtie2				#bowtie2 install
$ make
```

## Install program
However, it's important to note that some programs may still require manual installation. In such cases, you need to install these programs directly. For programs installed separately, you may also need to edit your bash_profile file to add the program and database directories to your system's $PATH for proper functionality. 

```bash
# create and specify installation folders
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