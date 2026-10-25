---
layout: about
title: home
permalink: /
subtitle: 

profile:
  align: right
  image: ProfilePic2.jpg #IMG-20251013-WA0009(1).jpg
  #image: 20241230_163648.jpg
  image_circular: false # crops the image to make it circular
  more_info: >
    <p>Research Intern</p>
    <p>Universität des Saarlandes</p>
#    <p>Saarbrücken, Saarland, Germany</p>

news: true # includes a list of news items
selected_papers: false # includes a list of papers marked as "selected={true}"
social: true # includes social icons at the bottom of the page
---

I am a Research Intern in Computational Biophysics at [Universität des Saarlandes](https://www.uni-saarland.de/) in Germany, where I leverage high-performance computing and molecular dynamics simulations to investigate how small-molecule drugs interact with lipid bilayers to inhibit membrane fusion. I hold a MSc Degree in Statistical Physics from [Cinvestav](https://cinvestav.mx/) in Mexico, where my research focused on Artificial Intelligence and Circular Dichroism spectra prediction.

Overall, my work sits at the intersection of Artificial Intelligence, Machine Learning, and Biophysics, with a focus on developing computational tools for biological and medical applications.

<div class="row justify-content-center text-center mt-4 mb-3 align-items-center">
  <div class="col-auto">
    <img src="/assets/img/biophysics2-icon.png" alt="Physics" class="img-fluid rounded" style="max-width: 65px;">
    <p class="mt-1 small"><strong>Biophysics</strong></p>
  </div>
  <div class="col-auto">
    <h4 class="text-muted mx-2 my-0">+</h4>
  </div>
  <div class="col-auto">
    <img src="/assets/img/ai2-icon.png" alt="AI" class="img-fluid rounded" style="max-width: 65px;">
    <p class="mt-1 small"><strong>Artificial Intelligence</strong></p>
  </div>
  <div class="col-auto">
    <h4 class="text-muted mx-2 my-0">+</h4>
  </div>
  <div class="col-auto">
    <img src="/assets/img/medicine2-icon.png" alt="Biology" class="img-fluid rounded" style="max-width: 65px;">
    <p class="mt-1 small"><strong>Medicine</strong></p>
  </div>
</div>

I am always open to collaborating or just meeting new people (both in and outside of science). If you would like to connect, feel free to reach out! 🔗🌐🧪🧬

---

# Projects

#### Molecular Dynamics Simulations of Membranes

At the [Computational Biophysics Group](https://biophys.uni-saarland.de/) at [Saarland University](https://www.uni-saarland.de/start.html), I am applying all-atom Molecular Dynamics to study lipid membrane mechanics. My current research focuses on how the antiviral compound Cf2642 interacts with POPC bilayers (**fig. 1**) to inhibit membrane fusion. Leveraging the Smaug HPC cluster, I use GROMACS and custom Python pipelines to analyze membrane density profiles and order parameters.

<figure class="text-center">
  <img src="/assets/img/cf2642.png" 
       class="img-fluid rounded"
       style="width: 100%; max-width: 540px;" 
       alt="Membrane">
</figure>
<div class="caption">
    <strong>Fig. 1. All-atom Molecular Dynamics simulations of POPC bilayers with a 20 mol% drug concentration, comparing modern force field parameterizations.</strong> <strong>(A)</strong> Simulation parameterized using AMBER LIPID21 for lipids and OpenFF for the ligand. <strong>(B)</strong> Simulation parameterized using CHARMM36 for lipids and CGenFF for the ligand.
</div>

#### AI-driven CD Spectra Prediction

My [Master's thesis](https://manuroag.github.io/projects/msc_thesis/) focused on enhancing the [KCD method](https://doi.org/10.1002/pro.4967)'s predictive capabilities for protein Circular Dichroism (CD) spectra (**fig. 2**). By designing and training deep Bayesian Neural Networks (BNNs), I achieved a 40% improvement in prediction accuracy compared to the original model.

<figure class="text-center">
  <img src="/assets/img/KCD_AI.png" 
       class="img-fluid rounded"
       style="width: 100%; max-width: 560px;" 
       alt="KCD AI Model">
</figure>
<div class="caption">
    <strong>Fig. 2. KCD-AI workflow.</strong> Four Bayesian Neural Networks were integrated into the KCD model to increase the accuracy in CD spectra predictions.
</div>

#### G-Protein-Coupled Receptors (GPCRs)

I am currently investigating a mutation in the human H2 receptor (hH2R) (**fig. 3**) using Molecular Dynamics (MD) simulations, in collaboration with Miroslava Carrasco from the [Department of Physiology, Biophysics and Neuroscience at Cinvestav](https://www.fisio.cinvestav.mx/).

<figure class="text-center">
  <img src="/assets/img/hH2R.png" 
       class="img-fluid rounded"
       style="width: 100%; max-width: 530px;" 
       alt="Human H2 Receptor">
</figure>
<div class="caption">
    <strong>Fig. 3. Cryo-EM structure of the histamine-bound H2R-Gs/Nb35/ND complex.</strong> <strong>(a)</strong> Cryo-EM density map. <strong>(b)</strong> Ribbon model. [Credit: <a href='https://www.nature.com/articles/s41467-024-46096-z'>Köck, Z. et al.</a>]
</div>

#### AI-driven Drug Discovery

Alongside this, I am developing "[Drug Hunter](https://manuroag.github.io/projects/drug_hunter/)," an independent project focused on predicting drug-protein binding affinity using Graph Convolutional Networks (GCNs) (**fig. 4**) to keep up with the aplications of AI to Science.

<figure class="text-center">
  <img src="/assets/img/GCN.png" 
       class="img-fluid rounded"
       style="width: 100%; max-width: 540px;" 
       alt="Graph Convolutional Network">
</figure>
<div class="caption">
    <strong>Fig. 4. Illustration of the graph convolutional network.</strong> [Modified from: <a href='https://onlinelibrary.wiley.com/doi/abs/10.1002/bkcs.11730'>Cho, H. & Choi, I.</a>]
</div>

--- 
