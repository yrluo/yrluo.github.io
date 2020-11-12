---
title: "A Network based Scheme for Financial News Representation and Sentiment Propagation"
collection: projects
type: "Group Work"
permalink: /projects/Financial-News-Sentiment-Representation
date: Sept, 2020
---

### Introduction
This project aims at developing a [Geometric Deep Learning](http://geometricdeeplearning.com/) based algorithm to gain an understanding of: 

1.	how financial news sentiment propagates through the company network,
1.	and its consequential impacts on the investor and stock movements.

The propagation is iterated over the news-affected companies (the minority class) to the remaining companies (the majority class). This approach is broadly applicable to instances where one has available a sparse signal (e.g., news sentiment for a subset of nodes or accounting information of listed companies) and would like to understand how the available signal measurements propagate through the network to the remaining nodes.

{% include image.html url="/images/company-network.png" description="The news sentiment propagation on the company network with anchor information" %}

### Technical Description
This approach can be seen as an instance of message passing problem \[1\] over the company network with anchors (news embeddings), where one would like to estimate the remaining unknown group elements (company without news embeddings) from noisy pairwise ratios of their mutual relations. 

The sliding windows correlation (or various denoised version) serves as the matrix of weighted pairwise group ratios, and those relationship signals generated from the empirical stock movements are treated as attentions that nodes should pay when anchors from their neighbours. 

The intergradation of anchors on the node level follows the message passing framework. On a given timestamp $t$, the nodes read (e.g., any permutation invariance concatenation function) anchor messages (attentions applied) of the neighbours and update their hidden states $h$ accordingly. They also broadcast their anchor messages to the company network so that other nodes can catch them. The unknown group elements can inherit anchor messages from the broadcasts and initialise their hidden states in this way.

The message passing pattern of the news sentiment propagation also imitates the real-world investor practices: a typical investor would tend to collect all useful information from related companies when making decisions on a target company. Accordingly, the average investor sentiment towards a given company (node) can be calculated via nonlinear transmissions (e.g., activation functions) of the completely propagated hidden states.

### Interactive Demo
<iframe src="company-network.html"  sandbox="allow-same-origin allow-scripts" width="120%"  height="600"  scrolling="no" seamless="seamless" frameborder="0" allowfullscreen>
</iframe>

### References
1. Gilmer, J., Schoenholz, S.S., Riley, P.F., Vinyals, O. and Dahl, G.E., 2017. Neural message passing for quantum chemistry. arXiv preprint arXiv:1704.01212.
1. Tetlock, P.C., 2007. Giving content to investor sentiment: The role of media in the stock market. The Journal of finance, 62(3), pp.1139-1168.
1. Garcia, D., 2013. Sentiment during recessions. The Journal of Finance, 68(3), pp.1267-1300.
