---
layout: page
title: "AI-driven Prediction of Circular Dichroism Spectra of Proteins"
description: My M.Sc. Thesis Overview.
img: assets/img/thesis.png
importance: 1
category: independent
related_publications: false
---

📓 See the [full Thesis here](/assets/pdf/MScThesis_JoseManuelRoblesAguilar.pdf).

---

## What is Circular Dichroism (CD)?

An important property of the amino acids that compose proteins is chirality. A molecule is chiral when it is not superimposable on its mirror image (**Fig. 1**). Chirality in amino acids arises from the presence of an asymmetric carbon, a carbon atom tetrahedrally bonded to four different atoms or groups. Glycine, which has a hydrogen atom as its side chain, is the only achiral amino acid.

Chiral structures can be distinguished and characterized by Circular Dichroism (CD) spectroscopy, a technique based on measuring the differential absorption of left- and right-circularly polarized light. For proteins, CD occurs in the near and far ultraviolet (UV) wavelength ranges, where the amide and carbonyl groups of the polypeptide backbone absorb light.

Circular Dichroism (CD) spectroscopy is a versatile and rapid method for characterizing the secondary structure (**Fig. 1**), conformation, and folding of proteins. While not a high-resolution technique, it is invaluable for analyzing protein-ligand interactions, validating computationally predicted structures, and assessing the effects of mutations.

<figure class="text-center">
  <img src="/assets/img/thesis.png" 
       class="img-fluid rounded"
       style="width: 100%; max-width: 580px;" 
       alt="CD Spectroscopy">
