---
title: "Djoser's Bulk RNAseq Tutorial Codex"
layout: post
author: Nourelden
categories: [Tutorials, RNAseq]
tags:
  [
    "Bulk RNAseq Tutorial Codex",
    "History",
    "Tutorial Outline",
    "Djoser Genomics",
    "2025",
  ]
image: "assets/images/Djoser Bulk RNAseq Tutorial Codex Landscape.png"
featured: true
hidden: false
---

A beginner friendly bulk RNAseq tutorial series told through step by step guides and inspired by ancient Egyptian History.

Welcome to **Djoser's Bulk RNAseq Tutorial Codex**, a series of tutorials where I walk you through bulk RNAseq analysis step by step, from raw FASTQ files to enrichment plots, using real tools and free resources.

This series is built for beginners, students, and anyone learning on their own - just like I did. Everything here is based on the exact workflow I used in [my first preprint](https://doi.org/10.1101/2025.05.18.654713), where I analyzed public RNAseq data to explore immune signals in cardiac disease.

---

## 📚 What This Series Offers

- **Bite-sized lessons** for each step of the RNAseq workflow
- Built using **free tools** like Google Colab, R, and public datasets
- **Minimal setup**, focused explanations, and reproducible code
- A light touch of **ancient Egyptian history**, each tutorial ends with a “Cultural Checkpoint” themed after a real historical figure who represents the spirit of that step

---

## 🧭 The Path Ahead (Tutorial Roadmap)

<!-- | Part | Title                                            | Theme                  |
| ---- | ------------------------------------------------ | ---------------------- |
| 1️⃣   | **Collecting Data & FASTQC**                     | _Imhotep’s Insight_    |
| 2️⃣   | **Kallisto Pseudoalignment**                     | _Senusret’s Precision_ |
| 3️⃣   | **Importing into R, Annotations & Study Design** | _Ptahhotep’s Order_    |
| 4️⃣   | **Differential Gene Expression with DESeq2**     | _Hatshepsut’s Resolve_ |
| 5️⃣   | **MA Plot, PCA, Volcano**                        | _Ramesses’ Reveal_     |
| 6️⃣   | **GO/KEGG Enrichment + Dot Plots**               | _Merit-Ptah’s Clarity_ |
| 7️⃣   | **GSEA + Enrichment Plots**                      | _Thutmose’s Strategy_  | -->

/Scroll-2-Hesy-Ras-Diagnostics/
| Part | Title | Theme/Status |
| ---- | ------------------------------------------------ | ------------------------------------------------------------------ |
| 1️⃣ | **Data Collection** | [Imhotep’s Insights]({{site_baseurl}}/Scroll-1-Imhoteps-Insights/) |
| 2️⃣ | **Quality Control** | [Hesy-Ra's Diagnostics]({{site_baseurl}}/Scroll-2-Hesy-Ras-Diagnostics/) |
| 3️⃣ | **Kallisto Pseudoalignment** | In Progress |
| 4️⃣ | **Importing into R, Annotations & Study Design** | In Progress |
| 5️⃣ | **Differential Gene Expression with DESeq2** | In Progress |
| 6️⃣ | **MA Plot, PCA, Volcano** | In Progress |
| 7️⃣ | **GO/KEGG Enrichment + Dot Plots** | In Progress |
| 8️⃣ | **GSEA + Enrichment Plots** | In Progress |

<br />

> You’ll find a clean, technical tutorial first in each post — then, for those curious, a brief **Cultural Checkpoint** to highlight the Egyptian figure who inspired it.

---

## 💬 Why I'm Doing This

I started learning bioinformatics alone, with no lab or mentor, no roadmap — just a drive to understand life through data. It’s been one of the hardest things I’ve done, but also the most rewarding.

This tutorial series is my way of giving back, building forward, and making space for others who might be walking a similar road.

Whether you’re a student, a researcher, or just bio-curious, welcome.  
Let’s build something together.

---

<style>
table, th, td {
    border: 1px solid black;
    border-collapse: collapse;
    padding: 10px;
    text-align: center;
}
</style>
