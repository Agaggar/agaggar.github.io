---
layout: blog
title: "Why Ergodic Control Matters"
date: 2026-04-02
category: blog
permalink: /blog/why-ergodic-control-matters/
description: "A short tour of why ergodic objectives show up in exploration, coverage, and active sensing—and what that means for learning-based perception."
mathjax: true
---

This note is a placeholder while the full essay is in progress. The goal is to connect **ergodic control**—distributing motion so that time spent in regions matches a target spatial distribution—to problems in robotics where you care about *where* the robot spends its attention, not just reaching a single goal.

Later sections will walk through a minimal example and, if useful, an interactive figure you can tweak here in the page. For now, thanks for reading the stub.

<h2>Comparing Coverages</h2>
TODO: Interactive demo showing time to "success" for various search strategies. (This could be finding all 3 hotspots, where "finding" is spending 10 .)

<h2>Intro</h2>
Is "ergodic control" a fancy, over-engineered algorithm used only in complicated settings? Is it a tool used only in academia to eke out the last bit of performance benefit? Maybe, but in this article, we'll explore what ergodic control promises, how to implement it, and it's pros/cons. At worst, you'll be introduced to another way of thinking about problems that span across machine learning, statistics, and robotics. At best, this will transform how you think about data collection as a roboticist.

<h2>Background</h2>
<a href="https://en.wikipedia.org/wiki/Exploration–exploitation_dilemma">Exploration vs explotiation</a> is a classic problem that shows up in many domains. In the cartoon below, how should you move in order to <em>maximize</em> total rewards? 

<ul>
    <li>Strategy #1: Exploration - Explore the environment as much as possible. <br>
        <div style="text-indent: 30px;">Pro: Increases exposure to potentially super high rewards.</div>
        <div style="text-indent: 30px;">Con: Don't do anything with knowledge of high reward areas.</div></li>
    <li>Strategy #2: Exploitation - Stay in the closest area with a reward (aka Greedy).
        <div style="text-indent: 30px;">Pro: Takes advantage of reward.</div>
        <div style="text-indent: 30px;">Con: Settle; don't explore for better reward areas.</div></li>
</ul>

TODO: Embed an interactive demo where you can "sample" N=100 trajectories and see the average reward over a slider amount of timesteps. Engineer the environment so that in some cases explore is better and some cases exploit is better

<figure>
  <img src="https://huggingface.co/blog/assets/63_deep_rl_intro/expexpltradeoff.jpg" alt="Exploration vs exploitation cartoon">
  <figcaption>PLACEHOLDER. Left: Exploration doesn't consider how good actions are, and instead just explores the environment as much as possible. Right: Exploitation leads to good short term benefits, but doesn't consider costlier actions with larger payoffs.</figcaption>
</figure>

Clearly, we need some balance between the two approaches. [^1] 

<figure>
  <img src="https://arxiv.org/html/2403.01536v3/x1.png" alt="Kernel ergodic search">
  <figcaption>Spoiler alert: Ergodic coverage balances uniform and greedy coverages. Source: <a href="https://arxiv.org/pdf/2403.01536">Fast Ergodic Search With Kernel Functions</a>. But we're getting ahead of outselves...</figcaption>
</figure>

<h2>The Lawnmower Example</h2>
<em>How long</em> an agent spends in an area matters just as much as <em>where</em> the agent is. For example, consider you have to mow a lawn with a particularly shitty lawnmover with only an on/off button. The longer you stay in a spot, the more grass will be cut.[^2] How should you mow the lawn? 

Intuitively, the answer is to spend more time where the grass is longer, and less time where the grass is shorter. This is exactly what <em>ergodicity</em> is.

<span style="color: #f46f25; font-size: 24px;">Ergodicity: Spend more time in areas with higher probability and less time in areas with lower probability.</span>[^3] 

The standard ergodic measure[^4] quantifies ergodicity as follows: 
$$ \mathcal{E} = \sum_{k=0}^{K} \Lambda_k \left| c_k - \phi_k \right|^2 $$. If you're interested in each of the math terms and how to set up the standard ergodic measure, check out this <a href="https://colab.research.google.com/github/MurpheyLab/ergodic-control-sandbox/blob/main/notebooks/ergodic_metric.ipynb">amazing tutorial</a>.

TODO: Add ergodic control gif visualization of coverage.

<h2>Applications</h2>
Ergodicity is a principled way of coverage with asymptotic guarantees of matching the target distribution. It provides a good balance to exploration vs exploitation, and can be integrated in closed-loop, receding horizon MPC. It's also been shown to improve RL performance for agents with dynamcis (all of robotics) by collected data following i.i.d. properties.

<h3>Non-Exhaustive List of Ergodic Control Techniques</h3>
<ul>
    <li>Standard Ergodic Control (SMC): Paper, <a href="https://colab.research.google.com/github/MurpheyLab/ergodic-control-sandbox/blob/main/notebooks/smc_ergodic_control.ipynb">Code</a></li>
    <li>Kernel Ergodic Control: <a href="https://arxiv.org/pdf/2403.01536">Paper</a>, <a href="https://colab.research.google.com/github/MurpheyLab/ergodic-control-sandbox/blob/main/notebooks/kernel_ergodic_control.ipynb">Code</a></li>
    <li>KL-E^3: <a href="https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=9312988&casa_token=gcqKNl1RpyEAAAAA:jPcyphsvJySR1OWHm33uDqjhcZLf0Eluor-XCiXj9Obq1yrgd8FC-3a3ZFeIOppnhj4g7Be6MQ&tag=1">Paper</a>, <a href="https://github.com/i-abr/KLE3">Code</a></li>
    <li>HEDAC: <a href="https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=7786872&casa_token=WX3Gy4kjk34AAAAA:7-5G0tcTIw_dpilhMPA5M2zs_xH1q3_5i2TwWYaNGKu4Kt9Lxn9T83deilubbFWOqRxELzCTLg">Paper</a>, <a href="https://gitlab.idiap.ch/rli/robotics-codes-from-scratch/-/blob/master/python/ergodic_control_HEDAC_2D.py?ref_type=heads">Code</a></li>
    <li>TensorTrain: <a href="https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=9473030&casa_token=12btchkp0GQAAAAA:BpHptl5nJOwSVE9cskhYSMcd7BSxCk3Rg4OIRi8-UmLGR11KYfZMlSS_JlZR-Xa0wF8XauV52A">Paper</a>, <a href="https://github.com/SuhanNShetty/Ergodic_Exploration_using_Tensor_Train">Code</a></li>
</ul>

TODO: add "table of contents" UI on the left side of all blog posts for all headers and subheaders, etc. (h2 and lower)

---
[^1]: Obviously, your strategy should depend on what the objective is. To maximize reward, an agent should just consistently find the highest reward source and stay there. But, as talekd about in Lawnmower example (link this), we're going to focus on robotics cases where the time-averaged trajectory matters.

[^2]: Contrived, I know. And yes, we're going to assume every blade of grass in the lawn needs to be cut, and that we can measure by how much and turn it into a probability distribution. Yes, this example is contrived. Deal with it.

[^3]: Mathy version: The ergodic measure quantifies the difference between the time-averaged spatial statistics of an agent with a target distribution. An agent's trajectory is ergodic if the empirical distribution of the agent's trajectory are proportional to the target probability density.

[^4]: The term "metric" cannot be used when using alternative measures for distance, such as KL-Divergence used by <a href="https://sites.google.com/view/kle3/home">KL-E^3</a>. I'm going to use ergodic "metric" and ergodic "measure" interchangeably since there's semantically no difference.