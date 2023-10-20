#Sequencing

## [1] Biological samples
1. Fecal sample 1 g 당 500ul RNAlater (Ambion)를 처리하여 -80℃에 보관한다. 

## [2] RNA preparation
### Reagents
-RLT buffer (Qiagen), β-mercaptoethanol, Superase-In 20U/μL (Thermo Fisher Scientific), proteinase K (20mg/mL), 100% ethanol, 70% ethanol, 3M sodium acetate, phenol/chloroform/isoamyl alcohol 25:24:1 (pH5.2), RNase-free water
-kit RNeasy mini plus kit (Qiagen), TURBO DNA-free™ (Ambion) 

### Equipment  
FastPrep-24™ 5G(MP), pipette, aerosol barrier pipette tips, microcetrifuge, 1mm zirconia/silica beads  
Optional; Qubit fluorometer (Thermo Fisher Scientific), Fragment analyzer  

### Stock solutions

| Stock solution A | volume |
| --- | ---|
| RLT buffer(Qiagen) | 975 μL |
| β-mercaptoethanol | 10 μL |
| Superase-In, 20U/μL | 15 μL |
| Total | 1 ml |

### RNA preparation
1. 각 screw-top tube에 fecal sample과 bead를 넣고 반응액을 처리한다.  
| Each tube | volume |
| --- | --- |
| Fecal sample | 150mg |
| 1.0mm zirconia/silica beads | ~20 |
| Stock solution A | 600 μL |

2. FastPrep-24™ 6.0m/s 40초 두 번 진행한다.
3. 12,000 rpm에서 3분간 원심분리 후, 상층액 600 μL를 e-tube 로 옮긴다.
4. Proteinase K 15 μL를 처리하고 상온에서 10분 반응시켜준다.
5. 12,000 rpm에서 3분간 원심분리 후, 상층액을 새 e-tube로 옮긴다.
6. 상층액과 같은 양의 phenol/chloroform/isoamyl alcohol 25:24:1을 처리하고 3분 vortexing한다.
7. 12,000 rpm에서 3분간 원심분리 후, 상층액을 새 e-tube로 옮기는 과정을 두 번 진행한다.
8. 상층액의 0.1배 volume의 3M sodium acetate와 2.5배 volume의 ethanol을 처리하고 30분 ice에서 반응시킨다
9. 12,000 rpm 4℃에서 30분간 원심분리 후, 상층액을 제거한다.
10. 100 μL 증류수로 pellet을 재현탁하고 RNeasy plus mini kit의 RLT plus buffer 600 μL를 처리한다
11. `10`의 용액을 RNeasy plus mini kit의 gDNA eliminator spin column에 처리한다.
12. 12,000 rpm에서 30초간 원심분리 후 column을 버리고 통과액에 1:1 비율로 70% ethanol을 처리한다.
13. RNeasy spin column에 `12`의 용액 700 μL를 옮기고 12,000 rpm에서 15초 원심분리 후 통과액을 버린다.
14. RW1 buffer 700 μL를 column에 처리하고 12,000 rpm에서 15초 원심분리 후 통과액을 버린다.
15. RPE buffer 500 μL를 column에 처리하고 12,000 rpm에서 15초 원심분리 후 통과액을 버린다.
16. RPE buffer 500 μL를 column에 처리하고 12,000 rpm에서 2분 원심분리 후 column을 새 e-tube에 옮긴다.
17. RNase-free water 30~50 μL를 column의 membrane에 처리하여 12,000 rpm에서 1분 원심분리 후 RNA를 얻는다.

[Optional: RNA QC]
18. Qubit fluorometer*로 RNA 농도를 측정한다.  
*NanoDrop spectrophotometer도 사용 가능 하지만 정확한 농도 측정을 위해 Qubit fluorometer를 추천함
19. Fragment analyzer를 활용하여 얻어진 RNA의 QC를 진행한다.

![Fragment analyzer 활용 RNA sample 분석 결과 예시](https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_2_1.png?raw=true)
> Fragment analyzer 활용 RNA sample 분석 결과 예시 

20. 10X TURBO DNase buffer가 1X가 되도록 처리하고, TURBO DNase 1 μL와 RNA에 처리한다
21. 37℃에 20-30분 반응시켜준다.
22. 0.1배의 DNase inactivation reagent를 처리한다.
23. 상온에서 5분 반응시켜준다
24. 10,000rpm에서 1분 30초 원심분리 후 상층액을 새 e-tube에 옮긴다.

### rRNA depletion
-Host rRNA 제거 Illumina TruSeq Stranded Total RNA Library Prep Plant Kit (Illumina, # 20020611)
-Bacterial rRNA 제거 Illumina Stranded Total RNA Library Prep with Ribo-Zero Plus kit (Illumina, #20040529)


## [3] Sequencing
### Sequencing library preparation  
-Divalent cations을 활용하여 mRNA fragmentation 수행  
-First strand cDNA 합성 SuperScript II reverse transcriptase (Invitrogen, #18064014), random primers 활용  
-Second strand cDNA 합성DNA Polymerase I, RNase H, dUTP  
-합성된 cDNA fragments로 end repair 진행, single ‘A’ 염기 부착 후 adaptor ligation  
-cDNA library 제작을 위한 PCR 수행  
*Sequencing library의 quantification 진행  
KAPA Library Quantificatoin kits for Illumina Sequecing platforms according to the qPCR Quantification Protocol Guide (KAPA BIOSYSTEMS, #KK4854)  
*Sequencing library의 QC 진행  
TapeStation D1000 ScreenTape (Agilent Technologies, # 5067-5582)   

### Sequencing  
-Indexing 된 최종 sequencing library로 Illumina NovaSeq (Illumina) 장비로 paired-end (2×150 bp) sequencing 수행함  
