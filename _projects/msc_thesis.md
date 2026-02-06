---
layout: page
title: "AI-driven Prediction of Circular Dichroism Spectra of Proteins"
description: My M.Sc. Thesis.
img: assets/img/thesis.png
importance: 1
category: independent
related_publications: false
---

📓 See the [full Thesis here](/assets/pdf/MScThesis_JoseManuelRoblesAguilar.pdf).

---

## Circular Dichroism (CD)

An important property of the amino acids that compose proteins is chirality. A molecule is chiral when it is not superimposable on its mirror image (**Fig. 1**). Chirality in amino acids arises from the presence of an asymmetric carbon, a carbon atom tetrahedrally bonded to four different atoms or groups. Glycine, which has a hydrogen atom as its side chain, is the only achiral amino acid.

Chiral structures can be distinguished and characterized by Circular Dichroism (CD) spectroscopy, a technique based on measuring the differential absorption of left- and right-circularly polarized light. For proteins, CD occurs in the near and far ultraviolet (UV) wavelength ranges, where the amide and carbonyl groups of the polypeptide backbone absorb light.

Circular Dichroism (CD) spectroscopy is a versatile and rapid method for characterizing the secondary structure (**Fig. 1**), conformation, and folding of proteins. While not a high-resolution technique, it is invaluable for analyzing protein-ligand interactions, validating computationally predicted structures, and assessing the effects of mutations.

<figure class="text-center">
  <img src="/assets/img/thesis.png" 
       class="img-fluid rounded"
       style="width: 100%; max-width: 600px;" 
       alt="CD Spectroscopy">
