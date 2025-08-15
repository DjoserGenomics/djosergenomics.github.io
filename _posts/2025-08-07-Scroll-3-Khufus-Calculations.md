---
title: "Scroll 3: Khufu's Calculations"
layout: post
author: Nourelden
categories: [Tutorials, RNAseq]
tags: ["Bulk RNAseq Tutorial Codex", "History", "Djoser Genomics", "2025"]
image: "assets/images/posts/Scroll-3-Khufus-Calculations/Scroll 3 Khufus Calculations.jpg"
featured: true
hidden: false
---

Welcome to **Scroll 3** of 8, from the [_Djoser’s Bulk RNAseq Tutorial Codex_]({{site_baseurl}}/Bulk-RNAseq-Tutorial-Codex/).

In this scroll, we perform pseudoalignment, a fast, reference-based mapping approach, to quantify transcripts from our RNA-seq reads. Like **Khufu**, the visionary behind the Great Pyramid, we rely on efficient design and foundational precision to build something monumental.

Let’s begin the alignment.

---

## 📜 Scroll Objectives

- [What Is Alignment, and Why Do We Do It](#what-is-alignment-and-why-do-we-do-it)
- [Common Tools for Alignment](#common-tools-for-alignment)
- [What is Pseudoalignment, and How Does It Differ from Alignment](#what-is-pseudoalignment-and-how-does-it-differ-from-alignment)
- [When is Pseudoalignment the Better Option?](#when-is-pseudoalignment-the-better-option)
- [Installing Kallisto on Google Colab](#installing-kallisto-on-google-colab)
- [Reference Transcriptome Indexing using Kallisto](#reference-transcriptome-indexing-using-kallisto)
- [Quantifying Expression with Kallisto](#quantifying-expression-with-kallisto)
- [Alignment Rate Check (Quality Control)](#alignment-rate-check-quality-control)
- [Cultural Spotlight: Khufu – Mastermind of the Great Pyramid](#cultural-spotlight-khufu-mastermind-of-the-great-pyramid)

---

## 🔹 <a id='what-is-alignment-and-why-do-we-do-it'> What Is Alignment, and Why Do We Do It? </a>

Before we push forward in our transcriptomics journey, we must first pause, and understand the concept of sequence alignment.

In RNA-seq analysis, after sequencing, we’re left with millions of short reads. But they’re just disconnected fragments. To make sense of them, we need to reconnect them to their original source: a reference genome or in our case **a reference transcriptome**.

**That’s what alignment does**:
It takes each read and finds the best-matching location in the genome or transcriptome, to help us understand where does this fragment come from in our genome or transcriptome

---

## 🛠️ <a id='common-tools-for-alignment'> Common Tools for Alignment </a>

These tools use algorithms to search for where reads fit:

- **HISAT2** – Fast, memory-efficient, often used for genome alignment.
- **STAR** – Extremely fast and splice-aware, ideal for eukaryotic transcriptome data.
- **BWA** – Great for DNA reads, used often in genomics pipelines.

But there's a catch, Alignment is powerful, but also **computationally expensive**. It can take hours, require a strong CPU, computational power and produce huge files (like **BAMs**). For large datasets or limited compute resources, it becomes a bottleneck.

That’s where **King Khufu** would raise an eyebrow, and perhaps suggest a more efficient architectural strategy.

---

## 🧭 <a id='what-is-pseudoalignment-and-how-does-it-differ-from-alignment'> What is Pseudoalignment, and How Does It Differ from Alignment? </a>

Pseudoalignment skips the base-by-base matching. Instead, it identifies **which transcripts** a read _could have_ originated from, without determining its exact position. It uses **k-mers** (short subsequences of length k) from the reads and compares them to a k-mer index of the transcriptome.

Think of it like asking: “Does this read _belong_ to transcript X, Y, or Z?” rather than: “Where exactly does this read align in the genome?”

The two most widely known pseudoaligners are:

- **Kallisto** – The tool we'll be using in this scroll.
- **Salmon** – Another fast and flexible pseudoaligner.

## 🚀 <a id='when-is-pseudoalignment-the-better-option'> When is Pseudoalignment the Better Option? </a>

Pseudoalignment is a great choice when:

- Your goal is **quantification**, estimating transcript/gene expression levels, not variant calling or splicing analysis.
- You want **speed and efficiency**, it can process large datasets _much_ faster than traditional aligners.
- You have **limited computational resources**, pseudoalignment uses less RAM and CPU.

However, it’s not suitable if you need:

- Precise **read locations** on the genome.
- Working on **splicing**.
- Using any other tools that use a BAM alignment files.

For bulk RNA-seq focused on quantification, **pseudoalignment offers an optimal balance between speed and accuracy**, which is exactly why we’re using Kallisto in this tutorial.

> If you want to learn more about alignment vs pseudoalignment (Kallisto), check out this [Awesome Video from DIY.transcriptomics](https://diytranscriptomics.com/project/lecture-02#part-3---a-discussion-of-traditional-and-alignment-free-pseudoalignment-methods-for-quantifying-gene-expression).

---

## ▶️ <a id='installing-kallisto-on-google-colab'> Installing Kallisto on Google Colab </a>

To run Kallisto in Google Colab, we need to install it manually using Conda.

### Step 1: Install Conda (Miniconda)

We’ll begin by downloading and installing **Miniconda**, a lightweight version of Conda:

```python
# Install Miniconda
!wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
!chmod +x Miniconda3-latest-Linux-x86_64.sh
!./Miniconda3-latest-Linux-x86_64.sh -b -f -p /usr/local
```

This code does the following:

- `wget` downloads the Miniconda installer.
- `chmod +x` gives execute permissions.
- The `./` command installs it to `/usr/local`

Then verify the installation:

```python
# Verify Conda installation
!conda --version
```

---

### Step 2: Update Environment Variables

After installing Miniconda, we need to ensure that the Conda commands are recognized in our Colab environment.

```python
import os
os.environ['PATH'] = '/usr/local/bin:' + os.environ['PATH']
```

This code makes sure Conda commands are recognized and can be used inside the Colab environment.

---

### Step 3: Add Conda Channels

We’ll add the required Conda channels to access bioinformatics tools:

```bash
!conda config --add channels defaults
!conda config --add channels bioconda
!conda config --set offline false
```

- `defaults` is the main Conda channel.
- `bioconda` contains bioinformatics software like Kallisto.

We also make sure Conda won’t default to offline mode.

You can confirm the channels were added:

```bash
!conda config --show channels
```

---

### Step 4: Install Kallisto

Now install Kallisto directly from Bioconda:

```bash
!conda install -c bioconda kallisto -y
```

The `-y` flag auto-confirms installation prompts.

Finally, test that it is successfully installed:

```bash
!kallisto
```

---

## 🛠️ <a id='reference-transcriptome-indexing-using-kallisto'> Reference Transcriptome Indexing using Kallisto </a>

Before we can pseudoalign RNA-seq reads using Kallisto, we need to **create an index** from a reference transcriptome. The index enables Kallisto to rapidly locate the origin of reads.

### 🧠 What is Indexing?

Indexing is the process of converting a FASTA reference file into a structured, searchable format that the aligner or pseudoaligner can use for quick read assignment.

For Kallisto, the input reference is usually a **cDNA (transcript-level)** FASTA file, not the full genome. This is because Kallisto performs transcript-level quantification.

Without indexing, Kallisto would have to scan the entire reference file for every read, this would be very slow and computationally inefficient. The index accelerates the process by using k-mer hashing.

---

### 🛠️️ Creating the Reference Transcriptome Index

First we will **Unzip** the FASTA file if it's compressed (`.gz`).

```python
# Unzipping the reference FASTA
!gunzip "/content/RNAseq/Homo_sapiens.GRCh38.cdna.all.fa.gz"
```

Then we will use `!kallisto index` to create the index file.

```python
# Defining file paths
fasta_file = os.path.join(folderPath, "Homo_sapiens.GRCh38.cdna.all.fa")
index_file = os.path.join(folderPath, "Homo_sapiens.GRCh38.cdna.all.index")

# Creating the kallisto index
!kallisto index -i {index_file} {fasta_file}

# Confirming success
print(f"Index created: {index_file}")
```

---

## 🚀 <a id='quantifying-expression-with-kallisto'> Quantifying Expression with Kallisto </a>

Once the reference transcriptome index is prepared, it's time to quantify transcript abundances for each sample using **Kallisto's `quant`** command.

`kallisto quant` takes your indexed reference and your raw FASTQ files and performs **psuedoalignment** to estimate how many transcripts are present in each sample, quickly and efficiently.

### 🗂️ Sample Setup

We define a list of our samples with corresponding FASTQ files:

```python
kallistoData = [['HS01', 'SRR24448340.fastq.gz'],
                ['HS02', 'SRR24448339.fastq.gz'],
                ['HS03', 'SRR24448338.fastq.gz'],
                ['CD01', 'SRR24448337.fastq.gz'],
                ['CD02', 'SRR24448336.fastq.gz'],
                ['CD03', 'SRR24448335.fastq.gz']]
```

- **HS** samples are healthy controls.
- **CD** samples are from cardiac disease patients.

> The **HS** and **CD** prefixes help us differentiate between healthy and disease samples, which is crucial for downstream analysis, You can know which sample is which through the sample metadata of each one on **ENA**.

---

### ⚙️ Run Kallisto for Each Sample

Let's Create our main Output folder for Kallisto results:

```python
mkdir RNAseq/kallisto
```

Then we run quantification with the following code:

```python
for data in kallistoData:
  folder = os.path.join(folderPath, f"kallisto/{data[0]}")
  filelocation = os.path.join(folderPath, data[1])

  !kallisto quant \
  -i {index_file} \
  -o "$folder" \
  --single -l 250 -s 30 \
  "$filelocation"
```

---

### 🧾 Explanation:

- `-i {index_file}`: The path to the reference transcriptome index you created earlier.
- `-o "$folder"`: Output folder for results (TPMs and estimated counts).
- `--single`: Specifies that the reads are single-end.
- `-l 250 -s 30`: Estimated average fragment length and standard deviation (important for single-end data).
- `"$filelocation"`: Input FASTQ file.

---

### ✅ Outcome:

Each sample will now produce a folder containing a file named abundance.tsv, which includes:

- Estimated counts
- TPMs (Transcripts Per Million)
- Effective lengths

---

## 📊 <a id='alignment-rate-check-quality-control'> Alignment Rate Check (Quality Control) </a>

Before moving forward, it's essential to check the alignment rate for each sample. It can be found in the `run_info.json` file inside each sample's output directory.

Open the `run_info.json` file and look for the `p_pseudoaligned` field. A **good alignment rate is typically above 70–80%**. Low alignment percentages might indicate issues like:

- Poor-quality reads
- Contamination
- Incorrect transcriptome index

> ⚠️ If alignment rates are unusually low, consider rechecking your FASTQ files or the transcriptome reference.

---

**That’s it!** You can now download the kallisto folder from the left sidebar in Google Colab.

You now have quantification results for all samples, ready to be imported into R for downstream analysis and visualization!

Now time for our next Cultural Spotlight.

---

## 🏛️ <a id="cultural-spotlight-khufu-mastermind-of-the-great-pyramid">Cultural Spotlight: Khufu – Mastermind of the Great Pyramid</a>

<div style="text-align: center;">
  <img src="/assets/images/posts/Scroll-3-Khufus-Calculations/Khufu.jpg" alt="Khufu" width="400"/>
  <p style="font-size: 0.8em; color: gray;"><a href="https://commons.wikimedia.org/wiki/File:Khufu.jpg" target="_blank">Khufu - © Wikimedia Commons / Osiritkos - CC BY-SA 4.0</a></p>
</div>

As we align sequences with surgical precision, let’s spotlight a figure known for monumental precision, **King Khufu (c. 2600 BC)**. Also known as **Cheops**, Khufu was the pharaoh behind the construction of the **Great Pyramid of Giza**, the largest and most iconic pyramid in Egypt.

<div style="text-align: center;">
  <img src="/assets/images/posts/Scroll-3-Khufus-Calculations/Great_Pyramid_of_Giza.jpg" alt="Great Pyramid of Giza" width="700"/>
  <p style="font-size: 0.8em; color: gray;"><a href="https://commons.wikimedia.org/wiki/File:Great_Pyramid_of_Giza_-_Pyramid_of_Khufu.jpg" target="_blank">Great Pyramid of Giza - © Wikimedia Commons / Douwe C. van der Zee - CC BY-SA 4.0</a></p>
</div>

Khufu’s pyramid stood as the tallest human-made structure on Earth for over 3,800 years, a true feat of ancient engineering, planning, and coordination. Much like genome indexing prepares the way for efficient data alignment, Khufu’s pyramid was a meticulously planned foundation that shaped architectural history.

---

> Papyrus Background from the Post's Cover photo is from [Freepik](https://www.freepik.com/free-photo/grunge-background_4258615.htm)

---
