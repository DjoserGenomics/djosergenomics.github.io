---
title: "Scroll 7: Thutmose's Trends"
layout: post
author: Nourelden
categories: [Tutorials, RNAseq]
tags: ["Bulk RNAseq Tutorial Codex", "History", "Djoser Genomics", "2025"]
image: "assets/images/posts/Scroll-7-Thutmoses-Trends/Scroll 7 Thutmoses Trends.jpg"
featured: true
hidden: false
---

Welcome to **Scroll 7** of 8, from the [_Djoser’s Bulk RNAseq Tutorial Codex_]({{site_baseurl}}/Bulk-RNAseq-Tutorial-Codex/).

In this scroll, we go beyond individual genes and step into the realm of **functional** and **pathway analysis**. Using our DEGs, we will investigate **Gene Ontology (GO)** categories and **KEGG pathways** to uncover the broader biological processes, molecular functions, and cellular components affected by our conditions.

Like **Thutmose III**, the strategic genius who expanded Egypt’s influence far beyond its borders, we will look beyond single genes to understand the larger systems and pathways shaping our results.

Let’s explore the bigger picture.

---

## 📜 Scroll Objectives

- [Functional Enrichment Analysis](#functional-enrichment-analysis)
- [Performing GO Enrichment Analysis](#performing-go-enrichment-analysis)
- [Pathway Enrichment Analysis](#pathway-enrichment-analysis)
- [Performing KEGG Enrichment Analysis](#performing-kegg-enrichment-analysis)
- [Cultural Spotlight: Thutmose III – The Conqueror Pharaoh of Egypt](#cultural-spotlight-thutmose-iii-the-conqueror-pharaoh-of-egypt)

---

## <a id="functional-enrichment-analysis">Functional Enrichment Analysis</a>

Functional enrichment analysis using **Gene Ontology (GO)** is a method to determine whether certain biological functions, processes, or cellular components are statistically overrepresented or _Enriched_ in a given set of genes compared to a background set (often the whole genome).

In RNA-seq, we often end up with a list of **differentially expressed genes (DEGs)**. While these lists tell us _which_ genes are differentially expressed, they don’t directly explain **what these changes mean biologically**. **_GO enrichment_** bridges this gap.

### Gene Ontology (GO)

GO terms are organized into three categories:

1. **Biological Process (BP):** The biological objectives a gene contributes to (e.g., “apoptotic process”, “cell cycle”).
2. **Molecular Function (MF):** The biochemical activity of a gene product (e.g., “ATP binding”, “DNA helicase activity”).
3. **Cellular Component (CC):** Where in the cell the gene product is active (e.g., “nucleus”, “mitochondrial membrane”).

### Why do we use GO Enrichment Analysis?

- **Biological Insight:** Instead of interpreting hundreds of genes individually, enrichment analysis summarizes them into higher-level functions or processes.
- **Pattern Discovery:** Identifies functional themes that might be driving the observed phenotype or condition.
- **Hypothesis Generation:** Highlights biological processes worth deeper investigation in follow-up experiments.
- **Cross-Species Comparison:** Since GO is standardized, you can compare findings across organisms.

If a specific GO term is significantly enriched in your DEGs compared to all genes, it suggests that the biological function represented by that term is **likely involved** in the biological condition or experimental factor you’re studying.

---

## <a id="performing-go-enrichment-analysis">Performing GO Enrichment Analysis</a>

To run GO enrichment, we’ll use the `clusterProfiler` package and `org.Hs.eg.db` which is the human organism database.

```r
library(clusterProfiler)
library(org.Hs.eg.db)

# GO Enrichment
ego <- enrichGO(
  gene = DEGs$gene_name,       # The list of genes for analysis (from our DEGs table)
  OrgDb = "org.Hs.eg.db",      # The organism database (here: Homo sapiens)
  keyType = "SYMBOL",          # The type of gene identifier we are using (SYMBOL = gene names)
  ont = "ALL",                 # Ontology: "BP", "MF", "CC", or "ALL" for all categories
  pvalueCutoff = 0.05,         # Maximum p-value to consider a term significant
  qvalueCutoff = 0.05          # Maximum adjusted p-value (FDR) to consider significant
)
```

- `gene` → our DEGs
- `OrgDb` → The organism-specific annotation database. For human, use "org.Hs.eg.db".
- `keyType` → Specifies the type of identifiers used in gene (e.g., "SYMBOL", "ENSEMBL", "ENTREZID").
- `ont` → The GO ontology category to search. "BP" = Biological Process, "MF" = Molecular Function, "CC" = Cellular Component, "ALL" = all categories together.
- `pvalueCutoff` → A filter to keep only terms with raw p-values ≤ this threshold.
- `qvalueCutoff` → A filter to keep only terms with adjusted p-values (**false discovery rate**) ≤ this threshold.

---

### Making the Results Easier to Read

By default, the ego object is not in the most user-friendly table format. So we'll convert it into a tibble, sort it by adjusted p-value, and filter only significant results:

```r
ego.df <- as_tibble(ego, rownames = 'OntologyID') %>%
  arrange(p.adjust) %>%
  filter(p.adjust < 0.05)
```

Now, we can easily view it:

```r
ego.df
```

This will display a table where each row represents an enriched GO term, along with statistics like the adjusted p-value, the number of DEGs annotated to that term, the description of the term and more.

---

### Plotting & Interpreting the Results

We can use a dot plot to visualize a subset of the GO Enrichment Results, and for that we will use the `enrichplot` library

We will create a dot plot of the top 3 terms per each GO category (BP/MF/CC)

```r
library(enrichplot)

# Dotplot - top 3 terms per each category
dotplot(ego, showCategory = 3, split = "ONTOLOGY", title = "Top GO Enrichment Terms: ~ BP/MF/CC")+
  facet_grid(ONTOLOGY ~ ., scales = "free")
```

<div style="text-align: center;">
  <img src="/assets/images/posts/Scroll-7-Thutmoses-Trends/GO_Dot_Plot.png" alt="GO Enrichment Dot Plot" width="500"/>
  <p style="font-size: 0.8em; color: gray;">GO Enrichment Dot Plot</p>
</div>

In GO Dot Plots:

- The **warmer** the color means higher **statistical significance**
- The **bigger** the circle means more of our DEGs share in this term (Gene Ratio)

so in our dot plot, for the Biological Pathways (BP), we can see that **Cytoplasmic Translation** is highly enriched, and highly significant followed by **Antigen Processing**.

These info can be used alongside Literature review to find connections and possible biological implications of the observed changes in gene expression.

---

## <a id="pathway-enrichment-analysis">Pathway Enrichment Analysis</a>

KEGG (Kyoto Encyclopedia of Genes and Genomes) pathway enrichment analysis is a method used to determine whether a set of genes is significantly associated with known biological pathways.  
These pathways represent networks of molecular interactions, reactions, and relationships in cells, for example, metabolic pathways, signaling pathways, and disease pathways.

It provides as much help as GO Enrichment Analysis in terms of Biological insights, Data reduction, Hypothesis generation and Comparison across studies.

---

## <a id="performing-kegg-enrichment-analysis">Performing KEGG Enrichment Analysis</a>

In R, KEGG pathway enrichment can be performed using the `clusterProfiler` package too, but we will need to get the `Entrez IDs` for each gene first.

we will create a `gene.map` where we will get the `Entrez ID` for each gene name using `bitr()`

```r
gene.map <- bitr(DEGs$gene_name,
                 fromType = "SYMBOL",
                 toType = "ENTREZID",
                 OrgDb = "org.Hs.eg.db")
```

Then we will perform our KEGG Enrichment Analysis using `enrichKEGG()` and then convert the results to a tidy tibble for easier viewing

```r
ekg <- enrichKEGG(
    gene = gene.map$ENTREZID,   # The list of genes in Entrez ID format
    organism = "hsa",           # 'hsa' specifies Homo sapiens (use 'mmu' for mouse, etc.)
    pvalueCutoff = 0.05,        # Only pathways with raw p-values < 0.05 are considered
    qvalueCutoff = 0.05         # Only pathways with adjusted p-values (FDR) < 0.05 are considered
)

# Convert the results to a tidy tibble
ekg.df <- as_tibble(ekg, rownames = 'hsa') %>%
    arrange(p.adjust) %>%       # Sort pathways by adjusted p-value (most significant first)
    filter(p.adjust < 0.05)     # Keep only pathways with significant adjusted p-values
```

---

### Plotting & Interpreting the Results

We can Plot the KEGG results on a dot plot in the same way as GO results.

```r
# Dotplot - top 10 pathways
dotplot(ekg, showCategory = 5, title = "Top 5 KEGG Pathways")
```

<div style="text-align: center;">
  <img src="/assets/images/posts/Scroll-7-Thutmoses-Trends/KEGG_Dot_Plot.png" alt="KEGG Enrichment Dot Plot" width="500"/>
  <p style="font-size: 0.8em; color: gray;">KEGG Enrichment Dot Plot</p>
</div>

The KEGG dot plot is also interpreted in the same way.

here we can see that **Coronavirus disease - COVID-19** is highly enriched, followed by **Tuberculosis** and **Staphylococcus aureus infection**.

> Appearance of Infectious Diseases in KEGG results doesn't directly imply the prescense of such infections, but implies a similar inflammatory and immune actions and responses similar to those found in such diseases.

---

**We're Done!** GO and KEGG Enrichment Analysis are very powerful as they can quickly group a huge amount of DEGs into specific Pathways and Functions that can give meaning and ease interpretation of your data.

If you want to continue, head over to the next and final scroll: [Djoser's Discoveries]({{site_baseurl}}/Scroll-8-Djosers-Discoveries/), where we’ll perform Gene Set Enrichment Analysis (GSEA)

Time for our Cultural Spotlight!

---

## 🏛️ <a id="cultural-spotlight-thutmose-iii-the-conqueror-pharaoh-of-egypt">Cultural Spotlight: Thutmose III – The Conqueror Pharaoh of Egypt</a>

<div style="text-align: center;">
  <img src="/assets/images/posts/Scroll-7-Thutmoses-Trends/Thutmose_III.jpg" alt="Thutmose III" width="400"/>
  <p style="font-size: 0.8em; color: gray;"><a href="https://commons.wikimedia.org/wiki/File:Upper_part_of_a_statue_of_Thutmose_III_MET_07.230.3_11.jpg" target="_blank">Thutmose III - © Wikimedia Commons - CC0 1.0</a></p>
</div>

**Thutmose III**, often hailed as the **Napoleon of Ancient Egypt**, reigned during the 15th century BCE and is celebrated as one of the greatest military leaders in ancient history. Ascending to the throne as a young co-regent under **Queen Hatshepsut**, he eventually took full control and transformed Egypt into the most powerful empire of its time.

<div style="text-align: center;">
  <img src="/assets/images/posts/Scroll-7-Thutmoses-Trends/Thutmose_Obelisk.jpg" alt="Thutmose III Obelisk" width="400"/>
  <p style="font-size: 0.8em; color: gray;"><a href="https://commons.wikimedia.org/wiki/File:Obelisk_of_Thutmose_III_in_the_Hippodrome_of_Constantinople.jpg" target="_blank">Thutmose III Obelisk - © Wikimedia Commons / Winstonza - CC BY-SA 3.0</a></p>
</div>

One enduring testament to his reign is the **obelisk** now standing in the **Hippodrome of Constantinople** (modern-day Istanbul). It was originally in **Karnak**, this granite needle bears hieroglyphic inscriptions that proclaim his glory, a monument that has endured thousands of years.

---

> Papyrus Background from the Post's Cover photo is from <a href="https://www.freepik.com/free-photo/grunge-background_4258615.htm" target="_blank">Freepik</a>

---
