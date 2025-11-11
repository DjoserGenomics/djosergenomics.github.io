---
layout: post
title: "Armored Phage: A Thermostable MS2 Phage Proposal"
author: Nourelden
categories: [Projects, Synthetic Biology, Protein Design]
tags: ["Djoser Genomics", "Projects", "Synthetic Biology", "HTGAA"]
image: "assets/images/posts/Armored-Phage-A-Thermostable-MS2-Phage-Proposal/Armored Phage Proposal Landscape.png"
featured: true
hidden: false
---

A Proposal to Engineer a Thermostable MS2 Bacteriophage Using Protein Design Techniques.

> This Proposal is part of **How To Grow Almost Anything (HTGAA)** Course Homework for Week 4 (Protein Design), Check the [Week 4 Homework]({{site_baseurl}}/Field-Note-11-Dispatch-HTGAA-Week-4-Homework/) for more details.

---

## **Project Goal**

The Goal of this project is to engineer a thermostable variant of the MS2 bacteriophage through reengineering its **Capsid protein** to be more resistant to high temperatures. This will create a robust phage, which is critical for applications like phage therapy.

### **Our Proposed Pipeline and Tools**

Our pipeline is 100% computational and leverages state-of-the-art protein design and structure prediction tools:

1. Analyze the MS2 Capsid Protein Structure using tools like **PyMOL** or **ChimeraX** (`PDB ID: 2MS2`):

   - Understand how the individual capsid protein monomers lock together to form the icosahedral shell.
   - Identify key structural features and regions that contribute to thermal stability.
   - Map out potential weakness sites that a mutation or an edit could enhance its thermal stability.

2. Use **AlphaFold** to Predict the structure of a single Capsid Protein Monomer:

   - The Target is to identify flexible regions or loops that break easily at high temperatures.
   - Usually these regions can be highlighted by low confidence scores in AlphaFold predictions.

3. Use **ProteinMPNN** to try and design mutations in the Capsid Protein:

   - Stable Regions would be masked to keep intact.
   - Only flexible regions would be targeted for mutations.

4. Predict and verify the structure of the mutated Capsid Protein Monomer using **AlphaFold**:
   - Ensure that the overall fold of the protein is maintained.
   - Check if the mutations introduced have improved the stability of the protein.
   - Look for increased hydrogen bonding, salt bridges, and hydrophobic interactions.

### **Why These Tools?**

- **PyMOL/ChimeraX**: These are powerful molecular visualization tools that allow us to view and analyze protein structures, making it easier to identify key features related to stability.

- **AlphaFold**: It provides highly accurate protein structure predictions, which is essential for identifying flexible regions and understanding how mutations may affect the protein's 3D folding.

- **ProteinMPNN**: It designs a new protein sequence based on 3D structural information, making it ideal for suggesting mutations that could enhance thermal stability and allows for masking stable regions to preserve essential structural features.

### **Potential Pitfalls**

1. **Function Loss**: By making the capsid protein more rigid and heat stable, we may unintentionally disrupt its ability to assemble into a functional phage capsid or interfere with its ability to infect host bacteria.

2. **Prediction Erros**: Our entire pipeline relies on computational predictions, which may not always accurately reflect real behaviour. Experimental validation would be necessary to confirm the effectiveness of the designed mutations.

3. **Limited Mutation Space**: The capsid protein may have limited sites that can be mutated without disrupting its structure, function, or folding which can limit our design options.
