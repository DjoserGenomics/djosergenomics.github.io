---
layout: post
title: "Field Note 09: Dispatch - HTGAA Week 2 Homework"
author: Nourelden
categories: [FieldNotes]
tags: ["Djoser Genomics", "FieldNotes", "Dispatch", "HTGAA", "2025"]
image: "assets/images/Djoser Genomics Field Notes Landscape.png"
featured: false
hidden: true
---

## **Part 3: DNA Design Challenge**

### **3.1. Choose your protein.**

**Tyrosinase** from Priestia megaterium (ACC86108.1). I chose this protein because my project is to create biological dyes, and this enzyme can convert a common precursor (Tyrosine) into a robust black/brown melanin pigment, making it a perfect 'MVP' for my project.

Here is the Protein Sequence from UniProt/NCBI:

`MSNKYRVRKNVLHLTDTEKRDFVRTVLILKEKGIYDRYIAWHGAAGKFHTPPGSDRNAAHMSSAFLPWHREYLLRFERDLQSINPEVTLPYWEWETDAQMDPSQSQIWSADFMGGNGNPIKDFIVDTGPFAAGRWTTIDEQGNPSGGLKRNFGATKEAPTLPTRDDVLNALKITQYDTPPWDMTSQNSFRNQLEGFINGPQLHNRVHRWVGGQMGVVPTAPNDPVFFLHHANVDRIWAVWQIHRNQNYQPMKNGPFGQNFRDPMYPWNTTPEDVMNHRKLGYVDIELRKSKRSS`

### **3.2. Reverse Translate: Protein (amino acid) sequence to DNA (nucleotide) sequence.**

Here is the original nucleotide sequence for P. megaterium **Tyrosinase** (from NCBI Accession EU627691)

`ATGAGTAACAAGTATAGAGTTAGAAAAAACGTATTACATCTTACCGACACGGAAAAAAGAGATTTTGTTCGTACCGTGCTAATACTAAAGGAAAAAGGGATATATGACCGCTATATAGCCTGGCATGGTGCAGCAGGTAAATTTCATACTCCTCCGGGCAGCGATCGAAATGCAGCACATATGAGTTCTGCTTTTTTACCGTGGCATCGTGAATACCTTTTACGATTCGAACGTGACCTTCAGTCAATCAATCCAGAAGTAACCCTTCCTTATTGGGAATGGGAAACGGACGCACAGATGCAGGATCCCTCACAATCACAAATTTGGAGTGCAGATTTTATGGGAGGAAACGGAAATCCCATAAAAGATTTTATCGTCGATACCGGGCCATTTGCAGCTGGGCGCTGGACGACGATCGATGAACAAGGAAATCCTTCCGGAGGGCTAAAACGTAATTTTGGAGCAACGAAAGAGGCACCTACACTCCCTACTCGAGATGATGTCCTCAATGCTTTAAAAATAACTCAGTATGATACGCCGCCTTGGGATATGACCAGCCAAAACAGCTTTCGTAATCAGCTTGAAGGATTTATTAACGGGCCACAGCTTCACAATCGCGTACACCGTTGGGTTGGCGGACAGATGGGCGTTGTGCCTACTGCTCCGAATGATCCTGTCTTCTTTTTACACCACGCAAATGTGGATCGTATTTGGGCTGTATGGCAAATTATTCATCGTAATCAAAACTATCAGCCGATGAAAAACGGGCCATTTGGTCAAAACTTTAGAGATCCGATGTACCCTTGGAATACAACCCCTGAAGACGTTATGAACCATCGAAAGCTTGGGTACGTATACGATATAGAATTAAGAAAATCAAAACGTTCCTCATAA`

### **3.3. Codon optimization.**

I need to codon optimize the gene to ensure it can be expressed at a high level in my new chassis. The original organism (P. megaterium) might have 'favorite' codons which are different than my 'factory' organism (E. coli). By optimizing, I'm 'translating' the gene into E. coli's preferred 'codons' to prevent the ribosome from stalling and to get the fastest, most efficient protein production.

I chose **E. coli K12**, because it is the standard and a well understood chassis for this type of metabolic engineering.

