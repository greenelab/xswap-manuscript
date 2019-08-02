---
author-meta:
- Michael Zietz
- Daniel S. Himmelstein
date-meta: '2019-08-02'
keywords:
- xswap
- permutation
- network
- hetnets
- degree
- bioinformatics
- python
- manubot
lang: en-US
title: 'The probability of edge existence due to node degree: a baseline for network-based
  predictions'
...






<small><em>
This manuscript
([permalink](https://greenelab.github.io/xswap-manuscript/v/b04d8d2c6d9e26093e0c413b9b4cd0ce9d08ba33/))
was automatically generated
from [greenelab/xswap-manuscript@b04d8d2](https://github.com/greenelab/xswap-manuscript/tree/b04d8d2c6d9e26093e0c413b9b4cd0ce9d08ba33)
on August 2, 2019.
</em></small>

## Authors



+ **Michael Zietz**<br>
    ![ORCID icon](images/orcid.svg){.inline_icon}
    [0000-0003-0539-630X](https://orcid.org/0000-0003-0539-630X)
    · ![GitHub icon](images/github.svg){.inline_icon}
    [zietzm](https://github.com/zietzm)
    · ![Twitter icon](images/twitter.svg){.inline_icon}
    [ZietzMichael](https://twitter.com/ZietzMichael)<br>
  <small>
     Department of Physics & Astronomy, University of Pennsylvania, Philadelphia, Pennsylvania, United States of America; Department of Systems Pharmacology and Translational Therapeutics, University of Pennsylvania, Philadelphia, Pennsylvania, United States of America
     · Funded by ['Roy and Diana Vagelos Scholars Program in the Molecular Life Sciences', 'GBMF4552']
  </small>

+ **Daniel S. Himmelstein**<br>
    ![ORCID icon](images/orcid.svg){.inline_icon}
    [0000-0002-3012-7446](https://orcid.org/0000-0002-3012-7446)
    · ![GitHub icon](images/github.svg){.inline_icon}
    [dhimmel](https://github.com/dhimmel)
    · ![Twitter icon](images/twitter.svg){.inline_icon}
    [dhimmel](https://twitter.com/dhimmel)<br>
  <small>
     Department of Systems Pharmacology and Translational Therapeutics, University of Pennsylvania, Philadelphia, Pennsylvania, United States of America
     · Funded by Pfizer Worldwide Research and Development; GBMF4552
  </small>



## Abstract {.page_break_before}

Networks of biomedical data rarely consist of all true relationships.
Instead, networks contain spurious relationships while omitting actual relationships.
How a network deviates from the real set of relationships is often biased according to node degree, resulting from processes such as inspection bias and experimental methods.
While degree is subject to potentially substantial biases, link prediction methods can be strongly affected by degree.
In the present work, we introduce a network permutation framework to quantify the effect of node degree on network-based methods and prediction tasks.
We introduce the "edge prior" to quantify the probability that two nodes are connected based only on their degree.
After demonstrating that this prior feature shows excellent discrimination and calibration performance for 20 different biomedical networks (16 bipartite, 3 undirected, 1 directed), we conclude that our prior feature represents a suitable baseline for network link prediction tasks, as performance exceeding the baseline is attributable to factors other than degree alone.
Additionally, we propose methods to incorporate network permutation and the edge prior into other predictive methods.
Our results highlight the importance of degree for link prediction and provide a way to account for its effects when degree bias may be present.
We have released a full implementation of our network permutation method and the edge prior as an open-source Python package on GitHub.


## Introduction

### Node degree

### Edge prediction

### Feature-degree correlation


## Methods

### Network permutation

### XSwap algorithm

### Edge prior

### Edge prior approximation

### Prediction tasks

### Degree-grouping

### Implementation and source code


## Results


## Discussion


## Conclusion


## References {.page_break_before}

<!-- Explicitly insert bibliography here -->
<div id="refs"></div>
