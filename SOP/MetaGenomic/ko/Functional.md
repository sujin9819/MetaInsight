# Functional annotation of contigs
<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_9_1.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>  
</figure>

Contig의 taxonomic annotation을 마치면 functional assignment를 하기 위해 contig 내 open reading frame에 관한 정보를 추출해야 한다.
Prodigal은 원핵생물의 protein coding sequence를 예측하는 기능을 가지며 complete 혹은 draft genome 분석 외에도 metagenome분석에도 활용될 수 있다.
Training이 필요하지 않은 unsupervised 머신 러닝 알고리즘을 쓰고 있으며 RBS 모티프, start codon usage나 coding statistics의 특성을 분석하여 예측할 수 있다.

```bash
# run prodigal
$ conda activate prodigal
$ prodigal -i final.contigs.fa -p meta -a final.contigs.prodigal.faa -d final.contigs.prodigal.fna -f gff -o final.contigs.prodigal.gff 
$ conda deactivate
```

Gene prediction이 완료된 contig 파일은 다양한 데이터베이스를 기반으로 functional annotation이 가능한데 가장 대표적으로 [KEGG](https://www.genome.jp/kegg/) 혹은 [COG](https://www.ncbi.nlm.nih.gov/research/cog-project/), [metaCyc](https://metacyc.org/) 데이터베이스를 통해 유전자의 기능을 유추할 수 있으며 [CAZyme](http://www.cazy.org/) 이나 [ARDB](https://ardb.cbcb.umd.edu/)와 같은 특수 데이터베이스 또한 활용이 가능하다.
[eggNOG-mapper](https://github.com/eggnogdb/eggnog-mapper)는 가장 광범위하게 쓰이는 functional annotation 프로그램으로써 European Molecular Biology Laboratory (EMBL)에서 제작한 ortholog와 phylogeny를 기반으로 제작된 eggNOG  database를 사용하여 novel 시퀀스의 빠른 functional annotation을 수행할 수 있다.
eggNOG-mapper 외에도 추가로 사용할 수 있는 tool로는 간단한 BLAST 혹은 [InterProScan](https://www.ebi.ac.uk/interpro/search/sequence/)과 같은 프로그램이 있다.


```bash
# run eggnog-mapper
$ conda activate eggnog
# download eggnog-mapper database
$ download_eggnog_data.py
# run eggnog-mapper
$ emapper.py -m diamond --cpu 5 -i final.contig.prodigal.faa -o eggnog.out
$ conda deactivate
```


<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_9_2.png?raw=true" style="width:90%">
  <figcaption><b>report.html 결과 예시</b></figcaption>  
</figure>

[eggNOG-mapper](http://eggNOG-mapper.embl.de/)는 stand alone버전 외에도 간단하게 web 상에서 분석할 수 있는 서비스를 제공하며 FASTA 포맷 내에서 최대 1000,000개의 protein까지 input으로 수용이 가능하다. 

