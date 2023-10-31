# Taxonomic annotation of contigs
<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_8_1.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>  
</figure> 

Metagenome dataset의 taxonomic profiling방식은 크게 3가지로 나뉠 수 있다. (1) DNA-to-DNA, (2) DNA-to-protein, (3) DNA-to-marker genes.
가장 많이 쓰이는 방법인 (1)번 방법은 BLASTn과 유사하며 genomic 데이터베이스를 사용하고, (2)번 방법은 BLASTx와 유사하며 protein 데이터베이스를 필요로 한다. 

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_8_2.png?raw=true" style="width:90%">
  <figcaption><b>>Comparison of the taxonomic classification tools ; <a href="https://doi.org/10.1016/j.cell.2019.07.010">[ref]</a></b></figcaption>  
</figure>

각 프로그램들은 장단점이 존재하는데, DNA-to-DNA 방법은 프로그램들이 메모리 소모가 적고 매우 속도가 빠르지만 DNA-to-protein 방식보다는 민감도가 떨어진다. 반면, DNA-to-protein 방법은 속도가 매우 느리고 메모리와 CPU의 소모가 크지만 amino acid 시퀀스 기반이기 때문에 매우 민감하고 정확도가 높다. 때문에 분석하려는 데이터의 특성과 목적, 그리고 데이터베이스에 따라서 최적의 프로그램을 사용해야 한다. Kaiju는 DNA-to-protein 프로그램 중 가장 대표적인 프로그램으로써 NCBI taxonomy와 protein reference database를 사용하며 미생물과 바이러스 classification이 가능하다.  
[Kaiju](https://bioinformatics-centre.github.io/kaiju/) 프로그램을 사용하기 위해서는 데이터베이스를 다운로드 받아야 하며 컴퓨터의 성능에 따라 시간이 오래 소요될 수 있다. 사용 가능한 데이터베이스는 다음 표와 같다.
<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_8_3.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>  
</figure>

```bash
# creating the reference database and index from NCBI nr database
$ conda activate kaiju
$ kaiju-makedb -s nr
```
Makedb 커맨드 후 생성되는 파일 : Kaiju_db_nr.fmi, nodes.dmp, names.dmp


```bash
$ kaiju -t nodes.dmp -f nr/kaiju_db_nr.fmi -i MEGAHIT_result/final.contigs.fa -o kaiju.out -z 15
$ kaiju2krona -t nodes.dmp -n names.dmp -i kaiju.out -o kaiju.out.krona
$ conda deactivate
$ conda activate krona
$ ktImportText -o kaiju.out.html kaiju.out.krona
$ conda deactivate
$ conda activate kaiju
$ kaiju2table -t nodes.dmp -n names.dmp -r genus -o kaiju_summary.tsv kaiju.out -l superkingdom,phylum,class,order,family,genus,species
$ kaiju-addTaxonNames -t nodes.dmp -n names.dmp -i kaiju.out -o kaiju.names.out
$ conda deactivate
```

kaiju프로그램 실행에는 3가지 옵션(`-t`, `-f`, `-i`)이 필수적이다. `–t` 옵션에는 nodes.dmp, `-f`옵션에는 kaiju_db_nr.fmi, `-i`옵션에는 assembled contig(final.contigs.fa)을 입력하면 된다.
`-o`옵션에는 kaiju의 결과파일에 대한 이름을 설정하고 `–z` 옵션을 통해 CPU thread 수를 조정할수 있다.
kaiju의 분석결과에 대한 시각화를 위해 kaiju.out 파일을 `kaiju2krona` 명령어를 통해 Krona프로그램의 입력파일 형태로 변환시켜준다.
이 후 krona프로그램을 활성화시키고 `ktImportText` 명렁어를 통해 html형식의 시각화 결과 파일을 받을 수 있다.

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_8_4.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>  
</figure>
