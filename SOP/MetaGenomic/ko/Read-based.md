# Read-based profiling 

Preprocessing이 완료된 reads를 분석하는 방법은 read-based profiling과 assembly-based profiling으로 나뉠 수 있다.
Read-based profiling은 assembly 과정 없이 taxonomic profiling과 functional profiling을 진행하며 주로 k-mer matching을 사용한다. 이러한 과정은 assemble이 쉽지 않은 low depth의 샘플들을 분석할 때 용이하고, 비교적 빠른 시간 안에 분석을 완료할 수 있다는 장점이 있다.
[HUMAnN 3.0](https://huttenhower.sph.harvard.edu/humann/)은 MetaPhlAn 프로그램을 이용하여 pre-taxonomic profiling을 한 뒤 unmapped reads를 대상으로 translated search를 진행하여 추가 분석 및 전체 pangenome에 대한 gene family 및 pathway의 정량화를 수행한다.

```bash
# download database
$ conda activate humann
$ humann_databases --download chocophlan full /database/humann
$ humann_databases --download uniref uniref90_diamond /database/humann
# concatenate all reads into a single FASTAQ file
$ cat kneaddata.trimmed.1.fastq kneaddata.trimmed.2.fastq > kneaddata.trimmed.fastq
# run human 3.0
$ humann3 --input kneaddata.trimmed.fastq --output humann3_out/ --nucleotide-database /database/humann/chocophlan/ --protein-database /database/humann/uniref/
```

▶Output files 예시
1. HUMAnN 3.0_genefamilies.tsv  
: Gene family의 abundance를 뜻하며 reads per kilobase (RPK) 값으로 계산된다. Taxonomy assignment가 성공적으로 수행된 경우 각 미생물 별로 contribution 값이 지정되어 나뉘어 출력된다. Gene family 들은 UniRef90 identifier가 “|” 구분자를 기점으로 첫 컬럼에 출력되고 부재 시 UniRef90_unknown으로 출력된다.

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_6_1.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>  
</figure>

2. HUMAnN 3.0_pathabundance.tsv  
: 각 샘플들의 pathway abundance를 나타내며 gene families 결과와 동일하게 RPK 값으로 계산된다. “|” 구분자를 기점으로 각 미생물들의 contribution 정도에 따라 나뉘어진다.

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_6_2.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>  
</figure>

서로 다른 시퀀싱 depth를 가지는 샘플들끼리 gene family들을 비교하기 위해서 relative abundance 수치 (relab)를 구하거나 유전자의 copy number를 백만read로 나누는 counts per million (CPM) 수치를 구하여 normalization을 수행할 수 있다. 이는 Human_renorm_table 커맨드에서 –-units 옵션에서 cpm 또는 relab으로 정해주면 된다.
```bash
# Normalization 
$ humann_renorm_table --input Trimmed_paired_merged_genefamilies.tsv --output Trimmed_paired_merged_genefamilies_relab.tsv --units cpm
```

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_6_3.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>  
</figure>

Normalization이 끝나면 UniRef gene families를 default database인 MetaCyc의 reaction 단위로 그룹화 한 뒤 abundance를 재 구성할 수 있다.
```bash
# Generate barplot for specific pathway
$ humann_barplot --input Trimmed_paired_merged_genefamilies_relab.tsv --output plot1.png --focal-feature 2-ISOPROPYLMALATESYN-RXN
# Generate sorted barplot by total sum of abundances
$ humann_barplot --input Trimmed_paired_merged_genefamilies_relab.tsv --output plot2_sorted.png --focal-feature 2-ISOPROPYLMALATESYN-RXN -–sort sum 
# Generate sorted barplot by bray-curtis distance and facetted by genera
$ humann_barplot --input Trimmed_paired_merged_genefamilies_relab.tsv --output plot3_sorted_facetted.png --focal-feature COA-PWY -–sort braycurtis –-as-genera –-remove-zeros
```
Reaction 단위로 그룹화 이후 특정 reaction을 plotting할 수 있으며 전체 abundance의 합을 기준으로 하거나 또는Bray-Curtis 거리 기준으로 bar graph들을 sorting하거나 genera 단위로 faceting 할 수 있다.
  
<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_6_4.png?raw=true" style="width:90%">
  <figcaption><b>Bar plot for METSYN_PWY (plot1.png)</b></figcaption>  
</figure>
  
<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_6_5.png?raw=true" style="width:90%">
  <figcaption><b>Sorted bar plot for METSYN_PWY (plot1_sorted.png)</b></figcaption>  
</figure>
  
<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_6_6.png?raw=true" style="width:90%">
  <figcaption><b>Sorted and facetted bar plot for COA-PWY</b></figcaption>  
</figure>
