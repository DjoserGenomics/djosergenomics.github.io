---
layout: post
title: "Project Menhed Update #2: When The Simulation Is Too Perfect"
author: Nourelden
categories: ["Project Menhed"]
tags: ["Djoser Genomics", "2026"]
image: "assets/images/Project Menhed Landscape.jpg"
featured: true
hidden: false
---

I am back with a new progress update and earlier than last time! :D

Sometimes, the hardest part of metabolic engineering is admitting that your model is too perfect.
Let's recap where we left off.

### **The Two-Stage Fermentation Strategy**

In the last update, I mentioned that I was considering using a **Two-Stage Fermentation** strategy to produce Lycopene, and here we are.

Basically, the idea is to have two separate phases in the fermentation process:

1. **Growth Phase**: Where the E. coli focuses on growing and multiplying & The goal is to maximize biomass production.
2. **Production Phase**: Once a sufficient biomass is achieved, the conditions are shifted to favor the production of the Lycopene.

---

## **The Biological Reality**

So I spent more time with the literature and then I got back to work and visited my production envelope again, to be able to visualize the amount of Lycopene being produced at different growth rates.

<div style="text-align: center;">
  <img src="/assets/images/posts/Project-Menhed-Update-1-The-Math-Won-For-Now/Growth vs Lycopene.png" alt="Growth vs Lycopene Production" width="500"/>
  <p style="font-size: 0.8em; color: gray;">Growth vs Lycopene Production</p>
</div>

However, I noticed something, when I try to compare the theoretical yields from the model to actual experimental data from literature, there is a **significant** gap.

Simple Static **FBA** models often overestimate production capabilities because they don't account for regulatory mechanisms, enzyme kinetics, and other cellular constraints present in real biological systems.

Additionally, FBA assumes that the cell machinery switches almost instantly between growth and production modes, which is not the case in reality.

### **So, What am i going to do?**

To address these constraints and limitations, I am planning to - as realistically as possible - to incorporate these limitations into my model to get as close to mimicking industrial fermentation conditions.

The Plan will include some constraints such as:

1. **Reducing Oxygen Bounds** to simulate microaerobic conditions during the production phase.
2. **Reducing Food Source Bounds** (Glucose/Glycerol/Fatty acids) to limit the carbon source availability.
3. **Adjusting ATP Maintenance Requirements** to reflect the energy demands of Lycopene synthesis.

To properly simulate the cell machinery lag between the two phases that FBA doesn't account for, I will be reading about and using **Minimization of Metabolic Adjustment (MOMA)** to simulate the transition between growth and production phases more realistically.

I will also look into **Dynamic FBA (dFBA)** to model the time-dependent changes in metabolite concentrations and fluxes.

### **What is next?**

If Everything goes smoothly, and I dont spend another couple of weeks fighting with the code and constraints, I should be able to have a working and somehow realistic simulation of the Two-Stage Fermentation by the next update.

Then we will start working on optimizing the production through various strategies including **Flux Scanning based on Enforced Objective Flux (FSEOF)** for overexpression candidates, exploring potential gene knockouts that could enhance Lycopene yield during the production phase and trying out alternative pathways, precursors, and feeding strategies to boost Lycopene synthesis (Which should be fun :D).

Oh and by the way, When i was in my Literature deep dive, I found this amazing paper, [Synergistic Production of Lycopene and &beta;-Alanine Through Engineered Redox Balancing in Escherichia coli](https://www.mdpi.com/3401834) which was really cool because i never thought that you can balance redox reactions by producing another compound at the same time. Definitely worth a read if you are into Metabolic Engineering :D.

---

**As Always Work Continues.**

See you in the next log. (Hopefully with more data and results!)

> All Updates will be available in the **Progress Updates** section of the [announcement post]({{site_baseurl}}/Introducing-Project-Menhed/)
