# Transcript _de novo_ assembly

메타유전체 분석 결과에 read를 mapping하는 방식으로 이루어지는 reference-guided 방식이 아닌, reference-independent 분석을 통해서도 얻을 수 있는 고유의 정보들이 있다.
메타전사체 데이터로 de novo assembly를 수행하면 (putative) transcriptional segment의 정보를 얻을 수 있다.

Assembly에 사용할 프로그램은 SPAdes라는 프로그램이다.
이 프로그램은 다양한 타입의 데이터를 지원하며 input 데이터에 따라 사용하는 명령어의 옵션이 달라진다. 메타유전체 데이터를 사용하면 metaSPAdes(또는 `--meta`)를 사용하고, RNA-seq reads를 사용하여 de novo assembly을 하고자 한다면 rnaSPAdes를 사용한다.
참고로, 그 외에도 plasmid, metaplasmid, RNA virus data등 다양한 종류의 input 데이터를 이용하여 assembly을 진행할 수 있다. 


```bash
#install SPAdes
$wget http://cab.spbu.ru/files/release3.15.3/SPAdes-3.15.3-Linux.tar.gz
$tar -xzf SPAdes-3.15.3-Linux.tar.gz
$cd SPAdes-3.15.3-Linux/bin/
#SPAdes running
#RNA single ends
$spades.py –-rna –s single_end_trimmed.fastq –o sample
#RNA paired ends
$spades.py –-rna –1 forward_trimmed.fastq -2 reverse_trimmed.fastq –o sample
```
