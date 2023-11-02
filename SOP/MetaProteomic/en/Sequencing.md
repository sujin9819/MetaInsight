# Sequencing
## Biological Samples
- Process 500 µL of RNAlater (Ambion) for every 1 g of fecal sample and store it at -80°C

## Ribosome-bound mRNA prep
### Reagents
- RLT buffer (Qiagen), β-mercaptoethanol, Superase-In 20U/μL, 100% ethanol, 3M sodium acetate, chloramphenicol 50mg/ml, 1M Tris-HCl (pH8.0), 1M NH4Cl, 1M MgOAc, RNase-free water, Ipecal CA-630, 1M MgCl2, 0.5M EGTA, 5M NaCl, MNase (NEB), 0.5M CaCl2, Qiazol (Qiagen), chloroform
- kit 
miRNeasy mini kit (Qiagen), TURBO DNA-free™ Kit (Ambion)  

### Equipment
FastPrep-24™ 5G, pipette, aerosol barrier pipette tips, microcentrifuge, 1mm zirconia/silica beads, Sephacryl S400 Microspin columns (Sigma-Aldrich)  
Optional; Qubit fluorometer (Thermo Fisher Scientific), Fragment analyzer

### Stock solutions

| stock solution A | volume |
| ---| --- |
| RLT buffer(Qiagen) | 965 μL |
| β-mercaptoethanol | 10 μL |
| Superase-In, 20U/μL | 15 μL |
| Chloramphenicol, 50mg/ml | 10 μL |
| Total | 1 ml |

| stock solution B | volume |
| ---| --- |
| Tris-HCl, pH 8.0,  1M | 25 μL |
| NH4Cl, 1M | 25 μL |
| MgOAc, 1M | 10 μL |
| Chloramphenicol, 50mg/ml | 10 μL |
| RNase-free water | 930 μL |
| Total | 1 ml |

| stock solution C | volume |
| ---| --- |
| Ipegal CA-630 | 100 μL |
| MgCl2, 1M | 500 μL |
| EGTA 0.5M | 500 μL |
| NaCl, 5M | 500 μL |
| Tris-HCl, pH 8.0, 1M | 500 μL |
| RNase-free water | 7.9 ml |
| Total | 10 ml |

### Ribosome-bound mRNA preparation
- Place a fecal sample and beads in each screw-top tube.
| Each tube | volume |
| ---| --- |
| Fecal sample | 150mg |
| 1.0mm zirconia/silica beads | ~20 |
| Stock solution A | 600 μL |
- Perform two rounds of MP FastPrep at 6.0 m/s for 40 seconds each.
- Centrifuge at 12,000 rpm for 3 minutes, and transfer 500 μL of the supernatant to a new e-tube.
- Add 50 μL of 3M sodium acetate and 1 mL of 100% ethanol to the supernatant.
- Incubate on ice (or at 4°C) for 30 minutes.
- Centrifuge at 12,000 rpm at 4°C for 30 minutes, and discard the supernatant.
- Re-suspend in 100 μL of Stock solution B.
- Dilute RNA 1/50 and measure RNA concentration with a Qubit.
- Incubate with MNase for 2 hours. 
| Total  | 200μL |
| ---| --- |
| Lysate | 80 μg |
| 0.5M CaCl2 | 2 μL |
| Superase-In (20U/μL) | 2 μL |
| NEB MNase (500U/μL) | 1 μL |
| RNase free water | To 200 μL |
- Add 2.5 μL of 0.5M EGTA to stop the reaction.
- Prepare a Sephacryl S400 MicroSpin column and re-suspend the resin inside the column.
- Centrifuge the column at 600 rpm for 1 minute, discard the flow-through.
- Add 500 μL of Stock solution C to the column, centrifuge at 600 rpm at 4°C for 1 minute, and discard the flow-through (repeat this step).
- Add 500 μL of Stock solution C to the column, centrifuge at 600 rpm at 4°C for 4 minutes, and transfer the column to a new e-tube.
- Add 100 μL of the MNase reaction mixture (from step 10) to each column, centrifuge at 600 rpm for 2 minutes, and collect the flow-through.
- Add 700 μL of Qiazol to the collected flow-through, vortex, and incubate at room temperature for 5 minutes.
- Add 140 μL of chloroform, shake for 15 seconds, and incubate at room temperature for 3 minutes.
- Centrifuge at 12,000 rpm at 4°C for 15 minutes, and transfer the upper phase to a new e-tube.
- Add approximately 525 μL (1.5 times the upper phase volume) of 100% ethanol to the upper phase and mix by pipetting. *
- Load the solution from step * onto an RNeasy mini column and centrifuge at 12,000 rpm for 15 seconds to discard the flow-through.
- Repeat previous step with the remaining solution from step *.
- Add 700 μL of RWT buffer to the column, centrifuge at 12,000 rpm for 15 seconds to discard the flow-through.
- Add 500 μL of RPE buffer to the column, centrifuge at 12,000 rpm for 15 seconds to discard the flow-through.
- Add 500 μL of RPE buffer to the column, centrifuge at 12,000 rpm for 2 minutes to discard the flow-through. Then, transfer the column to a new e-tube.
- Add 30-50 μL of RNase-free water to the column membrane, centrifuge at 12,000 rpm for 1 minute, and collect the ribosome-bound mRNA.

