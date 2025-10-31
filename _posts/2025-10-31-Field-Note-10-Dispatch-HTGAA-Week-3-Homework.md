---
layout: post
title: "Field Note 10: Dispatch - HTGAA Week 3 Homework"
author: Nourelden
categories: [FieldNotes, HTGAA]
tags: ["Djoser Genomics", "FieldNotes", "Dispatch"]
image: "assets/images/Djoser Genomics Field Notes Landscape.png"
featured: false
hidden: true
---

### **Write a description about what you intend to do with automation tools for your final project. You may include example pseudocode or Python scripts, procedures you may need to automate, 3D printed holders you may need, and more.**

My project is to create a "Bacterial Color Factory" using E. coli strain with multiple dye pathways. The biggest bottleneck will be the "Test" phase, since I will need to test many different versions of my engineered bacteria against a wide variety of conditions (e.g., different sugar levels, different temperatures). Doing this by hand in 96-well plates is time consuming and very susceptible to human error.

I would use the Opentrons to automate this high-throughput screening. I would write a Python protocol to perfectly and quickly prepare a 96-well test plate. The robot would be responsible for mixing every combination of (bacterial strain + chemical inducer + growth media) for me.

### **Find and describe a published paper that utilizes the Opentrons or similar automation tools to achieve novel biological applications (eg automated PACE)**

**Paper:** [Development of a Modular Lab Automation System with Applications to Animal and Bacteria Cell Culture (Hartman, T.W, MS thesis. University of South Dakota, 2024)](https://www.proquest.com/openview/718cddcf553d6c61c2df1434ecd1152a/1?pq-origsite=gscholar&cbl=18750&diss=y)

**Description:** This paper is a perfect example of why automation is critical for modern synthetic biology. The author identifies the key challenges of manual lab work: complex protocols are tedious, prone to human error, and suffers from a lack of reproducibility. and To solve this, the team developed a modular lab automation system. They validated their system through automating one of the most common and error-prone tasks in all of biology: cell culture, for both simple bacteria (prokaryotic) and complex animal cells (eukaryotic).

The most important part of their project isn't just the robot; it's their focus on transparency, quality control, and community reuse. They created a system that automatically generates Jupyter Notebooks as a "full protocol execution report," which makes the experiments perfectly documented and reusable. They also described how this modular system is the first step toward "self-driving labs," where AI and machine learning models can design and run their own experiments, possibly creating a fully automated DBTL cycle.

---

In the end, I will leave you with a drawing of the Djoser Genomics Step Pyramid, created using the Opentrons Python API :D

<div style="text-align: center;">
  <img src="/assets/images/posts/Field-Note-10-Dispatch-HTGAA-Week-3-Homework/Djoser Genomics Pyramid Logo-Opentrons.png" alt="Djoser Genomics Step Pyramid" width="600"/>
  <p style="font-size: 0.8em; color: gray;">Djoser Genomics Step Pyramid drawn using Opentrons Python API</p>
</div>
