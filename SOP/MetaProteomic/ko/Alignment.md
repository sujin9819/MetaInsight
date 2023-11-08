# Reads alignment

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaProteomic/img/P_6_1.png?raw=true" style="width:90%">
  <figcaption><b> </b></figcaption>  
</figure>

Pre-processing을 진행하여 sequence quality가 개선된 fastq 파일을 reference 시퀀스*에 mapping하여 alignment를 수행한다. 이때 STAR 프로그램을 이용하여 reference파일을 제작하고 만든 reference서열에 reads를 mapping하게 된다.
- __*Reference 시퀀스의 종류__
 1. 메타유전체 de novo assembly 파이프라인 분석 결과로 얻어진 final.contig.fa
 2. 메타유전체 MAG binning결과 로 얻어진 MAG.fa

```bash
#building STAR index
$ STAR --runMode genomeGenerate --genomeSAindexNbases 10 --runThreadN 8 --genomeDir ./index/sample --genomeFastaFiles sample_MAG.fa 
#mapping
$ STAR --genomeDir ./index/sample --runThreadN 8 --readFilesIn ./1.Trim/sample_kneaddata_paired_1.fastq ./1.Trim/sample_kneaddata_paired_2.fastq --outFileNamePrefix ./2.Align/sample_
```
STAR의 `runMode` 명령을 사용하여 metagenome의 MAG.fa 파일을 STAR running을 위한 index 파일을 생성한다. 생성된 index 파일을 기준으로 reference 시퀀스에 reads를 Mapping하여 각 유전자의 count의 정보가 부여된 .sam 파일을 얻을 수 있다.
STAR align결과는 따로 출력이 되지 않고 final.out 파일로 저장되어진다. Reads align결과는 Log.final.out 파일을 이용하여 확인 가능하며 전체 unique reads, multi-mapping reads 및 unmapped reads에 대한 정보를 얻을 수 있다. STAR결과 생성된 .sam파일은 용량이 크므로 용량이 작은 binary format의 .bam파일로 변환한다.  
Read mapping이후 mapping 정보를 alignment하기 위해, samtools내 view, sort를 기능을 활용하여 .sam 파일을 .bam 파일로 변환한다. 

```bash
#install samtools
$ tar -xvf samtools.zip
$ cd samtools
$ ./configure -prefix==/where/to/install
$ make
$ make install
#sam file sorting and indexing
$ samtools view -b -F 4 sample_Aligned.out.sam | samtools sort - > sample.bam
$ samtools index sample.bam
```

이러한 .bam파일은 IGV를 통해서 alignment 결과의 시각화를 진행할 수 있다.
IGV 프로그램으로 alignment결과를 확인하려면 메타유전체 de novo assembly 또는 MAG결과로 얻어진 MAG.fa이 필요하다.
추가적으로 MAG.fa 서열 내에 annotation 된 CDS (coding sequence) 정보도 함께 표시하고 싶다면 이를 annotation하여 얻어진 .gff파일*도 함께 import 할 수 있다.
또한, samtools 적용 결과 얻어진 coverage value 정보를 포함한 .bam과 samtools index 결과 생성된 .bam.bai파일이 필요하다.
해당 파일들이 모두 import 되면 reference 서열에 CDS 정보 및 메타전사체 분석 sequence reads가 mapping 된 위치와 각 위치에 mapping 된 메타전사체 read count정보도 시각화하여 보여준다.  
*gff (General Feature Format) 파일; MAG.fa에 대한 gff 파일 생성은 메타유전체 SOP 참고

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaProteomic/img/P_6_2.png?raw=true" style="width:90%">
  <figcaption><b>IGV 프로그램을 활용한 alignment 결과의 시각화 </b></figcaption>  
</figure>

```bash
# download prodigal from https://github.com/hyattpd/Prodigal/wiki/installation
# install prodigal
$ cd prodigal/
$ make install
# run prodigal
$ prodigal -i sample_MAG.fa -p meta -a sample_MAG.prodigal.faa -d sample_MAG.prodigal.fna -f gff -o sample_MAG.prodigal.gff 
```
Bedtools을 활용해서 각 functional annotation이 완료된 각 CDS에 대한 coverage (count) 정보를 얻을 수 있다. Bedtools 적용 전, bedtools활용에 필요한 정보만으로 .gff 항목을 간소화 하는 것이 좋다.
ParseGFFonlyCDS.R R스크립트를 사용하여 functional annotation으로 얻어진 gff 파일 정보 중, CDS 정보, CDS의 위치, locus tag정보만으로 구성된 간략화된 gff 파일로 parsing한다.

```bash
#make CDS only gff file with python-script
$ wget https://raw.githubusercontent.com/sujin9819/ngs/main/R_scripts/ParseGFFonlyCDS.R 
$ Rscript ParseGFFonlyCDS.R -i sample_MAG.prodigal.gff -o MAG.CDS.gff
```

Bedtools 내 `bamtobed` 명령은 .bam 파일을 bed 파일로 변환 할 때, bedtools coverage명령은 bed파일로부터 gff파일 내 항목을 기반으로 count값을 도출 할 때 사용한다.
gff파일 내 항목 중 CDS의 위치 정보와 bed 파일의 sequence reads가 mapping되는 위치 정보를 매칭하여 각 CDS의 count값을 계산해준다.
그 결과 CDS의 위치 정보 및 각 CDS에mapping되는 sequence read들의 count 정보, 그리고 유전자의 경우 strand 방향성에 대한 정보를 포함한 bed파일을 생성할 수 있다 (아래의 경우 sample.cov 로 표시함).

```bash
#install bedtools
$ tar -zxvf bedtools-2.29.1.tar.gz
$ cd bedtools2
#alignment
$ bedtools bamtobed –i sample.bam > sample.bed
$ bedtools coverage –a MAG.CDS.gff –b sample.bed –s > sample.cov
```

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaProteomic/img/P_6_3.png?raw=true" style="width:90%">
  <figcaption><b>Read alignment 결과 생성된 bed 파일 (sample.cov) 예시</b></figcaption>  
</figure>