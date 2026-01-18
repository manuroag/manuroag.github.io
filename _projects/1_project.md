---
layout: page
title: Radius of Gyration of Proteins
description: This repository contains data and Jupyter notebooks to compute and visualize the radius of gyration (Rg) of protein structures.
img: assets/img/rg_1ecz.png
importance: 1
category: work
related_publications: false
---

# Radius of Gyration of Proteins

This repository contains data and Jupyter notebooks to **compute and visualize the radius of gyration (Rg)** of protein structures.

The radius of gyration is a fundamental scalar quantity that characterizes the **spatial distribution of mass** in a protein and is widely used in:
- Structural biology
- Polymer physics
- Protein folding and compaction analysis

---

## 📐 What is Radius of Gyration?

For a protein with atomic coordinates $R_i$ and center of mass $R_{CM}$, the radius of gyration is defined as:

$${R_g}^2 = \sum_{i=1}^{N} (R_i - R_{CM} )^2 / N + \frac{3}{5} R^2 $$

It provides a measure of how extended or compact a protein structure is.

---

## 🧬 Visualization Approach

- Protein structure is shown as a **cartoon representation**
- The **center of mass (COM)** is shown as a black sphere
- The radius of gyration is visualized using **radial arrows** extending from the COM
- Arrow length corresponds to the computed **Rg**

This avoids misleading hard boundaries while clearly conveying the scale of Rg.

---

## 🖼️ Example Visualizations

### Example 1: Alpha-Helix Protein Radius of Gyration

![Radius of gyration visualization](assets/img/rg_1ymb.png)

---

### Example 2: Beta-Sheet Protein Radius of Gyration

![Radius of gyration visualization 2](assets/img/rg_1ecz.png)


---