**[Optional: QC]**  
- Measure the RNA concentration using a Qubit fluorometer*.  
*A NanoDrop spectrophotometer can also be used, but for accurate concentration measurement, it is recommended to use a Qubit fluorometer.
- Perform QC of the obtained RNA using a Fragment analyzer.
<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaProteomic/img/P_2_1.png?raw=true" style="width:90%">
  <figcaption><b>Example of ribosome-bound mRNA sample analysis results using a Fragment analyzer</b></figcaption>  
</figure>
A Fragment Analyzer can be used to assess the proportion of rRNA in RNA samples, in addition to mRNA. Unlike mRNA prepared for transcriptome analysis, ribosome profiling selectively prepares short mRNA fragments that are associated with ribosomes and small-sized rRNA.

- Prepare the 10X TURBO DNase buffer to a 1X concentration and add 1 μL of TURBO DNase to the RNA.
- Incubate at 37°C for 20-30 minutes.
- Add 0.1 times the volume of DNase inactivation reagent.
- Incubate at room temperature for 5 minutes.
- Centrifuge at 10,000 rpm for 1 minute and 30 seconds, and transfer the supernatant to a new e-tube.

### rRNA depletion
- Host rRNA remove Illumina TruSeq Stranded Total RNA Library Prep Plant Kit (Illumina, # 20020611)
- Bacterial rRNA remove Illumina Stranded Total RNA Library Prep with Ribo-Zero Plus kit (Illumina, #20040529)

## Sequencing
### Sequencing library preparation  
- Perform mRNA fragmentation using divalent cations.
- First strand cDNA synthesis using SuperScript II reverse transcriptase (Invitrogen, #18064014) with random primers. 
- Second strand cDNA synthesis using DNA Polymerase I, RNase H, and dUTP. 
- Perform end repair on synthesized cDNA fragments, followed by the attachment of a single 'A' base and adaptor ligation.  
- Perform PCR to create the cDNA library for sequencing.  
*Progress Sequencing library quantification  
KAPA Library Quantificatoin kits for Illumina Sequecing platforms according to the qPCR Quantification Protocol Guide (KAPA BIOSYSTEMS, #KK4854)  
*Conduct quality control (QC) for the sequencing library.  
TapeStation D1000 ScreenTape (Agilent Technologies, # 5067-5582)     

### Sequencing  
- Perform paired-end (2×150 bp) sequencing on an Illumina NovaSeq (Illumina) instrument using the final indexed sequencing library. 


