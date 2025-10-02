---
layout: single
title: ""
permalink: /graphscene/
author_profile: false
---

<style>
  .masthead { display: none !important; }
  a { color: white !important; }
  a:hover { color: white !important; }
  a:visited { color: white !important; }
</style>

# GraphSCENE: 
{: .text-center style="font-size: 2.5em; margin-bottom: 0.2em;"}

# On-Demand Critical Scenario Generation for Autonomous Vehicles in Simulation
{: .text-center style="margin-bottom: 1em;"}

**[Efimia Panagiotaki](https://efimiap.github.io/), Georgi Pramatarov, Lars Kunze, Daniele De Martini**<br/>
Oxford Robotics Institute, Department of Engineering Science<br/>University of Oxford
{: .text-center}


**IEEE IROS 2025**
{: .text-center style="font-size: 1em; margin-bottom: -1.2em; margin-top: -0.5em; "}





<div style="text-align: center; margin-top: 2em; margin-bottom: 3em;">
  <a href="https://arxiv.org/abs/2410.13514" style="display: inline-block; background-color: #002147; color: white !important; padding: 8px 16px; margin: 0 8px; border-radius: 15px; font-weight: bold; text-decoration: none; font-size: 0.9em;">📄 arXiv</a>
  <a href="{{ site.baseurl }}/images/graphscene/GraphSCENE Poster.png" target="_blank" style="display: inline-block; background-color: #002147; color: white !important; padding: 8px 16px; margin: 0 8px; border-radius: 15px; font-weight: bold; text-decoration: none; font-size: 0.9em;">🖼️ Poster</a>
  <a href="/coming-soon/" style="display: inline-block; background-color: #002147; color: white !important; padding: 8px 16px; margin: 0 8px; border-radius: 15px; font-weight: bold; text-decoration: none; font-size: 0.9em;">💻 Code</a>
  <a href="/coming-soon/" style="display: inline-block; background-color: #002147; color: white !important; padding: 8px 16px; margin: 0 8px; border-radius: 15px; font-weight: bold; text-decoration: none; font-size: 0.9em;">📊 Slides</a>
</div>

**A tool to automatically generate diverse, safety-critical traffic scenarios *on-demand* in simulation for autonomous vehicles testing.**
{: style="background-color: #eedffdff; padding: 5px; border-radius: 8px; display: inline-block; margin-bottom: -2.2em; margin-top: -1em;"}

<div style="text-align: center; margin: 30px 0;">
  <img src="{{ site.baseurl }}/images/graphscene/pipeline_graphscene_narrow_compressed.gif" alt="GraphSCENE Pipeline" style="max-width: 100%; height: auto;">
</div>

<!-- <div style="text-align: center; margin: 30px 0;">
  <div style="display: inline-block; margin: 10px 15px;">
    <img src="{{ site.baseurl }}/images/graphscene/avstopnearcollision.png" alt="AV Stop Near Collision" style="width: 350px; height: auto;">
    <p style="font-style: italic; text-align: center; margin-top: 5px; font-size: 0.8em;">Action: AV-Stop, Criticality: Near Collision</p>
  </div>
  <div style="display: inline-block; margin: 10px 15px;">
    <img src="{{ site.baseurl }}/images/graphscene/avturnright.png" alt="AV Turn Right" style="width: 350px; height: auto;">
    <p style="font-style: italic; text-align: center; margin-top: 5px; font-size: 0.8em;">Action: AV-TurnRight, Criticality: Visible</p>
  </div>
</div> -->


## Overview
{: style="font-size: 1.5em; margin-top: 0em; margin-bottom: 0.5em;"}
<!-- ![GraphSCENE Overview]({{ site.baseurl }}/images/graphscene/graphscene_small_horizontal.png)
{: .text-center} -->
<div style="line-height: 1.7; margin-bottom: 10px; font-size: 0.9em;">
Reliable AV deployment requires testing in <b>realistic, safety-critical, and diverse scenarios</b>, yet manually designing such environments is <b>costly and inefficient</b>.  <br/>
GraphSCENE solves this by automatically generating <b>dynamic traffic scenarios</b> tailored to user preferences. Based on temporal graph neural networks (GNN) and grounded in real-world traffic priors, GraphSCENE produces scenarios that are rendered directly in simulation.
</div>
<div style="border: 2px dashed rgba(6, 10, 51, 1); padding: 7px; margin: 20px 0; background-color: #ffffffff; border-radius: 5px;font-size: 0.9em;">
<b>GraphSCENE reduces the overhead of manual scenario creation, making AV testing more scalable, realistic, and effective.</b>
</div>


<div style="line-height: 1.7; margin-bottom: 10px; font-size: 0.9em;">
🚦 <b>Realistic traffic dynamics</b> - scenarios follow real-world behavioural constraints.<br/>
⚡  <b>Scalable & on-demand</b> - generate multiple scenarios fast, without manual design overhead.<br/>
🎯 <b>Tailored to user preferences</b> - users define the types of situations they want to test.<br/>
🧩 <b>Seamless simulation integration</b> - outputs are rendered in CARLA Sim.<br/>
🛡️ <b>Safety-critical coverage</b> - stress-test AVs under diverse and challenging conditions.
</div>


## Methodology
{: style="font-size: 1.5em; margin-top: 1.5em; margin-bottom: 0.5em;"}

![GraphSCENE Method]({{ site.baseurl }}/images/graphscene/graphscene_method_full.png)
{: .text-center}

<div style="line-height: 1.7; margin-bottom: 10px; font-size: 0.9em;">
<b>1. Scene Graph Extraction: </b>
Temporal scene graphs are extracted from real-world datasets, representing dynamic agents, static structures, and their relations, to create a database of <em>seed scene graphs</em>.<br/>
<b>2. Scenario Specification: </b>
Users define the type of scenario to test (criticality, AV action, agents).<br/>
<b>3. Graph Completion: </b>
A temporal graph neural network (GNN) predicts ego-vehicle interactions and relations over time, constrained by traffic priors and semantic rules.<br/>
<b>4. Validity Constraints</b>
Predictions are filtered through a domain ontology and real-world priors to ensure realistic, rule-consistent interactions.<br/>
<b>5. Simulation Integration</b>
The final scene graph is converted into CARLA Sim, producing scalable, safety-critical scenarios for AV validation
</div>

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

<div style="text-align: center; margin: 30px 0;">
  <img src="{{ site.baseurl }}/images/graphscene/GraphScene_results_compressed.gif" alt="GraphSCENE Results" style="max-width: 100%; height: auto;">
</div>

<div style="line-height: 1.7; margin-bottom: 10px; font-size: 0.9em;">
We compare our method against a few-shot LLM, a state-of-the-art link predictor, and a graph perturbation approach, assessing link prediction accuracy, contextual correctness, and scenario generation consistency and plausibility. GraphSCENE consistently outperforms all baselines, particularly in generating semantically valid ego-agent interactions and maintaining temporal coherence across scenes. Outputs are directly integrated into CARLA simulations, confirming both fidelity and utility for AV validation pipelines.
</div>




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