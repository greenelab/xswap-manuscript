---
author-meta:
- Michael Zietz
- Daniel S. Himmelstein
- Kyle Kloster
- Christopher Williams
- Michael W. Nagle
- Blair D. Sullivan
- Casey S. Greene
date-meta: '2019-09-09'
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
([permalink](https://greenelab.github.io/xswap-manuscript/v/76374a3ca76070b1951cfe00c63a88a437cc16c2/))
was automatically generated
from [greenelab/xswap-manuscript@76374a3](https://github.com/greenelab/xswap-manuscript/tree/76374a3ca76070b1951cfe00c63a88a437cc16c2)
on September 9, 2019.
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

+ **Kyle Kloster**<br>
    ![ORCID icon](images/orcid.svg){.inline_icon}
    [0000-0001-5678-7197](https://orcid.org/0000-0001-5678-7197)
    · ![GitHub icon](images/github.svg){.inline_icon}
    [kkloste](https://github.com/kkloste)
    · ![Twitter icon](images/twitter.svg){.inline_icon}
    [kylekloster](https://twitter.com/kylekloster)<br>
  <small>
     Department of Computer Science, North Carolina State University, Raleigh, North Carolina, United States of America
     · Funded by the Gordon and Betty Moore Foundation (GBMF4560)
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

+ **Blair D. Sullivan**<br>
    ![ORCID icon](images/orcid.svg){.inline_icon}
    [0000-0001-7720-6208](https://orcid.org/0000-0001-7720-6208)
    · ![GitHub icon](images/github.svg){.inline_icon}
    [bdsullivan](https://github.com/bdsullivan)
    · ![Twitter icon](images/twitter.svg){.inline_icon}
    [BlairDSullivan](https://twitter.com/BlairDSullivan)<br>
  <small>
     School of Computing, University of Utah, Salt Lake City, Utah, United States of America
     · Funded by ['the Gordon and Betty Moore Foundation (GBMF4560)']
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

Important tasks in biomedical discovery such as predicting gene functions, gene-disease associations, and drug repurposing opportunities are often framed as network edge prediction.
The number of edges connecting to a node, termed degree, can vary greatly across nodes in real biomedical networks, and the distribution of degrees varies between networks.
If degree strongly influences edge prediction, then imbalance or bias in the distribution of degrees could lead to nonspecific or misleading predictions.
We introduce a network permutation framework to quantify the effects of node degree on edge prediction.
Our framework decomposes performance into the proportions attributable to degree and the network's specific connections.
We discover that performance attributable to factors other than degree is often only a small portion of overall performance.
Degree's predictive performance diminishes when the networks used for training and testing---despite measuring the same biological relationships---were generated using distinct techniques and hence have large differences in degree distribution.
We introduce the permutation-derived edge prior as the probability that an edge exists based only on degree.
The edge prior shows excellent discrimination and calibration for 20 biomedical networks (16 bipartite, 3 undirected, 1 directed), with AUROCs frequently exceeding 0.85.
Researchers seeking to predict new or missing edges in biological networks should use the edge prior as a baseline to identify the fraction of performance that is nonspecific because of degree.
We released our methods as an open-source Python package (https://github.com/hetio/xswap/).


## Introduction

Networks contain information about relationships between entities (referred to here as "edges" between "nodes").
A node's degree is the number of edges it has in the network.
Networks contain many nodes, whose degrees can be aggregated to form the network's degree distribution.
Because different nodes can have very different degrees, real networks generally have highly variable degree distributions [@rly3gDig; @1mIOnArF; @GFS9MouO].
This is especially true for networks encoding biomedical knowledge or assays, where natural forces such as preferential attachment inherent to the problem domain combine with observation-based influences such as study methodology to create non-uniform degree distributions (Figure {@fig:hetionet}).

![
**Biomedical networks are characterized by non-uniform degree distributions.**
Eight degree distributions are plotted for six edge types Hetionet v1.0 [@O21tn8vf].
Hetionet integrates subnetworks for 24 different edge types, the degree distributions of which are analyzed separately.
Furthermore, bipartite (e.g. Anatomy→expresses→Gene) and directed (e.g. Gene→regulates→Gene) edge types have both source and target degrees that must be assessed separately.
Undirected edge types (e.g Compound–resembles–Compound) have only a single degree distribution.
Degree distributions are non-uniform and vary greatly between different networks.
The y-axis is log~10~-scaled to accomodate the common occurrence where most nodes have low degree while a small portion of nodes have high degree.
Several distributions have node degree ceilings corresponding to a node being connected to all other possible nodes.
Zero-degree nodes are not displayed, since methodological limitations often result in edge data only existing for a subset of nodes.
](https://github.com/greenelab/xswap-analysis/raw/b0db22c82b2e58bf1ef5ae78317167982016e26b/img/hetionet_degrees.png){#fig:hetionet width="100%"}

Degree is an important metric for differentiating between nodes, and it appears in many common edge prediction features [@ohIv6zMA].
However, reliance on degree can pose problems for edge prediction.
Firstly, bias in networks can distort node degree so that degree differences between two nodes may not be meaningful.
Secondly, reliance on degree can lead edge prediction methods to make nonspecific or trivial predictions and fail to identify novel or insightful relationships.

Most biomedical networks are imperfect representations of the true set of relationships.
Real networks often mistakenly include edges that do not exist and exclude edges that do exist.
How well a network represents the true relationships it attempts to represent depends on a number of factors, especially the methods used to generate the data in the network [@bo2VEmIz; @yJZSr6c6; @C4FHCVCz].
We define "degree bias" as the type of misrepresentation that occurs when the fraction of incorrectly existent/nonexistent relationships depends on node degree.
Depending on the type of data being represented, degree biases can arise due to experimental methods, inspection bias, or other factors [@bo2VEmIz].

Inspection bias indicates that entities are not uniformly studied [@lnDqu0oW], and it is likely to cause degree bias when networks are constructed using hypothesis-driven findings extracted from the literature, as newly-discovered relationships are not randomly sampled from the set of all true relationships.
Though there is a high correlation between the number of publications mentioning a gene and its degree in low-throughput interaction networks, the number of publications mentioning a gene has little correlation with its degree in a systematically-derived protein interaction network [Figure 6A in @LCyCrr7W].
This evidence suggests that many poorly studied genes have similar numbers of interactions as those scientists have preferentially examined and that these edges are missed due to inspection bias.
For networks with strong inspection bias, reliance on degree can lead to predictions that have good metrics when assessed by cross validation but little ability to generalize.

Another reason why a method's reliance on degree can be unfavorable is that degree imbalance can lead to prediction nonspecificity.
Nonspecific predictions are not made on the basis of the specific connectivity information contained in a network.
For example, Gillis et al. [@zB6RQrIj] examined the concept of prediction specificity in the context of gene function prediction and found that many predictions appear to rely primarily on multifunctionality and could be "potentially misleading with respect to causality."
Real networks have a variety of degree distributions (Figure {@fig:hetionet}), and they commonly exhibit degree imbalance [@GFS9MouO; @hbOjmCsZ; @1mIOnArF; @rly3gDig].
Degree imbalance leads high-degree nodes to dominate in the predictions made by degree-associated methods [@g059lh8v], which are effective predictors of connections in some biological networks [@1736TBtF6].
Consequently, degree-based predictions are more likely nonspecific, meaning the same set of predictions performs well for different tasks.

Depending on the prediction task, edge predictions involving very high degree nodes may be undesired, uninsightful, or nonspecific.
Model evaluation is challenging in this context: nonspecific or trivial predictions can dominate performance evaluations and may actually be correct, even if they are not the desired outputs of the predictive model.
For example, predicting that the highest degree node in a network shares edges with the remaining nodes to which it is not connected will often lead to many correct predictions, despite this prediction being generic to all other nodes in the network.

Degree is important in edge prediction, but it can cause undesired effects.
Degree-based features should often be included in the interpretation of predictions to disentangle desired from non-desired effects and to effectively evaluate and compare predictive models.
We sought to directly measure the effect of node degree on edge prediction methods.
We introduce a permutation-based framework and software implementation to find edge existence probabilities due to node degree and to quantify the contribution of degree to edge prediction methods.
This method allows edge predictions to be evaluated in the context of degree and its effects on the prediction task.
Our results demonstrate that degree-associated methods are very effective for reconstructing a network using a subsampled holdout.
However, these methods are ineffective for predicting edges between networks measuring the same biological processes in targeted and systematic ways because such networks have distinct degree distributions.
Using multiple different networks, we provide evidence that degree has a strong effect on the probability of edge existence and that our permutation-based edge prior feature best quantifies this probability.

## Methods

### Network permutation

Network permutation is a way to produce new networks by randomizing the connections of an existing network.
Specialized permutation strategies can be devised that randomize some aspects of networks while retaining other features.
Comparing between permuted and unpermuted networks gives insight to the effects of the retained network features.
For example, an edge prediction method that has superior reconstruction performance on a network compared to its permutations likely relies on information that is eliminated by permutation.
Conversely, identical predictive performance on true and permuted networks indicates that a method relies on information that is preserved during permutation.

Network permutation is a flexible framework for analyzing other methods, because it generates networks with identical formats to the original network.
We use network permutation to isolate degree and determine its effects in different contexts.
Degree-preserving network permutation obscures true connections and higher-order connectivity information while retaining node degree, and thereby, the network's degree sequence.
Thanks to the flexibility of permutation, our framework can quantify the effect of degree on any network edge prediction method.

### XSwap algorithm

Hanhijärvi, et al. presented XSwap [@iKOIEzQ9], an algorithm for the randomization ("permutation") of unweighted networks (Figure {@fig:algo}A).
The algorithm picks two existing edges at random, and if the edges constitute a valid swap, exchanges the targets between the edges.
This process is repeated many times until the maximum number of steps has been reached.
In general, the maximum number of steps should be chosen to be sufficiently large that the fraction of original edges retained in the permuted network is near its asymptotic value for a large number of steps.
The asymptotic fraction of original edges retained in permutation depends on network density, and higher density networks require more swap attempts per edge to reach their asymptotic fraction (Figure {@fig:swap-percent}).

To allow greater flexibility, we modified the original algorithm by adding two parameters, "`allow_loops`", and "`allow_antiparallel`" that allow a greater variety of network types to be permuted (Figure {@fig:algo}B and  Table {@tbl:xswap}).
Specifically, two chosen edges constitute a valid swap if they preserve degree for all four involved nodes and do not violate the above condition options.
The motivation for these generalizations is to make the permutation method applicable both to directed and undirected graphs, as well as to networks with different types of nodes, variously called multipartite, heterogeneous, or multimodal networks.

When permuting bipartite networks, our method ensures that each node's class membership and within-class degree is preserved.
Similarly, heterogeneous networks should be permuted by considering each edge type as a separate network [@WkPlH1ds; @xmFxwmUd].
This way, each node retains its within-edge-type degree for all edge types.
We provide documentation for parameter choices depending on the type of network being permuted in the GitHub repository (<https://github.com/hetio/xswap>).
The original algorithm and our proposed modification are given in Figure {@fig:algo}.

![
  **XSwap algorithm pseudocode.**
  **A.** XSwap algorithm presented by Hanhijärvi, et al. [@iKOIEzQ9].
  **B.** Extension of the XSwap algorithm to other types of networks.
](images/xswap_algorithms_combined_labels.png){#fig:algo width="85%"}

| Network type | Degree preserved | Figure | `allow_antiparallel` | `allow_loops` |
| :----------- | :--------------- | :----- | :------------------- | :----------------- |
| simple | all | ![](images/xswap_simple.png){height="85px"} | False | False |
| bipartite | in/out | ![](images/xswap_bipartite.png){height="85px"} | True | True |
| directed | in/out | ![](images/xswap_directed.png){height="85px"} | Depends on networks | Depends on networks |

Table:
Applications of the modified XSwap algorithm to various network types with appropriate parameter choices.
For simple networks, each node's degree is preserved. 
For bipartite networks, each node's number of connections to the other part is preserved, and the partite sets (node class memberships) are preserved.
For directed networks, each nodes' in- and out-degrees are preserved, though parameter choices depend on the network being permuted.
Some directed networks can include antiparallel edges or loops while others do not. {#tbl:xswap}

### Edge prior

We introduce the edge prior to quantify the probability that two nodes are connected based only on their degree.
The edge prior can be estimated using the fraction of permuted networks in which a given edge exists---the maximum likelihood estimate for the binomial distribution success probability.
Based only on permuted networks, the edge prior does not contain any information about the true edges in the (unpermuted) network.
The edge prior is a numerical feature that can be computed for every pair of nodes that could potentially share an edge, and we compared its ability to predict edges in three tasks, discussed below.

### Analytical approximation of the edge prior

We also considered whether the probability of an edge existing across permuted networks has a simple closed-form expression.
To derive such an expression, we first make the simplifying assumption that the probability of any given edge existing is independent of all other potential edges.
We were unable to find a closed-form solution giving the edge prior without assuming independence in this way, which we believe is incorrect for XSwap.
Nonetheless, we discovered a good analytical approximation to the edge prior for networks with many nodes and relatively low edge density (Figure {@fig:approx-quality}).

![
  **The XSwap-derived edge prior can be analytically approximated.**
  The analytical approximation is plotted against the XSwap-derived edge prior for three edge types from Hetionet.
  The strong correlation suggests that the approximation will be suitable for applications where computation time is a limiting factor.
](https://github.com/greenelab/xswap-analysis/raw/b0db22c82b2e58bf1ef5ae78317167982016e26b/img/prior_exact_vs_approx.png){#fig:approx-quality width="100%"}

Let $m$ be the total number of edges in the network, and $d(u_i)$, $d(v_j)$ be the source and target degrees of a node pair, respectively.
A good approximation of the edge prior is given by the following:

$$
  P_{i,j} = \frac{d(u_i) d(v_j)}{\sqrt{(d(u_i) d(v_j))^2 + (m - d(u_i) - d(v_j) + 1)^2}}
$$

Further discussion of this approximate edge prior and an derivation are available in [the supplement](#approx-prior-supp).

### Prediction tasks

We performed three prediction tasks to assess the performance of the edge prior.
We compared the permutation-based prior with two additional features: our analytical approximation of the edge prior and the product of source and target degree, scaled to the range [0, 1] to allow calibration assessment.
We used 20 biomedical networks from the Hetionet heterogeneous network [@O21tn8vf] that had at least 2000 edges for the first two tasks ([Supplemental table](#networks)).
In the first task, we computed the degree-based prediction features (edge prior, scaled degree product, and analytical prior approximation), and predicted the original edges in the network by rank-ordering node pair edge predictions by the node pairs' feature values.
We used node pairs that lacked an edge in the original network as negative examples and those with an edge as positive examples.
To assess the methods' predictive performances, we computed the area under the receiver operating characteristic (AUROC) curve for all three features.
In the second task, we sampled 70% of edges from each of the networks, computed features on the sampled network, then predicted held-out edges.
For this task, negative examples were node pairs in which an edge did not exist in either original or sampled network, while positive samples were those node pairs without an edge in the sampled network but with an edge in the original network.

The third task evaluated the ability of the edge prior to generalize to new degree distributions.
We used two domains where networks were available which shared nodes but had different degree distributions.
Protein-protein interactions (PPI) and transcription factor-target gene (TF-TG) relationships had networks created both by literature curation of low-throughput, hypothesis-driven research and by high-throughput, systematic, hypothesis-free experimentation.
For the PPI networks, we used the STRING network, which incorporates literature-mining to find relationships [@fkKIuC7X] and a combination of the high-throughput, proteome-scale interaction networks from Rual et al. [@lnDqu0oW] and Rolland et al. [@LCyCrr7W].
We used a transcription factor-target gene (TF-TG) literature-derived network from Han et al. [@z5ieI0Qg] and a high-throughput network from Lachmann et al. [@13Jzku9hE].
The pairs of networks for PPI and TF-TG data sources are ideal because in one we expect inspection bias and in the other we do not.

As a further basis of comparison, we added a time-resolved co-authorship network, which we partitioned by time to create two separate networks.
We created the co-authorship network of bioRxiv bioinformatics preprints using the Rxivist [@IYwQbTVz; @7668E40A] database, which was generated by crawling the bioRxiv server.
Unlike the other two networks, co-authorship does not have degree bias, as the network faithfully represents all true co-author relationships.
We include this network to offer a comparative prediction task in which the degree distributions between training (posted before 2018) and testing (posted during or after 2018) do not differ (Figure {@fig:degree-bias}A).
The goal of the third prediction task is to determine feature generalizability for network reconstruction between different degree distributions, especially predicting a network without degree bias using features from a degree-biased network.
Further information about the networks used can be found in [the supplement](#networks).

### Degree-grouping

Our method for degree-preserving permutation produces randomized networks that share few of their edges with the original network.
The feature values for two node pairs with the same source and target degree are drawn from the same distribution in permuted networks, so nodes with equal degree can be grouped when summarizing features.
We used this to augment each node pair's feature values in permuted networks, which allowed these pairs to have more permuted feature values than permuted networks.
For a given node pair, degree grouping treats other node pairs with the same degrees as additional permutations.
Degree grouping greatly increased the effective number of permutations for nodes with frequently observed degrees [@DwbABa00].
We used degree grouping throughout our analyses.

### Implementation and source code

We implemented our modified version of the XSwap algorithm as an open-source Python package.
The package contains submodules for permuting networks, computing the edge prior, and converting networks between adjacency matrix and edge list formats.
Additionally, we include the analytical approximation of the edge prior and functionality to assign unique identifiers to nodes.
The Python package is [available](https://pypi.org/project/xswap/) on the Python Packaging Index under the name "xswap".
The full source code for our method of degree-preserving network permutation has also been made freely available under the BSD 2-Clause License (<https://github.com/hetio/xswap>).

The edge swap mechanism---implemented in C++ for greater speed---uses a bitset to avoid producing edges which violate the conditions for a swap to be considered valid.
While the full bitset implementation is faster for smaller networks, our package uses a compressed bitset [@jNEBDktj] when a network would occupy memory above a user-adjustable threshold.
In addition to the validity conditions already described, our package allows specific edges to be excluded from permutation, and every network permutation returns both a permuted network and summary information about the numbers of swaps attempted, performed, and the reasons why invalid swaps were rejected.

In addition to the Python package, all code to generate the analyses and figures is available at <https://github.com/greenelab/xswap-analysis>.
The manuscript was written using the Manubot software [@YuJbg3zO ], which allows anyone to provide feedback or modifications via the public repository at <https://github.com/greenelab/xswap-manuscript>.

## Results

### Node degree bias is prevalent

We found examples of node degree bias in the PPI and TF-TG networks we investigated.
Figure {@fig:degree-bias} shows node degree in separate networks for the same type of data.
For the PPI networks, the literature-derived network has a larger mean degree and a longer tail than the systematic network, while in the TF-TG networks this relationship is reversed.
Because the TF-TG network contained far more transcription factors than target genes (144 and 1406, respectively), the distributions of target degrees were far more compact than those of source degrees.
Unlike the PPI and TF-TG networks, the co-authorship networks were split by date of first co-authorship, and they did not exhibit a great difference in their degree distributions.
All three types of networks (PPI, TF-TG, and co-authorship) exhibit degree imbalance to varying extents.
These results indicate that, depending on the methods by which the represented data were generated, networks of the same type of data may have overall degree distributions that differ greatly (Figure {@fig:degree-bias}A), and they may even assign very different degree to the same nodes (Figure {@fig:degree-bias}B).

A prediction task that uses only one type of network is challenging because degree distributions vary greatly within a single domain.
Predicting systematic edges using a literature-curated network is particularly challenging, because the degree distribution of systematic edges may be skewed toward higher or lower degree relative to the literature network.

![
  **A.** Degree distributions of networks with and without degree bias can be very different.
  Data on PPI and TF-TG were split between literature-derived and systematically-derived networks.
  In both cases, the networks exhibit large differences in degree distribution.
  Co-authorship relationship networks split by date of first co-authorship roughly share their degree distributions.
  **B.** Systematically-derived networks are not uniformly sampled from literature-derived networks or vice versa.
  Uniform random sampling produces linearly-correlated node degree, while non-random sampling produces non-correlated degree.
  70% of literature edges were sampled with uniform probability for the "Subsampled holdout" network.
](https://github.com/greenelab/xswap-analysis/raw/d7181e64a5c90f9720ab453334892aba164651e7/img/degree_bias.png){#fig:degree-bias width="100%"}

### The edge prior encapsulates degree

In the first prediction task, we computed three features---the XSwap edge prior, an analytical approximation to the edge prior, and the (scaled) product of source and target node degree---on networks from Hetionet.
We then evaluated the extent to which these features could reconstruct the 20 networks ([Supplemental table](#networks)).
The XSwap-derived edge prior reconstructed many of the networks with a high level of performance, as measured by the AUROC.
Of the 20 individual networks we extracted from Hetionet, 17 had an edge prior self-reconstruction AUROC >= 0.95, with the highest reconstruction AUROC at 0.9971 (network was the Compound–downregulates–Gene edge type).
Meanwhile, the lowest self-reconstruction performance (AUROC = 0.7697) occurred in the network having the fewest node pairs (network was the Disease–localizes–Anatomy edge type).

![
  **AUROC of network reconstruction by prediction task.**
  The edge prior shows strong performance for network reconstruction when computed on the original (Task 1) and sampled (Task 2) networks.
  The performance reduction from computing features on sampled networks is real but far smaller compared to a new degree distribution.
  ](https://github.com/greenelab/xswap-analysis/raw/c763473ee83c6157f2430bf9a64b19dc564b7dbc/img/auroc.png){#fig:discrimination width="60%"}

The three features that we compared were highly rank correlated (over 0.984 for all 20 metaedges).
The three features also had very similar AUROC reconstruction performance values for the first, second, and third prediction tasks (max difference < 0.027) because AUROC is rank-based.
The edge prior was slightly better than the approximations in 12 of 20 networks.
However, while the AUROC results were similar, the features were very different in their levels of calibration---the ability of the model to correctly estimate edge existence probabilities.
The edge prior was very well calibrated for all networks in the first and second tasks, and it provided the best calibration of the three features for each of the prediction tasks (Figure {@fig:calibration}A).
As the edge prior was not based on the networks' true edges, these results indicated that degree sequence alone was highly informative and that permutation was the only approach that provided a well-calibrated model.

![
  **The edge prior accurately assigns the probability of edge existence.**
  **A.** Calibration curves for full network reconstruction of 20 networks from Hetionet.
  For every unique feature value on the horizontal axis, the fraction of node pairs with that feature value having an edge in the network is shown on the vertical axis.
  The permutation-based edge prior's calibration was superior to the other two strategies based on degree.
  **B.** Calibration curves for sampled network reconstruction.
  The edge prior shows superior calibration in the 20 Hetionet networks.
  **C.** Individual Hetionet edge type calibration estimated by the two-component decomposition of the Brier score, in which lower scores indicate better calibration.
  The edge prior has excellent calibration in unsampled and sampled networks, and each considered method is sensitive to shifts in the degree distribution.
](https://github.com/zietzm/xswap-analysis/raw/c763473ee83c6157f2430bf9a64b19dc564b7dbc/img/fig4.calibration.png){#fig:calibration width="100%"}

The second prediction task mirrored the first task, but it involved reconstructing networks based on subsampled networks with only 70% of the original edges.
Because edges were sampled uniformly without replacement, the subsampled networks share similar degree distributions to the original networks (see Figure {@fig:degree-bias}B).
Unlike in the first task, edges that were present in the sampled network were not tested and therefore are not included in the performance metrics.
The results of the second prediction task further demonstrate a high level of performance for degree-sequence-based node pair features (Figure {@fig:discrimination}).
The edge prior was able to reconstruct the unsampled network with an AUROC of greater than 0.9 in 14 of 20 networks.
As was observed in the first task, node pair features computed in the second prediction task were highly rank-correlated, meaning the AUROC values for different features were similar.
While performance was slightly lower in the second task than the first, many networks were still well-reconstructed.
The edge prior was the best calibrated feature for both tasks.

In the third prediction task, we computed the three edge prediction features for paired networks representing data from PPI, TF-TG, and bioRxiv bioinformatics pre-print co-authorship.
The goal of the task was to compare predictive performance across different degree distributions for the same type of data.
We find that the task of predicting systematically-derived edges using a network with degree bias is significantly more challenging than network reconstruction, and we find consistently lower performance compared to the other tasks (Figure {@fig:discrimination}).
The edge prior was not able to predict the separate PPI network better than by random guessing (AUROC of roughly 0.5).
Only slightly better was its performance in predicting the separate TF-TG network, at an AUROC of 0.59.
We find superior performance in predicting the co-authorship relationships (AUROC 0.75), which was expected as the network being predicted shared roughly the same degree distribution as the network on which the edge prior was computed.
The results of the third prediction task show that a difference in degree distribution between the network on which features are computed and the network to be predicted can make prediction significantly more challenging.

The edge prior can be considered a baseline edge predictor that accurately captures degree's contribution to the probability of an edge existing.
The edge prior's low performance in the third task indicates that degree is less helpful for edge prediction tasks in which training and testing networks do not share their degree distributions.
Many biomedical prediction tasks can be framed as edge prediction tasks between different degree distributions.
In drug repurposing, for example, existing compound-disease treatment relationships are unlikely to be randomly sampled from all true treatment relationships.
However, all treatment relationships between existing compounds and diseases are desirable outputs in prediction.
Edge predictions can be based on both underlying biological properties and network degree distributions.
However, predictions based on biological properties may be more consistent and generalizable than those based on degree.
Degree's influence on edge prediction accuracy measures can reveal the relative contributions of these two factors.

### Degree can underly a large fraction of performance

We conducted a further edge prediction task as an example application of the edge prior and our permutation framework.
To begin, we chose the STRING PPI network for the comparison and computed five edge prediction features (Supplemental table {@tbl:edge-prediction}).
The goal of the task was to reconstruct the network on which the features were computed.
All five features were correlated with degree (Figure {@fig:feature-degree}), which we quantified for a node pair using the product of source and target degrees.
We expected features based on degree to show strong performance for a network reconstruction task without holdout, as found in the first prediction task.

![
  **Common edge-prediction metrics correlate with node degree.**
  Five common edge-prediction features (Supplemental table {@tbl:edge-prediction}) are correlated with node degree on the STRING PPI network [@fkKIuC7X].
  All five features show a positive relationship with degree, though the magnitude of this correlation is highly variable.
  The preferential attachment index is understandably perfectly correlated because it is equal to the product of source and target degree.
](https://github.com/greenelab/xswap-analysis/raw/f8dce1983243fd4056108c7c8bdcba895f6dfbaf/img/feature-degree.png){#fig:feature-degree width="100%"}

We used two permutation-derived null values to evaluate reconstruction and contextualize performance.
First, the performance of the edge prior was compared to determine the performance attributable to the degree sequence of the PPI network.
The first comparison gave insight into the ability of the PPI network to be reconstructed by degree.
Second, the five edge prediction features were computed on 100 permuted networks and used to reconstruct the unpermuted network.
Each permuted network corresponded to AUROC values quantifying the performances of features computed on it.
The second comparison gave insight into the performance of each feature if the feature was only capturing degree.

![
  **Identifying the fraction of a metric's performance resulting from degree alone.**
  Network reconstruction performances by five edge prediction features.
  Dotted red line indicates performance of the edge prior.
  Each feature was computed on the unpermuted and 100 permutations of the STRING PPI network.
  ](https://github.com/greenelab/xswap-analysis/raw/4d9137f43a16fbe6c6a02865adceaa9a3195fe2d/img/feature-auroc.png){#fig:feature-auroc width="85%"}

The edge prior encapsulates nonspecific predictions due to degree, and it reconstructed the PPI network with an AUROC of 0.797 (dotted red line in Figure {@fig:feature-auroc}).
In the second comparison, edge prediction features computed on permuted networks had performance equal or lower to their performances on the unpermuted networks.
This indicated that four out of five edge prediction features discern more than node degree for the prediction task.
The preferential attachment index is the product of source and target degree, and its performance did not differ from the edge prior or the feature's performance when computed on permuted networks.
The four remaining features had higher reconstruction performance than the edge prior or feature values computed on permuted networks.

This comparison quantified the performance of degree toward the prediction task and assessed degree's effect on five edge prediction features.
The edge prior provided the baseline level of performance attributable to degree alone.
Comparing the performances on permuted networks to the performance of the edge prior reveals the extent to which a feature measures degree.
Features whose performances on permuted networks were below that of the edge prior only imperfectly measured degree (eg: Jaccard index), whereas features whose performances equaled the edge prior completely captured degree (eg: preferential attachment index).

Features can also capture information beyond degree, and our method can quantify this performance.
For example, the superior performance on unpermuted networks relative to permuted networks indicated that RWR, resource allocation, Jaccard, and Adamic/Adar indices captured more than degree in this prediction task.
These results aligned with the definitions of each feature and validated that our permutation framework accurately assessed reliance on degree.

## Discussion

We focus on edge prediction in biomedical networks.
Our overall goal is to predict new edges with specificity, so that predictions reflect particular connectivity rather than generic node characteristics.
Our permutation framework measures the predictive performance attributable to degree to provide a baseline expectation for edge pairs.
We expect that non-specificity due to degree is not a unique property of biomedical networks.
For example, if node A connects to nearly all other nodes in a network, predicting that all remaining nodes share an edge with node A will likely result in many correct---though nonspecific---predictions, regardless of the type of data contained in the network.
Node degree should be accounted for to make correct predictions while being able to distinguish specific from nonspecific predictions.
Prediction without reliance on node degree is challenging because many effective methods for edge prediction are correlated with degree (Figure {@fig:feature-degree}).

The effects of node degree are obvious when edge prediction features are functions of degree.
For example, the resource allocation index is the sum of inverse degree of common neighbors between source and target nodes (in the symmetric case), while preferential attachment is the product of source and target degree [@1F96bsjSm; @suzIn5oo].
However, because many other edge prediction methods are not explicitly degree-based, it is important to have a general method for comparing the effects of node degree on edge prediction methods.

We developed a permutation framework to quantify the edge probability due to degree.
We term this probability the "edge prior", and we have identified two applications.
First, a probability associated with every node pair can be treated as a classification score.
Ordering these scores provides an assessment of performance based solely on degree, which can be used as a baseline for other classifiers.
Second, node pair probabilities can be used to adjust edge prediction features depending on the task.
If degree is a desired feature, then the edge prior can be treated like a Bayesian prior probability.
Alternatively, if degree is not a desired feature, then the edge prior can be used to calibrate features and thus potentially enhance predictive specificity.

Figure {@fig:feature-auroc} illustrates the utility of the edge prior and permutation framework for two purposes.
First, it contextualizes feature performances relative to the baseline of nonspecific, degree-based predictions, quantified by the edge prior.
Degree has varying utility for different edge prediction tasks.
The edge prior's performance on a task quantifies the utility of degree toward the task.
This comparison is useful because specific predictions (based on more than degree alone) are more valuable for some applications than nonspecific ones and because degree can be an expression of bias in many real-world networks.

Second, Figure {@fig:feature-auroc} compares five edge prediction features computed on and unpermuted networks.
This comparison identified the fraction of each feature's performance attributable to degree.
Some features, such as the preferential attachment index, perfectly and exclusively measure degree.
The Adamic/Adar index also almost completely captures degree because its performances from permuted networks are nearly at the performance of the edge prior.
However, the Adamic/Adar index had much higher performance when computed on the unpermuted network, indicating that it also extracts higher-order information.
This analysis, enabled by network permutation, measured the extent to which features rely on degree for a specific prediction task by assessing performance beyond the degree-based, nonspecific baseline.

## Conclusion

We developed a network permutation framework and open source software implementation that quantifies the probability of edge existence due to degree and can assess the fraction of feature performance attributable to degree.
We demonstrated the superiority of the edge prior over other degree-based features for quantifying the effect of degree on the probability of edge existence.
The XSwap methods and software provide a context for evaluating edge prediction methods and specific predictions for reliance on degree and, therefore, nonspecificity.
Network edge prediction is a common task in biological and biomedical research, and it can be greatly influenced by degree.
Degree should be considered directly in prediction approaches to avoid making nonspecific or trivial predictions due to degree imbalance or bias.
A careful accounting of degree's effects enables contextualized model evaluation and can help to quantify nonspecificity in biomedical network edge prediction.


## References {.page_break_before}

<!-- Explicitly insert bibliography here -->
<div id="refs"></div>

## Supplemental information

### Performance of the XSwap algorithm

The performance of the XSwap algorithm depends on a number of network properties.
We define network density to be the number of edges divided by the number of potential edges.
Increasing network density lowers the asymptotic fraction of edges changed, as greater density prevents the algorithm from removing certain edges.
Scale-free random graphs (via Barabási–Albert) can have a lower fraction of their edges swapped, asymptotically, as compared to basic random graphs (via Erdős–Rényi).

![Higher density networks have lower asymptotic fractions of edges swapped and take more attempts to reach these values.
  The Barabási–Albert model produces scale-free random graphs, while Erdős–Rényi generates random graphs where all edges are equally likely.
  ](https://github.com/greenelab/xswap-analysis/raw/47f67f85b1a5df2714d564c274515f1fdeb882ba/img/6_xswap_percent_swapped_iterations/lines_continuous.png){#fig:swap-percent width="100%"}

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
The eigenvector $\mathbf{v}$, normalized to sum to 1 as a probability vector, is given by

\begin{align*}
    \mathbf{v} = \frac{1}{r + q} \begin{bmatrix}
        r \\
        q
    \end{bmatrix}
\end{align*}

The asymptotic edge probability is therefore

$$\frac{q}{r + q}.$$

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

Interestingly, this expression can be derived by normalizing the eigenvector $\mathbf{v}$ to be a unit vector in the 2-norm instead of the 1-norm; that is, we use the value $q / \sqrt{r^2 + q^2}$ instead of $q/(r+q)$.
Because the modified form of the approximation offers a much superior fit to the data, we chose to include only the modified version in the Python package released, and we used the modified form throughout our analysis.

### Networks used for comparison {#networks}

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;border-width:1px;border-style:solid;border-color:#ccc;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:0px;overflow:hidden;word-break:normal;border-color:#ccc;color:#333;background-color:#fff;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:0px;overflow:hidden;word-break:normal;border-color:#ccc;color:#333;background-color:#f0f0f0;}
.tg .tg-buh4{background-color:#f9f9f9;text-align:left;vertical-align:top}
.tg .tg-mrzz{background-color:#f9f9f9;text-align:left}
.tg .tg-s268{text-align:left}
.tg .tg-0lax{text-align:left;vertical-align:top}
</style>
<table class="tg">
  <tr>
    <th class="tg-s268">Data</th>
    <th class="tg-s268">Network</th>
    <th class="tg-s268">Nodes</th>
    <th class="tg-0lax">Edges</th>
  </tr>
  <tr>
    <td class="tg-s268" rowspan="20">Hetionet</td>
    <td class="tg-mrzz">AdG</td>
    <td class="tg-mrzz">Source: 402, Target: 20945</td>
    <td class="tg-buh4">102240</td>
  </tr>
  <tr>
    <td class="tg-s268">AeG</td>
    <td class="tg-s268">Source: 402, Target: 20945</td>
    <td class="tg-0lax">526407</td>
  </tr>
  <tr>
    <td class="tg-mrzz">AlD</td>
    <td class="tg-mrzz">Source: 402, Target: 137</td>
    <td class="tg-buh4">3602</td>
  </tr>
  <tr>
    <td class="tg-s268">AuG</td>
    <td class="tg-s268">Source: 402, Target: 20945</td>
    <td class="tg-0lax">97848</td>
  </tr>
  <tr>
    <td class="tg-mrzz">BPpG</td>
    <td class="tg-mrzz">Source: 11381, Target: 20945</td>
    <td class="tg-buh4">559504</td>
  </tr>
  <tr>
    <td class="tg-s268">CCpG</td>
    <td class="tg-s268">Source: 1391, Target: 20945</td>
    <td class="tg-0lax">73566</td>
  </tr>
  <tr>
    <td class="tg-mrzz">CbG</td>
    <td class="tg-mrzz">Source: 1552, Target: 20945</td>
    <td class="tg-buh4">11571</td>
  </tr>
  <tr>
    <td class="tg-s268">CcSE</td>
    <td class="tg-s268">Source: 1552, Target: 5734</td>
    <td class="tg-0lax">138944</td>
  </tr>
  <tr>
    <td class="tg-mrzz">CdG</td>
    <td class="tg-mrzz">Source: 1552, Target: 20945</td>
    <td class="tg-buh4">21102</td>
  </tr>
  <tr>
    <td class="tg-s268">CrC</td>
    <td class="tg-s268">1552</td>
    <td class="tg-0lax">6486</td>
  </tr>
  <tr>
    <td class="tg-mrzz">CuG</td>
    <td class="tg-mrzz">Source: 1552, Target: 20945</td>
    <td class="tg-buh4">18756</td>
  </tr>
  <tr>
    <td class="tg-s268">DaG</td>
    <td class="tg-s268">Source: 137, Target: 20945</td>
    <td class="tg-0lax">12623</td>
  </tr>
  <tr>
    <td class="tg-mrzz">DdG</td>
    <td class="tg-mrzz">Source: 137, Target: 20945</td>
    <td class="tg-buh4">7623</td>
  </tr>
  <tr>
    <td class="tg-s268">DpS</td>
    <td class="tg-s268">Source: 137, Target: 438</td>
    <td class="tg-0lax">3357</td>
  </tr>
  <tr>
    <td class="tg-mrzz">DuG</td>
    <td class="tg-mrzz">Source: 137, Target: 20945</td>
    <td class="tg-buh4">7731</td>
  </tr>
  <tr>
    <td class="tg-s268">GuG</td>
    <td class="tg-s268">20945</td>
    <td class="tg-0lax">265672</td>
  </tr>
  <tr>
    <td class="tg-mrzz">GcG</td>
    <td class="tg-mrzz">20945</td>
    <td class="tg-buh4">61690</td>
  </tr>
  <tr>
    <td class="tg-s268">GiG</td>
    <td class="tg-s268">20945</td>
    <td class="tg-0lax">147164</td>
  </tr>
  <tr>
    <td class="tg-mrzz">GpMF</td>
    <td class="tg-mrzz">Source: 20945, Target: 2884</td>
    <td class="tg-buh4">97222</td>
  </tr>
  <tr>
    <td class="tg-s268">GpPW</td>
    <td class="tg-s268">Source: 20945, Target: 1822</td>
    <td class="tg-0lax">84372</td>
  </tr>
  <tr>
    <td class="tg-mrzz" rowspan="3">PPI</td>
    <td class="tg-mrzz">Sampled</td>
    <td class="tg-mrzz">3992</td>
    <td class="tg-buh4">255522</td>
  </tr>
  <tr>
    <td class="tg-s268">Literature</td>
    <td class="tg-s268">3992</td>
    <td class="tg-0lax">364743</td>
  </tr>
  <tr>
    <td class="tg-mrzz">Systematic</td>
    <td class="tg-mrzz">3916</td>
    <td class="tg-buh4">12913</td>
  </tr>
  <tr>
    <td class="tg-s268" rowspan="3">bioRxiv</td>
    <td class="tg-s268">Sampled</td>
    <td class="tg-s268">4587</td>
    <td class="tg-0lax">30686</td>
  </tr>
  <tr>
    <td class="tg-mrzz">&lt;2018</td>
    <td class="tg-mrzz">4615</td>
    <td class="tg-buh4">43691</td>
  </tr>
  <tr>
    <td class="tg-s268">All time</td>
    <td class="tg-s268">4615</td>
    <td class="tg-0lax">44963</td>
  </tr>
  <tr>
    <td class="tg-buh4" rowspan="3">TF-TG</td>
    <td class="tg-mrzz">Sampled</td>
    <td class="tg-mrzz">Source: 142, Target: 1396</td>
    <td class="tg-buh4">2689</td>
  </tr>
  <tr>
    <td class="tg-s268">Literature</td>
    <td class="tg-s268">Source: 144, Target: 1406</td>
    <td class="tg-0lax">3496</td>
  </tr>
  <tr>
    <td class="tg-mrzz">Systematic</td>
    <td class="tg-mrzz">Source: 144, Target: 1417</td>
    <td class="tg-buh4">29177</td>
  </tr>
</table>

### Edge prediction features

In the table that follows, let $k(u)$ denote the set of neighbors of node $u$.
Let $\mathbf{A}$ represent the normalized Laplacian adjacency matrix, and let $y_u$ be a vector with all ones except for a one in the $u$-th position.
$x$
For a directed graph, let $A(u)$ denote the set of nodes that node $u$ points to and $D(u)$ the set of nodes that point to $u$.
All definitions that follow are the score between nodes $u$ and $v$.

| Feature | Definition | Citation |
|--------------------------------|----------------------------|-------|
| Jaccard index | $\frac{|k(u) \cap k(v)|}{|k(u) \cup k(v)|}$ | [@EfWvuSjX] |
| Preferential attachment score | $|k(u)||k(v)|$ | [@EfWvuSjX] |
| Resource allocation index | $\sum_{w \in k(u) \cap k(v)} \frac{1}{|k(w)|}$ | [@1F96bsjSm] |
| Adamic/Adar index | $\sum_{w \in k(u) \cap k(v)} \frac{1}{log|k(w)|}$ | [@9dBDcARP] |
| Random walk with restart score | $c \bigg[ \bigg( \mathbb{I} - (1-c) \mathbf{A}\bigg)^{-1} \mathbf{y}_u \bigg]_v$ | [@HSmvOV9E;@1E6tdJtDz] |
| Inference score | $\frac{|A(u) \cap D(v)|}{|A(u)|} + \frac{|D(u) \cap D(v)|}{|D(u)|}$ | [@1EgqwD4S1] |

Table: Edge prediction features. {#tbl:edge-prediction}
