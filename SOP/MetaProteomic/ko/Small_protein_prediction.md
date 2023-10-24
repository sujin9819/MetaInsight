# Small protein prediction
<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaProteomic/img/P_11_1.png?raw=true" style="width:65%">
  <figcaption><b></b></figcaption>  
</figure>

Ribosome profiling 분석을 통해서 유전체나 전사체 분석에서 얻을 수 없었던 저분자 단백질에 대한 정보를 얻을 수 있다.
저분자 단백질이란 70aa보다 작은 크기의 단백질을 말한다. 이러한 저분자 단백질들은 다른 유전자의 발현 조절 또는 미생물의 key factor와 관련된 유전자에 해당한다고 알려져 있으나 기능에 대한 분석을 하기가 쉽지 않은 편이다.
그래서 해당 과정을 통해서 저분자 단백질을 분류하여 새로 annotation을 진행하여 이전에 annotation되지 않은 새로운 기능을 하는 유전자들을 찾고자 한다.
먼저 prodigal을 진행하여 얻은 DNA 서열 파일에서 < 70aa에 해당하는 유전자들을 필터링하는 것이 필요하다.
Linux에 존재하는 awk와 조건문을 통해서 저분자 단백질 만 존재하는 파일을 생성한다. 대부분 분리된 저분자 단백질의 경우, hypothetical protein에 해당한다

```bash
# run prodigal 
$ prodigal -i sample_MAG.fa -p meta -a sample_MAG.prodigal.faa -d sample_MAG.prodigal.fna -f gff -o sample_MAG.prodigal.gff
# small amino acid filtering
$ awk '/^>/ {if (length(seq) <= 210) {print header; print seq} } {if (/^>/) {header = $0; seq = ""} else {seq = seq $0}} END {if (length(seq) <= 10) {print header; print seq}}' sample_MAG.prodigal.ffn > MAG_smallprotein.fnn
# run CD-hit for clustering
$ cd-hit -i MAG_smallprotein.ffn -o example -n 2 -p 1 -c 0.5 -d 200 -M 50000 -l 5 -s 0.95 -aL 0.95 -g 1
```
그 후 최대한 비슷한역할의 유전자인지 새로운 저분자 단백질이 존재하는지 확인하고자 CD-HIT을 통해서 clustering을 진행한다.
그 결과 유사한 서열을 가진 유전자끼리 그룹화되어 각 클러스터를 대표하는 유전자들의 서열로 구성된 파일을 얻을 수 있다.

그 후 RNAcode로 분석을 진행하여 얻어진 유전자들의 단백질 코딩 영역에 대한 정보를 획득한다.
RNAcode는 input 파일로 alignment file을 필요로 하기 때문에 CD-HIT결과파일을 clustalW를 통해 DNA서열 alignment한다.
DNA서열 alignment 결과 파일을 RNAcode로 분석을 진행하여 저분자 단백질들의 코딩 서열을 추론할 수 있다. 더불어 Read alignment 정보를 이용하여 저분자 단백질의 발현정보를 얻을 수 있다.

```bash
# alignment multiple sequence
$ clustalw output
# run RNAcode
$ RNAcode output.aln --outfile results.gtf --gtf --best-only --cutoff 0.01 --eps data.aln
```