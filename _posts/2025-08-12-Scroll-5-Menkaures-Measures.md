---
title: "Scroll 5: Menkaure's Measures"
layout: post
author: Nourelden
categories: [Tutorials, RNAseq]
tags: ["Bulk RNAseq Tutorial Codex", "History", "Djoser Genomics", "2025"]
image: "assets/images/posts/Scroll-5-Menkaures-Measures/Scroll 5 Menkaures Measures.jpg"
featured: false
hidden: false
---

Welcome to **Scroll 5** of 8, from the [_Djoser’s Bulk RNAseq Tutorial Codex_]({{site_baseurl}}/Bulk-RNAseq-Tutorial-Codex/).

In this scroll, we perform **differential expression analysis (DEA)** using DESeq2, to identify which genes change significantly between our conditions. Like **Menkaure**, builder of the smallest yet most refined pyramid at Giza, we focus on precision and careful craftsmanship to uncover meaningful patterns.

Let’s begin the analysis.

---

## 📜 Scroll Objectives

- [What is Differential Expression Analysis (DEA)?](#what-is-differential-expression-analysis-dea)
- [Differential Expression Analysis (DEA) Expectations](#differential-expression-analysis-dea-expectations)
- [Data Cleaning Before Using `txi`](#data-cleaning-before-using-txi)
- [Preparing the Study Design for DESeq2](#preparing-the-study-design-for-deseq2)
- [Performing Differential Expression Analysis (DEA) with DESeq2](#performing-differential-expression-analysis-dea-with-deseq2)
- [Setting Cutoffs for DEGs](#setting-cutoffs-for-degs)
- [Interpreting DEGs](#interpreting-degs)
- [Cultural Spotlight: Menkaure – The Visionary of the Elegant Pyramid](#cultural-spotlight-menkaure-the-visionary-of-the-elegant-pyramid)

---

## <a id="what-is-differential-expression-analysis-dea">What is Differential Expression Analysis (DEA)?</a>

**Differential Expression Analysis (DEA)** is the process of identifying genes whose expression levels change significantly between different experimental conditions or sample groups.

For example:

- Healthy vs diseased tissue
- Treated vs untreated samples
- Different time points in a biological process

The goal is to find **Differentially Expressed Genes (DEGs)**, genes that are upregulated (higher expression) or downregulated (lower expression) under one condition compared to another.

DEA is a crucial step in RNA sequencing (RNA-seq) and transcriptomics studies, allowing us to:

- **Understand biology**: Discover which genes drive specific biological processes or diseases.
- **Identify biomarkers**: Find potential diagnostic, prognostic, or therapeutic targets.
- **Guide experiments**: Highlight pathways and mechanisms worth deeper investigation.
- **Support precision medicine**: Pinpoint gene activity patterns that could predict treatment responses.

Without DEA, RNA-seq data is just a massive table of numbers. DEA brings interpretation and actionable meaning.

---

## <a id="differential-expression-analysis-dea-expectations">Differential Expression Analysis (DEA) Expectations</a>

When running DEA, expect to see:

- Upregulated genes -> More active in your condition of interest.
- Downregulated genes -> Less active in your condition of interest.
- Statistical summaries -> Number of significant genes, effect sizes, and trends.

These findings can be later used to produce some graphs (Which will be covered in the next scroll), these include:

- **Volcano plots**: Showing significance vs fold change.
- **Heatmaps**: Highlighting expression patterns across samples.

### ⚠️ Keep in mind:

- Not all DEGs will be biologically meaningful, some may be artifacts.
- DEA results are the starting point, not the final story.
- Biological interpretation and validation are essential next steps.

---

## <a id="data-cleaning-before-using-txi">Data Cleaning Before Using `txi`</a>

Before proceeding with downstream analysis, it is crucial to clean the data to ensure that only meaningful and interpretable features (genes) are included in the differential expression pipeline. The following steps perform minor but important cleaning operations on our `txi` object.

---

### Step 1: Remove Rows with Empty or NA Gene Names

```r
# Removing Rows with '' or NA values
txi$counts <- txi$counts[!(rownames(txi$counts) == '' | is.na(rownames(txi$counts))), ]
```

- Each row in `txi$counts` represents a gene, and the row names hold the gene identifiers.
- If a row has an empty string ("") or missing value (`NA`) as its identifier, it cannot be properly matched to functional annotations or interpreted biologically.
- This step removes those rows to prevent downstream errors and ensure all genes have valid IDs.

---

### Step 2: Keep Only Genes with Sufficient Read Counts

```r
# Keeping any gene where total counts across all samples is more than or equal to 10
keepers <- rowSums(txi$counts) >= 10
txi$counts <- txi$counts[keepers,]
```

- `rowSums(txi$counts)` calculates the total read counts for each gene across all samples.
- Genes with very low total counts are likely the result of technical noise or extremely low expression, and they usually do not contribute reliable statistical signals in DEA.
- This step keeps only those genes where the sum of counts across all samples is ≥ 10.

#### Why Remove Low Count Genes?

Filtering low count genes is standard in RNA-seq preprocessing because:

- **Improved Statistical Power**: Low counts have high variance, reducing sensitivity for detecting differentially expressed genes.
- **Reduced Multiple Testing**: Filtering uninformative genes lowers the number of tests, decreasing the **false discovery rate (FDR)**.
- **Minimized Noise**: Low counts may reflect sequencing errors or background noise, not biological expression.

#### Choosing a Threshold

Low count gene filtering thresholds depend on:

- **Number of Samples**: More samples allow lower thresholds for reliable results.
- **Library Depth**: Deeper sequencing improves detection of lowly expressed genes.
- **Biological Context**: Rare transcript studies may need lenient thresholds.

Some common thresholds include:

- **10 total counts** across all samples (used here for small/medium datasets).
- **1 CPM** in at least X samples (edgeR/limma, X based on replicates).
- **Per-sample thresholds**: e.g., ≥5 counts in at least half of samples.

The goal is to remove genes with very low expression while retaining those meaningful for analysis.

---

## <a id="preparing-the-study-design-for-deseq2">Preparing the Study Design for DESeq2</a>

Before we can run DEA in DESeq2, we need to make sure the `studyDesign` data frame has sample names as its row names. This is important because DESeq2 uses the row names of the sample metadata to match samples with the count data.

```r
# Assigning "Sample" column to be rownames for the study design
studyDesign <- studyDesign %>% column_to_rownames("Sample")
```

The `column_to_rownames()` function from the tibble package takes the values from the "Sample" column and sets them as the row names of `studyDesign`.

---

## <a id="performing-differential-expression-analysis-dea-with-deseq2">Performing Differential Expression Analysis (DEA) with DESeq2</a>

Once we have quantified our RNA-seq data using Kallisto and imported via `tximport`, the next step is to use **DESeq2** to perform the statistical analysis that identifies **differentially expressed genes** (DEGs) between our conditions.

---

### 1. Import DESeq2 and Create a Dataset

```r
library(DESeq2)

dds <- DESeqDataSetFromTximport(
  txi = txi,
  colData = studyDesign,
  design = ~ Condition
)
```

- `txi`: The object produced by `tximport()` which contains the summarized counts (gene-level) for each sample.
- `colData`: A data frame describing your experimental design, in our case, this is `studyDesign`, which contains metadata for each sample.
- `design`: A formula describing the experimental design.

`~ Condition` means we are testing whether gene expression changes depend on the "Condition" column in our metadata.

This column should be a factor (categorical variable) with levels corresponding to your groups (e.g., "Healthy" and "Disease").

### 2. Understanding the design parameter

The design formula tells DESeq2 how to model your experiment.
Here are a few examples:

#### **Simple two-group comparison**:

```r
design = ~ Condition
```

where Condition could be **"Healthy"** vs **"Disease"**.

#### **Including an additional variable** (e.g., batch effect):

```r
design = ~ Batch + Condition
```

This controls for Batch while testing for differences due to Condition.

### 3. Running the DESeq Pipeline

```r
dds <- DESeq(dds)
```

This single function:

- Estimates size factors (normalization across samples).
- Estimates dispersion for each gene.
- Fits the negative binomial model.
- Performs hypothesis testing.

### 4. Extracting Results

```r
res <- results(
  dds,
  contrast = c("Condition", "Disease", "Healthy")
)
```

Explanation of `contrast`:

The vector `c("Condition", "Disease", "Healthy")` means:

- `"Condition"` → the column to test.
- `"Disease"` → the numerator (test group).
- `"Healthy"` → the denominator (reference group).

The output `res` contains many components, we will mainly focus on:

- `gene_name`: The name of the gene.
- `log2FoldChange`: how much expression changes (log2 scale).
- `pvalue` and `padj`: statistical significance (adjusted for multiple testing).

---

## <a id="setting-cutoffs-for-degs">Setting Cutoffs for DEGs</a>

When performing **DEA**, not all genes showing differences between conditions are biologically meaningful. We apply **cutoffs** to filter results and keep only the most relevant genes.

#### Common Approach

A widely used practice is to apply two main thresholds:

1. **Adjusted p-value (`padj`)**: Controls the **False Discovery Rate (FDR)**.
   - A common threshold is `padj < 0.05`, meaning we accept only genes with a statistically significant change after multiple testing correction.
2. **Absolute log2 Fold Change (`|log2FC|`)**: Represents the magnitude of change.
   - A common threshold is `|log2FC| >= 1`, meaning we keep genes with at least a **2-fold change** in expression (either up or down).

This combination helps ensure that the identified **DEGs** are both statistically reliable and biologically meaningful.

> Sometimes when stricter thresholds are needed for more filtering, we might use `padj < 0.01` and `|log2FC| >= 2`.

---

#### Example: Filtering DEGs in R

```r
# Removing DEGs where padj = NA
res.df <- res[!is.na(res$padj), ] %>%
  as_tibble(rownames = 'gene_name')

# Filtering DEGs with padj < 0.05 and |log2FC| >= 1
DEGs <- res.df %>%
  filter(padj < 0.05, abs(log2FoldChange) >= 1)
```

Here we make sure that:

- Genes with missing statistical values are excluded.
- Only significant genes with substantial expression changes are kept for downstream analyses such as functional or pathway enrichment analyses.

---

## <a id="interpreting-degs">Interpreting DEGs</a>

Once we run our differential expression analysis, we can view the results simply by typing `DEGs` in the R console.

```r
DEGs
```

This will print the top differentially expressed genes in a tabular format.
Here’s an example output:

| gene_name | baseMean | log2FoldChange | lfcSE | stat  | pvalue   | padj     |
| --------- | -------- | -------------- | ----- | ----- | -------- | -------- |
| A1BG      | 266      | 1.21           | 0.338 | 3.59  | 3.34e-04 | 0.0144   |
| ABCB11    | 68.3     | -6.18          | 0.926 | -6.67 | 2.63e-11 | 1.39e-07 |

<br />

How to interpret this table:

- **`gene_name`**: The gene symbol for the differentially expressed gene.
- **`baseMean`**: Average normalized expression across all samples.
- **`log2FoldChange`**: The magnitude and direction of change between conditions.
  - Positive values → gene is upregulated in the condition of interest.
  - Negative values → gene is downregulated in the condition of interest.
- **`lfcSE`**: Standard error for the log2 fold change estimate.
- **`stat`**: Test statistic from the statistical model.
- **`pvalue`**: Raw p-value for the gene's differential expression.
- **`padj`**: Adjusted p-value (after multiple testing correction).

---

#### Example interpretation

`A1BG`:

- **`log2FoldChange`** = 1.21 → ~2.3× higher expression in the condition of interest (Cardiac Disease).
- **`padj`** = 0.0144 → statistically significant.

Biological implication: May be associated with Cardiac Disease upregulation.

`ABCB11`:

- **`log2FoldChange`** = -6.18 → ~71× lower expression in the condition of interest (Cardiac Disease).
- **`padj`** = 1.39e-07 → extremely significant.

Biological implication: Strong candidate for Cardiac Disease downregulation.

---

**That’s it!** You’ve successfully performed differential expression analysis using DESeq2 and learned how to interpret the results.

If you want to continue, head over to the next scroll: [Ramses' Plots]({{site_baseurl}}/Scroll-6-Ramses-Plots/), where we’ll generate multiple plots and visualizations to help us interpret our findings even more.

Time for a Cultural Spotlight.

---

## 🏛️ <a id="cultural-spotlight-menkaure-the-visionary-of-the-elegant-pyramid">Cultural Spotlight: Menkaure – The Visionary of the Elegant Pyramid</a>

<div style="text-align: center;">
  <img src="/assets/images/posts/Scroll-5-Menkaures-Measures/Menkaure.jpg" alt="Menkaure" width="400"/>
  <p style="font-size: 0.8em; color: gray;"><a href="https://commons.wikimedia.org/wiki/File:Seated_Statue_of_King_Menkaure_MET_37.6.1_01.jpg" target="_blank">Menkaure - © Wikimedia Commons CC0 1.0</a></p>
</div>

**Menkaure**, also known as **Mykerinos**, was a ruler of Egypt’s Fourth Dynasty. He was the son of Khafre, He is most famous for his pyramid at Giza, the smallest of the three iconic pyramids, yet admired for its refined proportions and exquisite craftsmanship.

<div style="text-align: center;">
  <img src="/assets/images/posts/Scroll-5-Menkaures-Measures/Pyramid_of_Menkaure.jpg" alt="Great Pyramid of Giza" width="700"/>
  <p style="font-size: 0.8em; color: gray;"><a href="https://commons.wikimedia.org/wiki/File:Pyramid_of_Menkaure_(50035374516).jpg" target="_blank">Menkaure's Pyramid - © Wikimedia Commons / Vincent Brown - CC BY 2.0</a></p>
</div>

Unlike his predecessors, Menkaure’s pyramid was partly clad in granite instead of limestone, a choice that reflected both innovation and status. His reign is often associated with justice and benevolence, earning him a legacy of being a compassionate ruler in ancient Egypt.

---

> Papyrus Background from the Post's Cover photo is from <a href="https://www.freepik.com/free-photo/grunge-background_4258615.htm" target="_blank">Freepik</a>

---

<style>

table:not(.rouge-table), th, td:not(.rouge-gutter, .rouge-code) {
    border: 1px solid black;
    border-collapse: collapse;
    padding: 10px;
    text-align: center;
}
</style>
