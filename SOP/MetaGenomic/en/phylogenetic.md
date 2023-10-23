# Phylogenomic tree construction of the MAG
![pipeline](https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_11_1.png?raw=true){: width="100%"}

Metagenome으로부터 여러 유전체를 복원한 후에 taxonomic assignment를 진행하기 위해선 다양한 방법이 있는데, 그 중 GTDB 데이터베이스 (GTDB; https://gtdb.ecogenomic.org) [22]와 classification을 도와주는 GTDB-tk [23]가 가장 많이 사용된다.
GTDB는 RefSeq과 GenBank를 기반으로 다양한 환경 sample들에서 복원된 MAG 정보를 collection 한 데이터베이스이며 MAG기법의 발달과 함께 빠른 속도로 정보량이 증가하는 추세를 보이고 있다.  
GTDB-tk는 Prodigal과 HMMER를 이용한 identify step, marker gene들을 concatenation 하는 align step, 그리고 pplacer 프로그램과 maximum-likelihood placement 기법을 사용하여 GTDB reference tree에 비교 해주는 classify step으로 나뉠 수 있으며 이 세 step을 하나로 묶은 커맨드인 classify_wf도 사용할 수 있다. 


```bash
$ conda activate gtdbtk
# Download GTDB-Tk reference data & set the database PATH
$ wget https://data.gtdb.ecogenomic.org/releases/latest/auxillary_files/gtdbtk_v2_data.tar.gz
$ tar xvzf gtdbtk_v2_data.tar.gz
$ export GTDBTK_DATA_PATH=/path/to/unarchived/gtdbtk/release000
# run GTDB-tk (gene calling)
$ gtdbtk identify --genome_dir bins_dir/bin --out_dir /gtdbtk/identify --extension fa --cpus 2
# run GTDB-tk (align)
$ gtdbtk align --identify_dir /gtdbtk/identify --out_dir /gtdbtk/align --cpus 2
# run GTDB-tk (classify)
$ gtdbtk classify --genome_dir /gtdbtk/genomes --align_dir /gtdbtk/align --out_dir /gtdbtk/classify -x fa --cpus 2
$ conda deactivate
```

![gtdb_results](https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_11_2.png?raw=true)

GTDB-tk [23] 이외에도 최근 많이 사용되는 프로그램으로 PhyloPhlAn [24]이 있으며 매우 정확하고 빠를뿐만 아니라 간단한 커맨드라인으로 대용량의 미생물 유전체를 characterization 및 phylogenetic tree를 만들 수 있으며 간단한 visualization을 할 수 있는 커맨드도 제공한다. 

```bash
$ conda activate phylophlan3
$ phylophlan_metagenomic -i bins_dir -o output_metagenomic --nproc 4 -n 1 -d SGB.Jan19 --verbose 2>&1
$ phylophlan_draw_metagenomic -i output_metagenomic.tsv -o output_heatmap --map bin2meta.tsv --top 20 --verbose 2>&1
$ conda deactivate
```
PhyloPhlAn 3.0의 phylophlan_metagenomic 명령어를 사용하면 메타게놈 어셈블리 분석에서 나온 각 Bin에 대해서 가장 가까운 species-level genome bins (SGBs)을 할당 할 수 있다.
이 명령어를 수행할 때 `–nproc` 옵션을 통해 CPU thread 수를 조정할수 있으며, `-n` 옵션을 통해서는 각 입력되는 Bin에 대해 보고할 SGB의 수를 결정 할 수 있으며 기본 값은 10이다.
phylophlan_metagenomic 명령어의 결과파일 3가지 이며 이중 bin들의 평균Mash distance에 따라 SGBs들의 리스트를 제공하는 결과파일은 phylophlan_draw_metagenomic 명령어를 통해 heatmap으로 시각화 될 수 있고 이때 `--map` 옵션에 들어가는 Bin들에 대한 mapping 파일은 `.tsv` 파일 형식을 갖는다.
![phylophlan_results](https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_11_3.png?raw=true)
