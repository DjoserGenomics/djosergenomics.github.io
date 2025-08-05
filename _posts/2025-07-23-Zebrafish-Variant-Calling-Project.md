---
layout: post
title: "Discovering Mutations in fisheries-induced Selection of Zebrafish"
author: Nourelden
categories: [Variant Calling, Zebrafish, Projects]
tags: ["Mutations", "Marine Biology", "Djoser Genomics", "2025"]
image: "assets/images/posts/Zebrafish-Variant-Calling/Zebrafish.jpg"
featured: false
hidden: false
---

###### Zebrafish Variant Calling Training Project

Image by <a href="https://pixabay.com/users/kuznetsov_peter-15644238/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=4996610">Petr Kuznetsov</a> from <a href="https://pixabay.com//?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=4996610">Pixabay</a>

---

# 🐟 Variant Calling in Zebrafish

In this post, I document a hands-on training project I conducted using real sequencing data from the zebrafish study [PRJNA630223](https://www.ebi.ac.uk/ena/browser/view/PRJNA630223). This study from **University of Glasgow** investigated how **fisheries-induced selection** —specifically simulated trawling— affects the **genetic landscape of zebrafish**, with a focus on how **population density** modulates these responses.

> 📚 _The original study involved over 90 zebrafish samples, reared under different density conditions, gender and subjected to repeated harvest. However, my project only analyzes four samples for training purposes._

---

## 🧪 Objective

The goal of this project was to practice and understand the steps involved in a **variant calling pipeline**, from raw sequencing reads to functional variant annotation.

---

## 🧬 Data Used

I selected four male zebrafish samples, all from the baseline density group:

- 2 “**Captured**” fish: caught during simulated trawling
- 2 “**Escaped**” fish: those that evaded capture

This distinction is relevant because the study explores how behavioral traits like sociality or boldness may lead to **capture-associated selection**, potentially leaving **genomic signatures** that differ between groups.

📝 _Sample details and Accession IDs:_

- **Captured1**: SRR11676923
- **Captured2**: SRR11676919
- **Escaped1**: SRR11676853
- **Escaped2**: SRR11676862

---

## 🔬 Pipeline Overview

All steps were conducted using open-source tools within a Galaxy + Jupyter environment:

1. **Data download** from `ENA`
2. **Quality control** using `FastQC` & `MultiQC`
3. **Trimming** low-quality reads using `fastp`
4. **Alignment** with `minimap2`
5. **SAM/BAM processing** using `samtools`
6. **Variant calling** with `freebayes`
7. **Filtering** based on quality (`QUAL ≥ 20`) using `vcffilter`
8. **Annotation** using Ensembl’s `VEP` with a custom zebrafish GTF using Galaxy EU

---

## 📊 Results

> Note: These results are purely descriptive and reflect only the four samples I selected for training. They're not representative of the full study and aren't meant to support any biological claims — just to help me learn from real data.

### 1. Total Variants Per Sample

This bar plot shows the number of filtered variants (after `QUAL ≥ 20`) in each sample.

![Total Variants Per Sample](/assets/images/posts/Zebrafish-Variant-Calling/Total_Variants_per_Sample.png)

As seen above, **escaped fish tended to have more total variants** than captured ones.

---

### 2. Variant Impact Summary

Each variant was classified into one of four impact levels by [VEP](https://www.ensembl.org/info/genome/variation/prediction/predicted_data.html): `HIGH`, `MODERATE`, `LOW`, or `MODIFIER`.

| Impact Type | Captured1 | Captured2 | Escaped1 | Escaped2 |
| ----------- | --------- | --------- | -------- | -------- |
| HIGH        | 2691      | 2691      | 4157     | 4084     |
| MODERATE    | 52516     | 52516     | 74768    | 79037    |
| LOW         | 157776    | 157776    | 222393   | 235675   |
| MODIFIER    | 7266476   | 7266476   | 11115424 | 13651472 |

<br />

The plot below compares their distribution across samples.

> The plot excludes `MODIFIER` consequences, which dominate most genomes but are less informative in this training context and may obscure other types.

![VEP Impact Summary](/assets/images/posts/Zebrafish-Variant-Calling/Variant_Impact_Across_Samples.png)

While **LOW-impact variants** dominate across all samples, subtle differences exist in the counts of `HIGH` and `MODERATE` variants.

---

### 3. Variant Summary Table

| Sample    | Group    | Mapped Reads | Total Variants | SNPs    | Indels |
| --------- | -------- | ------------ | -------------- | ------- | ------ |
| Captured1 | Captured | 96.76%       | 3765889        | 2947257 | 83926  |
| Captured2 | Captured | 96.76%       | 3765889        | 2947257 | 83926  |
| Escaped1  | Escaped  | 97.10%       | 5734230        | 4459982 | 135088 |
| Escaped2  | Escaped  | 97.51%       | 7032765        | 5381912 | 189612 |

<br />

📌 _All counts based on filtered variants only._

---

## 🧠 What I Learned

This project helped me solidify several key concepts in variant analysis:

- 🛠️ **Practical tool use**: I became more comfortable using `minimap2`, `freebayes`, `samtools`, and `VEP` in a real workflow.
- 📈 **Data interpretation**: I learned how to read and summarize variant call statistics meaningfully.
- 🎨 **Visualization skills**: I explored how to represent genomic differences clearly using plots.
- 🧭 **Confidence for future work**: This training project gave me a clear roadmap for scaling up future analyses, whether for zebrafish, humans, or microbes.

---

## 📂 Code & Pipeline

You can find the pipeline notebook and documentation here:  
🔗 [GitHub Repo Link](https://github.com/DjoserGenomics/Zebrafish-Variant-Calling)

---

## 📚 Main Study

The Original study's datasets can be accessed here:  
🔗 [ENA Project PRJNA630223](https://www.ebi.ac.uk/ena/browser/view/PRJNA630223)

Original study Citation:

- Crespel A, Schneider K, Miller T, et al. Genomic basis of fishing-associated selection varies with population density. Proc Natl Acad Sci U S A. 2021;118(51):e2020833118. doi:10.1073/pnas.2020833118

---

<style>
table, th, td {
    border: 1px solid black;
    border-collapse: collapse;
    padding: 10px;
    text-align: center;
}
</style>
