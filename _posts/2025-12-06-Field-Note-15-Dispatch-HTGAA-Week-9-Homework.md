---
layout: post
title: "Field Note 15: Dispatch - HTGAA Week 9 Homework"
author: Nourelden
categories: [FieldNotes]
tags: ["Djoser Genomics", "FieldNotes", "Dispatch", "HTGAA", "2025"]
image: "assets/images/Djoser Genomics Field Notes Landscape.png"
featured: false
hidden: true
---

## **Homework Part A**

### **1. Explain the main advantages of cell-free protein synthesis over traditional in vivo methods, specifically in terms of flexibility and control over experimental variables. Name at least two cases where cell free expression is more beneficial than cell production.**

Main advantages of cell-free protein synthesis include the ability to control the reaction environment precisely, You can add or remove components as needed, without the constraints of maintaining cell viability. This also allows the production of proteins that may be toxic to living cells. And also allows for rapid prototyping and testing of genetic constructs since there is no need for transformation and cell growth.

### **2. Describe the main components of a cell-free expression system and explain the role of each component.**

You need a blueprint that contains the sequence of the protein you want to make, you also need the machinery to read that blueprint and make the protein, this includes polymerases, ribosomes, tRNAs, and various enzymes. You also need energy sources like ATP and GTP to fuel the synthesis process, as well as amino acids, nucleotides, and cofactors that are essential for protein assembly and function.

### **3. Why is energy provision regeneration critical in cell-free systems? Describe a method you could use to ensure continuous ATP supply in your cell-free experiment.**

Energy provision regeneration is critical in cell-free systems because the synthesis of proteins is an energy-intensive process that requires a continuous supply of ATP. Without sufficient energy, the reaction will stall, leading to low yields of the target protein. One method to ensure a continuous ATP supply is to use a coupled enzymatic system, such as the phosphoenolpyruvate (PEP) and pyruvate kinase system, which regenerates ATP from ADP during the protein synthesis process. This helps maintain a steady level of ATP throughout the reaction.

### **4. Compare prokaryotic versus eukaryotic cell-free expression systems. Choose a protein to produce in each system and explain why.**

- Prokaryotic cell-free expression systems, are faster and more cost effective, suitable for producing simple proteins that do not require complex post transctriptional modifications. For example, it can be used to produce simple enzymes like lysozyme which do not require glycosylation.

- Eukaryotic cell-free expression systems, on the other hand, are better suited for producing complex proteins that require post translational modifications and complex folding. It can be used to produce some membrane protein or for example, Antibodies which require complex folding and modifications that eukaryotic systems have the machinery to perform.

### **5. How would you design a cell-free experiment to optimize the expression of a membrane protein? Discuss the challenges and how you would address them in your setup.**

Membrane proteins are challenging since they require a lipid environment to fold and function properly and not aggregate and become non functional. To optimize the expression of a membrane protein in a cell-free system, I would incorporate liposomes or nanodiscs into the reaction mixture to provide a suitable lipid environment for proper folding.

### **6. Imagine you observe a low yield of your target protein in a cell-free system. Describe three possible reasons for this and suggest a troubleshooting strategy for each.**

- Low ATP levels: I would monitor the ATP concentration throughout the reaction and consider adding an ATP regeneration system if levels drop significantly.

- Incomplete transcription or translation: I would check the integrity of the DNA template and ensure that all necessary components for transcription and translation are present in sufficient quantities.

- Protein degradation: I would include protease inhibitors in the reaction mixture to prevent degradation of the target protein during synthesis.

## **Homework Part B - Individual Final Project Report**

### 1. Provide an **abstract/narrative/summary** for your final project.

**Project Menhed** aims to decouple color production from the petrochemical industry by engineering a scalable, biosynthetic alternative for commercial red dyes. Drawing inspiration from the ancient Egyptian scribe’s palette, this project focuses on the biomanufacturing of Lycopene, a vibrant red carotenoid, using a metabolically engineered bacterial chassis. We will utilize a modern computational stack, including AlphaFold for enzyme structural validation and COBRApy for metabolic flux analysis, to model and optimize the MEP/DOXP pathway for maximum theoretical yield. By the end of this project, we aim to present a comprehensive in-silico design and validation of a bacterial dye factory that could revolutionize the dye industry by providing a sustainable and eco-friendly alternative.

### 2. Provide a **background and motivation** section for your final project.

The modern textile and dye industry is built on extraction and toxicity, contributing significantly to global industrial water pollution. Despite the biological potential of bacteria to produce vibrant pigments, biomanufacturing has struggled to compete economically with cheap petrochemical synthesis. My motivation for Project Menhed is to bridge this gap by applying rigorous software engineering principles to biology. By leveraging computational tools, I aim to design a bacterial strain capable of producing Lycopene at a cost that undercuts synthetic dyes.

### 3. Aims

- To design and model a bacterial strain capable of high-yield Lycopene production using the MEP/DOXP pathway.
- To validate enzyme structures involved in the pathway using AlphaFold.
- To perform metabolic flux analysis using COBRApy to optimize precursor supply and minimize byproduct formation

### 4. Describe any _unexpected challenge(s)_ you faced in planning or executing your final project.

Data Gap is one of the major struggles, Extensive data on enzyme kinetics, expression levels, and metabolic fluxes are often unavailable or incomplete for non-model organisms. This lack of data can hinder accurate modeling and simulation efforts.

### 5. Describe the **_bioethical considerations_** involved in your project.

- Biosafety: Ensuring that any genetically modified organisms (GMOs) designed in silico do not pose a risk to human health or the environment if they were to be physically constructed in the future.
- Environmental Impact: Considering the potential environmental benefits of reducing reliance on petrochemical dyes while also assessing any unintended ecological consequences of deploying engineered organisms.

### 6. Describe any **_future work_**

- Experimental Validation: Once the in-silico designs are finalized, the next step would be to collaborate with a wet lab to physically construct and test the engineered bacterial strains for Lycopene production.
- Expansion to Other Pigments: Explore the potential for engineering bacteria to produce other commercially valuable pigments beyond Lycopene, such as carotenoids or anthocyanins, to broaden the impact of the project.
