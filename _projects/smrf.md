---
title: "SMRF: Statistical-genomics Mixed Random Forest"
date: 2026-09-06
layout: post
excerpt: "A machine-learning framework for genome-wide genotype–phenotype analysis."
---

**SMRF** stands for **Statistical-genomics Mixed Random Forest**.

SMRF is a machine-learning framework for analyzing genome-wide marker data while accounting for genetic relatedness among individuals. The method combines a mixed-model adjustment with a random forest trained on relatedness-adjusted trait values.

This project provides code, documentation, and a Quarto-based workflow for running SMRF on genome-wide genotype–phenotype data.

### Project links

- [SMRF tutorial website](https://talissafloriani.github.io/SMRF/)
- [GitHub repository](https://github.com/talissafloriani/SMRF)

### Main components

- Mixed-model adjustment for genetic relatedness
- Random forest modeling on adjusted residuals
- Marker-level feature importance
- Residual permutation testing
- Genome-Wide Feature Importance visualization

### Why this project matters

Many genome-wide analyses in crop species rely on single-marker additive models. These approaches are useful for detecting loci with additive effects, but they can be less flexible for genetic architectures involving rare variants, dominance, epistasis, or multi-locus signal.

SMRF was developed as a complementary machine-learning approach for genome-wide marker data. Instead of testing one marker at a time, SMRF uses tree-based partitioning across genome-wide SNPs after accounting for relatedness among individuals.

### Data availability

The GitHub repository stores the SMRF code, documentation, and small example files.
