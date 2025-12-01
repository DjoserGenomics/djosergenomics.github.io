---
layout: post
title: "Field Note 14: Dispatch - HTGAA Week 7 Homework"
author: Nourelden
categories: [FieldNotes]
tags: ["Djoser Genomics", "FieldNotes", "Dispatch", "HTGAA", "2025"]
image: "assets/images/Djoser Genomics Field Notes Landscape.png"
featured: false
hidden: true
---

### **1. How do endoribonucleases (ERNs) work to decrease protein levels? Name 2 differences between how ERNs work and how proteases work.**

- Endoribonucleases (ERNs) are enzymes that cut RNA molecules, leading to their degradation and preventing them from being translated into proteins.
- Two differences between how ERNs work and how proteases work are:
  1. ERNs target RNA molecules, while proteases target proteins.
  2. ERNs reduce protein levels by preventing protein synthesis at the RNA level, whereas proteases decrease protein levels by breaking down existing proteins.
- ERNs are much more efficent than proteases since a single mRNA can be translated multiple times before it degrades, while proteases can only degrade one protein at a time.

### **2. How does lipofectamine 3000 work? How does DNA get into human cells and how is it expressed?**

Lipofectamine 3000 is a transfection reagent that facilitates the delivery of nucleic acids (like DNA) into eukaryotic cells. It works by forming lipid-DNA complexes called lipoplexes, which can fuse with the cell membrane, then degrades allowing the DNA to enter the cell. Once inside the cell, the DNA is transported to the nucleus, where it can be transcribed into mRNA. The mRNA is then translated into proteins by the cell's ribosomes in the cytoplasm.

### **3. Explain what poly-transfection is and why it’s useful when building neuromorphic circuits.**

Transfection is the process of introducing nucleic acids into mamalian cells. Poly-transfection is the simultaneous transfection of multiple different plasmids (3 or more) into cells. This is useful when building neuromorphic circuits because it allows for the expression of multiple genes or genetic components within the same cell, enables weighing of the inputs by varying the amounts of each plasmid used.

### **4. Genetic Toggle Switches:**

#### **Provide a detailed explanation of the mechanism behind genetic toggle switches, including how bi-stability is established and maintained.**

Genetic toggle switches relies on mutual repression between two genes. Each gene produces a repressor protein that inhibits the expression of the other gene maintining bi-stability. When one gene is active, the other is repressed, and vice versa. The system can be switched between the two states by introducing specific inducers or environmental changes. The stability is maintained through feedback loops, where the active gene continues to produce its repressor, ensuring that the other gene remains off until an external signal triggers a switch.

#### **Describe at least one induction method used to switch states, including molecular signals or environmental factors involved.**

This is done through chemical inducers or environmental changes. For example, if Repressor A inhibits Gene B, adding an inducer that binds to repressor A and inactivates it will allow Gene B to be expressed, successfully switching the state of the toggle switch.

#### **Are there any limitations? How many ‘switches’ can we potentially chain? Is there a metabolic cost?**

Yes, Limitations include Noise or leaky expression, where a gene is always expressed but at very low levels, if increases this can cause unwanted switching. Also the more switches you chain, the more complex the circuit becomes, consuming more cellular resources thus increasing the metabolic cost which can slow growth and affect cell viability. The number of switches that can be chained is limited by the complexity of the system and the metabolic burden on the cell, but theoretically, multiple switches can be combined to create more complex circuits.

### **5. Natural Genetic Circuit Example:**

#### **Identify and describe in detail a naturally occurring genetic circuit, emphasizing its biological function, components, and regulatory interactions.**

A classic example of a natural genetic circuit is the ** lac operon** in E. coli, which functions as a metabolic logic gate to optimize energy efficiency. It operates as an AND NOT gate, ensuring that the machinery to digest lactose is produced only when lactose is present (the input) AND glucose is absent (the preferred source). This control is achieved through two regulatory mechanisms: the LacI repressor (a sensor for lactose), which acts as a "handbrake" by blocking transcription until lactose releases it, and the CAP activator (a sensor for low glucose), which acts as an "accelerator" by recruiting RNA polymerase only when glucose levels drop.

### **6. Synthetic Genetic Circuit:**

#### **Select and critically analyze a synthetic genetic circuit previously engineered by researchers (e.g., pDAWN). Provide details about its construction, components, intended function, and performance.**

The Repressilator (Elowitz & Leibler, Nature 2000)

The Repressilator is a foundational synthetic genetic oscillator constructed in E. coli using a cyclic negative feedback loop comprised of three specific repressor-promoter pairs. The circuit logic follows a "Rock-Paper-Scissors" dynamic where TetR represses $\lambda$ cI, $\lambda$ cI represses LacI, and LacI represses TetR, effectively creating an unstable system that perpetually cycles through states; a green fluorescent protein (GFP) reporter was co-expressed with tetR to visualize the output. Its intended function was to generate autonomous, periodic oscillations in gene expression independent of the cell cycle or external cues. The circuit successfully demonstrated that complex temporal behavior could be programmed using simple genetic components, producing visible oscillations in GFP fluorescence with periods longer than the cell division time, proving that biological "clocks" could be built from scratch.

#### **Discuss potential limitations or improvements suggested in subsequent literature or experimental data.**

- Noise & Drift: The original circuit was extremely "noisy". While individual cells blinked, they quickly became desynchronized. After a few hours, a population of bacteria would just look like a constant "average" green because every cell was blinking at a different time.

- Metabolic dependence: The oscillation period was heavily dependent on the cell's growth rate and environmental conditions.
