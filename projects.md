---
layout: default
title: "Projects"
permalink: /projects/
---

# Projects

## SMRF: Statistical-genomics Mixed Random Forest

**SMRF** is a machine-learning framework for analyzing genome-wide marker data while accounting for genetic relatedness among individuals.

The method combines an intercept-only linear mixed model adjustment with a random forest trained on relatedness-adjusted trait values. The main marker-level output is feature importance, which is used to prioritize genomic regions across the genome.

### Links

- [SMRF tutorial website](https://talissafloriani.github.io/SMRF/)
- [GitHub repository](https://github.com/talissafloriani/SMRF)

### Main components

- Mixed-model adjustment for genetic relatedness
- Random forest modeling on adjusted residuals
- Marker-level feature importance
- Residual permutation testing
- Genome-Wide Feature Importance visualization

Large cassava and maize/Ames datasets associated with the manuscript are archived separately and are not stored directly in the GitHub repository.
