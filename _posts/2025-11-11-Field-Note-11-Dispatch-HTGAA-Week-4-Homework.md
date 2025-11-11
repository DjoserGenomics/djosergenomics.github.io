---
layout: post
title: "Field Note 11: Dispatch - HTGAA Week 4 Homework"
author: Nourelden
categories: [FieldNotes]
tags: ["Djoser Genomics", "FieldNotes", "Dispatch", "HTGAA", "2025"]
image: "assets/images/Djoser Genomics Field Notes Landscape.png"
featured: false
hidden: true
---

## **Part B: Protein Analysis and Visualization**

### **Pick any protein (from any organism) of your interest that has a 3D structure and answer the following questions.**

#### **Briefly describe the protein you selected and why you selected it.**

Tyrosinase is an enzyme that plays a crucial role in the production of melanin pigment. As part of my interest in producing different colors and pigments using synthetic biology, I selected tyrosinase and the melanin pathway as my focus for this phase becuase it is a one enzyme pathway and should be relatively simple to work with.

#### **Identify the amino acid sequence of your protein.**

`MSNKYRVRKNVLHLTDTEKRDFVRTVLILKEKGIYDRYIAWHGAAGKFHTPPGSDRNAAHMSSAFLPWHREYLLRFERDLQSINPEVTLPYWEWETDAQMQDPSQSQIWSADFMGGNGNPIKDFIVDTGPFAAGRWTTIDEQGNPSGGLKRNFGATKEAPTLPTRDDVLNALKITQYDTPPWDMTSQNSFRNQLEGFINGPQLHNRVHRWVGGQMGVVPTAPNDPVFFLHHANVDRIWAVWQIIHRNQNYQPMKNGPFGQNFRDPMYPWNTTPEDVMNHRKLGYVYDIELRKSKRSS`

##### _How long is it? What is the most frequent amino acid?_

The Tyrosinase protein is 297 amino acids long. The most frequent amino acid is Proline (P), which appears 22 times.

##### _How many protein sequence homologs are there for your protein?_

Against the **ClusteredNR** database, there are 100 clusters of homologous sequences, some clusters range from 1-12 members, with a cluster contaning 166 members being the largest.

##### _Does your protein belong to any protein family?_

Tyrosinase belongs to the **Tyrosinase and Hemocyanin** family and the **Di-copper centre-containing domain superfamily**

#### **Identify the structure page of your protein in RCSB**

##### _When was the structure solved? Is it a good quality structure?_

The structure of Tyrosinase was deposited on **22nd June 2010**. It is of good quality with a resolution of **2.00 Å**.

##### _Are there any other molecules in the solved structure apart from protein?_

Yes, It contains **Copper (II) ions**, **Zinc ions**, **Chloride ions** & **Water molecules (HOH)**.

##### _Does your protein belong to any structure classification family?_

According to **SCOP/SCOPe Classification** it is classified as **All alpha proteins** and according to **CATH Classification** it belongs to the **Mainly alpha class**.

#### **Open the structure of your protein in any 3D molecule visualization software**

##### _Color the protein by secondary structure. Does it have more helices or sheets?_

It has more helices than sheets, I have colored the **Alpha Helices** in red and the **Beta Sheets** in yellow.

<div style="text-align: center;">
  <img src="/assets/images/posts/Field-Note-11-Dispatch-HTGAA-Week-4-Homework/Tyrosinase Structural View.PNG" alt="Structural View of Tyrosinase" width="600"/>
  <p style="font-size: 0.8em; color: gray;">Structural View of Tyrosinase (Red Alpha Helices, Yellow Beta Sheets)</p>
</div>

##### _Color the protein by residue type. What can you tell about the distribution of hydrophobic vs hydrophilic residues?_

Hydrophilic Residues (in Blue) are more abundant than the Hydrophobic Residues (in Red).

<div style="text-align: center;">
  <img src="/assets/images/posts/Field-Note-11-Dispatch-HTGAA-Week-4-Homework/Tyrosinase Hydrophilic vs Hydrophobic.PNG" alt="Tyrosinase Hydrophilic vs Hydrophobic" width="600"/>
  <p style="font-size: 0.8em; color: gray;">Hydrophilic (Blue) vs Hydrophobic (Red) Residues in Tyrosinase</p>
</div>

##### _Visualize the surface of the protein. Does it have any "holes" (aka binding pockets)?_

It has 2 binding pockets, I have colored the **Copper (II) ions** in orange to highlight the location of binding pockets.

<div style="text-align: center;">
  <img src="/assets/images/posts/Field-Note-11-Dispatch-HTGAA-Week-4-Homework/Tyrosinase Active Sites.PNG" alt="Tyrosinase Active Sites" width="600"/>
  <p style="font-size: 0.8em; color: gray;">Active Sites of Tyrosinase (Copper (II) ions in Orange) - Transparency = 0.35</p>
</div>

---

## **Part C. Using ML-Based Protein Protein Tools**

### **Fold your protein with AlphaFold or ESMFold or Boltz and compare it to the real structure.**

I folded my 297 amino acid Tyrosinase sequence using the AlphaFold web server. The resulting prediction was highly accurate and very similar to the experimental PDB structure (3NM8).

> Note that i used AlphaFold Monomer for this prediction, while the Tyrosinase structure is a Dimer.

<div style="text-align: center;">
  <img src="/assets/images/posts/Field-Note-11-Dispatch-HTGAA-Week-4-Homework/Alphafold Tyrosinase Monomer.png" alt="AlphaFold Tyrosinase Monomer" width="600"/>
  <p style="font-size: 0.8em; color: gray;">AlphaFold Prediction of Tyrosinase Monomer</p>
</div>

#### _Any predicted vs. experimental differences._

Apart from the Dimer vs Monomer difference, the alphafold prediction doesn't also show the Copper (II) ions that are present in the experimental structure.

#### _Low-confidence regions and why do you think they are low confidence?_

The prediction was extremely confident, with a pTM score of 0.95. The vast majority of the structure was "dark blue," indicating very high confidence. There were only a few small loops with lower confidence (yellow to orange), likely due to their inherent flexibility or lack of defined structure.

### **Inverse-fold your structure with ProteinMPNN**

#### _What sequence do you get?_

`>T=0.1, sample=0, score=0.7689, seq_recovery=0.4561
MSRVRKPVEDLTDEEWKKYVAAVQKLRDDGTYRKFVDDWRDAYLHKIPPGSTRNAIANGPSFIPAHIAMLYRFEKALQAVDPTVTLPYIDFDKIAELEDPSKSIVFRDDRLGGNGDAATGNKVTTGPFAAGKWETYDANGNPSGGLTRNLGASAEAPKLPTQAEVDAALKIKNYSTPPYDETSKNSFVNAIEGYENYPKLFRRILKWFGGEMATPLTAMNDPAFWLIHAYVVKVYDKWKKKHKNVSYYPKSGGPKGANYNDPIYPTDITAKDVEDLEKLGFRFAG`

#### _Is it the same as the original sequence you folded? Why yes or no?_

No, it was completely different from the original (the "sequence recovery" was only 45%).

This is because the **amino acid code** is redundant, just like the DNA codon code. many amino acids can code for the same structural job. so 2 diffrerent amino acid sequences can fold into very similar 3D structures that have the same function or job.

---

**Part D. Group Brainstorm on Bacteriophage Engineering**

You can View the _Proposal_ Through [Here]({{site_baseurl}}/Armored-Phage-A-Thermostable-MS2-Phage-Proposal/)
