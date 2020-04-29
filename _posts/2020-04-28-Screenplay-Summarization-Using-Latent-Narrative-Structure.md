---
title: 'Screenplay Summarization Using Latent Narrative Structure'
date: 2020-04-28
permalink: /posts/2020/08/screenplay-summarization/
tags:
  - screenplay
  - summarization
  - structure
---

## Screenplay summarization as scene selection

Given a screenplay, which is naturally segmented into scenes, the objective is to select an optimal subsequence of scenes that presents the main story -storyline- from beginning to end while omitting all unnecessary details and decreasing drastically the video length.

**Input**: screenplay as a sequence of scenes each of which has description parts (i.e., what the camera sees) and dialogue parts between the characters.

<p align="center">
  <img src="./_posts/Images/wpb9fac2df_1a.png" height="500">
</p>

**Output**: much smaller subsequence of scenes containing most important events in the story; video summary by merging the respective videos for the selected scenes.

## General summarization algorithms

**Unsupervised: _TextRank_** 

_TextRank_ is one of the most well-known and used unsupervised summarization algorithms. The core idea is that you have units (most commonly phrases or sentences but in our case that would be scenes, i.e., small documents). You compute the pairwise textual similarity between those units and create a densely connected graph, where the nodes are the textual units and the edges are the similarity measure. Finally, you calculate the centrality of each such unit (i.e., how densely connected it is with all other nodes in the graph) and you select the N most central ones as your summary. The hypothesis for this selection is that the units that present high similarity with a lot of nodes and especially with other central ones are important enough to be included in the summary.

**Supervised: _SummaSuNNeR_**

In a supervised scenario, we assume that binary labels are given denoting the scenes that belong to the summary. In this case, standard summarization algorithms select the desired subsequence of scenes based on standard criteria: content, salience (i.e., similarity with a document encoding), position and novelty (i.e., dissimilarity with previous selected units). 

**Our approach: _SUMMER**

![High Level]("https://github.com/ppapalampidi/ppapalampidi.github.io/tree/master/_posts/Images/highlevel_diff-crop.pdf")


## Incorporating the narrative structure




