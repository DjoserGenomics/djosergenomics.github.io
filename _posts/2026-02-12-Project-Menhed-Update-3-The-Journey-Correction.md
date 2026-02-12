---
layout: post
title: "Project Menhed Update #3: The Journey Correction"
author: Nourelden
categories: ["Project Menhed"]
tags: ["Djoser Genomics", "2026"]
image: "assets/images/Project Menhed Landscape.jpg"
featured: true
hidden: false
---

Well, Things didn't go smoothly, and I spent another couple of weeks fighting with the code and constraints XD.

But i have learned the most important lesson of all, which is that **You can't perfectly simulate real biological systems and fluxes** yet.

### **What was i trying to do?**

I was trying to simulate a Two-Stage Fermentation Strategy, where i would have a growth phase and a production phase, and i would try to optimize the production phase to get the maximum yield of Lycopene and my plan was to compare the production numbers i get from COBRApy with the experimental data from literature and as i said before the gap was huge

I tried to address this issue with many proposed solutions that i discussed in the previous [Update #2 Log]({{site_baseurl}}/Project-Menhed-Update-2-When-The-Simulation-Is-Too-Perfect/) but the gap remained huge; I went on a journey through literature, other projects and even asked AI models until i realized something crucial, the way i understood it was **Currently tools like COBRApy cannot present actual production numbers because you can't perfectly simulate real biology in it, it can though be useful to compare strategies and see which ones are better.**

And this conclusion made sense to me, You can use the model to refine your strategies, figure out the best ones, or ones that are worth trying, but Wet Lab validations are the only way to get actual and accurate production numbers.

---

### **The Journey Correction**

So now that realization has hit in, i have to change my approach, so i will be continuing this project with a new strategy, where i will be using COBRApy to compare different strategies, different overexpressions, gene knockouts, and different feeding strategies to compare the production of Lycopene from each one.

Let me show a simple example

<div style="text-align: center;">
  <img src="/assets/images/posts/Project-Menhed-Update-3-The-Journey-Correction/Glucose vs Glycerol - Lycopene Production Envelopes.png" alt="Production vs Growth Rate" width="500"/>
  <p style="font-size: 0.8em; color: gray;">Glucose vs Glycerol [Equimolar Carbon Basis (60 C-mmol)] - Lycopene Production Envelopes</p>
</div>

This Graph shows the production of Lycopene against different growth rates using two different carbon sources, Glucose and Glycerol. As you can see, Both the production of Lycopene and the growth rate are much higher when using Glycerol as a carbon source.

However this can prove wrong in wet lab validation, as e coli uptake and usage of Glycerol is not as smooth and fast as it uses Glucose, this is why kinetic models are as important to Stoichiometric models.

This is just a simple example, but i plan to use this strategy to compare different strategies, different overexpressions, gene knockouts, and different feeding strategies to compare the production of Lycopene from each one.

---

### **Not Only Production Envelopes**

Such production envelopes can be useful to infer or predict the production of Lycopene across different growth rates but it doesn't necessarily mean that the e coli will produce the Lycopene at all. This is why i will also explore ways to actually produce lycopene in the e coli while maintaining Biomass production as its objective as this can be much more useful and realistic than setting the production of lycopene as the objective.

The Objective point was very crucial for me to understand, because so far any comparisons i tried to make were all based on the theoritical maximum production of lycopene, where everything is already optimized through Flux Balance Analysis (FBA) so i need to change this and monitor the fluxes while Biomass remains as the objective. One important source that i found online about this point is [This PDF by Keesha Erickson](https://cnls.lanl.gov/external/qbio2018/Slides/FBA%202/qBio-FBA-lab-slides.pdf) where they managed to produce Lycopene in E Coli while maintaining Biomass production as its objective through a series of overexpressions.

---

**As Always, Work Continues.**

See you in the next log.

> All Updates will be available in the **Progress Updates** section of the [announcement post]({{site_baseurl}}/Introducing-Project-Menhed/)