</figure>
<div class="caption">
    <strong>Fig. 1.</strong> Example of the chiral amino acid Alanine and the characteristic far-UV CD spectra of different protein architectures which exhibit characteristic spectral shapes.
    [Credit: <a href='https://commons.wikimedia.org/w/index.php?curid=139489607
'>Wikipedia</a> & <a href='https://doi.org/10.1007/978-1-0716-0892-0_11'>Micsonai A, et al.</a>]
</div>

---

## Why Predict CD Spectra?

Computational prediction of CD spectra is particularly useful for comparing two proteins when the high-resolution structure of one protein (determined by methods such as X-ray diffraction, cryo-EM, or NMR) or a predicted structure (e.g., from AlphaFold or similar tools) is available, but only the CD spectrum of the second protein is known. These comparisons serve various purposes, including validating structural similarity (homology), assessing the folding of mutated proteins, observing the effects of ligand binding, or environmental factors on protein conformation, and determining whether modeled (or predicted) structures have CD spectra similar to experimental spectra (**Fig. 2**).

<figure class="text-center">
  <img src="/assets/img/validation.png" 
       class="img-fluid rounded"
       style="width: 100%; max-width: 500px;" 
       alt="CD model validation">
</figure>
<div class="caption">
    <strong>Fig. 2. Validation example using KCD-AI.</strong> CD spectra for protein 1K6J (NmrA), which has a large missing loop (indicated by the orange-circled region in the structure). The experimental spectrum (Exp, red circles) is compared with the KCD-AI prediction from the original, incomplete structure (Orig, dotted gray line) and with predictions from three computationally-completed models: Modeller (Mod, blue line), AlphaFold3 (AF3, green line), and I-Tasser (I-Ta, solid gray line).
</div>

---

## The Knowledge-based Circular Dichroism (KCD) method

The Knowledge-based Circular Dichroism (KCD) method utilizes a model based on the classical theory of optical activity with a complex set of atomic polarizabilities, **α**, to predict far-UV CD spectra, which corresponds to the imaginary part of the equation:

$$[o_p] = - \sum_{a,a'} \alpha_{ap} \alpha_{a'p} \langle C_{aa'}^{p} G_{aa'}^{p} \rangle_{\Omega}$$ 

where

$$\alpha_{ap} = \sum_b c_{bp} \alpha_{ab}.$$

The weight constants, _**c**_, in this equation, are determined by the rule of proximity:

$$c_{bp} = 100\exp{\left( \frac{-50[|s_{\alpha b} - s_{\alpha p}| + |s_{\beta b} - s_{\beta p}| + |s_{cb} - s_{cp}| + |s_{ob} - s_{op}|]}{\tau} \right)}$$ 

This rule have led to the KCD model’s notable accuracy. However, this accuracy can be further enhanced by identifying a more effective method for determining these weight constants, thereby yielding more precise atomic polarizabilities. Deep neural networks are a powerful machine learning approach that excel at discovering intricate relationships within data. By mimicking the learning processes found in biological organisms, they are ideally suited to find a new rule that could provide better weight constants for the KCD model.

---

## Bayesian Neural Networks (BNN)

The effectiveness of a neural network heavily depends on matching its architecture to the structure and characteristics of the input data. A domain-specific understanding of the data is therefore crucial for designing or selecting an appropriate specialized neural architecture.

In this work, the input features that determine the weight constants for atomic polarizabilities are represented as feature vectors lacking any inherent spatial or temporal dependencies. Therefore, our data is fundamentally tabular, a structure that can be effectively addressed by Bayesian Neural Networks (BNN), which will form the basis of the networks implemented in this study.

<figure class="text-center">
  <img src="/assets/img/BNN.png" 
       class="img-fluid rounded"
       style="width: 100%; max-width: 600px;" 
       alt="BNN">
</figure>
<div class="caption">
    <strong>Fig. 3. (a) Point estimate neural network and (b) Bayesian neural network with a probability distribution over the weights.</strong> Bayesian Neural Networks (BNNs) are stochastic neural networks that leverage Bayesian inference. Instead of learning a single set of optimal weights, BNNs treat the weights, θ, as random variables with associated probability distributions, p(θ). This process simulates an ensemble of multiple possible models. Just as an ensemble of independent, average-performing predictors can outperform a single well-performing model, BNNs provide robust predictions and, crucially, quantify the model’s inherent uncertainty.
    [Credit: <a href='https://arxiv.org/pdf/2007.06823'>Jospin, L. et al.</a>]
</div>


---

## KCD-AI

To handle the complexity of predicting 125 weight constants from only 4 feature inputs (secondary structure content), we designed a ”divide-and-conquer” architecture. Instead of one large Bayesian Neural Network (BNN) predicting all 125 weight constants, we trained four smaller, specialized BNNs.

Once the four Bayesian Neural Networks are trained, they are integrated into the KCD model to function as a single prediction engine. When a new protein _p_ is entered for analysis, its four secondary structure features are fed as input to all four BNNs simultaneously.

Each BNN then predicts its own disjoint subset of the weight constants. These four partial outputs are concatenated, reassembling the complete 125-dimensional vector of predicted weight constants. This final vector is then used by the KCD model to perform the usual computations and calculate the protein’s CD spectrum. This complete workflow is illustrated in **Figure 4**, and is referred to as KCD-AI.

<figure class="text-center">
  <img src="/assets/img/KCD_AI.png" 
       class="img-fluid rounded"
       style="width: 100%; max-width: 680px;" 
       alt="KCD AI Model">
</figure>
<div class="caption">
    <strong>Fig. 4. Conceptual workflow of the KCD-AI integration.</strong> (1) The secondary structure content of a protein (top left) is provided as input. (2) This is fed into the deep neural network framework (top right), which is represented here as a single block but conceptually consists of the four BNNs. (3) The BNNs output the 125 predicted weight constants. (4) The KCD model uses these constants to calculate the final CD spectrum (bottom left), which is then compared to the experimental spectrum.
</div>

---

## Impact on KCD Predictions

##### KCD-AI vs The Original KCD

We first evaluated the model on a test set of 50 proteins, comparing the performance of KCD-AI and KCD (**Fig. 5**). We computed the average NAD for KCD as 0.25 ± 0.21 and for KCD-AI as 0.15 ± 0.14. This represents a 40% reduction in the average prediction error.

Additionally, the KCD-AI model provides a mean NAD and standard deviation for each protein, quantifying the reliability of its prediction. We note that proteins lacking significant α-helix content remain the most problematic, a common challenge for CD prediction models. However, KCD-AI successfully reduced the NAD for the majority of proteins compared to the original KCD.

<figure class="text-center">
  <img src="/assets/img/KCDAIvsKCD.png" 
       class="img-fluid rounded"
       style="width: 100%; max-width: 500px;" 
       alt="KCD AI vs KCD">
</figure>
<div class="caption">
    <strong>Fig. 5. Comparison of the Normalized Absolute Deviation (NAD) for CD spectra predictions per protein in the test set between KCD-AI and KCD, plotted as a function of protein α-helix content (%).</strong> The results for the KCD-AI model are shown as blue circles (mean) with their corresponding standard deviations (error bars). The results for the original KCD method are shown as sienna stars. The solid lines indicate the average NAD for each method: KCD-AI (blue, 0.15 ± 0.14) and KCD (sienna, 0.25 ± 0.21). The y-axis is on a logarithmic scale.
</div>

##### KCD-AI vs State-of-The-Art Methods

In addition to comparing KCD-AI with the original KCD, we benchmarked it against several state-of-the-art CD spectra prediction tools: PDBMD2CD, SESCA, and DichroCalc. We computed the NAD for predictions from all methods across the 50-protein test set (**Fig. 6**). The analysis found the following average NAD values:
- **KCD-AI:** 0.15 ± 0.14
- **PDBMD2CD (P2CD):** 0.25 ± 0.24
- **SESCA:** 0.28 ± 0.21
- **DichroCalc (DC):** 0.49 ± 0.40

KCD-AI demonstrated superior accuracy, achieving the lowest average prediction error on the test set.

<figure class="text-center">
  <img src="/assets/img/KCDAIvsOthers.png" 
       class="img-fluid rounded"
       style="width: 100%; max-width: 500px;" 
       alt="KCD AI vs Others">
</figure>
<div class="caption">
    <strong>Fig. 6. Comparison of the Normalized Absolute Deviation (NAD) for CD spectra predictions per protein in the test set between KCD-AI and other methods, plotted as a function of protein α-helix content (%).</strong> The plot compares the performance of KCD-AI with three other state-of-the-art methods. KCD-AI results are shown as blue circles. PDBMD2CD (PDB2CD) results are shown as red squares. SESCA results are shown as green, upward-pointing triangles. DichroCalc (DC) results are shown as orange, downward-pointing triangles. The solid lines indicate the average NAD for each method: KCD-AI (blue, 0.15 ± 0.14), PDB2CD (red, 0.25 ± 0.24), SESCA (green, 0.28 ± 0.21), and DC (orange, 0.49 ± 0.40). The y-axis is on a logarithmic scale.
</div>

##### CD Spectra Predictions for Complex Cases

In **Figure 7**, we show predictions for four representative proteins from the test set known to be challenging for CD prediction. Their secondary structure compositions are as follows:
- **1SR5 (Antithrombin):** ∼16% α-helix, ∼26% β-sheet, ∼20% coil
- **3QTK (VEGF-A):** ∼8% α-helix, ∼56% β-sheet, ∼16% coil
- **5A37 (α-Actin-2):** ∼44% α-helix, ∼2% β-sheet, ∼26% coil
- **3GO0 (α-Defensin):** ∼0% α-helix, ∼53% β-sheet, ∼17% coil

The protein 3GO0 is a particularly difficult case as it is composed entirely of D-amino acids. As shown in the figure, KCD-AI consistently provides superior performance, accurately predicting the spectra for these complex proteins. Notably, it is the only method to successfully predict the spectrum for the all-D-amino-acid protein, a case where all other benchmarked methods fail.

<figure class="text-center">
  <img src="/assets/img/Results.png" 
       class="img-fluid rounded"
       style="width: 100%; max-width: 600px;" 
       alt="KCD AI vs Others">
</figure>
<div class="caption">
    <strong>Fig. 7. Comparison of predicted vs. experimental CD spectra for four proteins from the test set.</strong> 1SR5 (Antithrombin), 3QTK (VEGF-A), 5A37 (α-Actin-2), and the all-D-amino-acid protein 3GO0 (α-Defensin). Each panel plots the molar ellipticity per residue ([θ]/Nr) as a function of wavelength (λ). The experimental SRCD spectrum (Exp, red circles) is compared against four prediction methods: KCD-AI (solid blue line), PDBMD2CD (P2CD, solid thick gray line), SESCA (solid thin gray line), and DichroCalc (DC, dotted gray line).
</div>

---

## Conclusions

- We have successfully developed KCD-AI, the first model to integrate deep learning into the KCD framework. This refined computational model offers a powerful new tool for the structural characterization of proteins, improving predictive accuracy on average by 40% with respect to the original KCD.

- A key methodological advance of KCD-AI is its use of Bayesian Neural Networks, which provide a quantitative measure of uncertainty (i.e., a standard deviation) for each prediction. This allows researchers to not only see the predicted spectrum but also to assess the model’s "confidence", a feature absent in the original KCD and other deterministic methods.

- While KCD-AI demonstrated significant improvement on average, its performance was not uniform. For a small subset of proteins, its predictive accuracy was comparable to the original KCD, and in a few isolated cases, its predictions were less accurate than the original method.

- This highlights key areas for future research. First, a detailed analysis of these challenging cases is required to further refine the model. Second, expanding the training dataset is key to unlocking the full predictive power of our deep learning architecture. Finally, this work also served to identify fundamental limitations in the original KCD model itself. Addressing these underlying limitations will be crucial for building a stronger foundation for all future enhancements of the KCD method, including KCD-AI.