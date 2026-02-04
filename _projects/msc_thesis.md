---
layout: page
title: "AI-driven Prediction of Circular Dichroism Spectra of Proteins"
description: My M.Sc. Thesis.
img: assets/img/thesis.png
importance: 3
category: independent
related_publications: false
---

📓 See the [full Thesis here](/assets/pdf/MScThesis_JoseManuelRoblesAguilar.pdf).

---

## ➿ Circular Dichroism (CD)

An important property of the amino acids that compose proteins is chirality. A molecule is chiral when it is not superimposable on its mirror image. Chirality in amino acids arises from the presence of an asymmetric carbon, a carbon atom tetrahedrally bonded to four different atoms or groups. Glycine, which has a hydrogen atom as its side chain, is the only achiral amino acid.

Chiral structures can be distinguished and characterized by Circular Dichroism (CD) spectroscopy, a technique based on measuring the differential absorption of left- and right-circularly polarized light. For proteins, CD occurs in the near and far ultraviolet (UV) wavelength ranges, where the amide and carbonyl groups of the polypeptide backbone absorb light.

Circular Dichroism (CD) spectroscopy is a versatile and rapid method for characterizing the secondary structure, conformation, and folding of proteins. While not a high-resolution technique, it is invaluable for analyzing protein-ligand interactions, validating computationally predicted structures, and assessing the effects of mutations.

<figure class="text-center">
  <img src="/assets/img/thesis.png" 
       class="img-fluid rounded"
       style="width: 100%; max-width: 680px;" 
       alt="CD Spectroscopy">
</figure>
<div class="caption">
    Credit: <a href='https://commons.wikimedia.org/w/index.php?curid=139489607
'>Wikipedia</a> & <a href='https://doi.org/10.1007/978-1-0716-0892-0_11'>Micsonai A, et al.</a>
</div>

---

## 💻 Why to Predict CD Spectra?

Computational prediction of CD spectra is particularly useful for comparing two proteins when the high-resolution structure of one protein (determined by methods such as X-ray diffraction, cryo-EM, or NMR) or a predicted structure (e.g., from AlphaFold or similar tools) is available, but only the CD spectrum of the second protein is known. These comparisons serve various purposes, including validating structural similarity (homology), assessing the folding of mutated proteins, observing the effects of ligand binding, or environmental factors on protein conformation, and determining whether modeled (or predicted) structures have CD spectra similar to experimental spectra.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/validation.png" title="CD model validation" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Computational prediction of CD spectra is a powerful tool for structural comparison and validation.
</div>

---

## 📖 The Knowledge-based Circular Dichroism (KCD) method

The Knowledge-based Circular Dichroism (KCD) server utilizes a model based on the classical theory of optical activity with a complex set of atomic polarizabilities. These polarizabilities are obtained from a base of SRCD spectra and PDB structures from the PCDDB to predict far-UV CD spectra from the three-dimensional structural information of a target protein. This information includes the secondary structure content provided by the Structural Identification (STRIDE) algorithm and the atoms belonging to D-amino acid residues. The KCD server accepts a PDB file of the target protein as input and an optional spectrum file for normalization and comparison, which should be a simple two-column ASCII file (.dat or similar). The user is also required to provide their name and email address. The results are sent to the user via email and include a plot of the experimental and predicted spectra superimposed, a bar graph with the percentage content of secondary structures (alpha, beta, coils, and others) and D-residues, and the ASCII data file of the predicted spectrum.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/KCD.png" title="KCD" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Credit: <a href='https://doi.org/10.1002/slct.202300408'>Takashi Misawa, Yokuse Demizu.</a> & <a href='https://doi.org/10.1002/pro.4967'>Jacinto Méndez, D. et al.</a>
</div>

---

## 📄 The DeVoe's Theory of Optical Activity and KCD

Howard DeVoe, in two seminal papers, presented a classical theoretical description of
optical properties, including ellipticity, optical rotation, and extinction coefficients. This
model has been widely applied to structural problems in organic, inorganic, and polymer
chemistry. One of its primary advantages is its simplified framework, which treats the
protein’s chromophores as damped oscillators modeled as point dipoles. This provides a
suitable method for deriving optical properties while allowing for the polarizabilities to
be determined externally.

---

## 🤖 KCD-AI