---
author-meta:
- Michael Zietz
- Daniel S. Himmelstein
- Christopher Williams
- Michael W. Nagle
- Casey S. Greene
date-meta: '2019-08-13'
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
([permalink](https://greenelab.github.io/xswap-manuscript/v/e198478ed9882f653422698c020a5d6920aa675a/))
was automatically generated
from [greenelab/xswap-manuscript@e198478](https://github.com/greenelab/xswap-manuscript/tree/e198478ed9882f653422698c020a5d6920aa675a)
on August 13, 2019.
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
     · Funded by ['Roy and Diana Vagelos Scholars Program in the Molecular Life Sciences', 'the Gordon and Betty Moore Foundation (GBMF4552)']
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
     · Funded by Pfizer Worldwide Research, Development, and Medical; the Gordon and Betty Moore Foundation (GBMF4552)
  </small>

+ **Christopher Williams**<br>
    · ![GitHub icon](images/github.svg){.inline_icon}
    [chrsunwil](https://github.com/chrsunwil)<br>
  <small>
     Department of Systems Pharmacology and Translational Therapeutics, University of Pennsylvania, Philadelphia, Pennsylvania, United States of America
  </small>

+ **Michael W. Nagle**<br>
    ![ORCID icon](images/orcid.svg){.inline_icon}
    [0000-0002-4677-7582](https://orcid.org/0000-0002-4677-7582)
    · ![GitHub icon](images/github.svg){.inline_icon}
    [naglem](https://github.com/naglem)
    · ![Twitter icon](images/twitter.svg){.inline_icon}
    [MikeNagle84](https://twitter.com/MikeNagle84)<br>
  <small>
     Internal Medicine Research Unit, Pfizer Worldwide Research, Development, and Medical
  </small>

+ **Casey S. Greene**<br>
    ![ORCID icon](images/orcid.svg){.inline_icon}
    [0000-0001-8713-9213](https://orcid.org/0000-0001-8713-9213)
    · ![GitHub icon](images/github.svg){.inline_icon}
    [cgreene](https://github.com/cgreene)
    · ![Twitter icon](images/twitter.svg){.inline_icon}
    [greenescientist](https://twitter.com/greenescientist)<br>
  <small>
     Department of Systems Pharmacology and Translational Therapeutics, University of Pennsylvania, Philadelphia, Pennsylvania, United States of America
     · Funded by ['Pfizer Worldwide Research, Development, and Medical', 'the Gordon and Betty Moore Foundation (GBMF4552)', 'the National Institutes of Health (R01 HG010067)']
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

Networks contain information about relationships between entities ("edges between nodes").
A node's degree is the number of relationships it has in the network.
Networks contain many nodes, whose degrees can be aggregated to form the network's degree distribution.
Because different nodes can have very different degrees, real networks have highly variable degree distributions (Figure {@fig:hetionet}).

![Degree distribution can vary greatly between networks, even between the source and target degree distributions within the same (directed or bipartite) network.
  Shown are seven degree distributions for six edge type subnetworks of Hetionet [@O21tn8vf].
  (The final two are the source and target distributions of the gene-regulates-gene directed edge type.)
](https://github.com/greenelab/xswap-analysis/raw/5a257c9d28e0a4c3cc8f2fd8493f27ff4652f2c6/img/hetionet_degrees.png){#fig:hetionet width="100%"}

Degree is an important metric for differentiating between nodes, and it appears in many common edge prediction features [@ohIv6zMA].
However, reliance on degree can pose problems for edge prediction.
Firstly, bias in the data can distort node degree so that degree differences between two nodes may not be meaningful.
Secondly, reliance on degree can lead edge prediction methods to make nonspecific or trivial predictions and fail to identify novel or insightful relationships.

Most biomedical data networks are imperfect representations of the true set of relationships.
Real networks often mistakenly include edges that do not exist and exclude edges that do exist.
How well a network represents the true relationships it attempts to represent depends on a number of factors, especially the methods used to generate the data in the network [@bo2VEmIz; @yJZSr6c6; @C4FHCVCz].
We define "degree bias" as the type of misrepresentation that occurs when the fraction of incorrectly existent/nonexistent relationships depends on the number of connections that nodes make (their "degrees").
Depending on the type of data being represented, degree biases can arise due to experimental methods, inspection bias, or other factors [@bo2VEmIz].

Inspection bias indicates that entities are not uniformly studied [@lnDqu0oW], and it is likely to cause degree bias when networks are constructed using hypothesis-driven findings extracted from the literature, as newly-discovered relationships are not randomly sampled from the set of all true relationships.
For example, the number of publications mentioning a gene has little correlation with its degree in a systematically-derived protein interaction network [Figure 6A in @LCyCrr7W].
Therefore, the high correlation between number of publications and degree in low-throughput interaction networks is almost entirely the result of inspection bias.
This evidence suggests that many poorly studied genes have similar numbers of interactions as the genes scientists have preferentially examined.
The consequence of degree bias is that a difference in degree between two nodes may not reflect a difference in the number of true edges.
Reliance on degree may be unfavorable depending on the prediction/analysis task being conducted and the magnitude of possible degree bias in the data.

Another reason why a method's reliance on degree can be unfavorable is that degree imbalance can lead to prediction nonspecificity.
Nonspecific predictions are made on the basis of generic characteristics rather than the specific connectivity information contained in a network.
For example, Gillis et al. [@zB6RQrIj] examined the concept of prediction specificity in the context of gene function prediction and found that many predictions appear to rely primarily on multifunctionality and could be "potentially misleading with respect to causality."
Real networks have a variety of degree distributions (Figure {@fig:hetionet}), and they commonly exhibit degree imbalance [@GFS9MouO; @hbOjmCsZ; @1mIOnArF].
Degree imbalance leads high-degree nodes to dominate in the predictions made by degree-associated methods [@g059lh8v], which are effective predictors of connections in some biological networks [@1736TBtF6].

Consequently, degree-based predictions are more likely nonspecific, meaning the same set of predictions performs well for different tasks.
However, depending on the prediction task, edge predictions between very high degree nodes may be undesired, uninsightful, or nonspecific.
Model evaluation is challenging in this context, as nonspecific or trivial predictions need not be incorrect, even if they are not the desired outputs of the predictive model.
For example, predicting that the highest degree node in a network shares edges with the remaining nodes to which it is not connected will often lead to many correct predictions, despite the predictions being generic to all nodes in the network.
Degree-based features should often be included in the interpretation of predictions to disentangle desired from non-desired effects and to effectively evaluate and compare predictive models.

Degree is important in edge prediction, but it can cause undesired effects.
We sought to understand the effect of node degree on edge prediction methods.
We introduce a permutation-based framework to find edge existence probabilities due to node degree and to quantify the contribution of degree to edge prediction methods.
This method allows edge predictions to be evaluated in the context of degree and its effects on the prediction task.
Our results demonstrate that degree-associated methods are very effective for reconstructing a network using a subsampled holdout but ineffective for predicting edges between distinct degree distributions.
Using a number of different networks, we provide evidence that degree has a strong effect on the probability of edge existence and that our "edge prior" feature best quantifies this probability.

## Methods

### Network permutation

Network permutation is a way to produce new networks by randomizing the connections of an existing network.
Specialized permutation strategies can be devised that randomize some aspects of networks while retaining other features.
Comparing between permuted and unpermuted networks gives insight to the effects of the retained network features.
For example, an edge prediction method that has superior reconstruction performance on a network compared to its permutations likely relies on information that is eliminated by permutation.
Conversely, identical predictive performance on true and permuted networks indicates that a method relies on information that is preserved during permutation.
Network permutation is a flexible framework for analyzing other methods, because it generates networks with identical formats to the original network.
We propose using network permutation to isolate degree and determine its effects in different contexts.
Degree-preserving network permutation obscures true connections and higher-order connectivity information while retaining node degree, and thereby, the network's degree sequence.
Thanks to the flexibility of permutation, our framework can quantify the effect of degree on any network edge prediction method.

### XSwap algorithm

Hanhijärvi, et al. presented XSwap [@iKOIEzQ9], an algorithm for the randomization ("permutation") of unweighted networks (Figure {@fig:algo}A).
The algorithm picks two existing edges at random, and if the edges constitute a valid swap, exchanges the targets between the edges (Figure {@tbl:xswap}).
This process is repeated many times until the maximum number of steps has been reached.
In general, the maximum number of steps should be chosen to be sufficiently large that the fraction of original edges retained in the permuted network is near its asymptotic value for a large number of steps.

To allow greater flexibility, we modified the algorithm by adding two parameters, "`allow_loops`", and "`allow_antiparallel`" that allow a greater variety of network types to be permuted (Figure {@fig:algo}B).
Specifically, two chosen edges constitute a valid swap if they preserve degree for all four involved nodes and do not violate the above condition options.
The motivation for these generalizations is to make the permutation method applicable both to directed and undirected graphs, as well as to networks with different types of nodes, variously called multipartite, heterogeneous, or multimodal networks.

When permuting bipartite networks, our method ensures that each nodes class membership and with-class degree is preserved.
Similarly, heterogeneous networks should be permuted by considering each edge type as a separate network.
This way, each node retains its within-edge-type degree for all edge types.
We provide documentation for parameter choices depending on the type of network being permuted in the GitHub repository (https://github.com/hetio/xswap).
The original algorithm and our proposed modification are given in Figure {@fig:algo}.

![
  **A.** XSwap algorithm due to Hanhijärvi, et al. [@iKOIEzQ9].
  **B.** Proposed modification to XSwap algorithm](images/xswap_algorithms_combined_labels.png){#fig:algo width="85%"}

| Network type | Degree preserved | Figure | `allow_antiparallel` | `allow_loops` |
| :----------- | :--------------- | :----- | :------------------- | :----------------- |
| simple | all | ![](images/xswap_simple.png){height="85px"} | False | False |
| bipartite | in/out | ![](images/xswap_bipartite.png){height="85px"} | True | True |
| directed | in/out | ![](images/xswap_directed.png){height="85px"} | ? | ? |

Table: Applications of the modified XSwap algorithm to various network types with appropriate parameter choices.
For simple networks, each node's degree is preserved. For bipartite networks, each node's number of connections to the other part is preserved, and overall node class memberships are preserved. For directed networks, each nodes' in- and out-degrees are preserved, though parameter choices depend on the network being permuted. Some directed networks can include antiparallel edges or loops while others do not. {#tbl:xswap}

### Edge prior

We introduce the "edge prior" to quantify the probability that two nodes are connected based only on their degree.
The edge prior can be estimated using the fraction of permuted networks in which a given edge exists---the maximum likelihood estimate for the binomial distribution success probability.
Based only on permuted networks, the edge prior does not contain any information about the true edges in the (unpermuted) network.
The edge prior is a numerical feature that can be computed for every pair of nodes that could potentially share an edge, and we compared its ability to predict edges in three tasks, discussed below.

### Edge prior analytical approximation

We also considered the possibility that the probability of an edge existing across permuted networks could be written as a closed form equation involving the node pair's degree.
A major simplification is the assumption that the probability of an edge existing is independent of all other potential edges.
We were unable to find a closed-form solution giving the edge prior without assuming independence in this way, which we believe is incorrect for XSwap.
Nonetheless, we discovered a good analytical approximation to the edge prior for networks with many nodes and relatively low edge density.

Let $m$ be the total number of edges in the network, and $d(u_i)$, $d(v_j)$ be the source and target degrees of a node pair, respectively.
A good approximation of the edge prior is given by the following:
\begin{equation}
    P_{i,j} = \frac{d(u_i) d(v_j)}{\sqrt{(d(u_i) d(v_j))^2 + (m - d(u_i) - d(v_j) + 1)^2}}
\end{equation}

Further discussion of this approximate edge prior and an derivation are available in [the supplement](#approx-prior-supp).

### Prediction tasks

### Degree-grouping

Our method for degree-preserving permutation produces randomized networks that share few of their edges with the original network.
The feature values for two node pairs with the same source and target degree are drawn from the same distribution in permuted networks, so nodes with equal degree can be grouped when summarizing features.
We used this to augment each node pair's feature values in permuted networks, which allowed these pairs to have more permuted feature values than permuted networks.
Degree grouping greatly increased the effective number of permutations for nodes with frequently observed degrees [@DwbABa00].
We used degree grouping throughout our analyses.

### Implementation and source code

We implemented the modified XSwap algorithm as a Python package, with the actual edge swap mechanism implemented in C++ for greater speed.
In addition to functions that permute networks (represented as edge lists), the package contains utilities for computing the edge prior, converting a network between adjacency matrix and edge list formats, and for assigning unique identifiers to nodes.
The Python package is available on the Python Packaging Index under the name "xswap".
The full source code for our method of degree-preserving network permutation has also been made freely available ([https://github.com/hetio/xswap](https://github.com/hetio/xswap)), as has the code for the analysis, figure generation ([https://github.com/greenelab/xswap-analysis](https://github.com/greenelab/xswap-analysis)), and manuscript ([https://github.com/greenelab/xswap-manuscript](https://github.com/greenelab/xswap-manuscript)).

## Results

![Discrimination figure](){#fig:discrimination width="100%"}

![Calibration figure](){#fig:calibration width="100%"}

## Discussion


## Conclusion


## References {.page_break_before}

<!-- Explicitly insert bibliography here -->
<div id="refs"></div>

## Supplemental information

### Approximate edge prior {#approx-prior-supp}

To approximate the edge prior, we began by making two simplifications.
First, we assumed independence between node pairs.
This assumption does not actually hold for the XSwap algorithm, though it is a reasonable simplification for large, sparse networks.
Second, we assumed that the XSwap process is stationary.
This assumption also does not actually hold, but it was made because it significantly simplifies the problem.
A single node pair has two possible states, "edge" and "no edge".
These states are not transient, and they are not periodic so long as more than one possible swap exists in the network.
In almost all cases, then, our simplified model of the algorithm gives the state of a node pair as an ergodic process, independent of other node pairs.

Let $A_{i,j}$ represent the existence of edge $(i, j)$
For a given node pair, $(i, j)$, then, let $q_{i,j}$ represent the transition probability from the "no edge" state to the "edge" state in one successful iteration of the XSwap algorithm.
Let $r_{i,j}$ represent the probability of the opposite transition ("edge" to "no edge") in one successful iteration.
With "no edge" represented as $[1, 0]^T$ and "edge" represented as $[0, 1]^T$, the transition matrix, $P$, is given by the following:

\begin{align*}
    P^T &= \begin{bmatrix}
       1-q & r \\
       q & 1-r
     \end{bmatrix}
\end{align*}

The stationary distribution of this system should correspond to the distribution when the number of swaps goes to infinity.
It can be found by computing the eigenvectors of the system, as we know that the stationary distribution vector, $\mathbf{v}$ satisfies $P^T \mathbf{v} = \mathbf{v}$.
The normalized eigenvector $\mathbf{v}$ is given by

\begin{align*}
    \mathbf{v} = \frac{1}{r/q + 1} \begin{bmatrix}
        r/q \\
        1
    \end{bmatrix}
\end{align*}

The asymptotic edge probability is therefore

$$\frac{1}{r/q + 1}.$$

Since node pairs are being treated as independent, the probability of an edge being created in one successful iteration, given that the edge does not currently exist, is the ratio of the number of edge choices involving nodes $i$ and $j$ to the total number of possible swaps, $S$.
Let $d(u_i)$ represent the degree of source node $i$ and $d(v_j)$ represent the degree of target node $j$.

$$q_{i,j} = \frac{d(u_i)d(v_j)}{S}$$

Similarly, the probability of an edge being eliminated in one iteration is the ratio of the number of edge choices involving $(i,j)$ and any other valid edge to the total number of possible swaps.
Let $m$ be the total number of edges in the network.

$$r_{i,j} = \frac{m - d(u_i) - d(v_j) + 1}{S}$$

The approximate edge prior is, therefore,

$$\frac{d(u_i)d(v_j)}{m - d(u_i) - d(v_j) + 1 + d(u_i)d(v_j)}.$$

Unfortunately, we found that the above edge prior approximation is a poor approximation in many cases.
We found that the following modified form (introduced in Methods) affords a superior approximation:

\begin{equation}
    P_{i,j} = \frac{d(u_i) d(v_j)}{\sqrt{(d(u_i) d(v_j))^2 + (m - d(u_i) - d(v_j) + 1)^2}}
\end{equation}

Because the modified form of the approximation offers a much superior fit to the data, we chose to include only the modified version in the Python package released, and we used only the modified form throughout our analysis.
