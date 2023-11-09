# *De novo* assembly
<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_7_1.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>  
</figure>

## Short reads 
Read-based profiling은 빠른 시간 내에 metagenome에 대한 전반적인 분석결과를 제공할 수 있지만 시퀀서의 발달에도 불구하고 sequence read length가 짧기 때문에 database 상에 alignment되지 못하는 unmapped read들이 다량 존재한다.
때문에 assembler를 사용하여de novo assembly를 수행하게 되면 overlapping 되는 reads가 길게 이어져 contig혹은 scaffolds를 형성하고 유전체 성분의 심도 있는 profiling이 가능하며 database와 무관한 프로세스이기 때문에 기존에 알려지지 않은 새로운 서열의 정보 또한 얻을 수 있다.  
현재 다양한 방법과 퍼포먼스를 보이는 어셈블러들이 존재하고 있고 특히 short read 를 assemble 하는데 용이한 프로그램들이 많이 활용되고 있다.
가장 광범위하게 쓰이는 assembler로는 [MEGAHIT](https://github.com/voutcn/megahit)과 [metaSPAdes](https://cab.spbu.ru/software/meta-spades/)가 있는데, 높은 depth를 가지는 sample일수록 metaSPAdes가 좋은 퍼포먼스를 보인다고 알려져 있지만 작은 샘플 수에도 고용량의 메모리가 필요하기 때문에 그의 대체 프로그램으로 MEGAHIT이 많은 연구에서 사용되고 있다 [&#91;ref&#93;](https://doi.org/10.1038/s41596-020-00480-3).  
MEGAHIT은 k-mer 를 사용하는데 `--k-min`과 `--k-max` 옵션을 사용하여 샘플의 복잡도에 따라 크기를 설정해 줄 수 있다.
만약 샘플의 depth가 매우 크다면 de Bruijn graph의 복잡도가 지나치게 증가할 수 있어 상대적으로 큰 `k-mer`를 설정 (25-31)해 주는 것이 좋다. 반대로 depth가 매우 낮아 assembly가 잘 되지 않는다면 `--no-mercy` 옵션을 사용하여 낮은 read들의 assemble 효율을 높일 수 있다.
Paired end read라면 반드시 `-1`과 `-2`로 forward와 reverse read 파일명을 따로 지정해주어야 하며 single read일땐 `-r` 옵션을 사용한다.
de Bruijn graph구성에 사용되는 최대 메모리는 옵션 `–m`으로 설정 할 수 있으며 `0-1`사이로 시스템 총 메모리를 설정 할 수 있다.
기본값은 `0.9`로 설정 되어 있다. `–t` 옵션은 CPU thread 수를 설정해주는 옵션이며 최소 2개 이상 지정해줘야 하며 기본값은 서버가 이용가능한 모든 CPU thread수를 자동으로 계산하여 총 동원 할 수 있게 설정해준다.

```bash
# run MEGAHIT 
$ conda activate MEGAHIT
$ MEGAHIT -1 kneaddata.trimmed.1.fastq  -2 kneaddata.trimmed.2.fastq  -m 0.5  -t 12 -o MEGAHIT_result
$ conda deactivate
```

## Long reads assembly

```bash
# run hifiasm_meta 
$ conda activate hifiam_meta
$ hifiasm_meta -o N14.asm -t 60 N14.aln.unmapped.fq > N14.log
$ conda deactivate
# .gfa 파일을 .fa 파일로 변환
$ awk '/^S/{print ">"$2;print $3}' test.p_ctg.gfa > test.p_ctg.fa
```

“.gfa”는 graphical fragment assembly의 약자로, 그래프 기반 어셈블리 정보를 저장하는 파일 형식으로 어셈블리 과정에서 생성된 그래프의 정보를 담고 있다. 그래프 파일은 De Bruijin 그래프와 유사한 구조로, 노드와 엣지들의 연결관계를 표현한다. 이 그래프는 겹치는 DNA 서열들의 상호작용을 표현하여 어셈블리를 도와주는 역할을 한다.

[Hifiasm-meta](https://github.com/lh3/hifiasm-meta) 수행시 다음과 같은 결과 파일들이 나온다.
1. Raw unitig graph : asm.r_utg*.gfa  
이 파일은 어셈블리 과정에서 생성된 raw unitig 그래프를 담고 있다. Raw unitig 그래프는 어셈블리를 위한 초기 그래프로, 겹치는 서열 정보를 바탕으로 노드와 엣지를 구성한다.

2. Cleaned unitig graph: asm.p_utg*.gfa  
이 파일은 전처리된 cleaned unitig 그래프를 담고 있다. 전처리는 raw unitig 그래프에서 에러를 제거하고 정확성을 향상시키는 과정을 의미한다. 

3. Contig graph: asm.p_ctg*.gfa, asm.a_ctg*.gfa  
이 파일은 contig 그래프를 담고 있다. asm.p_ctg*.gfa 파일은 primary contig를, asm.a_ctg*.gfa는 alternate contig를 의미한다.

__* Unitig란. __  
Unitig는 unique sequence 의 줄임말로 어셈블리 중간 단계의 결과물로 겹치는 DNA 서열들을 하나로 묶어서 구성한 단위이다. 각 unitig는 하나 이상의 DNA 서열들로 구성되어 있으며 겹치는 부분들을 포함한다. 어셈블리 과정에서 raw unitig 그래프를 생성한다. 이렇게 만들어진 raw unitig 그래프에는 여러 에러들이 포함되어 있을 수 있다. 이후 처리 과정을 통해 raw unitg 그래프에서 에러를 제거하고 cleaned unitig 그래프를 생성한다. 

## Contig check
long read assembly 결과는 bandage plot으로 시각화 할 수 있다. Bandage plot은 어셈블리 결과를 시각화하는 도구 중 하나이다. 이 도구는 De Bruijin 그래프나 오버렙 그래프 등과 같이 복잡한 어셈블리 결과를 직관적이고 이해하기 쉬운 상태로 표현한다. Long read 데이터를 이용한 어셈블리에서는 단순히 선형으로 서열을 조합하는 것보다 더 복잡한 그래프 형태가 나타날수 있는데 이 그래프를 시각화하는 데에 bandage plot이 사용된다.
다음과 같은 정보를 제공한다.  
▪ 노드와 엣지 표시 : 노드는 어셈블리 결과에서 생성된 서열조각을 나타내며, 엣지는 서열들 간의 연결을 나타낸다.  
▪ 분기점 확인 : 그래프 내에서 분기점이나 연결부위를 시각화하여, 서로 다른 서열 간의 관계와 겹치는 부분을 파악할 수 있다.  
▪ bandage plot은 Bandage(a Bioinformatics Application for Navigating De novo Assembly Graphs Easily) 프로그램을 통해 나타낼수 있다. Bandage는 http://rrwick.github.io/Bandage/ 에서 다운 받을 수 있다. 리눅스 환경에 설치할 경우 dependency 들이 존재하므로, Window나 Mac 환경에 설치하는 것이 더 쉽다. 

Bandage 프로그램을 실행시킨 후 상단의 File > Load graph에서 *p_ctg.gfa 파일을 load해주면 된다. 파일이 loading 되면 Graph drawing에서 Draw graph 를 클릭해주어야 그래프가 나타난다. 

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_7_2.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>  
</figure>

Assembly가 끝나면 생산된 contig들의 정보를 알기 위해 [QUAST](https://github.com/ablab/quast)(Quality assessment tool)을 사용하여 assemble 결과 및quality를 확인한다.
```bash
# calculate assembly statistics
$ conda activate quast
$ quast.py MEGAHIT_result/final.contigs.fa -o MEGAHIT_quast
$ conda deactivate
```

 
<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_7_3.png?raw=true" style="width:90%">
  <figcaption><b>▶report.html 결과 예시</b></figcaption>  
</figure>

- contigs : assembly 후 생산된 contig의 개수  
- Largest contig : assembly 후 생성된 contig들 중 가장 긴 contig의 길이  
- Total length : assembly 후 생성된 contig들의 총 base 수  
- N50 : assembly 후 생성된 contig들 중 상위 50% 길이를 가지는 contig의 길이  
- N75 : assembly 후 생성된 contig들 중 상위 75% 길이를 가지는 contig의 길이  
- L50 : assembly 후 생성된 contig 들 중 N50의 길이를 가지는 contig들의 개수  
- L75 : assembly 후 생성된 contig 들 중 N75의 길이를 가지는 contig들의 개수  
- Mismatches # N’s : assembly가 되지 않은 uncalled bases 개수  
- Mismatches # N’s per 100kbp : 100000 base 당 uncalled 된 bases의 개수  
- Contig 인덱스 증가에 따른 누적 길이를 나타내는 그래프와 contigs의 GC contents를 나타내는 그래프   
<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_7_4.png?raw=true" style="width:90%">
  <figcaption><b>Metagenomics overview</b></figcaption>  
</figure>
