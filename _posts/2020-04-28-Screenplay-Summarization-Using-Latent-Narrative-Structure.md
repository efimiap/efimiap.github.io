---
layout: archive
title: 'Screenplay Summarization Using Latent Narrative Structure'
date: 2020-04-28
permalink: /posts/2020/08/screenplay-summarization/
author_profile: true
tags:
  - screenplay
  - summarization
  - structure
---

<head>
<style>
* {
  box-sizing: border-box;
}

.column {
  float: left;
  width: 33.33%;
  padding: 5px;
}

.narrow_column {
  float: left;
  width: 5%;
  padding: 5px;
}

/* Clearfix (clear floats) */
.row::after {
  content: "";
  clear: both;
  display: table;
}
</style>
</head>

This is a blog post for our paper [*Screenplay Summarization Using Latent Narrative Structure*](https://arxiv.org/pdf/2004.12727.pdf) accepted at ACL 2020.

We summarize episodes from the TV series CSI: Crime Scene Investigation based on their screenplays and produce video summaries. We propose ways to incorporate knowledge about the narrative structure into general unsupervised and supervised extractive summarization algorithms. 

You can find the CSI dataset for summarization [*here*](https://github.com/EdinburghNLP/csi-corpus), our pytorch code [*here*](https://github.com/ppapalampidi/SUMMER) and our automatically created video summaries [*here*](https://github.com/ppapalampidi/SUMMER/blob/master/video_summaries/video_summaries_link.csv). 


## Screenplay summarization as scene selection

Given a screenplay, which is naturally segmented into $N$ scenes $s$, we want to select an optimal subsequence of $M$ scenes that presents the main story -storyline- from beginning to end while omitting all unnecessary details and decreasing drastically the video length.

**Input**: Screenplay as a sequence of scenes $\mathcal{D}$. Each scene $s$ has description parts (i.e., what the camera sees) and dialogue parts between the characters.
**Output**: much smaller subsequence of scenes containing most important events in the story; video summary by merging the videos of the selected scenes. E.g.:
<div class="row">
  <div class="column">
    <img src="https://raw.githubusercontent.com/ppapalampidi/ppapalampidi.github.io/master/images/wpb9fac2df_1a.png" width="400">
  </div>
  <div class="narrow_column">
    &#8594;
  </div>
  <div class="column">
    <video controls="" height="300" ><source src="https://s3.eu-west-2.amazonaws.com/csivideosummaries/SUMMER/csi_final.webm" type="video/mp4"  width="400" /> Your browser does not support the video tag.</video>
  </div>
</div>

## General summarization algorithms

Previous work on automatic summarization is mostly focused on news summarization. When summarizing news articles, models can explicitly or implicitly take into advantage their simple structure: first few sentences reveal topic and key information; further details follow. In this domain, there are two popular extractive summarization models:

**Unsupervised as a graph** 

_TextRank_[1] is a well-known unsupervised summarization algorithm. For _TextRank_, we create a fully-connected graph $G=(V,E)$, where $V$ is the set of nodes and $E$ is the set of edges. In our case, $V$ is the set of scenes contained in the screenplay and $E$ is the set of interactions between scenes, i.e., the semantic similarity between any two scenes. In a recent extension of _TextRank_[2], a directed neural version was proposed. The new version considers neural representations as node features in $G$ and directed edges $E$. In the directed neural $G$, we compute the centrality of each scene, i.e., how connected the scene is with the rest of the graph, as follows:
<p align="center">
$\textit{centrality}(s_i) = \lambda_1  \sum_{j<i}e_{ij} + \lambda_2  \sum_{j>i}e_{ij}$
</p>
where $e_{ij}$ is the semantic similarity between two scenes $s_i,s_j$ and $\lambda_1,\lambda_2$ are the parameters that define whether prior or future scenes influence more the centrality score of a current scene.
Finally, we select the top $M$ scenes that have the highest centralities as the summary.

**Supervised as a sequence**

Now we assume that the scenes belonging to the episode summary are given. 

In a supervised scenario, we assume that binary labels are given denoting the scenes that belong to the summary. In this case, standard summarization algorithms (_SummaRuNNeR_[3]) consider a document as a sequence (for us that would be a sequence of scene representations) and perform selection based on:

1. content, i.e., scene representation

2. salience i.e., similarity with a global document representation

3. position & novelty, i.e., encoded position in the document and similarity with previous selections 

**Is general algorithms appropriate for summarizing episodes?**

No! TV episodes and narratives in general present significantly different structure and differ in the way that deliver information. In narratives, information is delivered piecemeal, the direction of the story often follows different paths as events unfold and the viewer/reader should watch/read the whole narrative in order to affirmatively conclude about what the story is about. 

Hence, we hypothesize that general summarization algorithms cannot be transferred directly from clean, straightforward articles to messy, complex and entangled stories, such as TV episodes.


**Our solution: Narrative structure**

We aim at exploiting the underlying narrative structure of the CSI episodes for facilitating summarization. 

According to screenwriting theory [4], all films and TV shows independently of their genre have a common high-level structure. In order for a story to be compelling, certain key events, called turning points (TPs) should be present in specific points of the story. These key events further segment the story into meaningful semantic sections (i.e., acts). 

There are several different schemes in order to describe narrative structure. Here, we use a modern variation of traditional narrative analysis that is used by screenwriters as a practical guide to creating films and TV shows. According to that scheme there are *5 turning points* which segment the narrative into *6 thematic sections*. We are mostly interested in the definition of the turning points:

<span style='color:green'>*TP1* Opportunity: Introductory event to the story occuring right after the presentation of the story setting and some background information about the protagonists.</span>

<span style='color:darkgreen'>*TP2* Change of plans: Event where the main goal of the story is revealed. Thereafter the action begins to increase.</span>

<span style='color:olive'>*TP3* Point of no return: Event the pushs the protagonist(s) to fully commit to their goal; thereafter there is no return to pre-story state for them.</span>

<span style='color:red'>*TP4* Major setback: The biggest obsacle for the protagonist(s); momen that everything falls apart (temporarily or permantently).</span>

<span style='color:indianred'> *TP5* Climax: moment of resolution, final event of the story and the ''biggest spoiler'' in a film.

Previous work [5] demonstrated that such events can be identified in various Hollywood movies by both human annotators and automatic approaches. However, is those events truly universal for all types of narratives? We want to apply these rules in a different type of narrative now: a TV show and specifically episodes where crime investigations are conducted.

Let's see how these events can be applied to an actual CSI episode:

<p align="center">
  <img src="https://raw.githubusercontent.com/ppapalampidi/ppapalampidi.github.io/master/images/csi_example.gif" height="60">
</p>

So, it seems like a good fit for our dataset as well. However, we do not have any information about the narrative structure of the CSI episodes neither can we infer the TPs based on writing conventions (in comparison with news articles). 

**Pre-training on TP identification**

For this reason we use the TRIPOD dataset containing movie screenplays and annotated TP events in order to pre-train a TP identification network. We use the same architecture as in [5], but we simplify the network to only consider screenplay scenes --we exclude the plot synopsis information-- and predict the scenes that act as TP events. For each of the five TPs, the network outputs a probability for each screenplay scene to represent the given event. 

## SUMMER

How can we incorporate the knowledge about the narrative structure --via the pre-trained TP identification network-- into the general summarization algorithms presented above?

The general idea is this:

<p align="center">
  <img src="https://raw.githubusercontent.com/ppapalampidi/ppapalampidi.github.io/master/images/ezgif.com-gif-maker.gif" height="70">
</p>

So, given the screenplay segmented into scenes, we first identify the scenes that act as TPs. Then, we decide which scenes to include to the summary based on their relationship with these key events. Finally, we have a video summary by combining the selected scenes.

**Unsupervised as structure-aware TextRank**

First, we consider our unsupervised method: TextRank. For each screenplay scene $s_i$ we compute a score $f_i$ that represents the maximum probability that the scene acts as any TP event. Then, we incorporate these scores in the centrality calculation of the scene as follows:

<p align="center">
$\textit{centrality}(s_i) = \lambda_1  \sum_{j<i}(e_{ij} + f_j) + \lambda_2  \sum_{j>i}(e_{ij} + f_i)$
</p>

Intuitively, the $f_j$ term in the first part of the equation (i.e., forward sum) increases increamentally the centrality scores assigned to scenes as the story moves on and we go to later sections of the narrative. The $f_i$ term in the second part of the equation (i.e., backward sum) increases the scores of the scenes that act as TPs.


**Supervised via latent structure representations**

In the supervised version of SUMMER we again select scenes for the summary based on similar criteria as SummaRuNNeR. However, we define the salience of a scene differently from before: instead of naively computed a global screenplay representation as a weighted average of all scene representation --it is unclear what a global representation stands for-- we explictly use the latent narrative structure in order to define the salience of a scene in the screenplay.

<p align="center">
  <img src="https://raw.githubusercontent.com/ppapalampidi/ppapalampidi.github.io/master/images/summer.gif" height="150">
</p>

So, as shown above we decide about the summary scenes based on each scene's content and relation with the key events (i.e., salience: maximum similarity with TPs).

**Training** We train SUMMER end-to-end using using BCE, i.e. binary cross-entropy loss. However, we also add two extra regularization terms to the loss function in order to control the TP-specific attention distributions used for computing the latent tp representations:
<p align="center">
$\mathcal{L} = \textit{BCE} + a O + b F$
</p>

Orthogonal regularization ($O$): we want to encourage tp representations to capture different information from the screenplay and not diverge to the same point in the episode. For this reason we maximize the Kullback-Leibler (KL) divergence~$\mathcal{D}_{KL}$ between all pairs of TP attention distributions:
<p align="center">
$O = \sum_{i \in [1,5]}\sum_{j \in [1,5], j \ne i}\log \frac{1}{\mathcal{D}_{KL}\left(tp_i \middle\| tp_j\right) + \epsilon}$
</p>

Focal regularization ($F$): we also want to discourage the TP distributions from deviating drastically from the expecting positions for each TP event. The expected positions for TPs are analyzed in screenwriting theory extensively. For this reason the focal loss minimizes the KL divergence between each TP attention distribution and the corresponding expected position distribution:
<p align="center">
$F = \sum_{i \in [1,5]}\mathcal{D}_{KL}\left(tp_i \middle\| th_i\right)$
</p>

## CSI dataset

We use the [*CSI dataset*](https://github.com/EdinburghNLP/csi-corpus) for summarization. Our dataset consists of 39 episodes. For each episode we have gold-standard scene-level binary annotations indicating whether the scene belongs to the summary. Moreover, for each summary scene we have further information about what aspect(s) of the summary the scene refers to. We consider 6 different aspects for each summary:

1. Crime scene 
2. Victim
3. Death cause
4. Evidence
5. Perpetrator
6. Motive


## Findings

Our experimental results demonstrate that knowledge about the narrative structure can boost the performance of both unsupervised and supervised methods. Interestingly, structure knowledge appears to be more important than character-based information (e.g., who is participating in the scene, what is the ratio of the main protagonists in the scene) that is tradionally analyzed for narratives. Human annotators also agree with our automatic evaluation.

However, we also investigate what is captured as ''narrative structure'' in the latent space by investigating the TP-specific distributions. These distributions are close to few-hot vectors and hence we can observe the scenes identified as TP events. Here is an illustration:

<p align="center">
  <img src="https://raw.githubusercontent.com/ppapalampidi/ppapalampidi.github.io/master/images/all.png" width="900">
</p>

We emperically see that different TP events as identified in the latent space tend to capture information about different aspects of the summary. We find that the latent TP representations cover the 70.25% of the aspects presented in a episode (in comparison with a randomly initialized model with no regularization which covers only 44.48% on average).

Moreover, we find that specific TP events correlate with specific aspects:

<span style='color:green'>*TP1* Opportunity</span> &#8594; Crime scene, Victim

<span style='color:darkgreen'>*TP2* Change of plans</span> &#8594; Victim, Death cause

<span style='color:olive'>*TP3* Point of no return</span> &#8594; Evidence, Perpetrator

<span style='color:red'>*TP4* Major setback</span> &#8594; Evidence

<span style='color:indianred'> *TP5* Climax</span> &#8594; Motive

Finally, during human evaluation we again find that SUMMER is able to cover more aspects producing more diverse and complete video summaries. [*Here*](https://github.com/ppapalampidi/SUMMER/blob/master/video_summaries/video_summaries_link.csv) are the actual video summaries produced by SUMMER and used for human evaluation.

## References

[1] Mihalcea, Rada, and Paul Tarau. "Textrank: Bringing order into text." Proceedings of the 2004 conference on empirical methods in natural language processing. 2004.

[2] Zheng, Hao, and Mirella Lapata. "Sentence Centrality Revisited for Unsupervised Summarization." Proceedings of the 57th Annual Meeting of the Association for Computational Linguistics. 2019.

[3] Nallapati, Ramesh, Feifei Zhai, and Bowen Zhou. "Summarunner: A recurrent neural network based sequence model for extractive summarization of documents." Thirty-First AAAI Conference on Artificial Intelligence. 2017.

[4] Michael Hauge. 2017.Storytelling Made Easy:  Per-suade and Transform Your Audiences, Buyers, andClients  –  Simply,  Quickly,  and  Profitably.IndieBooks International.

[5] Papalampidi, Pinelopi, Frank Keller, and Mirella Lapata. "Movie Plot Analysis via Turning Point Identification." Proceedings of the 2019 Conference on Empirical Methods in Natural Language Processing and the 9th International Joint Conference on Natural Language Processing (EMNLP-IJCNLP). 2019.

