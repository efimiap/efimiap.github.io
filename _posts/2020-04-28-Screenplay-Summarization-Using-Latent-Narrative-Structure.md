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

**Output**: subsequence of scenes containing most important events in the story; video summary by merging the respective videos for the selected scenes.

### General summarization algorithms

**Unsupervised**: _TextRank_ is one of the most well-known and used unsupervised summarization algorithms. The core idea is that you have units (most commonly phrases or sentences but in our case that would be scenes, i.e., small documents) 

![High Level](https://github.com/ppapalampidi/ppapalampidi.github.io/_posts/Images/highlevel_diff-crop.pdf)