`ATGAGCAACAAATATCGCGTGCGCAAAAACGTGCTGCATCTGACCGATACCGAAAAACGCGATTTTGTGCGCACCGTGCTGATTCTGAAAGAAAAAGGCATTTATGATCGCTATATTGCGTGGCATGGCGCGGCGGGCAAATTTCATACCCCGCCGGGCAGCGATCGCAACGCGGCGCATATGAGCAGCGCGTTTCTGCCGTGGCATCGCGAATATCTGCTGCGCTTTGAACGCGATCTGCAGAGCATTAACCCGGAAGTGACCCTGCCGTATTGGGAATGGGAAACCGATGCGCAGATGCAGGATCCGAGCCAGAGCCAGATTTGGAGCGCGGATTTTATGGGCGGCAACGGCAACCCGATTAAAGATTTTATTGTGGATACCGGCCCGTTTGCGGCGGGCCGCTGGACCACCATTGATGAACAGGGCAACCCGAGCGGCGGCCTGAAACGCAACTTTGGCGCGACCAAAGAAGCGCCGACCCTGCCGACCCGCGATGATGTGCTGAACGCGCTGAAAATTACCCAGTATGATACCCCGCCGTGGGATATGACCAGCCAGAACAGCTTTCGCAACCAGCTGGAAGGCTTTATTAACGGCCCGCAGCTGCATAACCGCGTGCATCGCTGGGTGGGCGGCCAGATGGGCGTGGTGCCGACCGCGCCGAACGATCCGGTGTTTTTTCTGCATCATGCGAACGTGGATCGCATTTGGGCGGTGTGGCAGATTATTCATCGCAACCAGAACTATCAGCCGATGAAAAACGGCCCGTTTGGCCAGAACTTTCGCGATCCGATGTATCCGTGGAACACCACCCCGGAAGATGTGATGAACCATCGCAAACTGGGCTATGTGTATGATATTGAACTGCGCAAAAGCAAACGCAGCAGC`

### **3.4. You have a sequence! Now what?**

Once i have the codon optimized sequence for **Tyrosinase**, I now need to synthesize the DNA. after synthesis, I can clone into a plasmid vector and then introduce it to E. coli through a process called transformation, which can be done using heat or electric shock.

Once in there, the bacteria can start producing the **Tyrosinase** enzyme through first Transcription of the gene from the DNA to create mRNA and then Translation of the mRNA to create the protein. This process will continue, and **Tyrosinase** will start converting Tyrosine into melanin pigment, until the bacteria accumilate enough pigment and then can be extracted and purified for use as a biological dye.

### **_3.5. [Optional] How does it work in nature/biological systems?_**

### **Describe how does a single gene code for multiple proteins at the transcriptional level?**

Alternative Splicing. A single Gene in Eukaryotes can code for multiple proteins through a process called Alternative Splicing, It takes on many forms, like Exon Skipping, where a certain exon might be skipped possibly altering the protein function, or Alternative 5' or 3' Splicing, where some exons can be longer or shorter hence affecting the number of produced amino acids altering the function too, another way is intron retention where some introns are not spliced out which can introduce a stop codon and can cause the protein to decay using the Nonsense mediated decay pathway.

## **Part 4: DNA Read/Write/Edit**

### **4.1 DNA Read**

#### **(i) What DNA would you want to sequence (e.g., read) and why?**

I want to find new pigment-producing enzymes. The original **Tyrosinase** gene came from Priestia megaterium. I would want to perform whole genome sequencing on this bacterium. By sequencing its entire genome, I can use bioinformatics to search for and discover the entire metabolic pathway for melanin, and potentially maybe find other novel enzyme pathways for different colors that we don't even know about yet.

#### **(ii) In lecture, a variety of sequencing technologies were mentioned. What technology or technologies would you use to perform sequencing on your DNA and why?  Also answer the following questions:**

I would use **Illumina Sequencing** technology to perform a whole genome sequencing of the Priestia megaterium bacterium. Illumina is known for its high accuracy, throughput, and cost-effectiveness, making it suitable for confirming the sequence of a specific gene like Tyrosinase.

##### **1. Is your method first-, second- or third-generation or other? How so?**

Illumina Sequencing is considered a second-generation sequencing technology. It utilizes massively parallel sequencing, where millions of DNA fragments are sequenced simultaneously, allowing for high throughput and accuracy compared to first-generation methods like Sanger sequencing.

##### **2. What is your input? How do you prepare your input (e.g. fragmentation, adapter ligation, PCR)? List the essential steps.**

My input is the DNA of the Priestia megaterium bacterium. First i will need to extract the genomic DNA from the bacterial cells. Then, I will need to fragment the DNA into smaller pieces using mechanical shearing or enzymatic digestion. Next, I need to add adapters to both ends of the DNA fragments through a process called adapter ligation. Then, I will amplify them all using PCR to create a library of DNA fragments ready for sequencing.

##### **3. What are the essential steps of your chosen sequencing technology, how does it decode the bases of your DNA sample (base calling)?**

