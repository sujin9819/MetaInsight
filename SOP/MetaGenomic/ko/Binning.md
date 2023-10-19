# Binning
![pipeline](https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_10_1.png?raw=true)  
Metagenome 분석에서 binning이란 contig들을 특정 조건하에 그룹화 시키는 과정으로써 주로 sequence의 조성과 coverage 데이터가 사용된다.
Binning 프로그램을 통해 contig를 클러스터링 함으로써 완성도 높은 하나의 미생물 유전체를 확보할 수 있으며 오염도(contamination)와 완벽도 (completeness)에 따라서 quality 측정이 가능하다.
MetaBAT2 [18]외에도 광범위하게 쓰이는 다른 binning 프로그램으로는 MaxBin 2.0 [19], CONCOCT [20]가 있다.  
MetaBAT2를 이용하여 binning을 하기 위해선 coverage information을 포함한sam 파일이 필요한데, short reads데이터의 경우,  이는 BBmap 스크립트를 사용하여 assembly 된 contig를 template로 trimmed sequence를 mapping 하여 얻을 수 있다.
Long read 데이터의 경우, bbmap 대신 minimap2를 사용하여 mapping을 수행한다.
형성된 sam파일을 압축하고 indexing 하여 바이너리 형식인 bam파일로 변환한다.

```bash
# calculate coverage information from short reads assembly
$ conda activate bbmap
$ bbmap.sh in=trimmed.reads_1.fastq in2=trimmed.reads_2.fastq covstats=covstats.txt out=MEGAHIT.sam threads=3 ref=/MEGAHIT_result/final.contigs.fa
$ conda deactivate 

# generate bam file from sam file
$ conda activate samtools
$ samtools view -bS -o MEGAHIT.bam MEGAHIT.sam -@ 5
# sort the bam file
$ samtools sort MEGAHIT.bam –o MEGAHIT.sorted.bam -@ 5
$ conda deactivate 
```

```bash
# calculate coverage information  from long reads assembly
$ conda activate minimap2
# align host read-filtered read file(N008.aln.unamapped.fq) to assembled contig file(N_008_HiFi.p_ctg.fa)
$ minimap2 -ax map-hifi N_008_HiFi.p_ctg.fa N008.aln.unmapped.fq > N_008_HiFi.p_ctg_mapped.sam
$ conda deactivate 

# generate bam file from sam file
$ conda activate samtools
$ samtools view -bS -o N_008_HiFi.p_ctg_mapped.bam N_008_HiFi.p_ctg_mapped.sam -@ 5
# sort the bam file
$ samtools sort N_008_HiFi.p_ctg_mapped.bam -o 
```

Coverage 정보인 bam파일이 준비되면 MetaBAT2에서 제공하는 jgi_summarize_ bam_contig_depth 스크립트를 사용하여 최종 depth.txt 파일을 생성한 뒤 assemble한 contig와 함께 binning을 수행한다. 
```bash
$ conda activate MetaBAT2
# generate depth file from bam file
$ jgi_summarize_bam_contig_depths --outputDepth jgi.depth.txt MEGAHIT.sorted.bam
# run MetaBAT2
$ MetaBAT2 -i final.contigs.fa -a jgi.depth.txt -o bins_dir/bin
$ conda deactivate 
```

MetaBAT2를 이용하여 binning이 완료된 후 형성된 bin들의 quality control을 CheckM [21]을 사용하여 시행한다.
CheckM은 복원된 isolates, single cell 혹은 metagenome에서 복원된 유전체의 quality를 측정해주는 프로그램으로써 유전체가 가지는 single copy 유전자를 이용하여 phylogenetic lineage와 유전적 특성 (GC contents, coding density) 그리고 contamination과 completeness 그리고 strain heterogeneity 정보를 제공한다.

```bash
$ conda activate CheckM
# download CheckM database from https://data.ace.uq.edu.au/public/CheckM_databases/
$ export CHECKM_DATA_PATH=/path/to/my_CheckM_data
# run CheckM
$ CheckM lineage_wf –x fa bins_dir bins_CheckM
```
▶CheckM결과 예시  
생성된 Bin이 속해 있는 marker lineage와 마커유전자 개수, 그리고 마지막 세 열에는 복원된 유전체의 completeness, contamination, strain heterogeneity가 출력된다.

![checkm_results](https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_10_2.png?raw=true)