</figure>
<div class="caption">
    <strong>Fig. 1.</strong> Example of the chiral amino acid Alanine and the characteristic far-UV CD spectra of different protein architectures which exhibit characteristic spectral shapes.
    [Credit: <a href='https://commons.wikimedia.org/w/index.php?curid=139489607
'>Wikipedia</a> & <a href='https://doi.org/10.1007/978-1-0716-0892-0_11'>Micsonai A, et al.</a>]
</div>

---

## Why to Predict CD Spectra?

Computational prediction of CD spectra is particularly useful for comparing two proteins when the high-resolution structure of one protein (determined by methods such as X-ray diffraction, cryo-EM, or NMR) or a predicted structure (e.g., from AlphaFold or similar tools) is available, but only the CD spectrum of the second protein is known. These comparisons serve various purposes, including validating structural similarity (homology), assessing the folding of mutated proteins, observing the effects of ligand binding, or environmental factors on protein conformation, and determining whether modeled (or predicted) structures have CD spectra similar to experimental spectra (**Fig. 2**).

<figure class="text-center">
  <img src="/assets/img/validation.png" 
       class="img-fluid rounded"
       style="width: 100%; max-width: 500px;" 
       alt="CD model validation">
</figure>
<div class="caption">
    <strong>Fig. 2.</strong> Validation example using KCD-AI: CD spectra for protein 1K6J (NmrA), which has a large missing loop (indicated by the orange-circled region in the structure). The experimental spectrum (Exp, red circles) is compared with the KCD-AI prediction from the original, incomplete structure (Orig, dotted gray line) and with predictions from three computationally-completed models: Modeller (Mod, blue line), AlphaFold3 (AF3, green line), and I-Tasser (I-Ta, solid gray line).
</div>

---

## The Knowledge-based Circular Dichroism (KCD) method

The Knowledge-based Circular Dichroism (KCD) server utilizes a model based on the classical theory of optical activity with a complex set of atomic polarizabilities. These polarizabilities are obtained from a base of SRCD spectra and PDB structures from the PCDDB to predict far-UV CD spectra from the three-dimensional structural information of a target protein. This information includes the secondary structure content provided by the Structural Identification (STRIDE) algorithm and the atoms belonging to D-amino acid residues. The KCD server accepts a PDB file of the target protein as input and an optional spectrum file for normalization and comparison, which should be a simple two-column ASCII file (.dat or similar). The user is also required to provide their name and email address. The results are sent to the user via email and include a plot of the experimental and predicted spectra superimposed, a bar graph with the percentage content of secondary structures (alpha, beta, coils, and others) and D-residues, and the ASCII data file of the predicted spectrum.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/KCD.png" title="KCD" class="img-fluid rounded" %}
    </div>
</div>
<div class="caption">
    <strong>Fig. 3.</strong> Workflow of the KCD server.
    [Credit: <a href='https://doi.org/10.1002/slct.202300408'>Takashi Misawa, Yokuse Demizu.</a> & <a href='https://doi.org/10.1002/pro.4967'>Jacinto Méndez, D. et al.</a>]
</div>

The KCD model predicts circular dichroism (CD) spectra by calculating suitable atomic polarizabilities using:

$$[o_p] = - \sum_{a,a'} \alpha_{ap} \alpha_{a'p} \langle C_{aa'}^{p} G_{aa'}^{p} \rangle_{\Omega}$$ 

where

$$\alpha_{ap} = \sum_b c_{bp} \alpha_{ab}.$$

The weight constants in this equation, are determined by the rule of proximity:

$$c_{bp} = 100\exp{\left( \frac{-50[|s_{\alpha b} - s_{\alpha p}| + |s_{\beta b} - s_{\beta p}| + |s_{cb} - s_{cp}| + |s_{ob} - s_{op}|]}{\tau} \right)}$$ 

This rule have led to the KCD model’s notable accuracy. However, this accuracy can be further enhanced by identifying a more effective method for determining these weight constants, thereby yielding more precise atomic polarizabilities. Deep neural networks are a powerful machine learning approach that excel at discovering intricate relationships within data. By mimicking the learning processes found in biological organisms, they are ideally suited to find a new rule that could provide better weight constants for the KCD model.

The effectiveness of a neural network heavily depends on matching its architecture to the structure and characteristics of the input data. A domain-specific understanding of the data is therefore crucial for designing or selecting an appropriate specialized neural architecture.

In this work, the input features that determine the weight constants for atomic polarizabilities are represented as feature vectors lacking any inherent spatial or temporal dependencies. Therefore, our data is fundamentally tabular, a structure that can be effectively addressed by Bayesian Neural Networks (BNN), which will form the basis of the networks implemented in this study

---

## KCD-AI

To handle the complexity of predicting 125 weight constants from only 4 feature inputs (secondary structure content), we designed a ”divide-and-conquer” architecture. Instead of one large Bayesian Neural Network (BNN) predicting all 125 weight constants, we trained four smaller, specialized BNNs.

Once the four Bayesian Neural Networks are trained, they are integrated into the KCD model to function as a single prediction engine. When a new protein _p_ is entered for analysis, its four secondary structure features are fed as input to all four BNNs simultaneously.

Each BNN then predicts its own disjoint subset of the weight constants. These four partial outputs are concatenated, reassembling the complete 125-dimensional vector of predicted weight constants. This final vector is then used by the KCD model to perform the usual computations and calculate the protein’s CD spectrum. This complete workflow is illustrated in **Fig. 4.**, and is referred to as KCD-AI.

<figure class="text-center">
  <img src="/assets/img/KCD_AI.png" 
       class="img-fluid rounded"
       style="width: 100%; max-width: 680px;" 
       alt="KCD AI Model">
</figure>
<div class="caption">
    <strong>Fig. 4.</strong> Conceptual workflow of the KCD-AI integration. (1) The secondary structure content of a protein (top left) is provided as input. (2) This is fed into the deep neural network framework (top right), which is represented here as a single block but conceptually consists of the four BNNs. (3) The BNNs output the 125 predicted weight constants. (4) The KCD model uses these constants to calculate the final CD spectrum (bottom left), which is then compared to the experimental spectrum.
</div>

---

## Impact on KCD Predictions

We first evaluated the model on a test set of 50 proteins, comparing the performance of KCD-AI and KCD (**Fig. 5**). We computed the average NAD for KCD as 0.25±0.21 and for KCD-AI as 0.15±0.14. This represents a 40% reduction in the average prediction error.

Additionally, the KCD-AI model provides a mean NAD and standard deviation for each protein, quantifying the reliability of its prediction. We note that proteins lacking significant α-helix content remain the most problematic, a common challenge for CD prediction models. However, KCD-AI successfully reduced the NAD for the majority of proteins compared to the original KCD.



In addition to comparing KCD-AI with the original KCD, we benchmarked it against several state-of-the-art CD spectra prediction tools: PDBMD2CD, SESCA, and DichroCalc. We computed the NAD for predictions from all methods across the 50-protein test set (**Fig. 6**). The analysis found the following average NAD values:
- KCD-AI: 0.15±0.14
- PDBMD2CD (P2CD): 0.25±0.24
- SESCA: 0.28±0.21
- DichroCalc (DC): 0.49 ± 0.40
KCD-AI demonstrated superior accuracy, achieving the lowest average prediction error on the test set.