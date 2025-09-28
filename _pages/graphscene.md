---
layout: single
title: ""
permalink: /graphscene/
author_profile: false
---

<style>
  .masthead { display: none !important; }
  a { color: #0066CC !important; }
  a:hover { color: #0066CC !important; }
  a:visited { color: #0066CC !important; }
</style>

# GraphSCENE: 
{: .text-center style="font-size: 2.5em; margin-bottom: 0.2em;"}

# On-Demand Critical Scenario Generation for Autonomous Vehicles in Simulation
{: .text-center style="margin-bottom: 1em;"}

**[Efimia Panagiotaki](https://efimiap.github.io/), Georgi Pramatarov, Lars Kunze, Daniele De Martini**<br/>
Oxford Robotics Institute, Department of Engineering Science<br/>University of Oxford
{: .text-center}

**IEEE IROS 2025**
{: .text-center style="font-size: 0.9em; margin-bottom: -1.2em;"}

<div style="text-align: center; margin-top: 2em; margin-bottom: 3em;">
  <a href="https://arxiv.org/abs/2410.13514" style="display: inline-block; background-color: #002147; color: white; padding: 8px 16px; margin: 0 8px; border-radius: 15px; font-weight: bold; text-decoration: none; font-size: 0.9em;">📄 arXiv</a>
  <a href="{{ site.baseurl }}/images/graphscene/GraphSCENE Poster.png" target="_blank" style="display: inline-block; background-color: #002147; color: white; padding: 8px 16px; margin: 0 8px; border-radius: 15px; font-weight: bold; text-decoration: none; font-size: 0.9em;">🖼️ Poster</a>
  <a href="/coming-soon/" style="display: inline-block; background-color: #002147; color: white; padding: 8px 16px; margin: 0 8px; border-radius: 15px; font-weight: bold; text-decoration: none; font-size: 0.9em;">💻 Code</a>
  <a href="/coming-soon/" style="display: inline-block; background-color: #002147; color: white; padding: 8px 16px; margin: 0 8px; border-radius: 15px; font-weight: bold; text-decoration: none; font-size: 0.9em;">📊 Slides</a>
</div>


**A tool to automatically generate diverse, safety-critical traffic scenarios *on-demand* in simulation for testing autonomous vehicles.**
{: style="background-color: #eedffdff; padding: 5px; border-radius: 8px; display: inline-block; margin-bottom: -2.2em;"}

<div style="text-align: center; margin: 30px 0;">
  <div style="display: inline-block; margin: 10px 15px;">
    <img src="{{ site.baseurl }}/images/graphscene/avstopnearcollision.png" alt="AV Stop Near Collision" style="width: 350px; height: auto;">
  </div>
  <div style="display: inline-block; margin: 10px 15px;">
    <img src="{{ site.baseurl }}/images/graphscene/avturnright.png" alt="AV Turn Right" style="width: 350px; height: auto;">
  </div>
</div>


## Overview
{: style="font-size: 1.5em; margin-top: 1.5em; margin-bottom: 0.5em;"}


<!-- ![GraphSCENE Overview]({{ site.baseurl }}/images/graphscene/graphscene_small_horizontal.png)
{: .text-center} -->

Reliable AV deployment requires testing in safety-critical and diverse scenarios, yet manually designing such environments is costly and inefficient. GraphSCENE is a method to automatically generate dynamic traffic scenarios tailored to user preferences. Using a temporal GNN constrained by real-world priors and traffic patterns, our method generates temporal scene graphs that correspond to the requested scenario. The generated scenarios are then rendered in simulation, providing scalable and effective testing environments for AVs.

<div style="border: 2px dashed rgba(6, 10, 51, 1); padding: 7px; margin: 20px 0; background-color: #ffffffff; border-radius: 5px;">
This work reduces the overhead of manual scenario creation, enabling scalable, on-demand generation of realistic, safety-critical testing environments, facilitating AV validation.
</div>


## Methodology
{: style="font-size: 1.5em; margin-top: 1.5em; margin-bottom: 0.5em;"}

![GraphSCENE Method]({{ site.baseurl }}/images/graphscene/graphscene_method_full.png)
{: .text-center}

<!-- <div style="text-align: center; margin: 30px 0;">
  <div style="display: inline-block; margin: 10px 15px;">
    <img src="{{ site.baseurl }}/images/graphscene/avmovenear.png" alt="AV Move Near" style="width: 350px; height: auto;">
  </div>
  <div style="display: inline-block; margin: 10px 15px;">
    <img src="{{ site.baseurl }}/images/graphscene/avstopnear.png" alt="AV Stop Near" style="width: 350px; height: auto;">
  </div>
</div> -->



## Results
{: style="font-size: 1.5em; margin-top: 1.5em; margin-bottom: 0.5em;"}



## BibTex
{: style="font-size: 1.5em; margin-top: 1.5em; margin-bottom: 0.5em;"}

```
@misc{panagiotaki2025graphsceneondemandcriticalscenario,
      title={GraphSCENE: On-Demand Critical Scenario Generation for Autonomous Vehicles in Simulation}, 
      author={Efimia Panagiotaki and Georgi Pramatarov and Lars Kunze and Daniele De Martini},
      year={2025},
      eprint={2410.13514},
      archivePrefix={arXiv},
      primaryClass={cs.RO},
      url={https://arxiv.org/abs/2410.13514}, 
}
```