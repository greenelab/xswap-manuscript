---
author-meta:
- John Doe
- Daniel S. Himmelstein
date-meta: '2019-08-01'
keywords:
- markdown
- publishing
- manubot
lang: en-US
title: 'Manubot Rootstock: Manuscript Title'
...






<small><em>
This manuscript
([permalink](https://greenelab.github.io/xswap-manuscript/v/b396a35d45ba534812a06011e3982021d6ef2ca0/))
was automatically generated
from [greenelab/xswap-manuscript@b396a35](https://github.com/greenelab/xswap-manuscript/tree/b396a35d45ba534812a06011e3982021d6ef2ca0)
on August 1, 2019.
</em></small>

## Authors



+ **John Doe**<br>
    ![ORCID icon](images/orcid.svg){height="13px" width="13px"}
    [XXXX-XXXX-XXXX-XXXX](https://orcid.org/XXXX-XXXX-XXXX-XXXX)
    · ![GitHub icon](images/github.svg){height="13px" width="13px"}
    [johndoe](https://github.com/johndoe)
    · ![Twitter icon](images/twitter.svg){height="13px" width="13px"}
    [johndoe](https://twitter.com/johndoe)<br>
  <small>
     Department of Something, University of Whatever
     · Funded by Grant XXXXXXXX
  </small>

+ **Daniel S. Himmelstein**<br>
    ![ORCID icon](images/orcid.svg){height="13px" width="13px"}
    [0000-0002-3012-7446](https://orcid.org/0000-0002-3012-7446)
    · ![GitHub icon](images/github.svg){height="13px" width="13px"}
    [dhimmel](https://github.com/dhimmel)
    · ![Twitter icon](images/twitter.svg){height="13px" width="13px"}
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