First is Cluster Generation, where the prepared DNA library is loaded onto a flow cell and the fragments are amplified to form clusters of identical sequences. Next is Sequencing by Synthesis, where fluorescented-Nucleotides are added and incorporated into the DNA strands one at a time by DNA polymerase. Each time it is added, a camera snaps a picture to detect the fluorescence color, which corresponds to a specific base (A, T, C, or G). This process is repeated for multiple cycles to read the entire sequence of each fragment. Finally, the data is processed through base calling algorithms that analyze the fluorescence signals to determine the sequence of bases in the DNA fragments.

##### **4. What is the output of your chosen sequencing technology?**

A FASTQ file containing the sequenced reads along with their quality scores.

### **4.2 DNA Write**

#### **(i) What DNA would you want to synthesize (e.g., write) and why?**

I would like to design and synthesize a genetic circuit that can produce a range of vibrant biological pigments in E. coli based on some certain inputs or triggers, the circuit would include genes, promoters, terminators and Ribosome Binding Sites (RBS) for multiple different pigment-producing enzymes, that are codon optimized for E. coli expression, Thus Creating a versatile colorful bacterial biological dye factory.

#### **(ii) What technology or technologies would you use to perform this DNA synthesis and why? Also answer the following questions:**

I would use **Oligonucleotide synthesis** combined with Gibson Assembly to synthesize the genetic circuit. **Oligonucleotide synthesis** allows for the precise creation of short DNA sequences, which can be assembled into larger constructs using Gibson Assembly.

##### **1. What are the essential steps of your chosen synthesis methods?**

First the Genetic circuit will need to be designed and optimized for the chosen chassis (E. coli). Then, the plasmid would be sent to DNA synthesis companies like **Twist Bioscience** to construct the full plasmid containing my genetic circuit. Next, the fragments would be assembled together using Gibson Assembly, which allows for joining multiple DNA fragments into a single one without leaving scar sites behind. Finally the plasmid would be sequenced to confirm the correct sequence and no errors have occured during the synthesis process.

##### **2. What are the limitations of your synthesis method (if any) in terms of speed, accuracy, scalability?**

DNA synthesis while now is much cheaper than before, still remains relatively expensive for large constructs. Additionally, the Chemistry is not 100% perfect so to minimize errors, they have to be constructed in smaller fragments (Oligos) and then assembled since longer sequences tend to have higher error rates. The speed of synthesis can also be a limitation, as it may take several days to weeks to receive the synthesized DNA from companies. Also, Some DNA sequences with high GC content or repetitive regions can be challenging to synthesize accurately or even impossible to do so (With today's technology at least :D).

### **4.3 DNA Edit.**

#### **(i) What DNA would you want to edit and why?**

I would like to edit the DNA of some crops like wheat to enhance their nutritional content by introducing genes that can produce essential vitamins and minerals that are otherwise lacking in these staple foods.

#### **(ii) What technology or technologies would you use to perform these DNA edits and why? Also answer the following questions:**

I'd use **CRISPR-Cas9** for its precision, efficiency, and versatility in editing specific genes within the crop genome.

##### **1. How does your technology of choice edit DNA? What are the essential steps?**

**CRISPR-Cas9** edits DNA by utilizing a guide RNA (gRNA) that is designed to match a specific target sequence in the genome. The Cas9 protein, then binds to the target DNA and creates a double-strand break at that location. Since I need precision edit and replace, I'd want the cell to repair the break using **Homology Directed Repair (HDR)** and to achieve that, I would provide multiple copies of the desired repair template (containing the new gene I want to insert or the changes I want to make) into the cell so that the cell can use it as a template for repairing the break, thus introducing the desired edit into the genome.

##### **2. What preparation do you need to do (e.g. design steps) and what is the input (e.g. DNA template, enzymes, plasmids, primers, guides, cells) for the editing?**

for the preparation, I first would need to choose the cas9 variant that best suits my needs which would depend on the my DNA and the PAM sites availability. Then I would design the guide RNA (gRNA) to specifically target the gene or region that i want to edit. Then I need to design and synthesize my repair template containing my desired changes so that it can be used by the cell during HDR.

##### **3. What are the limitations of your editing methods (if any) in terms of efficiency or precision?**

One of the limitations of CRISPR-Cas9 is off-targets and their effects, which is the cas9 making cuts at unintended or unexpected locations in the genome, which can range from no effect to harmful and sometimes lethal effects. Also, the HDR pathway is not very efficient in many cell types, lowering success rates compared to the more error prone Non-Homologous End Joining (NHEJ) repair pathway.

> Check out Other HTGAA Submissions from [Here]({{site_baseurl}}/HTGAA-Assignments/)
