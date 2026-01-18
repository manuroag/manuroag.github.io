---
layout: page
title: "Drug Hunter: AI-driven Binding Affinity Prediction"
description: A Geometric Deep Learning pipeline predicting drug-target binding affinity ($K_d$) using Graph Neural Networks (GNNs).
img: assets/img/drug_hunter.png
importance: 2
category: independent
related_publications: false
---

## 🚧 Status: In Development

This project is currently being finalized. The repository will utilize **PyTorch Geometric** and the **Therapeutics Data Commons (TDC)**.

**Coming soon:** A live Streamlit dashboard for real-time inference.
<a href="https://github.com/manuroag">Follow my GitHub for the release</a>.

---

**Drug Hunter** is an AI-driven framework designed to predict the binding strength between a potential drug molecule and a target protein. Unlike traditional physics-based docking, this project treats chemistry as a data science problem, leveraging **Geometric Deep Learning** to handle non-Euclidean molecular data.

**Key Objectives:**
- **Input:** Drug SMILES string (e.g., Aspirin: `CC(=O)OC1=CC=CC=C1C(=O)O`)
- **Task:** Regression Analysis on graph-structured data
- **Output:** Predicted Binding Affinity ($pK_d$ or $IC_{50}$)

---

## 🕸️ From Chemistry to Graphs

The core challenge in AI drug discovery is representing molecules in a way computers can understand. We strictly avoid "flat" features (like molecular weight) and instead preserve the **topological structure** of the molecule.

Using `rdkit`, we convert raw SMILES strings into **Graph Objects**:
- **Nodes ($V$):** Represent atoms (Carbon, Oxygen, Nitrogen).
- **Edges ($E$):** Represent chemical bonds (Single, Double, Aromatic).

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/drug_hunter.png" title="Radius of gyration visualization" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Credit: <a href='https://www.researchgate.net/figure/Modelling-a-molecule-as-a-graph-Individual-atoms-and-ring-structures-are-mapped-to_fig1_330845050'>Hernandez, Maritza, et al.</a>
</div>

This allows the model to learn spatial and connectivity patterns that drive chemical reactivity.

---

## 🧠 The Architecture: Dual-Encoder

The model uses a **Dual-Encoder Strategy** to process the two distinct data modalities involved in drug binding:

1.  **Ligand Encoder (GNN):** A Message Passing Neural Network (MPNN) or Graph Attention Network (GAT) processes the drug molecule graph.
2.  **Protein Encoder (1D-CNN):** A Convolutional Neural Network processes the amino acid sequence of the target protein.

$$\hat{y} = \text{MLP}( \text{Concat}( \mathbf{h}_{drug}, \mathbf{h}_{protein} ) )$$

Where $\mathbf{h}_{drug}$ is the learned graph embedding and $\mathbf{h}_{protein}$ is the sequence embedding. The final output is the predicted dissociation constant ($K_d$).

---

## 📊 Interactive Visualization

A key feature of this project is the **"Data Science Twist"**, moving beyond static error metrics (MSE) to interactive usability.

---
