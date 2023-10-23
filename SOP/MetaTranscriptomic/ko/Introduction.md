# NGS기반 마이크로바이옴 전사체 분석 SOP


## 메타전사체 (Metatranscriptome) 개요

마이크로바이옴(microbiome)은 한 환경에 서식하는 미생물군집(마이크로바이오타, microbiota)과 이들이 가지고 있는 전체 유전정보을 포함하는 개념이다.
미생물군집 연구는 환경 DNA로부터 리보솜 유전자 등 계통분석 표지 유전자(marker gene)의 일부 보존된 영역을 PCR로 증폭 후 서열 분석을 실시하여 환경 내 존재하는 미생물의 종류를 파악할 수 있는 반면, 마이크로바이옴 연구는 환경 DNA 전체 서열 정보 분석을 통한 전 메타유전체 서열 분석으로 환경 내 존재하는 미생물 종류 뿐 아니라 미생물들이 보유하고 있는 유전자 종류와 기능까지 파악이 가능하다.
메타유전체((metagenome) 데이터는 특정 종이나 유전자의 유무를 알려주지만 그것들이 마이크로바이옴 생태 시스템 내에서 활성화된 그룹인지를 파악할 수 없는 한계점이 있다.
미생물 군집이 환경의 변화에 의해 어떻게 반응하는지를 살피기 위해 메타전사체 분석이 이루어지기 시작하였으며, 마이크로바이옴의 생태 시스템을 이해하는 데에는 메타전사체 정보가 중요한 역할을 할 것이다.

<figure align = "center">
<img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_0_1.png?raw=true" style="width:90%">
<figcaption><b>> 멀티오믹스 정보기반 마이크로바이옴 기능 분석</b></figcaption>  
</figure>

대용량 염기서열 분석법이 도입되기 이전부터 qPCR을 활용한 관심있는 유전자의 RNA의 발현 정도 측정 및 microarray 기술을 활용한 특정 개체의 알려져 있는 transcript의 발현양상 연구가 이루어져 왔으며, NGS 기술의 상용화로 알려져 있는 transcript target의 발현 정도 뿐 만이 아니라 non-coding RNA를 비롯한 알려져 있지 않았던 transcript 및 transcript variants 등 특정 환경의 모든 전사체(transcriptome) 정보를 RNA sequencing(RNA-seq) 데이터 분석으로 얻을 수 있게 되었다.
이러한 이유로 RNA-seq은 마이크로바이옴 연구에서도 활용되는 빈도가 높아지고 있으며 유전자 발현 분석, 집단 내 높은 활성을 보이는 미생물군 규명, 조절인자 규명, 미생물간 상호작용, 숙주와의 상호작용 연구 등 다양한 분야에 응용되고 있다.

이러한 요구들을 근거로 RNA-seq은 마이크로바이옴 연구에서 활용되는 빈도가 높아지고 있으며 본 SOP에서는 메타유전체으로 얻어진 de novo assembled contig 및 metagenome-assembled genome (MAG) 서열에 RNA-seq read들을 mapping하는 방식을 기반으로 하는 reference-guided 메타전사체 분석과 reference-independent 메타전사체 분석 방법을 기술하고자 한다.

<figure align = "center">
<img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_0_2.png?raw=true" style="width:65%">
<figcaption><b>Reference-guided 및 reference-independent 메타전사체 분석 방법</b></figcaption>  
</figure>
본격적인 SOP 소개에 앞서 메타전사체 분석에 활용할 수 있는 여러가지 툴을 소개한다.
본 SOP에 소개된 툴 이외에도 표 1에 나열된 툴 혹은 유사한 목적을 가진 툴을 각 단계에 선택적으로 적용 가능하다.


[cutadapt](https://cutadapt.readthedocs.io/en/stable/)


<table>
<thead>
  <tr>
    <th>Category</th>
    <th>Tools</th>
    <th>Description</th>
    <th>Year</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="3">Trimming</td>
    <td><a href="https://cutadapt.readthedocs.io/en/stable/">cutadapt</a></td>
    <td>5' adaptor trimming 가능</td>
    <td>2011</td>
  </tr>
  <tr>
    <td><a href="https://github.com/FelixKrueger/TrimGalore">TrimGalore</a></td>
    <td>cutadapt기반의 trimming 프로그램<br>paired-end trimming가능</td>
    <td>2013</td>
  </tr>
  <tr>
    <td><a href="http://www.usadellab.org/cms/?page=trimmomatic">trimmomatic</a></td>
    <td>Paired-end trimming 가능</td>
    <td>2014</td>
  </tr>
  <tr>
    <td rowspan="5">Alignment</td>
    <td><a href="https://bowtie-bio.sourceforge.net/bowtie2/manual.shtml">bowtie2</a></td>
    <td>Short read mapping, local alignment, FM-index algorithm 사용</td>
    <td>2012</td>
  </tr>
  <tr>
    <td><a href="https://github.com/lh3/bwa">BWA</a></td>
    <td>Low-divergent sequences mapping, genome reference필요, BWT및 FM index algorithm 사용</td>
    <td>2009</td>
  </tr>
  <tr>
    <td><a href"https://daehwankimlab.github.io/hisat2/manual/">HiSat2</a></td>
    <td>Human 데이터 분석에 활용도가 높음. Human Leukocyte Antigen(HLA)타이핑 및 DNA 지문 채취 등에 이용, FM index 사용</td>
    <td>2019</td>
  </tr>
  <tr>
    <td><a href="https://github.com/alexdobin/STAR">STAR</a></td>
    <td><em>de novo</em> RNA-seq 문제 보완 및 long read mRNA mapping 가능</td>
    <td>2013</td>
  </tr>
  <tr>
    <td><a href="">TopHat2</a></td>
    <td>bowtie 기반의 short read mapping</td>
    <td>2013</td>
  </tr>
  <tr>
    <td rowspan="6">DE analysis</td>
    <td><a href="">Cuffdiiff2</a></td>
    <td>cufflink 연계 tool. sam(bam)파일을 이용하여 gene, isoform 수준에서 발현 비교 </td>
    <td>2013</td>
  </tr>
  <tr>
    <td><a hre="">DESeq2</a></td>
    <td>R package, shrinkage estimation 기법을 이용. RLE(Relative Log Expression) normalization 사용</td>
    <td>2014</td>
  </tr>
  <tr>
    <td><a hre="">EdgeR</a></td>
    <td>R package, input파일로 raw count값을 사용. TMM(Trimmed Mean M-values) normalization 사용</td>
    <td>2010</td>
  </tr>
  <tr>
    <td><a hre="">limma</a></td>
    <td>R package. 적은 수의 표본에 대해서 효과적이며 TMM normalization 사용</td>
    <td>2015</td>
  </tr>
  <tr>
    <td><a hre="">NOISeq</a></td>
    <td>R package. 비모수적 접근 방식 및 RPKM/TMM/upper quartile normalization방식 사용</td>
    <td>2011</td>
  </tr>
  <tr>
    <td><a hre="">SAMSeq</a></td>
    <td>R package. sam 파일을 input파일로 사용하는 gene-level DE분석. 전체 count의 mean값을 기준으로 normalization 진행</td>
    <td>2013</td>
  </tr>
  <tr>
    <td rowspan="3"><em>de novo</em> assembly</td>
    <td><a hre="">megahit</a></td>
    <td>Single genome assembly, multiple libraries 가능</td>
    <td>2015</td>
  </tr>
  <tr>
    <td><a hre="">SPAdes</a></td>
    <td>RNA, virus RNA, plasmid등 다양한 종류의 data assembly가능. fastq, fasta파일 뿐만 아니라 bam파일 input가능</td>
    <td>2012</td>
  </tr>
  <tr>
    <td><a hre="">trinity</a></td>
    <td>Transcriptome assembler</td>
    <td>2011</td>
  </tr>
  <tr>
    <td rowspan="4">Taxonomy assignment</td>
    <td><a hre="">kaiju</a></td>
    <td>메타유전체의 전체 서열 또는 메타전사체의 서열을 GenBank protein non-redundant database를 이용하여 분석</td>
    <td>2016</td>
  </tr>
  <tr>
    <td><a hre="">kraken</a></td>
    <td>GenBank nucleotide non-redundant database를 이용하여 taxonomy 분석</td>
    <td>2014</td>
  </tr>
  <tr>
    <td><a hre="">MetaPhlAn</a></td>
    <td>종 수준에서 메타유전체 정보로부터 미생물 조성 분석. 자체적인 marker gene을 이용</td>
    <td>2012</td>
  </tr>
  <tr>
    <td><a hre="">onecodex</a></td>
    <td>Genome database와 targeted loci database를 이용한 web 기반 분석 도구</td>
    <td>2015</td>
  </tr>
  <tr>
    <td rowspan="4">Format transition</td>
    <td><a hre="">BEDTools</a></td>
    <td>bam 또는 bed 파일을 이용하는 소프트웨어. Raw count값을 얻을 수 있지만 후보정이 필요</td>
    <td>2010</td>
  </tr>
  <tr>
    <td><a hre="">Cufflink</a></td>
    <td>RNA-seq mapping결과(sam파일)를 assembly하고 abundance를 계산하는 도구로 FPKM값을 결과값으로 가짐</td>
    <td>2010</td>
  </tr>
  <tr>
    <td><a hre="">HTSeq</a></td>
    <td>Python package, gff정보를 이용한 read mapping 계산</td>
    <td>2015</td>
  </tr>
  <tr>
    <td><a hre="">SAMTools</a></td>
    <td>sam 파일을 변환하거나 sorting하는 소프트웨어</td>
    <td>2009</td>
  </tr>
</tbody>
</table>