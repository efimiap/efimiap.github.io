---
layout: splash
title: 'Screenplay Summarization Using Latent Narrative Structure'
date: 2020-04-28
permalink: /posts/2020/08/screenplay-summarization/
author_profile: true
tags:
  - screenplay
  - summarization
  - structure
---

This is a blog post for the paper [*Screenplay Summarization Using Latent Narrative Structure*](https://arxiv.org/pdf/2004.12727.pdf) accepted at ACL 2020.

## Screenplay summarization as scene selection

Given a screenplay, which is naturally segmented into $N$ scenes $s$, the objective is to select an optimal subsequence of $M$ scenes that presents the main story -storyline- from beginning to end while omitting all unnecessary details and decreasing drastically the video length.

**Input**: Screenplay as a sequence of scenes $\mathcal{D}$. Each scene $s$ has description parts (i.e., what the camera sees) and dialogue parts between the characters. E.g.:

<p align="center">
  <img src="https://raw.githubusercontent.com/ppapalampidi/ppapalampidi.github.io/master/images/wpb9fac2df_1a.png" height="50">
</p>

**Output**: much smaller subsequence of scenes containing most important events in the story; video summary by merging the respective videos for the selected scenes.

## General summarization algorithms

**Unsupervised: _TextRank_** 

_TextRank_[1] is a well-known unsupervised summarization algorithm. For _TextRank_, we create a fully-connected graph $G=(V,E)$, where $V$ is the set of nodes and $E$ is the set of edges. The nodes $V$ are the textual units (in our case that would be the scenes) and the edges $E$ are the semantic similarity between two scenes. In a recent extension of _TextRank_[2], a directed neural version was proposed. The new version considers neural representations of the textual units as node features in $G$ and considers directed edges $E$. In the directed neural $G$, we compute the centrality of each scene, i.e., how connected the scene is with the rest of the graph, as follows:
<p align="center">
$\textit{centrality}(s_i) = \lambda_1  \sum_{j<i}e_{ij} + \lambda_2  \sum_{j>i}e_{ij}$
</p>

Finally, we select the top $M$ scenes that have the highest centralities as the summary.

**Supervised: _SummaSuNNeR_**

Now we assume the scenes that belong to the summary of an episode. 

In a supervised scenario, we assume that binary labels are given denoting the scenes that belong to the summary. In this case, standard summarization algorithms select the desired subsequence of scenes based on standard criteria: content, salience (i.e., similarity with a document encoding), position and novelty (i.e., dissimilarity with previous selected units). 

**Our approach: _SUMMER_**

<p align="center">
  <img src="https://raw.githubusercontent.com/ppapalampidi/ppapalampidi.github.io/master/images/ezgif.com-gif-maker.gif" height="100">
</p>

## Incorporating the narrative structure into the generic algorithms


## References

[1] Mihalcea, Rada, and Paul Tarau. "Textrank: Bringing order into text." Proceedings of the 2004 conference on empirical methods in natural language processing. 2004.
[2] Zheng, Hao, and Mirella Lapata. "Sentence Centrality Revisited for Unsupervised Summarization." Proceedings of the 57th Annual Meeting of the Association for Computational Linguistics. 2019.


