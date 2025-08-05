---
title: "Scroll 1: Imhotep's Insights"
layout: post
author: Nourelden
categories: [Tutorials, RNAseq, Transcriptomics]
tags: ["Bulk RNAseq Tutorial Codex", "Djoser Genomics", "2025"]
image: "assets/images/posts/Scroll-1-Imhoteps-Insights/Scroll 1 Imhoteps Insights.jpg"
featured: true
hidden: false
---

Welcome to **Scroll 1** of 8, from the [_Djoser’s Bulk RNAseq Tutorial Codex_]({{site_baseurl}}/Bulk-RNAseq-Tutorial-Codex/) — a collection imagined as if preserved from the ancient halls of knowledge.

This first scroll opens with the foundational act: collecting real RNA-seq data for analysis, much like laying the first stones in a structure. It is said that all great endeavors begin with order — perhaps even Imhotep would have agreed.

---

## 📜 Scroll Objectives

- [Finding Real RNA-seq Datasets](#finding-real-rna-seq-datasets)
- [Dataset Used in This Tutorial](#dataset-used-in-this-tutorial)
- [Downloading the Data in Google Colab](#downloading-the-data-in-google-colab)
  - [Create a Directory for Your Data](#create-a-directory-for-your-data)
  - [Define the Download URLs](#define-the-download-urls)
  - [Download Each File](#download-each-file)
- [Cultural Checkpoint: Imhotep & the Legacy of Saqqara](#cultural-checkpoint-imhotep-the-legacy-of-saqqara)

---

## 🧪 <a id="finding-real-rna-seq-datasets">Step 1: Finding Real RNA-seq Datasets</a>

Before diving into bioinformatics tools, we need real-world RNA-seq data to work with.

There are multiple public databases that host such data, including:

- **ENA** (European Nucleotide Archive)
- **NCBI SRA** (Sequence Read Archive)
- **GEO** (Gene Expression Omnibus)

Each of these databases contains raw sequencing data submitted by researchers worldwide, often linked to published papers.

For this tutorial, we’ll use **ENA**, which offers direct FTP access to FASTQ files, making it ideal for scripting and reproducibility.

You can explore ENA at:  
🔗 [https://www.ebi.ac.uk/ena/browser/home](https://www.ebi.ac.uk/ena/browser/home)

To find datasets, try searching with keywords like:

- `"Homo sapiens RNA-seq"`
- or directly by project ID, such as `PRJNA967653`

Each project page provides sample descriptions and links to raw `.fastq.gz` files that we can download.

> 💡 **Tip:** When you're just starting out, it's a good idea to work with datasets that have around 6–8 samples — small enough to process quickly, but large enough to learn meaningful concepts.

---

## 🧬 <a id="dataset-used-in-this-tutorial">Dataset Used in This Tutorial</a>

We’ll use a publicly available human dataset from [ENA Project PRJNA967653](https://www.ebi.ac.uk/ena/browser/view/PRJNA967653), which examines gene expression changes in human superior cervical ganglia with and without cardiac diseases.

We’ll download the following 6 samples _(in step 2)_:

- SRR24448335 (Cardiac Disease)
- SRR24448336 (Cardiac Disease)
- SRR24448337 (Cardiac Disease)
- SRR24448338 (Healthy)
- SRR24448339 (Healthy)
- SRR24448340 (Healthy)

In addition to the RNA-seq reads, we’ll download the **reference human transcriptome (cdna)** (FASTA format) from [**Ensembl**](https://www.ensembl.org/index.html) _(in step 2)_.

- Go to [Ensembl](https://ftp.ensembl.org/pub/release-113/fasta/homo_sapiens/cdna/)
- Choose the Human Genome
- From **Gene annotation** Choose **Download FASTA files for genes, cDNAs, ncRNA, proteins**
- Choose **cdna** folder
- Download the file: `Homo_sapiens.GRCh38.cdna.all.fa.gz`

> This file contains all known coding transcripts (mRNAs) for Homo sapiens, and it will be used in the alignment step to match our reads to known genes.

---

## 💾 <a id="downloading-the-data-in-google-colab">Step 2: Downloading the Data in Google Colab</a>

We’ll be running everything inside **[Google Colab](https://colab.research.google.com/)** — a free, cloud-based Jupyter notebook that supports Python and shell commands, making it perfect for bioinformatics tutorials.

Open a new Colab notebook and follow along step by step.

---

### 📁 <a id="create-a-directory-for-your-data">1. Create a Directory for Your Data</a>

This block of code creates a folder inside Colab’s virtual environment to store the RNA-seq data we’ll download.

```python
import os

folderPath = '/content/RNAseq'

# Create the directory if it doesn't exist
if not os.path.exists(folderPath):
    os.makedirs(folderPath)
```

---

### 🔗 2. <a id="define-the-download-urls">Define the Download URLs</a>

Now we list all the datasets and the reference transcriptome file that we want to download:

```python
datasets = [
    'ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR244/035/SRR24448335/SRR24448335.fastq.gz',
    'ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR244/036/SRR24448336/SRR24448336.fastq.gz',
    'ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR244/037/SRR24448337/SRR24448337.fastq.gz',
    'ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR244/038/SRR24448338/SRR24448338.fastq.gz',
    'ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR244/039/SRR24448339/SRR24448339.fastq.gz',
    'ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR244/040/SRR24448340/SRR24448340.fastq.gz',
    'https://ftp.ensembl.org/pub/release-113/fasta/homo_sapiens/cdna/Homo_sapiens.GRCh38.cdna.all.fa.gz'
]
```

📌 Explanation:

- These are direct FTP/HTTP links to `.fastq.gz` files from ENA and the transcriptome FASTA file from Ensembl.
- We’ve listed the links inside a Python list so we can loop over them next.

---

### ⬇️ 3. <a id="download-each-file">Download Each File</a>

Now we loop over each URL and download the corresponding file using `wget`.

```python
for url in datasets:
    filename = url.split("/")[-1]
    !wget "$url" -P "$folderPath"

    file_path = os.path.join(folderPath, filename)
    if os.path.exists(file_path):
        print(f"✅ Downloaded: {filename}")
    else:
        print(f"❌ Failed to download: {filename}")
```

📌 Explanation:

- `filename = url.split("/")[-1]`: extracts the file name from the URL.
- `!wget "$url" -P "$folderPath"`: downloads the file using the Unix `wget` command directly inside Colab.
- We use `os.path.exists()` to check whether the download was successful and print a confirmation message.

---

✅ **After running this step**, your `/content/RNAseq` folder in Colab should contain:

- 6 `.fastq.gz` RNA-seq files
- 1 `.fa.gz` transcriptome reference file

🧪 That’s everything covered in **Imhotep’s Insights Scroll**.

In this scroll, we gathered real RNA-seq data from ENA and prepared it for analysis in Google Colab — following the same foundational steps researchers take every day in transcriptomics workflows.

Let’s now shift gears from code to culture in our **Cultural Checkpoint** below.

---

## 🏛️ <a id='cultural-checkpoint-imhotep-the-legacy-of-saqqara'>Cultural Checkpoint: Imhotep & the Legacy of Saqqara</a>

<div style="text-align: center;">
  <img src="/assets/images/posts/Scroll-1-Imhoteps-Insights/Imhotep.jpg" alt="Imhotep Statue" width="400"/>
  <p style="font-size: 0.8em; color: gray;"><a href="https://commons.wikimedia.org/wiki/File:Statue_of_Seated_Imhotep_MET_DP112608.jpg" target="_blank">Image credit: Wikimedia Commons</a></p>
</div>

**Imhotep** is one of the most remarkable figures in ancient Egyptian history. Serving under Pharaoh Djoser, he was a **polymath** — an architect, high priest, physician, and adviser. Though not a scientist in the modern sense, his legacy in organizing knowledge and healing earns him symbolic credit here as a timeless figure of structure and insight.

He is best known for designing the **Step Pyramid of Saqqara**, considered the first monumental stone building in human history — a revolutionary act of precision, planning, and foresight.

<div style="text-align: center;">
  <img src="/assets/images/posts/Scroll-1-Imhoteps-Insights/Step Pyramid of Djoser.jpg" alt="Pyramid of Djoser - Saqqara" width="700"/>
  <p style="font-size: 0.8em; color: gray;"><a href="https://commons.wikimedia.org/wiki/File:Sakkara-10-Djoser-Pyramide-1982-gje.jpg" target="_blank">Image credit: Wikimedia Commons / Gerd Eichmann</a></p>
</div>

The legacy of **Imhotep**, **Djoser** _(Will show up in a future scroll ;D)_ and the **Step Pyramid of Djoser** at Saqqara is what inspired **Djoser Genomics**. It’s a reminder that every structure — ancient or scientific — begins with a strong, thoughtful foundation, step by step.

---
