#Sequencing

## [1] Biological samples
1. Process 500 µL of RNAlater (Ambion) for every 1 g of fecal sample and store it at -80°C

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
1. Place fecal sample and beads in each screw-top tube and process the reaction mixture.  
| Each tube |  |
| --- | --- |
| Fecal sample | 150mg |
| 1.0mm zirconia/silica beads | ~20 |
| Stock solution A | 600 μL |

2. Perform two cycles of FastPrep-24™ at 6.0 m/s for 40 seconds each.
3. Centrifuge at 12,000 rpm for 3 minutes, transfer 600 μL of the supernatant to an e-tube.
4. Add 15 μL of Proteinase K and incubate at room temperature for 10 minutes.
5. Centrifuge at 12,000 rpm for 3 minutes, and transfer the supernatant to a new e-tube.
6. Treat with an equal volume of phenol/chloroform/isoamyl alcohol 25:24:1 and vortex for 3 minutes.
7. Centrifuge at 12,000 rpm for 3 minutes, and repeat the process of transferring the supernatant to a new e-tube twice.
8. Add 0.1 times the volume of 3M sodium acetate and 2.5 times the volume of ethanol to the supernatant and incubate on ice for 30 minutes.
9. Centrifuge at 12,000 rpm at 4°C for 30 minutes and remove the supernatant.
10. Resuspend the pellet in 100 μL of distilled water and add 600 μL of RLT plus buffer from the RNeasy plus mini kit.
11. Apply the solution from step 10 to the gDNA eliminator spin column of the RNeasy plus mini kit.
12. Centrifuge at 12,000 rpm for 30 seconds, discard the column, and treat the flow-through with 70% ethanol at a 1:1 ratio.
13. Transfer the solution from step 12 to the RNeasy spin column, centrifuge at 12,000 rpm for 15 seconds, and discard the flow-through.
14. Add 700 μL of RW1 buffer to the column, centrifuge at 12,000 rpm for 15 seconds, and discard the flow-through.
15. Add 500 μL of RPE buffer to the column, centrifuge at 12,000 rpm for 15 seconds, and discard the flow-through.
16. Add another 500 μL of RPE buffer to the column, centrifuge at 12,000 rpm for 2 minutes, and transfer the column to a new e-tube.
17. Treat the column's membrane with 30-50 μL of RNase-free water and centrifuge at 12,000 rpm for 1 minute to obtain RNA.

[Optional: RNA QC]
18. Measure the RNA concentration using a Qubit fluorometer.  
*A NanoDrop spectrophotometer can also be used, but for accurate concentration measurement, it is recommended to use a Qubit fluorometer.
19. Perform QC of the obtained RNA using a Fragment analyzer.

![Example of RNA sample analysis results using a Fragment analyzer.](https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_2_1.png?raw=true)
> Example of RNA sample analysis results using a Fragment analyzer.

20. Prepare the 10X TURBO DNase buffer to a 1X concentration and add 1 μL of TURBO DNase to the RNA.
21. Incubate at 37°C for 20-30 minutes.
22. Add 0.1 times the volume of DNase inactivation reagent.
23. Incubate at room temperature for 5 minutes.
24. Centrifuge at 10,000 rpm for 1 minute and 30 seconds, and transfer the supernatant to a new e-tube.

### rRNA depletion
-Host rRNA remove Illumina TruSeq Stranded Total RNA Library Prep Plant Kit (Illumina, # 20020611)
-Bacterial rRNA remove Illumina Stranded Total RNA Library Prep with Ribo-Zero Plus kit (Illumina, #20040529)


## [3] Sequencing
### Sequencing library preparation  
-Perform mRNA fragmentation using divalent cations.
-First strand cDNA synthesis using SuperScript II reverse transcriptase (Invitrogen, #18064014) with random primers.
-Second strand cDNA synthesis using DNA Polymerase I, RNase H, and dUTP. 
-Perform end repair on synthesized cDNA fragments, followed by the attachment of a single 'A' base and adaptor ligation.  
-Perform PCR to create the cDNA library for sequencing.
*Progress Sequencing library quantification 
KAPA Library Quantificatoin kits for Illumina Sequecing platforms according to the qPCR Quantification Protocol Guide (KAPA BIOSYSTEMS, #KK4854)  
*Conduct quality control (QC) for the sequencing library.  
TapeStation D1000 ScreenTape (Agilent Technologies, # 5067-5582)   

### Sequencing  
-Perform paired-end (2×150 bp) sequencing on an Illumina NovaSeq (Illumina) instrument using the final indexed sequencing library. 
